---
title: Connetti [!DNL MongoDB] tramite tunnel SSH
description: Scopri come connetterti [!DNL MongoDB] attraverso il tunnel SSH.
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# Connetti [!DNL MongoDB] tramite tunnel SSH

Per collegare [!DNL MongoDB] database a [!DNL Commerce Intelligence] tramite un tunnel SSH, è necessario eseguire alcune operazioni:

1. [Recupera il [!DNL Commerce Intelligence] chiave pubblica](#retrieve)
1. [Consenti accesso a [!DNL Commerce Intelligence] Indirizzo IP](#allowlist)
1. [Creare un utente Linux per Commerce Intelligence](#linux)
1. [Creare un [!DNL MongoDB] utente per Commerce Intelligence](#mongodb)
1. [Immetti la connessione e le informazioni utente in [!DNL Commerce Intelligence]](#finish)

>[!NOTE]
>
>A causa della natura tecnica di questa configurazione, Adobe consiglia di effettuare il loop in uno sviluppatore per aiutare se non l’hai già fatto.

## Recupero di [!DNL Commerce Intelligence] chiave pubblica {#retrieve}

Il `public key` viene utilizzato per autorizzare [!DNL Commerce Intelligence] `Linux` utente. La sezione successiva illustra come creare l’utente e importare le chiavi.

1. Vai a **[!UICONTROL Data** > **Connections]** e fai clic su **[!UICONTROL Add New Data Source]**.
1. Fai clic su [!DNL MONGODB] icona.
1. Dopo il [!DNL MongoDB] viene visualizzata la pagina delle credenziali, modificare la `Encrypted` passa a `Yes`. Viene visualizzato il modulo di configurazione SSH.
1. Il `public key` si trova sotto questo modulo.

Lascia aperta questa pagina per tutta la durata dell’esercitazione: sarà necessario visualizzarla nella sezione successiva e alla fine.

Se sei un po&#39; perso, ecco come navigare attraverso [!DNL Commerce Intelligence] per recuperare la chiave:

![Recupero della chiave pubblica RJMetrics](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## Consenti accesso a [!DNL Commerce Intelligence] Indirizzo IP {#allowlist}

Affinché la connessione abbia esito positivo, è necessario configurare il firewall per consentire l&#39;accesso dagli indirizzi IP. Sono `54.88.76.97` e `34.250.211.151`, ma è anche nel [!DNL MongoDB] pagina credenziali:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Creazione di un `Linux` utente per [!DNL Commerce Intelligence] {#linux}

>[!IMPORTANT]
>
>Se il `sshd_config` il file associato al server non è impostato sull&#39;opzione predefinita, solo alcuni utenti dispongono dell&#39;accesso al server. [!DNL Commerce Intelligence]. In questi casi, è necessario eseguire un comando come `AllowUsers` per consentire `rjmetric` accesso utente al server.

Può trattarsi di un computer di produzione o secondario, purché contenga dati in tempo reale (o aggiornati di frequente). Puoi limitare questo utente come preferisci, purché mantenga il diritto di connessione al [!DNL MongoDB] server.

Per aggiungere il nuovo utente, eseguire i seguenti comandi come radice sul `Linux` server:

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

Ricorda la `public key` hai recuperato nella prima sezione? Per garantire che l’utente abbia accesso al database, devi importare la chiave in `authorized_keys`. Copia l’intera chiave in `authorized_keys` file come segue:

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

Per completare la creazione dell’utente, modifica le autorizzazioni nella directory /home/rjmetric per consentire l’accesso tramite SSH:

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## Creazione di un [!DNL Commerce Intelligence] [!DNL MongoDB] utente {#mongodb}

[!DNL MongoDB] i server dispongono di due modalità di esecuzione: [uno con l’opzione &quot;auth&quot;](#auth) `(mongod -- auth)` e uno senza, [che è il valore predefinito](#default). I passaggi per la creazione di un [!DNL MongoDB] varia a seconda della modalità utilizzata dal server. Verifica la modalità prima di continuare.

### Se il server utilizza `Auth` Opzione: {#auth}

Quando ci si connette a più database, è possibile aggiungere l&#39;utente accedendo a [!DNL MongoDB] come utente amministratore ed eseguendo i seguenti comandi.

>[!NOTE]
>
>Per visualizzare tutti i database disponibili, [!DNL Commerce Intelligence] l&#39;utente richiede le autorizzazioni per eseguire `listDatabases.`

Questo comando concede il [!DNL Commerce Intelligence] accesso utente `to all databases`:

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

Utilizzare questo comando per concedere [!DNL Commerce Intelligence] accesso utente `to a single database`:

```bash
    use < database name >
    db.createUser('rjmetric', '< secure password here >', true)
```

In questo modo viene stampata una risposta simile alla seguente:

```bash
    {
    "id": ObjectId("< some object id here >"),
    "user": "rjmetric",
    "readOnly": true,
    "pwd": "< some hash here >"
    }
```

### Se il server utilizza l&#39;opzione predefinita {#default}

Se il server non utilizza `auth` modalità, il tuo [!DNL MongoDB] è accessibile anche senza nome utente e password. Tuttavia, è necessario assicurarsi che `mongodb.conf` file `(/etc/mongodb.conf)` contiene le righe seguenti. In caso contrario, riavviare il server dopo averle aggiunte.

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

Per associare il [!DNL MongoDB] a un indirizzo diverso, regola di conseguenza il nome host del database nel passaggio successivo.

## Immissione della connessione e delle informazioni utente in [!DNL Commerce Intelligence] {#finish}

Per concludere, devi immettere la connessione e le informazioni utente in [!DNL Commerce Intelligence]. Hai lasciato il [!DNL MongoDB] la pagina delle credenziali è aperta? In caso contrario, vai a **[!UICONTROL Data > Connections]** e fai clic su **[!UICONTROL Add New Data Source]**, quindi [!DNL MongoDB] icona. Non dimenticare di modificare il `Encrypted` passa a `Yes`.

Immetti le seguenti informazioni in questa pagina, iniziando da `Database Connection` sezione:

* `Host`: `127.0.0.1`
* `Username`: Il [!DNL Commerce Intelligence] [!DNL MongoDB] nome utente (deve essere `rjmetric`)
* `Password`: Il [!DNL Commerce Intelligence] [!DNL MongoDB] password
* `Port`: porta di MongoDB sul server (`27017` per impostazione predefinita)
* `Database Name` (Facoltativo): se è stato consentito l&#39;accesso a un solo database, specificare il nome del database.

Sotto `SSH Connection` sezione:

* `Remote Address`: indirizzo IP o nome host del server in cui SSH eseguirà l’operazione
* `Username`: Il [!DNL Commerce Intelligence] Nome utente Linux (SSH) (deve essere rjmetric)
* `SSH Port`: porta SSH sul server (22 per impostazione predefinita)

Al termine, fai clic su **[!UICONTROL Save Test]** per completare la configurazione.

### Correlato

* [Reautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
