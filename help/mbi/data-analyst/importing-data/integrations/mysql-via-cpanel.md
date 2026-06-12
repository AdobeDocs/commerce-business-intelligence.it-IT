---
title: Connetti MySQL tramite cPanel
description: Scopri come connettere MySQL tramite cPanel.
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
TQID: https://experienceleague.adobe.com/Ou9gOlYKFuoYQHTi7zhyecvfGlKEKF2eRSr5vctsW1s
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 3a6b80d7bcfa5db4d86ab4da81239e3ea804f6ad
workflow-type: tm+mt
source-wordcount: 400
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

>[!NOTE]
>
>Se si utilizza un tunnel SSH, vedere [Verifica chiave host SSH](ssh-host-key-verification.md) per la registrazione, l&#39;aggiornamento, i messaggi di errore e la risoluzione dei problemi.

## Correlato {#related}

* [Verifica chiave host SSH](ssh-host-key-verification.md)
* [Reautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
