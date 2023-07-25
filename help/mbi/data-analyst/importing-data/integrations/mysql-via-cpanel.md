---
title: Connetti MySQL tramite cPanel
description: Scopri come connettere MySQL tramite cPanel.
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# Connetti [!DNL MySQL] tramite [!DNL cPanel]

* [Creare un [!DNL Commerce Intelligence] [!DNL MySQL] utente in [!DNL cPanel]](#cpanel)
* [Immetti connessione e informazioni utente in [!DNL Commerce Intelligence]](#finish)

## Passa a

* [[!DNL MySQL] tramite tunnel SSH](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] tramite connessione diretta](../integrations/mysql-via-a-direct-connection.md)

>[!IMPORTANT]
>
>[!DNL Adobe] consiglia di utilizzare SSH o altre forme di crittografia per proteggere i dati. Se questa non è un&#39;opzione, è comunque possibile connettersi direttamente [!DNL Commerce Intelligence] nel database seguendo le istruzioni riportate in questo argomento.

Questo argomento illustra come connettere direttamente [!DNL MySQL] database a [!DNL Commerce Intelligence] utilizzo [!DNL cPanel]. Questo processo può essere utilizzato anche per la connessione [!DNL Adobe Commerce] e qualsiasi altro database eCommerce basato su MySQL a [!DNL Commerce Intelligence].

1. Creare un [!DNL Commerce Intelligence] [!DNL MySQL] utente in [!DNL cPanel]
1. Immetti connessione e informazioni utente in [!DNL Commerce Intelligence]

Inizia.

## Creazione di un [!DNL Commerce Intelligence] [!DNL MySQL] utente in [!DNL cPanel] {#cpanel}

1. Accedi a [!DNL cPanel] tramite il provider di hosting.
1. Clic **[!UICONTROL [!DNL MySQL] Databases]**, che si trova in `Database` sezione.
1. Scorri verso il basso fino a `Add New User` e creare un utente per [!DNL Commerce Intelligence]:

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. Clic **[!UICONTROL Create User]**.
1. Dopo aver creato l&#39;utente, è necessario associarlo a un database. Torna a `Add New User` sezione - consulta le impostazioni per `Add User to Database?` Questo è ciò di cui avete bisogno.
1. In `User` in questa sezione, seleziona l’utente creato.
1. In `Database` in questa sezione, selezionare il database a cui si desidera connettersi [!DNL Commerce Intelligence].
1. Clic **[!UICONTROL Add]**.
1. Quando viene visualizzato l&#39;elenco di controllo dei privilegi, selezionare la casella accanto a `SELECT` - tutto qui [!DNL Commerce Intelligence] deve connettersi al database.

## Immissione della connessione e delle informazioni utente in [!DNL Commerce Intelligence] {#finish}

Per concludere, devi immettere la connessione e le informazioni utente in [!DNL Commerce Intelligence]. Hai lasciato il [!DNL MySQL] la pagina delle credenziali è aperta? In caso contrario, vai a **[!UICONTROL Manage Data** > **Connections]** e fai clic su **[!UICONTROL Add New Data Source]**, quindi [!DNL MySQL] icona.

Immetti le seguenti informazioni in questa pagina nel `Database Connection` sezione:

* `Username`: nome utente per [!DNL Commerce Intelligence] [!DNL MySQL] utente
* `Password`: password per [!DNL Commerce Intelligence] [!DNL MySQL] utente
* `Port`: porta MySQL sul server (`3306` per impostazione predefinita)
* `Host`: l’indirizzo pubblico del `MySQL` server [!DNL Commerce Intelligence] si connette a. In genere si tratta dell’URL utilizzato per accedere a `[!DNL cPanel]`.

Se si utilizza un’ [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md), è necessario immettere le informazioni di crittografia. Imposta il `Encrypted` passa a `Yes` per visualizzare il modulo.

* `Connection Type`: imposta su `SSH Tunnel`
* `Remote Address`: indirizzo IP o nome host del server [!DNL Commerce Intelligence] si trasformerà in
* `Username`: nome utente per [!DNL Commerce Intelligence] `SSH (Linux)` utente, consulta [istruzioni](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) su come farlo, se non lo hai già fatto)
* `SSH Port`: porta SSH sul server (`22` per impostazione predefinita)

Al termine, fai clic su **[!UICONTROL Save & Test]** per completare la configurazione.

## Correlato:

* [Reautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
