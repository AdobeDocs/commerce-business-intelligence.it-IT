---
title: Connetti [!DNL MongoDB] tramite tunnel SSH
description: Scopri come connettersi [!DNL MongoDB] tramite tunnel SSH.
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 0%

---

# Connetti [!DNL MongoDB] tramite tunnel SSH

Per connettere il database [!DNL MongoDB] a [!DNL Commerce Intelligence] tramite un tunnel SSH, è necessario eseguire alcune operazioni:

1. [Recupera la chiave pubblica  [!DNL Commerce Intelligence] &#x200B;](#retrieve)
1. [Consenti accesso all&#39;indirizzo IP  [!DNL Commerce Intelligence] &#x200B;](#allowlist)
1. [Creare un utente Linux per Commerce Intelligence](#linux)
1. [Crea un utente  [!DNL MongoDB]  per Commerce Intelligence](#mongodb)
1. [Immetti la connessione e le informazioni utente in  [!DNL Commerce Intelligence]](#finish)

>[!NOTE]
>
>A causa della natura tecnica di questa configurazione, Adobe consiglia di effettuare il loop in uno sviluppatore per fornire assistenza, se non l’hai già fatto.

## Recupero della chiave pubblica [!DNL Commerce Intelligence] {#retrieve}

`public key` viene utilizzato per autorizzare l&#39;utente [!DNL Commerce Intelligence] `Linux`. La sezione successiva illustra come creare l’utente e importare le chiavi.

1. Vai a **[!UICONTROL Data** > **Connections]** e fai clic su **[!UICONTROL Add New Data Source]**.
1. Fare clic sull&#39;icona [!DNL MONGODB].
1. Una volta aperta la pagina delle credenziali [!DNL MongoDB], cambiare `Encrypted` in `Yes`. Viene visualizzato il modulo di configurazione SSH.
1. `public key` si trova sotto questo modulo.

Lascia aperta questa pagina per tutta la durata dell’esercitazione: sarà necessario visualizzarla nella sezione successiva e alla fine.

Se sei un po&#39; perso, ecco come navigare in [!DNL Commerce Intelligence] per recuperare la chiave:

![Recupero della chiave pubblica RJMetrics](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## Consenti accesso all&#39;indirizzo IP [!DNL Commerce Intelligence] {#allowlist}

Affinché la connessione abbia esito positivo, è necessario configurare il firewall per consentire l&#39;accesso dagli indirizzi IP. Sono `54.88.76.97` e `34.250.211.151`, ma si trova anche nella pagina delle credenziali di [!DNL MongoDB]:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Creazione di un utente `Linux` per [!DNL Commerce Intelligence] {#linux}

>[!IMPORTANT]
>
>Se il file `sshd_config` associato al server non è impostato sull&#39;opzione predefinita, solo alcuni utenti dispongono dell&#39;accesso al server. Ciò impedisce la connessione a [!DNL Commerce Intelligence]. In questi casi, è necessario eseguire un comando come `AllowUsers` per consentire all&#39;utente `rjmetric` di accedere al server.

Può trattarsi di un computer di produzione o secondario, purché contenga dati in tempo reale (o aggiornati di frequente). È possibile limitare questo utente in qualsiasi modo, purché conservi il diritto di connettersi al server [!DNL MongoDB].

Per aggiungere il nuovo utente, eseguire i comandi seguenti come radice nel server `Linux`:

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

Ricordi `public key` recuperato nella prima sezione? Per assicurarsi che l&#39;utente abbia accesso al database, è necessario importare la chiave in `authorized_keys`. Copiare l&#39;intera chiave nel file `authorized_keys` come segue:

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

Per completare la creazione dell’utente, modifica le autorizzazioni nella directory /home/rjmetric per consentire l’accesso tramite SSH:

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## Creazione di un utente [!DNL Commerce Intelligence] [!DNL MongoDB] {#mongodb}

I server [!DNL MongoDB] dispongono di due modalità di esecuzione: [una con opzione &quot;auth&quot;](#auth) `(mongod -- auth)` e una senza, [che è l&#39;impostazione predefinita](#default). I passaggi per la creazione di un utente [!DNL MongoDB] variano a seconda della modalità utilizzata dal server. Verifica la modalità prima di continuare.

### Se il server utilizza l&#39;opzione `Auth`: {#auth}

Quando ci si connette a più database, è possibile aggiungere l&#39;utente accedendo a [!DNL MongoDB] come utente amministratore ed eseguendo i seguenti comandi.

>[!NOTE]
>
>Per visualizzare tutti i database disponibili, l&#39;utente [!DNL Commerce Intelligence] richiede le autorizzazioni per eseguire `listDatabases.`

Questo comando concede all&#39;utente [!DNL Commerce Intelligence] l&#39;accesso `to all databases`:

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

Utilizzare questo comando per concedere all&#39;utente [!DNL Commerce Intelligence] l&#39;accesso `to a single database`:

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

Se il server non utilizza la modalità `auth`, il server [!DNL MongoDB] sarà accessibile anche senza nome utente e password. Verificare tuttavia che il file `mongodb.conf` `(/etc/mongodb.conf)` contenga le righe seguenti. In caso contrario, riavviare il server dopo averlo aggiunto.

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

Per associare il server [!DNL MongoDB] a un indirizzo diverso, modificare di conseguenza il nome host del database nel passaggio successivo.

## Immissione della connessione e delle informazioni utente in [!DNL Commerce Intelligence] {#finish}

Per concludere, devi immettere la connessione e le informazioni utente in [!DNL Commerce Intelligence]. Hai lasciato aperta la pagina delle credenziali di [!DNL MongoDB]? In caso contrario, passare a **[!UICONTROL Data > Connections]** e fare clic su **[!UICONTROL Add New Data Source]**, quindi sull&#39;icona [!DNL MongoDB]. Non dimenticare di cambiare `Encrypted` in `Yes`.

Immettere le informazioni seguenti in questa pagina, a partire dalla sezione `Database Connection`:

* `Host`: `127.0.0.1`
* `Username`: nome utente [!DNL Commerce Intelligence] [!DNL MongoDB] (deve essere `rjmetric`)
* `Password`: la password [!DNL Commerce Intelligence] [!DNL MongoDB]
* `Port`: porta di MongoDB sul server (`27017` per impostazione predefinita)
* `Database Name` (facoltativo): se è stato consentito l&#39;accesso a un solo database, specificare il nome del database.

Nella sezione `SSH Connection`:

* `Remote Address`: indirizzo IP o nome host del server in cui verrà eseguito SSH
* `Username`: nome utente [!DNL Commerce Intelligence] Linux (SSH) (deve essere rjmetric)
* `SSH Port`: la porta SSH sul server (22 per impostazione predefinita)

Al termine, fare clic su **[!UICONTROL Save Test]** per completare la configurazione.

### Correlato

* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=it)
