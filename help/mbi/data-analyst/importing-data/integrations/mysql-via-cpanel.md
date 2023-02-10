---
title: Connetti MySQL tramite cPanel
description: Scopri come collegare MySQL tramite cPanel.
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
source-git-commit: 9974cc5c5cf89829ca522ba620b8c0c2d509610c
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Connetti MySQL tramite cPanel

* [Crea un [!DNL MBI] Utente MySQL in cPanel](#cpanel)
* [Immettere la connessione e le informazioni utente in MBI](#finish)

## Passa a

* [MySQL tramite tunnel SSH](../integrations/mysql-via-ssh-tunnel.md)
* [MySQL tramite connessione diretta](../integrations/mysql-via-a-direct-connection.md)

* **`MySQL via cPanel`**

>[!IMPORTANT]
>
>Ti consigliamo vivamente di utilizzare SSH o qualsiasi altra forma di crittografia per proteggere i tuoi dati! Se questa non è un&#39;opzione, è comunque possibile connettersi direttamente [!DNL MBI] al database utilizzando le istruzioni contenute in questo articolo.

In questo articolo viene descritto come collegare direttamente il database MySQL a [!DNL MBI] cPanel&quot;. Questo processo può essere utilizzato anche per la connessione [!DNL Adobe Commerce] e qualsiasi altro database eCommerce basato su MySQL a [!DNL MBI].

1. Crea un [!DNL MBI] Utente MySQL in `cPanel`
1. Immettere la connessione e le informazioni utente in [!DNL MBI]

Inizia.

## Creazione di una [!DNL MBI] Utente MySQL in `cPanel` {#cpanel}

1. Accedi a [`cPanel`](../../../data-analyst/importing-data/integrations/mysql-via-cpanel.md) tramite il provider di hosting.
1. Fai clic su **[!UICONTROL MySQL Databases]**, situato nella `Database` sezione .
1. Scorri verso il basso fino a `Add New User` creare un utente per [!DNL MBI]:

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. Fai clic su **[!UICONTROL Create User]**.
1. Dopo aver creato l&#39;utente, è necessario associarlo a un database. Torna alla pagina `Add New User` sezione : consulta le impostazioni per `Add User to Database?` Questo è ciò di cui abbiamo bisogno.
1. In `User` a discesa di questa sezione, seleziona l’utente creato.
1. In `Database` a discesa di questa sezione, selezionare il database a cui si desidera connettersi [!DNL MBI].
1. Fai clic su **[!UICONTROL Add]**.
1. Quando viene visualizzato l&#39;elenco di controllo dei privilegi, seleziona la casella accanto a `SELECT` - questo è tutto [!DNL MBI] deve connettersi al database.

## Inserimento della connessione e delle informazioni utente in [!DNL MBI] {#finish}

Per concludere, dobbiamo inserire la connessione e le informazioni utente in [!DNL MBI]. Hai lasciato aperta la pagina delle credenziali MySQL? In caso contrario, vai a **[!UICONTROL Manage Data** > **Connections]** e fai clic su **[!UICONTROL Add New Data Source]**, quindi l&#39;icona MySQL.

Immetti le seguenti informazioni in questa pagina nel `Database Connection` sezione:

* `Username`: Il nome utente per il [!DNL MBI] Utente MySQL
* `Password`: La password per [!DNL MBI] Utente MySQL
* `Port`: Porta di MySQL sul server (`3306` per impostazione predefinita)
* `Host`: Indirizzo pubblico del `MySQL` server [!DNL MBI] si connetterà a. Questo è solitamente l’URL a cui si accede `cPanel`.

Se utilizzi un [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md), sarà inoltre necessario immettere le informazioni di cifratura. Imposta la `Encrypted` passa a `Yes` per visualizzare il modulo.

* `Connection Type`: Imposta questo su `SSH Tunnel`
* `Remote Address`: Indirizzo IP o nome host del server [!DNL MBI] si trasformerà in
* `Username`: Il nome utente per il [!DNL MBI] `SSH (Linux)` utente, vedi [istruzioni](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) su come farlo, se non lo hai già fatto)
* `SSH Port`: Porta SSH sul server (`22` per impostazione predefinita)

Tutto qui! Al termine, fai clic su **[!UICONTROL Save & Test]** per completare la configurazione.

## Correlati:

* [Riautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
