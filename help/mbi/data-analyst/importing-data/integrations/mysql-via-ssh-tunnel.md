---
title: Connessione [!DNL MySQL] tramite tunnel SSH
description: Scopri come connetterti [!DNL MySQL] tramite tunnel SSH.
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# Connetti [!DNL MySQL] tramite [!DNL SSH Tunnel]

* [Recupera il [!DNL Commerce Intelligence] chiave pubblica](#retrieve)
* [Consenti accesso a [!DNL Commerce Intelligence] Indirizzo IP](#allowlist)
* [Creare un utente Linux per [!DNL Commerce Intelligence]](#linux)
* [Creare un [!DNL MySQL] utente per [!DNL Commerce Intelligence]](#mysql)
* [Immetti la connessione e le informazioni utente in [!DNL Commerce Intelligence]](#finish)

## PASSA A

* [[!DNL MySQL] tramite ](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL MySQL] tramite [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

Per collegare [!DNL MySQL] database a [!DNL Commerce Intelligence] tramite un `SSH tunnel`, è necessario eseguire alcune operazioni:

1. Recupera il [!DNL Commerce Intelligence] `public key`
1. Consenti accesso a [!DNL Commerce Intelligence] `IP address`
1. Creare un `Linux` utente per [!DNL Commerce Intelligence]
1. Creare un `MySQL` utente per [!DNL Commerce Intelligence]
1. Immetti la connessione e le informazioni utente in [!DNL Commerce Intelligence]


## Recupero di [!DNL Commerce Intelligence] chiave pubblica {#retrieve}

Il `public key` viene utilizzato per autorizzare [!DNL Commerce Intelligence] `Linux` utente. Nella sezione successiva, creerai l’utente e importerai la chiave.

1. Vai a **[!UICONTROL Manage Data** > **Connections]** e fai clic su **[!UICONTROL Add New Data Source]**.
1. Fai clic su `MySQL` icona.
1. Dopo il `MySQL credentials` viene visualizzata la pagina, impostare `Encrypted` passa a `Yes`. Viene visualizzato il modulo di configurazione SSH.
1. Il `public key` si trova sotto questo modulo.

Lascia aperta questa pagina per tutta la durata dell’esercitazione: sarà necessario visualizzarla nella sezione successiva e alla fine.

Ecco come navigare [!DNL Commerce Intelligence] per recuperare la chiave:

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## Consenti accesso a [!DNL Commerce Intelligence] Indirizzo IP {#allowlist}

Affinché la connessione abbia esito positivo, è necessario configurare il firewall per consentire l&#39;accesso dagli indirizzi IP. Sono `54.88.76.97` e `34.250.211.151` ma sono anche in corso `MySQL credentials` pagina. Vedi la casella blu in GIF.

## Creazione di un [!DNL Linux] utente per [!DNL Commerce Intelligence] {#linux}

Può trattarsi di un computer di produzione o secondario, purché contenga dati in tempo reale (o aggiornati di frequente). È possibile [limita questo utente](../../../administrator/account-management/restrict-db-access.md) in qualsiasi modo, purché conservi il diritto di connessione al `MySQL` server.

1. Per aggiungere il nuovo utente, eseguire i seguenti comandi come radice sul [!DNL Linux] server:

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
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>Se il `sshd\_config` il file associato al server non è impostato sull&#39;opzione predefinita, solo alcuni utenti dispongono dell&#39;accesso al server. [!DNL Commerce Intelligence]. In questi casi, è necessario eseguire un comando come `AllowUsers` per consentire `rjmetric` accesso utente al server.

## Creazione di un [!DNL MySQL] utente per [!DNL Commerce Intelligence] {#mysql}

La tua organizzazione potrebbe richiedere un processo diverso, ma il modo più semplice per creare questo utente è quello di eseguire la seguente query al momento dell’accesso [!DNL MySQL] come utente con il diritto di concedere privilegi:

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

Sostituisci `secure password here` con una password sicura, che può essere diversa dalla `SSH` password.

Per impedire a questo utente di accedere ai dati in database, tabelle o colonne specifiche, è invece possibile eseguire query GRANT che consentono solo l&#39;accesso ai dati consentiti.

## Immissione della connessione e delle informazioni utente in [!DNL Commerce Intelligence] {#finish}

Per concludere, devi immettere la connessione e le informazioni utente in [!DNL Commerce Intelligence]. Hai lasciato il `MySQL credentials` pagina aperta? In caso contrario, vai a **[!UICONTROL Data** > **Connections]** e fai clic su **[!UICONTROL Add New Data Source]**, quindi [!DNL MySQL] icona. Non dimenticare di impostare `Encrypted` passa a `Yes`.

Immetti le seguenti informazioni in questa pagina, iniziando da `Database Connection` sezione:

* `Username`: nome utente per [!DNL Commerce Intelligence] [!DNL MySQL] utente
* `Password`: password per [!DNL Commerce Intelligence] [!DNL MySQL] utente
* `Port`: [!DNL MySQL] porta sul server (3306 per impostazione predefinita)
* `Host` Per impostazione predefinita, è localhost. In generale, è il valore bind-address per il [!DNL MySQL] , che per impostazione predefinita è `127.0.0.1 (localhost)`, ma potrebbe anche essere un indirizzo di rete locale (ad esempio, `192.168.0.1`) o l&#39;indirizzo IP pubblico del server.

   Il valore si trova nella `my.cnf` file (che si trova in `/etc/my.cnf`) sotto la riga che recita `\[mysqld\]`. Se la riga dell&#39;indirizzo di associazione viene inserita come commento in tale file, il server viene protetto dai tentativi di connessione esterni.

In `SSH Connection` sezione:

* `Remote Address`: indirizzo IP o nome host del server [!DNL Commerce Intelligence] si trasformerà in
* `Username`: nome utente per [!DNL Commerce Intelligence] SSH ([!DNL Linux]) utente
* `SSH Port`: porta SSH sul server (22 per impostazione predefinita)

Al termine, fai clic su **[!UICONTROL Save & Test]** per completare la configurazione.

## Correlato:

* [Reautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
