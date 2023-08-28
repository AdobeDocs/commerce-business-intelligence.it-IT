---
title: Attiva [!DNL Adobe Commerce Intelligence] Account
description: Scopri chi contattare per attivare il tuo [!DNL Commerce Intelligence] account.
exl-id: 0efac7b4-2457-48c7-947a-d2776b90a1dd
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: cdd2373c2b9afd85427d437c6d8450f4d4e03350
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 0%

---

# Attiva [!DNL Commerce Intelligence] Account per sottoscrizioni locali e iniziali

Per attivare [!DNL Commerce Intelligence] per gli abbonamenti on-premise, crea innanzitutto un [!DNL Commerce Intelligence] , immettere le informazioni sulle impostazioni, quindi connettersi [!DNL Commerce Intelligence] al tuo [!DNL Commerce] database. <!-- For information about activation in `Cloud Starter` projects, see [Activating your [!DNL Commerce Intelligence] Account for `Cloud Starter` Subscriptions](../getting-started/cloud-activation.md).-->

## Crea [!DNL Commerce Intelligence] account

Per creare il tuo account, contatta il team dell’account Adobe o il consulente tecnico del cliente.

## Crea la password

Dopo la creazione dell’account, verifica la presenza di un’e-mail di notifica dell’account da [!DNL The Magento BI Team@rjmetrics.com]. Utilizza il collegamento fornito nell’e-mail per accedere al [!DNL Commerce Intelligence] e creare la password. Vai alla tua casella in entrata e verifica il tuo indirizzo e-mail.

