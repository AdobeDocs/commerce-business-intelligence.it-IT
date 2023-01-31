---
title: Connetti [!DNL MongoDB] tramite tunnel SSH
description: Scopri come connettersi [!DNL MongoDB] tramite tunnel SSH.
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# Connetti [!DNL MongoDB] tramite tunnel SSH


Per collegare il [!DNL MongoDB] database a [!DNL MBI] tramite un tunnel SSH, dovrai fare alcune cose (o il tuo team, se non sei un tecnico):

1. [Recupera il [!DNL MBI] chiave pubblica](#retrieve)
1. [Consenti accesso al [!DNL MBI] Indirizzo IP](#allowlist)
1. [Creare un utente Linux per MBI](#linux)
1. [Crea un [!DNL MongoDB] utente per MBI](#mongodb)
1. [Immetti la connessione e le informazioni utente in [!DNL MBI]](#finish)

>[!NOTE]
>
>A causa della natura tecnica di questa configurazione, ti consigliamo di eseguire un ciclo in uno sviluppatore per aiutarti se non lo hai fatto prima.

## Recupero del [!DNL MBI] chiave pubblica {#retrieve}

La `public key` viene utilizzato per autorizzare [!DNL MBI] `Linux` utente. Nella sezione successiva, creiamo l’utente e importiamo la chiave.

1. Vai a **[!UICONTROL Data** > **Connections]** e fai clic su **[!UICONTROL Add New Data Source]**.
1. Fai clic sul pulsante [!DNL MONGODB] icona.
1. Dopo la [!DNL MongoDB] si apre la pagina delle credenziali, modifica `Encrypted` passa a `Yes`. Verrà visualizzato il modulo di configurazione SSH.
1. La `public key` si trova sotto questo modulo.

Lascia aperta questa pagina per l’intera esercitazione; sarà necessario nella sezione successiva e alla fine.

Se siete un po &#39;persi, Ecco come navigare attraverso [!DNL MBI] per recuperare la chiave:

![Recupero della chiave pubblica RJMetrics](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## Consenti accesso al [!DNL MBI] Indirizzo IP {#allowlist}

Affinché la connessione abbia successo, devi configurare il firewall per consentire l’accesso dai nostri indirizzi IP. Sono `54.88.76.97` e `34.250.211.151`, ma è anche sul [!DNL MongoDB] pagina delle credenziali:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Creazione di una `Linux` utente per [!DNL MBI] {#linux}

>[!IMPORTANT]
>
>Se la `sshd_config` il file associato al server non è impostato sull&#39;opzione predefinita. Solo alcuni utenti avranno accesso al server, il che impedirà la riuscita della connessione a [!DNL MBI]. In questi casi è necessario eseguire un comando come `AllowUsers` consentire `rjmetric` accesso utente al server.

Può trattarsi di una macchina di produzione o secondaria, purché contenga dati in tempo reale (o aggiornati frequentemente). È possibile limitare l&#39;utente in qualsiasi modo si desideri purché mantenga il diritto di connettersi al [!DNL MongoDB] server.

Per aggiungere il nuovo utente, esegui i seguenti comandi come root sul tuo `Linux` server:

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

Ricorda `public key` abbiamo recuperato nella prima sezione? Per garantire l&#39;accesso dell&#39;utente al database, è necessario importare la chiave in `authorized_keys`. Copia l’intera chiave nel `authorized_keys` file come segue:

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

Per terminare la creazione dell&#39;utente, modifica le autorizzazioni nella directory /home/rjmetric per consentire l&#39;accesso tramite SSH:

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## Creazione di un [!DNL MBI] [!DNL MongoDB] user {#mongodb}

[!DNL MongoDB] i server dispongono di due modalità di esecuzione: [con l’opzione &quot;auth&quot;](#auth) `(mongod -- auth)` e uno senza [predefinito](#default). Passaggi per la creazione di un [!DNL MongoDB] l&#39;utente può variare a seconda della modalità utilizzata dal server, quindi assicurati di verificare la modalità prima di continuare.

### Se il server utilizza `Auth` Opzione: {#auth}

Quando ti connetti a più database, puoi aggiungere l&#39;utente accedendo a [!DNL MongoDB] come utente amministratore ed esegui i seguenti comandi.

>[!NOTE]
>
>Per visualizzare tutti i database disponibili, è necessario [!DNL MBI] l&#39;utente richiede le autorizzazioni per eseguire `listDatabases.`

Questo comando concederà la [!DNL MBI] accesso utente `to all databases`:

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

Usa questo comando per concedere il [!DNL MBI] accesso utente `to a single database`:

```bash
    use < database name >
    db.createUser('rjmetric', '< secure password here >', true)
```

Verrà stampata una risposta simile alla seguente:

```bash
    {
    "id": ObjectId("< some object id here >"),
    "user": "rjmetric",
    "readOnly": true,
    "pwd": "< some hash here >"
    }
```

### Se il server utilizza l’opzione predefinita {#default}

Se il server non utilizza `auth` modalità [!DNL MongoDB] il server sarà ancora accessibile anche senza un nome utente e una password. Tuttavia, assicurati che `mongodb.conf` file `(/etc/mongodb.conf)` dispone delle seguenti righe - in caso contrario, riavvia il server dopo averle aggiunte.

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

Per eseguire un binding [!DNL MongoDB] su un indirizzo diverso, regola di conseguenza il nome host del database nel passaggio successivo.

## Inserimento della connessione e delle informazioni utente in [!DNL MBI] {#finish}

Per concludere, dobbiamo inserire la connessione e le informazioni utente in [!DNL MBI]. Se ne è andata dalla [!DNL MongoDB] pagina delle credenziali aperta? In caso contrario, vai a **[!UICONTROL Data > Connections]** e fai clic su **[!UICONTROL Add New Data Source]**, quindi [!DNL MongoDB] icona. non dimenticare di modificare le `Encrypted` passa a `Yes`.

Immetti le seguenti informazioni in questa pagina, a partire dal `Database Connection` sezione:

* `Host`: `127.0.0.1`
* `Username`: La [!DNL MBI] [!DNL MongoDB] username (deve essere `rjmetric`)
* `Password`: La [!DNL MBI] [!DNL MongoDB] password
* `Port`: Porta MongoDB sul server (`27017` per impostazione predefinita)
* `Database Name` (Facoltativo): Se si consente l&#39;accesso a un solo database, specificare il nome del database.

Sotto la `SSH Connection` sezione:

* `Remote Address`: L’indirizzo IP o il nome host del server in cui verrà eseguito il SSH
* `Username`: La [!DNL MBI] Nome utente Linux (SSH) (dovrebbe essere jmetric)
* `SSH Port`: La porta SSH sul server (22 per impostazione predefinita)

Tutto qui! Al termine, fai clic su **[!UICONTROL Save Test]** per completare la configurazione.

### Correlati

* [Riautenticazione delle integrazioni](https://support.magento.com/hc/en-us/articles/360016733151)
