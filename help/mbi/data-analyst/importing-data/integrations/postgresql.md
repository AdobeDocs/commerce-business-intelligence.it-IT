---
title: Connetti PostgreSQL tramite tunnel SSH
description: Scopri come collegare il database PostgreSQL a [!DNL MBI] attraverso un tunnel SSH.
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 0%

---

# Connetti `PostgreSQL` tramite `SSH` Tunnel

Per collegare `PostgreSQL` database a [!DNL MBI] tramite un `SSH tunnel`, tu (o il tuo team, se non sei un tecnico) devi fare alcune cose:

1. [Recupera il [!DNL MBI] chiave pubblica](#retrieve)
1. [Consenti accesso a [!DNL MBI] Indirizzo IP](#allowlist)
1. [Creare un sistema Linux](#linux)
1. [Creare un utente Postgres per [!DNL MBI] ](#postgres)
1. [Immetti la connessione e le informazioni utente in MBI](#finish)

Non è complicato come potrebbe sembrare. Inizia.

## Recupero di [!DNL MBI] `public key` {#retrieve}

Il `public key` viene utilizzato per autorizzare [!DNL MBI] Utente Linux®. Nella sezione successiva, creerai l’utente e importerai la chiave.

1. Vai a **[!UICONTROL Manage Data** > **Connections]** e fai clic su **[!UICONTROL Add a Data Source]**.
1. Fai clic su `PostgreSQL` icona.
1. Dopo il `PostgreSQL credentials` viene visualizzata la pagina, impostare `Encrypted` passa a `Yes`. Viene visualizzata la `SSH` modulo di configurazione.
1. Il `public key` si trova sotto questo modulo.

Lascia aperta questa pagina per tutta la durata dell’esercitazione: sarà necessario visualizzarla nella sezione successiva e alla fine.

Se sei un po&#39; perso, ecco come navigare [!DNL MBI] per recuperare la chiave:

![Recupero della chiave pubblica RJMetrics](../../../assets/get-mbi-public-key.gif)

## Consenti accesso a [!DNL MBI] Indirizzo IP {#allowlist}

Affinché la connessione abbia esito positivo, è necessario configurare il firewall per consentire l&#39;accesso dall&#39;indirizzo IP. È `54.88.76.97/32`, ma è anche nel `PostgreSQL` pagina delle credenziali. Vedi la casella blu in GIF? Tutto qui!

## Creazione di un `Linux` utente per [!DNL MBI] {#linux}

Può trattarsi di un computer di produzione o secondario, purché contenga dati in tempo reale (o aggiornati di frequente). È possibile [limita questo utente](../../../administrator/account-management/restrict-db-access.md) in qualsiasi modo, purché conservi il diritto di connettersi al server PostgreSQL.

1. Per aggiungere il nuovo utente, eseguire i seguenti comandi come radice sul `Linux` server:

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. Ricorda la `public key` hai recuperato nella prima sezione? Per garantire che l’utente abbia accesso al database, devi importare la chiave in `authorized\_keys`.

   Copia l’intera chiave in `authorized\_keys` file come segue:

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. Per completare la creazione dell&#39;utente, modificare le autorizzazioni per `/home/rjmetric` directory per consentire l&#39;accesso tramite `SSH`:

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
```

>[!IMPORTANT]
>
>Se il `sshd\_config` il file associato al server non è impostato sull&#39;opzione predefinita, solo alcuni utenti dispongono dell&#39;accesso al server. [!DNL MBI]. In questi casi, è necessario eseguire un comando come `AllowUsers` per consentire all&#39;utente rjmetric di accedere al server.

## Creazione di un [!DNL MBI] Utente Postgres {#postgres}

La tua organizzazione potrebbe richiedere un processo diverso, ma il modo più semplice per creare questo utente è quello di eseguire la seguente query quando si accede a Postgres come utente con il diritto di concedere privilegi. L’utente deve anche essere proprietario dello schema che [!DNL MBI] Le è stato concesso l’accesso a.

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

Sostituisci `secure password` con una tua password sicura, che può essere diversa dalla password SSH. Assicurati inoltre di sostituire `database name` e `schema name` con i nomi appropriati nel database.

Se si desidera connettere più database o schemi, ripetere il processo in base alle esigenze.

## Immissione della connessione e delle informazioni utente in [!DNL MBI] {#finish}

Per concludere, devi immettere la connessione e le informazioni utente in [!DNL MBI]. Hai lasciato aperta la pagina delle credenziali PostgreSQL? In caso contrario, vai a **[!UICONTROL Manage Data > Connections]** e fai clic su **[!UICONTROL Add a Data Source]**, quindi l&#39;icona PostgreSQL. Non dimenticare di impostare `Encrypted` passa a `Yes`.

Immettere le seguenti informazioni in questa pagina, a partire dalla sezione Connessione al database:

* `Username`: nome utente RJMetrics Postgres (deve essere rjmetric)
* `Password`: password RJMetrics Postgres
* `Port`: porta PostgreSQL sul server (5432 per impostazione predefinita)
* `Host`: 127.0.0.1

Sotto `SSH Connection`:

* `Remote Address`: indirizzo IP o nome host del server in cui SSH eseguirà l’operazione
* `Username`: nome di accesso SSH (deve essere rjmetric)
* `SSH Port`: porta SSH sul server (22 per impostazione predefinita)

Tutto qui! Al termine, fai clic su **Salva e prova** per completare la configurazione.

### Correlato

* [Reautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