Se non hai ricevuto un’e-mail, [contatta l’assistenza](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

![](../assets/create-account-4.png)

## Imposta le preferenze del Negozio

Prima di configurare la connessione al database, completare il modulo per le informazioni sull&#39;archivio. Queste informazioni sono necessarie per completare **[!UICONTROL Connect your Database]** configurazione.

![](../assets/create-account-6.png)

## Aggiungi [!DNL Commerce Intelligence] utenti

Dopo aver impostato la password e aver effettuato l’accesso a [!DNL Commerce Intelligence], puoi aggiungere altri utenti al tuo [!DNL Commerce Intelligence] account. Quando aggiungi degli utenti, aggiungi gli utenti amministratore con le autorizzazioni appropriate per completare il processo di attivazione.

![](../assets/create-account-5.png)

## Creare un [!DNL Commerce Intelligence] utente in [!DNL Commerce] admin

Da utilizzare [!DNL Commerce Intelligence], devi aggiungere un utente permanente e dedicato al [!DNL Commerce] progetto. Questo utente dedicato funge da connessione permanente a [!DNL Commerce] che consente il recupero e il trasferimento di nuovi dati al [!DNL Commerce Intelligence] Data Warehouse.

Configurazione di un [!DNL Commerce Intelligence] si assicura che l’account non venga disattivato o eliminato, bloccando in tal modo [!DNL Commerce Intelligence] connessione.


>[!NOTE]
>
>L’Adobe incoraggia l’utilizzo di un nome account che ne indichi lo stato permanente (ad esempio ACI-dedicato, ACI-database-connector e così via).

Dopo aver creato l’utente dedicato per [!DNL Commerce Intelligence] in Admin, aggiungi lo stesso utente all’ambiente principale del [!DNL Commerce] progetto con un **[!UICONTROL Master]** impostazione di `Contributor`.

![](../assets/commerce-add-user-settings.png)

## Ottenere le chiavi SSH di Commerce Intelligence

1. Il giorno [!UICONTROL Connect your database] pagina per [!DNL Commerce Intelligence] imposta, scorri verso il basso e seleziona **[!UICONTROL Encryption settings]**.

1. Per **Tipo di crittografia**, seleziona `SSH Tunnel`.

1. Dall’elenco a discesa, copia la chiave pubblica fornita.

   ![](../assets/encryption-setting-new-account.png)

## Aggiungi la chiave pubblica al [!DNL Commerce Intelligence]

1. Dalla sezione [!DNL Commerce Admin], accedere utilizzando le informazioni di accesso per [!DNL Commerce Intelligence] utente appena creato.

1. Seleziona la **Impostazioni account** scheda.

1. Scorri verso il basso ed espandi **[!UICONTROL SSH Keys]** a discesa. Quindi, seleziona **[!UICONTROL Add a public key]**.

   ![](../assets/add-public-key.png)

1. Incolla la chiave pubblica copiata in [!DNL Encryption Type] sopra.

   ![](../assets/paste-public-key.png)

## Fornire [!DNL Commerce Intelligence] Elementi di base `MySQL` credenziali

1. Aggiorna il tuo `.magento/services.yaml`.

   ![](../assets/update-magento-services-yaml.png)

1. Aggiorna il tuo `.magento.app.yaml`.

   ![](../assets/magento-app-yaml-relationships.png)

## Ottieni informazioni sulla connessione al database

Ottenere le informazioni sulla connessione al database [!DNL Commerce] database a [!DNL Commerce Intelligence]

1. Eseguire il comando seguente per ottenere le informazioni.

   `echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 --decode | json_pp`

1. Esaminare le informazioni del database, che devono essere simili a quelle dell&#39;esempio seguente.

   ![](../assets/example-database-information.png)

## Connetti [!DNL Commerce Intelligence] al tuo [!DNL Commerce] database che utilizza una connessione crittografata

>[!NOTE]
>
>L’Adobe consiglia vivamente di utilizzare un [`SSH tunnel`](../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) per stabilire la connessione al database. Tuttavia, se questo metodo non è un&#39;opzione, è comunque possibile collegare [!DNL Commerce Intelligence] al database utilizzando una [`direct connection`](../data-analyst/importing-data/integrations/mysql-via-a-direct-connection.md).

Immetti il [!DNL Commerce Intelligence] informazioni in [!UICONTROL Connect your Magento Database] schermo.

![](../assets/connect-magento-db.png)

**Input:**

[!UICONTROL Integration Name]: [scegli un nome per il tuo [!DNL Commerce Intelligence] istanza]

[!UICONTROL Host]: `mbi.internal`

[!UICONTROL Port]: `3306`

[!UICONTROL Username]: `mbi`

[!UICONTROL Password]: [password di input visualizzata nella sezione precedente]

[!UICONTROL Database Name]: `main`

[!UICONTROL Table Prefixes]: [lascia vuoto se non sono presenti prefissi di tabella]

## Imposta il [!UICONTROL **Fuso orario**] impostazioni

![](../assets/time-zone-settings.png)

**Input:**

[!UICONTROL Database Timezone]: `UTC`

[!UICONTROL Desired Timezone]: [scegliere il fuso orario per il quale si desidera visualizzare i dati]

## Ottenere le informazioni sulle impostazioni di crittografia

L’interfaccia utente del progetto fornisce una stringa di accesso SSH. Questa stringa può essere utilizzata per raccogliere le informazioni necessarie per [!UICONTROL **Indirizzo remoto**] e [!UICONTROL **Nome utente**]. Utilizza la stringa di accesso SSH selezionando il pulsante del sito di accesso nel ramo principale dell’interfaccia utente del progetto. Quindi, trova il tuo [!UICONTROL User Name] e [!UICONTROL Remote Address] come mostrato di seguito.

![](../assets/master-branch-settings.png)

## Inserisci il tuo [!DNL Encryption] impostazioni

![](../assets/encryption-settings-2.png)

**Input:**

[!UICONTROL Encryption Type]: `SSH Tunnel`

[!UICONTROL Remote Address]: `ssh.us-3.magento.cloud`  [dal passaggio precedente]

[!UICONTROL Username]: `vfbfui4vmfez6-master-7rqtwti—mymagento`  [dal passaggio precedente]

[!UICONTROL Port]: `22`

## Salva l’integrazione.

Dopo aver completato i passaggi di configurazione, applica le modifiche selezionando [!UICONTROL **Salva integrazione**].

Hai connesso correttamente il tuo [!DNL Commerce] al tuo database [!DNL Commerce Intelligence] account.

>[!NOTE]
>
>Se sei un [!DNL Adobe Commerce Intelligence Pro] cliente, contatta il tuo Customer Success Manager o Customer Technical Advisor per coordinare i passaggi successivi.

Dopo aver completato la configurazione, [accedi](../getting-started/sign-in.md) al tuo [!DNL Commerce Intelligence] account.

<!---# Activate your [!DNL Commerce Intelligence] Account 

To activate [!DNL Commerce Intelligence] for on-premise or `Cloud Pro` subscriptions, [contact support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

>[!NOTE]
>
>Adobe no longer supports new `Cloud Starter` subscriptions.--->
