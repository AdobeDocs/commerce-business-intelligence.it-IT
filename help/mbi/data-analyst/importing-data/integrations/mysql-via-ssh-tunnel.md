---
title: Connessione in corso  [!DNL MySQL]  tramite tunnel SSH
description: Scopri come connettersi [!DNL MySQL] tramite tunnel SSH.
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# Connetti [!DNL MySQL] tramite [!DNL SSH Tunnel]

* [Recupera la chiave pubblica  [!DNL Commerce Intelligence] ](#retrieve)
* [Consenti accesso all&#39;indirizzo IP  [!DNL Commerce Intelligence] ](#allowlist)
* [Crea un utente Linux per  [!DNL Commerce Intelligence]](#linux)
* [Crea un  [!DNL MySQL]  utente per  [!DNL Commerce Intelligence]](#mysql)
* [Immetti la connessione e le informazioni utente in  [!DNL Commerce Intelligence]](#finish)

## PASSA A

* [[!DNL MySQL] tramite ](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL MySQL] tramite [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

Per connettere il database [!DNL MySQL] a [!DNL Commerce Intelligence] tramite `SSH tunnel`, è necessario eseguire alcune operazioni:

1. Recupera [!DNL Commerce Intelligence] `public key`
1. Consenti accesso a [!DNL Commerce Intelligence] `IP address`
1. Crea un utente `Linux` per [!DNL Commerce Intelligence]
1. Crea un utente `MySQL` per [!DNL Commerce Intelligence]
1. Immettere la connessione e le informazioni utente in [!DNL Commerce Intelligence]


## Recupero della chiave pubblica [!DNL Commerce Intelligence] {#retrieve}

`public key` viene utilizzato per autorizzare l&#39;utente [!DNL Commerce Intelligence] `Linux`. Nella sezione successiva, creerai l’utente e importerai la chiave.

1. Vai a **[!UICONTROL Manage Data** > **Connections]** e fai clic su **[!UICONTROL Add New Data Source]**.
1. Fare clic sull&#39;icona `MySQL`.
1. Dopo l&#39;apertura della pagina `MySQL credentials`, impostare `Encrypted` su `Yes`. Viene visualizzato il modulo di configurazione SSH.
1. `public key` si trova sotto questo modulo.

Lascia aperta questa pagina per tutta la durata dell’esercitazione: sarà necessario visualizzarla nella sezione successiva e alla fine.

Ecco come navigare in [!DNL Commerce Intelligence] per recuperare la chiave:

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## Consenti accesso all&#39;indirizzo IP [!DNL Commerce Intelligence] {#allowlist}

Affinché la connessione abbia esito positivo, è necessario configurare il firewall per consentire l&#39;accesso dagli indirizzi IP. Sono `54.88.76.97` e `34.250.211.151` ma si trovano anche nella pagina `MySQL credentials`. Vedi la casella blu in GIF.

## Creazione di un utente [!DNL Linux] per [!DNL Commerce Intelligence] {#linux}

Può trattarsi di un computer di produzione o secondario, purché contenga dati in tempo reale (o aggiornati di frequente). È possibile [limitare l&#39;utente](../../../administrator/account-management/restrict-db-access.md) in qualsiasi modo, purché conservi il diritto di connettersi al server `MySQL`.

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
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>Se il file `sshd\_config` associato al server non è impostato sull&#39;opzione predefinita, solo alcuni utenti dispongono dell&#39;accesso al server. Ciò impedisce la connessione a [!DNL Commerce Intelligence]. In questi casi, è necessario eseguire un comando come `AllowUsers` per consentire all&#39;utente `rjmetric` di accedere al server.

## Creazione di un utente [!DNL MySQL] per [!DNL Commerce Intelligence] {#mysql}

La tua organizzazione potrebbe richiedere un processo diverso, ma il modo più semplice per creare questo utente è quello di eseguire la seguente query quando si è connessi a [!DNL MySQL] come utente con il diritto di concedere privilegi:

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

Sostituire `secure password here` con una password sicura, che può essere diversa dalla password `SSH`.

Per impedire a questo utente di accedere ai dati in database, tabelle o colonne specifiche, è invece possibile eseguire query GRANT che consentono solo l&#39;accesso ai dati consentiti.

## Immissione della connessione e delle informazioni utente in [!DNL Commerce Intelligence] {#finish}

Per concludere, devi immettere la connessione e le informazioni utente in [!DNL Commerce Intelligence]. Hai lasciato aperta la pagina `MySQL credentials`? In caso contrario, passare a **[!UICONTROL Data** > **Connections]** e fare clic su **[!UICONTROL Add New Data Source]**, quindi sull&#39;icona [!DNL MySQL]. Non dimenticare di impostare `Encrypted` su `Yes`.

Immettere le informazioni seguenti in questa pagina, a partire dalla sezione `Database Connection`:

* `Username`: nome utente per l&#39;utente [!DNL Commerce Intelligence] [!DNL MySQL]
* `Password`: password per l&#39;utente [!DNL Commerce Intelligence] [!DNL MySQL]
* `Port`: [!DNL MySQL] porta sul server (3306 per impostazione predefinita)
* `Host` Per impostazione predefinita, è localhost. In generale, si tratta del valore di indirizzo di binding per il server [!DNL MySQL], che per impostazione predefinita è `127.0.0.1 (localhost)`, ma potrebbe anche essere un indirizzo di rete locale (ad esempio, `192.168.0.1`) o l&#39;indirizzo IP pubblico del server.

  Il valore si trova nel file `my.cnf` (che si trova in `/etc/my.cnf`) sotto la riga che recita `\[mysqld\]`. Se la riga dell&#39;indirizzo di associazione viene inserita come commento in tale file, il server viene protetto dai tentativi di connessione esterni.

Nella sezione `SSH Connection`:

* `Remote Address`: l&#39;indirizzo IP o il nome host del server [!DNL Commerce Intelligence] verrà sottoposto a tunneling in
* `Username`: nome utente per l&#39;utente SSH ([!DNL Linux]) di [!DNL Commerce Intelligence]
* `SSH Port`: porta SSH sul server (22 per impostazione predefinita)

Al termine, fare clic su **[!UICONTROL Save & Test]** per completare la configurazione.

## Correlato:

* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
