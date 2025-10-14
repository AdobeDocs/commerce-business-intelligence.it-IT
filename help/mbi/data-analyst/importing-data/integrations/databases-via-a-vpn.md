---
title: Collegare i database tramite VPN
description: Scopri come connettere i database tramite VPN invece del tunnel SSH.
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Collegare i database tramite VPN

Adobe consiglia di connettere i database utilizzando `SSH tunnel`, ma è anche possibile utilizzare una connessione `VPN` crittografata per mantenere la protezione. Un `VPN` può essere utilizzato per qualsiasi integrazione di database e, per semplificare le cose, il processo è quasi lo stesso della configurazione di un `SSH tunnel`:

1. [Crea un utente del database  [!DNL Commerce Intelligence] &#x200B;](#database)
1. [Crea un utente VPN  [!DNL Commerce Intelligence] &#x200B;](#vpn)
1. [Consenti accesso all&#39;indirizzo IP  [!DNL Commerce Intelligence] &#x200B;](#allowlist)
1. [Immetti la connessione e le informazioni utente VPN in Commerce Intelligence](#finish)

Oltre alle credenziali del database, è necessario immettere le credenziali per consentire a un utente VPN di completare la procedura. Qualsiasi utente VPN funziona, ma Adobe consiglia di creare un utente [!DNL Commerce Intelligence], in quanto ti consente di tenere traccia più facilmente degli utenti sul tuo account.

## Creazione di un utente del database per [!DNL Commerce Intelligence] {#database}

Il processo di creazione di un utente di database varia a seconda del tipo di database che si sta connettendo. Per visualizzare le istruzioni per ogni tipo di database, fare clic sui collegamenti riportati di seguito.

* [MICROSOFT SQL](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## Creazione di un utente `VPN` per [!DNL Commerce Intelligence] {#vpn}

Come accennato in precedenza, qualsiasi utente `VPN` valido funziona, ma Adobe consiglia di creare un utente solo per l&#39;utilizzo [!DNL Commerce Intelligence].

## Consenti accesso agli indirizzi IP [!DNL Commerce Intelligence] {#allowlist}

Affinché la connessione abbia esito positivo, è necessario configurare il firewall per consentire l&#39;accesso dagli indirizzi IP. Sono `54.88.76.97` e `34.250.211.151`, ma si trova anche nella pagina `credentials` per qualsiasi integrazione di database:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Immissione della connessione e delle informazioni utente di `VPN` in [!DNL Commerce Intelligence] {#finish}

Per concludere, devi immettere la connessione e le informazioni utente in [!DNL Commerce Intelligence]. Hai lasciato aperta la pagina `credentials` del database? In caso contrario, passare a **[!UICONTROL Manage Data** > **Connections]**. Fare clic su **[!UICONTROL Add New Data Source]** e quindi sull&#39;icona del database che si sta connettendo. Non dimenticare di cambiare `Encrypted` in `Yes`.

Immettere le informazioni seguenti in questa pagina, a partire dalla sezione `Database Connection`:

* `Username`: nome utente per l&#39;utente del database [!DNL Commerce Intelligence]
* `Password`: password per l&#39;utente del database [!DNL Commerce Intelligence]
* `Port`: la porta del database sul server. I valori predefiniti sono:
   * `MicrosoftSQL`: `1433`
   * `MongoDB`: `27017`
   * `MySQL`: `3306`
   * `PostgreSQL`: `5432`
* `Host`: per impostazione predefinita, è localhost `127.0.0.1`, ma potrebbe anche essere l&#39;indirizzo IP pubblico del server o un indirizzo di rete locale.
* `Database Name (optional)`: se è stato consentito l&#39;accesso a un solo database (specificato durante il passaggio di creazione dell&#39;utente del database), immettere qui il nome del database.

Nella sezione `Encryption Connection`:

* `Encryption Type`: imposta su `Cisco IPsec VPN`
* `Gateway Address`: indirizzo IP del server VPN
* `Group Name`: nome del gruppo utilizzato per l&#39;autenticazione del gruppo
* `Group Secret`: password corrispondente al gruppo.
* `Username`: nome utente [!DNL Commerce Intelligence] `VPN`
* `Password`: password utente [!DNL Commerce Intelligence] `VPN`

Al termine, fare clic su **[!UICONTROL Save & Test]** per completare la configurazione.
