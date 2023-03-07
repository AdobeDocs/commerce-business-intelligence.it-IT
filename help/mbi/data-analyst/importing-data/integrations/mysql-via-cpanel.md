---
title: Connetti MySQL tramite cPanel
description: Scopri come connettere MySQL tramite cPanel.
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
source-git-commit: e4ac176492913623ae461484c8ef2abe034e5f62
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# Connetti MySQL tramite cPanel

* [Creare un [!DNL MBI] Utente MySQL in cPanel](#cpanel)
* [Immetti la connessione e le informazioni utente in MBI](#finish)

## Passa a

* [MySQL tramite tunnel SSH](../integrations/mysql-via-ssh-tunnel.md)
* [MySQL tramite connessione diretta](../integrations/mysql-via-a-direct-connection.md)

* **`MySQL via cPanel`**

>[!IMPORTANT]
>
>L’Adobe consiglia di utilizzare SSH o altre forme di crittografia per proteggere i dati. Se questa non è un&#39;opzione, è comunque possibile connettersi direttamente [!DNL MBI] nel database seguendo le istruzioni riportate in questo articolo.

Questo articolo illustra come collegare direttamente il database MySQL a [!DNL MBI] utilizzo `cPanel`. Questo processo può essere utilizzato anche per la connessione [!DNL Adobe Commerce] e qualsiasi altro database eCommerce basato su MySQL a [!DNL MBI].

1. Creare un [!DNL MBI] Utente MySQL in `cPanel`
1. Immetti connessione e informazioni utente in [!DNL MBI]

Inizia.

## Creazione di un [!DNL MBI] Utente MySQL in `cPanel` {#cpanel}

1. Accedi a [`cPanel`](../../../data-analyst/importing-data/integrations/mysql-via-cpanel.md) tramite il provider di hosting.
1. Clic **[!UICONTROL MySQL Databases]**, che si trova in `Database` sezione.
1. Scorri verso il basso fino a `Add New User` e creare un utente per [!DNL MBI]:

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. Clic **[!UICONTROL Create User]**.
1. Dopo aver creato l&#39;utente, è necessario associarlo a un database. Torna a `Add New User` sezione - consulta le impostazioni per `Add User to Database?` Questo è ciò di cui avete bisogno.
1. In `User` in questa sezione, seleziona l’utente creato.
1. In `Database` in questa sezione, selezionare il database a cui si desidera connettersi [!DNL MBI].
1. Clic **[!UICONTROL Add]**.
1. Quando viene visualizzato l&#39;elenco di controllo dei privilegi, selezionare la casella accanto a `SELECT` - tutto qui [!DNL MBI] deve connettersi al database.

## Immissione della connessione e delle informazioni utente in [!DNL MBI] {#finish}

Per concludere, devi immettere la connessione e le informazioni utente in [!DNL MBI]. La pagina Credenziali MySQL è stata lasciata aperta? In caso contrario, vai a **[!UICONTROL Manage Data** > **Connections]** e fai clic su **[!UICONTROL Add New Data Source]**, quindi l&#39;icona MySQL.

Immetti le seguenti informazioni in questa pagina nel `Database Connection` sezione:

* `Username`: nome utente per [!DNL MBI] Utente MySQL
* `Password`: password per [!DNL MBI] Utente MySQL
* `Port`: porta MySQL sul server (`3306` per impostazione predefinita)
* `Host`: l’indirizzo pubblico del `MySQL` server [!DNL MBI] si connette a. In genere si tratta dell’URL utilizzato per accedere a `cPanel`.

Se si utilizza un’ [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md), è necessario immettere le informazioni di crittografia. Imposta il `Encrypted` passa a `Yes` per visualizzare il modulo.

* `Connection Type`: imposta su `SSH Tunnel`
* `Remote Address`: indirizzo IP o nome host del server [!DNL MBI] si trasformerà in
* `Username`: nome utente per [!DNL MBI] `SSH (Linux)` utente, consulta [istruzioni](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) su come farlo, se non lo hai già fatto)
* `SSH Port`: porta SSH sul server (`22` per impostazione predefinita)

Tutto qui! Al termine, fai clic su **[!UICONTROL Save & Test]** per completare la configurazione.

## Correlato:

* [Reautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
