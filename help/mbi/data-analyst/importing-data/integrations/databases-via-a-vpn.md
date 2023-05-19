---
title: Collegare i database tramite VPN
description: Scopri come connettere i database tramite VPN invece del tunnel SSH.
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# Collegare i database tramite VPN

L&#39;Adobe consiglia di connettere i database utilizzando un `SSH tunnel`, è inoltre possibile utilizzare un `VPN` connessione per garantire la protezione. A `VPN` può essere utilizzato per qualsiasi integrazione di database e, per semplificare, il processo è quasi identico a quello di configurazione di un `SSH tunnel`:

1. [Creare un [!DNL Commerce Intelligence] utente del database](#database)
1. [Creare un [!DNL Commerce Intelligence] Utente VPN](#vpn)
1. [Consenti accesso a [!DNL Commerce Intelligence] Indirizzo IP](#allowlist)
1. [Immetti la connessione e le informazioni utente VPN in Commerce Intelligence](#finish)

Oltre alle credenziali del database, è necessario immettere le credenziali per consentire a un utente VPN di completare la procedura. Qualsiasi utente VPN funziona, ma l’Adobe consiglia di creare un [!DNL Commerce Intelligence] utente, in quanto consente di tenere traccia più facilmente degli utenti sul tuo account.

## Creazione di un utente del database per [!DNL Commerce Intelligence] {#database}

Il processo di creazione di un utente di database varia a seconda del tipo di database che si sta connettendo. Per visualizzare le istruzioni per ogni tipo di database, fare clic sui collegamenti riportati di seguito.

* [MICROSOFT SQL](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## Creazione di un `VPN` utente per [!DNL Commerce Intelligence] {#vpn}

Come accennato in precedenza, qualsiasi `VPN` l’utente funziona, ma l’Adobe consiglia di creare un utente esclusivamente per [!DNL Commerce Intelligence] utilizzare.

## Consenti accesso a [!DNL Commerce Intelligence] Indirizzi IP {#allowlist}

Affinché la connessione abbia esito positivo, è necessario configurare il firewall per consentire l&#39;accesso dagli indirizzi IP. Sono `54.88.76.97` e `34.250.211.151`, ma è anche nel `credentials` pagina per qualsiasi integrazione di database:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Inserimento della connessione e `VPN` informazioni utente in [!DNL Commerce Intelligence] {#finish}

Per concludere, devi immettere la connessione e le informazioni utente in [!DNL Commerce Intelligence]. Hai lasciato il database? `credentials` pagina aperta? In caso contrario, vai a **[!UICONTROL Manage Data** > **Connections]**. Clic **[!UICONTROL Add New Data Source]**, quindi fare clic sull&#39;icona del database che si sta connettendo. Non dimenticare di modificare il `Encrypted` passa a `Yes`.

Immetti le seguenti informazioni in questa pagina, iniziando da `Database Connection` sezione:

* `Username`: nome utente per [!DNL Commerce Intelligence] utente del database
* `Password`: password per [!DNL Commerce Intelligence] utente del database
* `Port`: porta del database sul server. I valori predefiniti sono:
   * `MicrosoftSQL`: `1433`
   * `MongoDB`: `27017`
   * `MySQL`: `3306`
   * `PostgreSQL`: `5432`
* `Host`: per impostazione predefinita, è localhost `127.0.0.1`, ma potrebbe anche essere l&#39;indirizzo IP pubblico del server o un indirizzo di rete locale.
* `Database Name (optional)`: se è stato consentito l&#39;accesso a un solo database (specificato durante il passaggio di creazione dell&#39;utente del database), immettere qui il nome del database.

Sotto `Encryption Connection` sezione:

* `Encryption Type`: imposta su `Cisco IPsec VPN`
* `Gateway Address`: indirizzo IP del server VPN
* `Group Name`: nome del gruppo utilizzato per l’autenticazione del gruppo
* `Group Secret`: password corrispondente al gruppo.
* `Username`: Il [!DNL Commerce Intelligence] `VPN` nome utente
* `Password`: Il [!DNL Commerce Intelligence] `VPN` password utente

Al termine, fai clic su **[!UICONTROL Save & Test]** per completare la configurazione.
