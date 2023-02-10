---
title: Connetti PostgreSQL tramite tunnel SSH
description: Scopri come collegare il database PostgreSQL a [!DNL MBI] tramite un tunnel SSH.
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# Connetti `PostgreSQL` tramite `SSH` Tunnel

Per collegare il `PostgreSQL` database a [!DNL MBI] tramite `SSH tunnel`, tu (o il tuo team, se non sei un tecnico) dovrai fare alcune cose:

1. [Recupera il [!DNL MBI] chiave pubblica](#retrieve)
1. [Consenti accesso al [!DNL MBI] Indirizzo IP](#allowlist)
1. [Creare un utente Linux per [!DNL MBI] ](#linux)
1. [Creare un utente di Postgres per [!DNL MBI] ](#postgres)
1. [Immettere la connessione e le informazioni utente in MBI](#finish)

Non è complicato come potrebbe sembrare. Inizia.

## Recupero del [!DNL MBI] `public key` {#retrieve}

La `public key` viene utilizzato per autorizzare [!DNL MBI] Utente Linux. Nella sezione successiva, creeremo l’utente e importeremo la chiave.

1. Vai a **[!UICONTROL Manage Data** > **Connections]** e fai clic su **[!UICONTROL Add a Data Source]**.
1. Fai clic sul pulsante `PostgreSQL` icona.
1. Dopo la `PostgreSQL credentials` si apre la pagina, imposta `Encrypted` passa a `Yes`. Verrà visualizzata la `SSH` modulo di installazione.
1. La `public key` si trova sotto questo modulo.

Lascia aperta questa pagina per l’intera esercitazione; sarà necessario nella sezione successiva e alla fine.

Se siete un po&#39; persi, questo è come navigare [!DNL MBI] per recuperare la chiave:

![Recupero della chiave pubblica RJMetrics](../../../assets/get-mbi-public-key.gif)

## Consenti accesso al [!DNL MBI] Indirizzo IP {#allowlist}

Affinché la connessione abbia successo, devi configurare il firewall per consentire l’accesso dal nostro indirizzo IP. è `54.88.76.97/32`, ma è anche sul `PostgreSQL` pagina delle credenziali. Vedi la scatola blu nel GIF sopra? Tutto qui!

## Creazione di una `Linux` utente per [!DNL MBI] {#linux}

Può trattarsi di una macchina di produzione o secondaria, purché contenga dati in tempo reale (o aggiornati frequentemente). È possibile [limita questo utente](../../../administrator/account-management/restrict-db-access.md) qualsiasi modo tu voglia, purché mantenga il diritto di connettersi al server PostgreSQL.

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
```

>[!IMPORTANT]
>
>Se la `sshd\_config` il file associato al server non è impostato sull&#39;opzione predefinita. Solo alcuni utenti avranno accesso al server, il che impedirà la riuscita della connessione a [!DNL MBI]. In questi casi è necessario eseguire un comando come `AllowUsers` per consentire all’utente jmetric di accedere al server.

## Creazione di un [!DNL MBI] Utente dei post {#postgres}

La tua organizzazione può richiedere un processo diverso, ma il modo più semplice per creare questo utente è quello di eseguire la seguente query quando hai effettuato l’accesso a Postgres come utente con il diritto di concedere privilegi. L&#39;utente deve anche possedere lo schema che [!DNL MBI] viene concesso l&#39;accesso a.

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

Sostituisci `secure password` con la tua password sicura, che può essere diversa dalla password SSH. Inoltre, assicurati di sostituire `database name` e `schema name` con i nomi appropriati nel database.

Se si desidera collegare più database o schemi, ripetere il processo se necessario.

## Inserimento della connessione e delle informazioni utente in [!DNL MBI] {#finish}

Per concludere, dobbiamo inserire la connessione e le informazioni utente in [!DNL MBI]. Hai lasciato aperta la pagina delle credenziali PostgreSQL? In caso contrario, vai a **[!UICONTROL Manage Data > Connections]** e fai clic su **[!UICONTROL Add a Data Source]**, quindi l&#39;icona PostgreSQL. Non dimenticare di impostare il `Encrypted` passa a `Yes`.

Immettere le seguenti informazioni in questa pagina, a partire dalla sezione Connessione al database:

* `Username`: Nome utente RJMetrics Postgres (deve essere jmetric)
* `Password`: Password RJMetrics Postgres
* `Port`: Porta PostgreSQL sul server (5432 per impostazione predefinita)
* `Host`: 127.0.0.1

Sotto `SSH Connection`:

* `Remote Address`: L’indirizzo IP o il nome host del server in cui verrà eseguito il SSH
* `Username`: Il nostro nome di accesso SSH (dovrebbe essere jmetric)
* `SSH Port`: Porta SSH sul server (22 per impostazione predefinita)

Tutto qui! Al termine, fai clic su **Salva e prova** per completare la configurazione.

### Correlati

* [Riautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
