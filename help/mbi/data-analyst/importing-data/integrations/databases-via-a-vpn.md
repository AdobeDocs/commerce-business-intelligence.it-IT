---
title: Collegare i database tramite VPN
description: Scopri come collegare i database tramite VPN invece di SSH Tunnel.
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# Collegare i database tramite VPN

Mentre si consiglia di collegare i database utilizzando un tunnel SSH, è anche possibile utilizzare una connessione VPN crittografata per proteggere gli elementi. A `VPN` può essere utilizzato per qualsiasi delle nostre integrazioni di database e, per semplificare le cose, il processo è quasi lo stesso della configurazione di un `SSH tunnel`:

1. [Crea un [!DNL MBI] utente del database](#database)
1. [Crea un [!DNL MBI] Utente VPN](#vpn)
1. [Consenti accesso al [!DNL MBI] Indirizzo IP](#allowlist)
1. [Immettere la connessione e le informazioni utente VPN in MBI](#finish)

Oltre alle credenziali del database, sarà necessario immettere le credenziali per un utente VPN per completare le operazioni. Qualsiasi utente VPN funzionerà, ma ti consigliamo di creare un [!DNL MBI] utente : ti consente di tenere traccia degli utenti sul tuo account in modo più semplice.

Cominciamo.

## Creazione di un utente di database per [!DNL MBI] {#database}

Il processo di creazione di un utente di database varia a seconda del tipo di database che si sta connettendo. Per visualizzare le istruzioni per ogni tipo di database, fare clic sui collegamenti riportati di seguito.

* [Microsoft SQL](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## Creazione di una `VPN` utente per [!DNL MBI] {#vpn}

Come abbiamo detto prima, qualsiasi valido `VPN` l&#39;utente funzionerà, ma si consiglia vivamente di creare un utente solo per [!DNL MBI] utilizzare.

## Consenti accesso al [!DNL MBI] Indirizzi IP {#allowlist}

Affinché la connessione abbia successo, devi configurare il firewall per consentire l’accesso dai nostri indirizzi IP. Sono `54.88.76.97` e `34.250.211.151`, ma è anche sul `credentials` pagina per qualsiasi integrazione di database:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Inserimento della connessione e `VPN` informazioni utente in [!DNL MBI] {#finish}

Per concludere, dobbiamo inserire la connessione e le informazioni utente in [!DNL MBI]. Ha lasciato il database? `credentials` pagina aperta? In caso contrario, vai a **[!UICONTROL Manage Data** > **Connections]** e fai clic su **[!UICONTROL Add New Data Source]**, quindi l’icona del database che si sta connettendo. non dimenticare di modificare le `Encrypted` passa a `Yes`.

Immetti le seguenti informazioni in questa pagina, a partire dal `Database Connection` sezione:

* `Username`: Il nome utente per il [!DNL MBI] utente del database
* `Password`: La password per [!DNL MBI] utente del database
* `Port`: La porta del database sul server. I valori predefiniti sono:
* `MicrosoftSQL`: `1433`
* `MongoDB`: `27017`
* `MySQL`: `3306`
* `PostgreSQL`: `5432`
* `Host`: Per impostazione predefinita, è localhost `127.0.0.1`, ma potrebbe anche essere l&#39;indirizzo IP pubblico del server o un indirizzo di rete locale.
* `Database Name (optional)`: Se è consentito l&#39;accesso a un solo database (specificato durante il passaggio di creazione dell&#39;utente del database), immettere il nome del database.

Sotto la `Encryption Connection` sezione:

* `Encryption Type`: Imposta questo su `Cisco IPsec VPN`
* `Gateway Address`: Indirizzo IP del server VPN
* `Group Name`: Nome del gruppo utilizzato per l&#39;autenticazione del gruppo
* `Group Secret`: Password corrispondente al gruppo.
* `Username`: La [!DNL MBI] `VPN` username
* `Password`: La [!DNL MBI] `VPN` password utente

Tutto qui! Al termine, fai clic su **[!UICONTROL Save & Test]** per completare la configurazione.
