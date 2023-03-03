---
title: Attiva [!DNL MBI] Account per abbonamenti a Cloud Starter
description: Scopri come attivare [!DNL MBI] per progetti Cloud Starter.
exl-id: 172439ee-fa1d-4872-b6a9-c61a212a7cbe
source-git-commit: 6f018ab220f2ae573cbc9016f9efb83c27a254be
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# Attiva [!DNL MBI] Account per `Cloud Starter` Iscrizioni

Per attivare [!DNL MBI] per `Cloud Starter` progetti, crea prima un [!DNL MBI] , quindi crea un `SSH` , quindi connettersi al database Commerce. Consulta [attivazione di abbonamenti on-premise](../getting-started/onpremise-activation.md).

>[!NOTE]
>
>Per assistenza nell’attivazione [!DNL MBI] per `Cloud Pro` progetti, contatta il team dell’account Adobe o il consulente tecnico del cliente.

1. Crea [!DNL MBI] Account.

   - Vai a [Accesso all’account Adobe Commerce](https://account.magento.com/customer/account/login)

   - Vai a **[!UICONTROL My Account** > **My [!DNL MBI] Instances]**.

   - Clic **[!UICONTROL Create Instance]**. Se non trovi questo pulsante, contatta il team dell’account di Adobe o il consulente tecnico del cliente.

   - Seleziona il `Cloud Starter` abbonamento. Se si dispone solo di `cloud starter` abbonamento questo verrà selezionato automaticamente.

   - Clic **[!UICONTROL Continue]**.

   - Inserisci le informazioni per creare l’account.

   ![](../assets/create-account-2.png)

   - Vai alla tua casella in entrata e verifica il tuo indirizzo e-mail.

   ![](../assets/create-account-3.png)

   - Crea la password.

   ![](../assets/create-account-4.png)

   - Dopo aver creato l’account, avrai la possibilità di aggiungere utenti al nuovo account. È ora possibile aggiungere gli amministratori tecnici per eseguire i seguenti passaggi.

   ![](../assets/create-account-5.png)

1. Inserisci informazioni sul tuo Negozio per impostare le tue preferenze.

   ![](../assets/create-account-6.png)

   Prima di collegare il database per il terzo passaggio del flusso di onboarding è necessario raccogliere alcune informazioni. Verrà compilato il `Connect your database` al passaggio 9.

1. Crea dedicato [!DNL MBI] Utente.

   - Crea un nuovo utente nel tuo [Account Adobe Commerce](https://accounts.magento.com).

   - _Perché un nuovo utente?_ [!DNL MBI] ha bisogno che un utente aggiunto al progetto recuperi continuamente nuovi dati da trasferire nel [!DNL MBI] data warehouse. Questo utente fungerà da connessione. L’aggiunta di questo utente al progetto avverrà nel passaggio 4.

   - Il motivo per cui è necessario disporre di un [!DNL MBI] L&#39;utente deve impedire che l&#39;utente aggiunto venga inavvertitamente disattivato o eliminato e che venga arrestato [!DNL MBI] connessione.

1. Aggiungi l’utente appena creato all’ambiente principale del progetto come `Contributor`.

   ![](../assets/create-account-7.png)

1. Ottieni [!DNL MBI] `SSH` tasti.

   - Vai a `Connect your database` pagina di [!DNL MBI] configurare l’interfaccia utente e scorrere verso il basso fino a `Encryption settings`.

   - Per `Encryption Type` campo, scegli `SSH Tunnel`.

   - Dal menu a discesa, puoi copiare e incollare il fornito [!DNL MBI] `Public Key`.

   ![](../assets/create-account-8.png)

1. Aggiungi il nuovo [!DNL MBI] `Public key` al [!DNL MBI] creato nel passaggio 5.

   - Vai a [il tuo account cloud Adobe Commerce](https://accounts.magento.cloud/). Accedi con le informazioni di accesso del tuo account per il nuovo [!DNL MBI] utente creato. Quindi vai al `Account Settings` scheda.

   - Scorrere la pagina ed espandere il menu a discesa per `SSH` tasti. Quindi fai clic su **[!UICONTROL Add a public key]**.

   ![](../assets/create-account-9.png)

   - Aggiungi il [!DNL MBI] `SSH Public Key` dall&#39;alto.

   ![](../assets/create-account-10.png)

1. Fornire [!DNL MBI] Credenziali MySQL.

   - Aggiorna il tuo `.magento/services.yaml`

   ```sql
   mysql:
       type: mysql:10.0
       disk: 2048
       configuration:
           schemas:
               - main
           endpoints:
               mysql:
                   default_schema: main
                   privileges:
                       main: admin
               mbi:
                   default_schema: main
                   privileges:
                       main: ro
   ```

   - Aggiorna il tuo `.magento.app.yaml`

   ```sql
           relationships:
               database: "mysql:mysql"
               mbi: "mysql:mbi"
               redis: "redis:redis"
   ```

1. Ottenere informazioni sulla connessione del database a [!DNL MBI].

   Esegui
   `echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 --decode | json_pp`

   per ottenere informazioni sulla connessione al database.

   Dovresti ricevere informazioni simili a quelle riportate di seguito:

   ```json
           "mbi" : [
                 {
                    "scheme" : "mysql",
                    "rel" : "mbi",
                    "cluster" : "vfbfui4vmfez6-master-7rqtwti",
                    "query" : {
                       "is_master" : true
                    },
                    "ip" : "169.254.169.143",
                    "path" : "main",
                    "host" : "[!DNL MBI].internal",
                    "hostname" : "3m7xizydbomhnulyglx2ku4wpq.mysql.service._.magentosite.cloud",
                    "username" : "mbi",
                    "service" : "mysql",
                    "port" : 3306,
                    "password" : "[password]"
                 }
              ],
   ```

1. Connettere il database Commerce

   ![](../assets/create-account-11.png)

   - `Integration Name`: [Scegli un nome per l’integrazione.]

   - `Host`: `[!DNL MBI].internal`

   - `Port`: `3306`

   - `Username`: `mbi`

   - `Password`: [password di input fornita nell&#39;output per il passaggio 8.]

   - `Database Name`: `main`

   - `Table Prefixes`: [lascia vuoto se non sono presenti prefissi di tabella]

1. Imposta il fuso orario.

   ![Input](../assets/create-account-12.png)

   - `Database`: `Timezone: UTC`

   - `Desired Timezone`: [Scegli il fuso orario in cui visualizzare i dati.]

1. Ottieni informazioni sulle impostazioni di crittografia.

   - L’interfaccia utente del progetto fornisce un’ `SSH` stringa di accesso. Questa stringa può essere utilizzata per raccogliere le informazioni necessarie per `Remote Address` e `Username` nella configurazione di `Encryption` impostazioni. Utilizza il `SSH Access` stringa trovata facendo clic sul pulsante Accedi al sito nel ramo principale dell’interfaccia utente del progetto e individua `User Name` e `Remote Address` come mostrato di seguito.

   ![](../assets/create-account-13.png)

   ![](../assets/create-account-14.png)

1. Informazioni di input per `Encryption` impostazioni

   ![](../assets/create-account-15.png)

   **Input**

   - `Encryption Type`: `SSH Tunnel`

   - `Remote Address`: `ssh.us-3.magento.cloud`

   - `Username`: `vfbfui4vmfez6-master-7rqtwti--mymagento`

   - `Port`: `22`

1. Clic **[!UICONTROL Save Integration]**.

1. Connessione a [!DNL MBI] account.

1. Dopo aver effettuato correttamente la connessione [!DNL MBI] nel database Commerce, contatta il team dell’account Adobe per coordinare i passaggi successivi, ad esempio la configurazione delle integrazioni e altri passaggi di configurazione.

1. Al termine della configurazione, puoi [accedi](../getting-started/sign-in.md) al tuo [!DNL MBI] account.
