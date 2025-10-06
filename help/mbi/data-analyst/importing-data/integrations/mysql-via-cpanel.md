---
title: Connetti MySQL tramite cPanel
description: Scopri come connettere MySQL tramite cPanel.
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# Connetti [!DNL MySQL] tramite [!DNL cPanel]

* [Crea un utente  [!DNL Commerce Intelligence] [!DNL MySQL] in [!DNL cPanel]](#cpanel)
* [Immetti la connessione e le informazioni utente in  [!DNL Commerce Intelligence]](#finish)

## Passa a

* [[!DNL MySQL] tramite tunnel SSH](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] tramite connessione diretta](../integrations/mysql-via-a-direct-connection.md)

>[!IMPORTANT]
>
>[!DNL Adobe] consiglia di utilizzare SSH o altre forme di crittografia per proteggere i dati. Se questa non è un&#39;opzione, è comunque possibile connettere direttamente [!DNL Commerce Intelligence] al database utilizzando le istruzioni riportate in questo argomento.

Questo argomento illustra come collegare direttamente il database [!DNL MySQL] a [!DNL Commerce Intelligence] utilizzando [!DNL cPanel]. Questo processo può essere utilizzato anche per connettere [!DNL Adobe Commerce] e altri database eCommerce basati su MySQL a [!DNL Commerce Intelligence].

1. Crea un utente [!DNL Commerce Intelligence] [!DNL MySQL] in [!DNL cPanel]
1. Immetti la connessione e le informazioni utente in [!DNL Commerce Intelligence]

Inizia.

## Creazione di un utente [!DNL Commerce Intelligence] [!DNL MySQL] in [!DNL cPanel] {#cpanel}

1. Accedi a [!DNL cPanel] tramite il provider di hosting.
1. Fare clic su **[!UICONTROL [!DNL MySQL] Databases]**, che si trova nella sezione `Database`.
1. Scorri verso il basso fino alla sezione `Add New User` e crea un utente per [!DNL Commerce Intelligence]:

   ![interfaccia dei database MySQL del pannello che mostra il modulo utente per la creazione](../../../assets/create-mbi-mysql-user-cpanel.png)

1. Fare clic su **[!UICONTROL Create User]**.
1. Dopo aver creato l&#39;utente, è necessario associarlo a un database. Tornare alla sezione `Add New User`. Vedere le impostazioni per `Add User to Database?`.
1. Nel menu a discesa `User` di questa sezione, seleziona l&#39;utente creato.
1. Nel menu a discesa `Database` di questa sezione, selezionare il database a cui si desidera connettersi [!DNL Commerce Intelligence].
1. Fare clic su **[!UICONTROL Add]**.
1. Quando viene visualizzato l&#39;elenco di controllo dei privilegi, selezionare la casella accanto a `SELECT`. Questo è tutto ciò che [!DNL Commerce Intelligence] deve connettersi al database.

## Immissione della connessione e delle informazioni utente in [!DNL Commerce Intelligence] {#finish}

Per concludere, devi immettere la connessione e le informazioni utente in [!DNL Commerce Intelligence]. Hai lasciato aperta la pagina delle credenziali di [!DNL MySQL]? In caso contrario, passare a **[!UICONTROL Manage Data** > **Connections]** e fare clic su **[!UICONTROL Add New Data Source]**, quindi sull&#39;icona [!DNL MySQL].

Immettere le informazioni seguenti in questa pagina nella sezione `Database Connection`:

* `Username`: nome utente per l&#39;utente [!DNL Commerce Intelligence] [!DNL MySQL]
* `Password`: password per l&#39;utente [!DNL Commerce Intelligence] [!DNL MySQL]
* `Port`: porta MySQL nel server (`3306` per impostazione predefinita)
* `Host`: l&#39;indirizzo pubblico del server `MySQL` [!DNL Commerce Intelligence] si connette a. Questo è in genere l&#39;URL utilizzato per accedere a `[!DNL cPanel]`.

Se si utilizza un [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md), è necessario immettere le informazioni di crittografia. Impostare `Encrypted` su `Yes` per visualizzare il modulo.

* `Connection Type`: imposta su `SSH Tunnel`
* `Remote Address`: l&#39;indirizzo IP o il nome host del server [!DNL Commerce Intelligence] verrà sottoposto a tunneling in
* `Username`: nome utente per l&#39;utente [!DNL Commerce Intelligence] `SSH (Linux)`. Vedere [istruzioni](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) su come eseguire questa operazione, se non si dispone già di questa autorizzazione)
* `SSH Port`: porta SSH sul server (`22` per impostazione predefinita)

Al termine, fare clic su **[!UICONTROL Save & Test]** per completare la configurazione.

## Correlato:

* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
