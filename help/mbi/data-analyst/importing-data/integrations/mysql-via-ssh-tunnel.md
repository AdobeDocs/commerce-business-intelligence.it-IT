---
title: Connessione di MySQL tramite tunnel SSH
description: Scopri come collegare MySQL tramite sintonizzatore SSH.
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# Connetti `MySQL` tramite `SSH Tunnel`

* [Recupera il [!DNL MBI] chiave pubblica](#retrieve)
* [Consenti accesso al [!DNL MBI] Indirizzo IP](#allowlist)
* [Creare un utente Linux per [!DNL MBI]](#linux)
* [Creare un utente MySQL per [!DNL MBI]](#mysql)
* [Immetti la connessione e le informazioni utente in [!DNL MBI]](#finish)

## PASSA A

* `MySQL via SSH tunnel`
* [`MySQL`](../integrations/mysql-via-a-direct-connection.md)
* [`MySQL`](../integrations/mysql-via-cpanel.md)

Per collegare il `MySQL` database a [!DNL MBI] tramite `SSH tunnel`, tu (o il tuo team, se non sei un tecnico) dovrai fare alcune cose:

1. Recupera il [!DNL MBI] `public key`
1. Consenti accesso al [!DNL MBI] `IP address`
1. Crea un `Linux` utente per [!DNL MBI]
1. Crea un `MySQL` utente per [!DNL MBI]
1. Immetti la connessione e le informazioni utente in [!DNL MBI]

Non è complicato come potrebbe sembrare. Cominciamo.

## Recupero del [!DNL MBI] chiave pubblica {#retrieve}

La `public key` viene utilizzato per autorizzare [!DNL MBI] `Linux` utente. Nella sezione successiva, creeremo l’utente e importeremo la chiave.

1. Vai a **[!UICONTROL Manage Data** > **Connections]** e fai clic su **[!UICONTROL Add New Data Source]**.
1. Fai clic sul pulsante `MySQL` icona.
1. Dopo la `MySQL credentials` si apre la pagina, imposta `Encrypted` passa a `Yes`. Verrà visualizzato il modulo di configurazione SSH.
1. La `public key` si trova sotto questo modulo.

Lascia aperta questa pagina per l’intera esercitazione; sarà necessario nella sezione successiva e alla fine.

Se siete un po&#39; persi, ecco come navigare [!DNL MBI] per recuperare la chiave:

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## Consenti accesso al [!DNL MBI] Indirizzo IP {#allowlist}

Affinché la connessione abbia successo, devi configurare il firewall per consentire l’accesso dai nostri indirizzi IP. Sono `54.88.76.97` e `34.250.211.151` ma sono anche sul `MySQL credentials` pagina. Vedi la scatola blu nel GIF sopra? Tutto qui!

## Creazione di una `Linux` utente per [!DNL MBI] {#linux}

Può trattarsi di una macchina di produzione o secondaria, purché contenga dati in tempo reale (o aggiornati frequentemente). È possibile [limita questo utente](../../../administrator/account-management/restrict-db-access.md) qualsiasi modo tu voglia, purché mantenga il diritto di connettersi al `MySQL` server.

1. Per aggiungere il nuovo utente, esegui i seguenti comandi come root sul tuo `Linux` server:

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. Ricorda `public key` abbiamo recuperato nella prima sezione? Per garantire l&#39;accesso dell&#39;utente al database, è necessario importare la chiave in `authorized\_keys`.

   Copia l’intera chiave nel `authorized\_keys` file come segue:

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. Per terminare la creazione dell&#39;utente, modifica le autorizzazioni di `/home/rjmetric` per consentire l&#39;accesso tramite `SSH`:

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>Se la `sshd\_config` il file associato al server non è impostato sull&#39;opzione predefinita. Solo alcuni utenti avranno accesso al server, il che impedirà la riuscita della connessione a [!DNL MBI]. In questi casi è necessario eseguire un comando come `AllowUsers` consentire `rjmetric` accesso utente al server.

## Creazione di una `MySQL` utente per [!DNL MBI] {#mysql}

La tua organizzazione può richiedere un processo diverso, ma il modo più semplice per creare questo utente è quello di eseguire la seguente query al momento dell&#39;accesso `MySQL` come utente con il diritto di concedere privilegi:

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

Sostituisci `secure password here` con una password sicura, che può essere diversa dalla `SSH` password.

Per impedire all&#39;utente di accedere ai dati in database, tabelle o colonne specifici, è invece possibile eseguire query GRANT che consentono solo l&#39;accesso ai dati consentiti.

## Inserimento della connessione e delle informazioni utente in [!DNL MBI] {#finish}

Per concludere, dobbiamo inserire la connessione e le informazioni utente in [!DNL MBI]. Se ne è andata dalla `MySQL credentials` pagina aperta? In caso contrario, vai a **[!UICONTROL Data** > **Connections]** e fai clic su **[!UICONTROL Add New Data Source]**, quindi l&#39;icona MySQL. non dimenticare di impostare `Encrypted` passa a `Yes`.

Immettere le seguenti informazioni in questa pagina, a partire dalla sezione Connessione al database:

* `Username`: Il nome utente per il [!DNL MBI] Utente MySQL
* `Password`: La password per [!DNL MBI] Utente MySQL
* `Port`: Porta di MySQL sul server (3306 per impostazione predefinita)
* `Host` Per impostazione predefinita, è localhost. In generale, sarà il valore bind-address per il server MySQL, che per impostazione predefinita è `127.0.0.1 (localhost)`, ma potrebbe anche essere un indirizzo di rete locale (ad esempio, `192.168.0.1`) o l&#39;indirizzo IP pubblico del server.

   Il valore si trova nella `my.cnf` file (di solito si trova in `/etc/my.cnf`) sotto la riga che legge `\[mysqld\]`. Se nel file viene commentata la riga dell&#39;indirizzo di binding, il server viene protetto da tentativi di connessione esterni.

In `SSH Connection` sezione:

* `Remote Address`: Indirizzo IP o nome host del server [!DNL MBI] si trasformerà in
* `Username`: Il nome utente per il [!DNL MBI] Utente SSH (Linux)
* `SSH Port`: Porta SSH sul server (22 per impostazione predefinita)

Tutto qui! Al termine, fai clic su **[!UICONTROL Save & Test]** per completare la configurazione.

## Correlati:

* [Riautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
