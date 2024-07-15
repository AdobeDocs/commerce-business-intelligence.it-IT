---
title: Connetti PostgreSQL tramite tunnel SSH
description: Scopri come collegare il database PostgreSQL a Commerce Intelligence tramite un tunnel SSH.
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# Connetti [!DNL PostgreSQL] tramite [!DNL SSH Tunnel]

Per connettere il database [!DNL PostgreSQL] a [!DNL Commerce Intelligence] tramite `SSH tunnel`, è necessario eseguire alcune operazioni:

1. [Recupera la chiave pubblica  [!DNL Commerce Intelligence] ](#retrieve)
1. [Consenti accesso all&#39;indirizzo IP  [!DNL Commerce Intelligence] ](#allowlist)
1. [Crea un  [!DNL Linux]  utente per  [!DNL Commerce Intelligence]](#linux)
1. [Crea un  [!DNL PostgreSQL]  utente per  [!DNL Commerce Intelligence]](#postgres)
1. [Immetti la connessione e le informazioni utente in  [!DNL Commerce Intelligence]](#finish)

## Recupero di [!DNL Commerce Intelligence] [!DNL public key] {#retrieve}

`public key` viene utilizzato per autorizzare l&#39;utente [!DNL Commerce Intelligence] [!DNL Linux]. Ora puoi creare l’utente e importare la chiave.

1. Vai a **[!UICONTROL Manage Data** > **Connections]** e fai clic su **[!UICONTROL Add a Data Source]**.
1. Fare clic sull&#39;icona [!DNL PostgreSQL].
1. Dopo l&#39;apertura della pagina `PostgreSQL credentials`, impostare `Encrypted` su `Yes`. Verrà visualizzato il modulo di installazione di `SSH`.
1. `public key` si trova sotto questo modulo.

Lascia aperta questa pagina per tutta la durata dell’esercitazione: sarà necessario visualizzarla nella sezione successiva e alla fine.

Di seguito viene illustrato come spostarsi in [!DNL Commerce Intelligence] per recuperare la chiave:

![Recupero della chiave pubblica RJMetrics](../../../assets/get-mbi-public-key.gif)

## Consenti accesso all&#39;indirizzo IP [!DNL Commerce Intelligence] {#allowlist}

Affinché la connessione abbia esito positivo, è necessario configurare il firewall per consentire l&#39;accesso dall&#39;indirizzo IP. È `54.88.76.97/32`, ma si trova anche nella pagina delle credenziali di `PostgreSQL`. Vedi la casella blu in GIF.

## Creazione di un utente [!DNL Linux] per [!DNL Commerce Intelligence] {#linux}

Può trattarsi di un computer di produzione o secondario, purché contenga dati in tempo reale (o aggiornati di frequente). È possibile [limitare l&#39;utente](../../../administrator/account-management/restrict-db-access.md) in qualsiasi modo, purché conservi il diritto di connettersi al server [!DNL PostgreSQL].

1. Per aggiungere il nuovo utente, eseguire i comandi seguenti come radice nel server [!DNL Linux]:

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. Ricordi `public key` recuperato nella prima sezione? Per assicurarsi che l&#39;utente abbia accesso al database, è necessario importare la chiave in `authorized\_keys`.

   Copiare l&#39;intera chiave nel file `authorized\_keys` come segue:

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. Per completare la creazione dell&#39;utente, modificare le autorizzazioni nella directory `/home/rjmetric` per consentire l&#39;accesso tramite `SSH`:

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
```

>[!IMPORTANT]
>
>Se il file `sshd\_config` associato al server non è impostato sull&#39;opzione predefinita, solo alcuni utenti dispongono dell&#39;accesso al server. Ciò impedisce la connessione a [!DNL Commerce Intelligence]. In questi casi, è necessario eseguire un comando come `AllowUsers` per consentire all&#39;utente rjmetric di accedere al server.

## Creazione di un utente [!DNL Commerce Intelligence] [!DNL Postgres] {#postgres}

La tua organizzazione potrebbe richiedere un processo diverso, ma il modo più semplice per creare questo utente è quello di eseguire la seguente query quando si accede a Postgres come utente con il diritto di concedere privilegi. L&#39;utente deve inoltre essere proprietario dello schema a cui è concesso l&#39;accesso a [!DNL Commerce Intelligence].

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

Sostituisci `secure password` con la tua password sicura, che può essere diversa dalla password SSH. Assicurarsi inoltre di sostituire `database name` e `schema name` con i nomi appropriati nel database.

Se si desidera connettere più database o schemi, ripetere il processo in base alle esigenze.

## Immissione della connessione e delle informazioni utente in [!DNL Commerce Intelligence] {#finish}

Per concludere, devi immettere la connessione e le informazioni utente in [!DNL Commerce Intelligence]. Hai lasciato aperta la pagina delle credenziali di [!DNL PostgreSQL]? In caso contrario, passare a **[!UICONTROL Manage Data > Connections]** e fare clic su **[!UICONTROL Add a Data Source]**, quindi sull&#39;icona [!DNL PostgreSQL]. Non dimenticare di impostare `Encrypted` su `Yes`.

Immettere le informazioni seguenti in questa pagina, a partire dalla sezione `Database Connection`:

* `Username`: nome utente RJMetrics Postgres (deve essere rjmetric)
* `Password`: password RJMetrics Postgres
* `Port`: porta PostgreSQL sul server (5432 per impostazione predefinita)
* `Host`: 127.0.0.1

In `SSH Connection`:

* `Remote Address`: indirizzo IP o nome host del server in cui verrà eseguito SSH
* `Username`: nome di accesso SSH (deve essere rjmetric)
* `SSH Port`: porta SSH sul server (22 per impostazione predefinita)

Al termine, fare clic su **Salva e prova** per completare l&#39;installazione.

### Correlato

* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
