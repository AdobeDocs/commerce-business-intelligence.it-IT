---
title: Connetti Zendesk
description: Scopri come consolidare il reporting dell'helpdesk in [!DNL Commerce Intelligence].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# Connetti [!DNL Zendesk]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![Logo Zendesk](../../../assets/Zendesk_logo.png)

La connessione dei dati di [!DNL Zendesk] consente di consolidare il reporting dell&#39;helpdesk in [!DNL Commerce Intelligence]. Questo consente di ottimizzare l&#39;assistenza clienti e monitorare le prestazioni dell&#39;help desk insieme ai ricavi.

La connessione dei dati di [!DNL Zendesk] è un semplice processo in tre fasi:

1. [Apri la pagina delle credenziali  [!DNL Zendesk]  in [!DNL Commerce Intelligence]](#stepone)
1. [Recupera il token API  [!DNL Zendesk] &#x200B;](#steptwo)
1. [Immetti le tue  [!DNL Zendesk] informazioni di accesso e il token in [!DNL Commerce Intelligence]](#stepthree)

Per completare il processo, è necessario aprire due finestre o schede del browser: una per [!DNL Commerce Intelligence] e l&#39;altra per l&#39;account [!DNL Zendesk].

## Apri la pagina delle credenziali di [!DNL Zendesk] in [!DNL Commerce Intelligence] {#stepone}

1. Vai alla pagina `Integrations` in **[!UICONTROL Manage Data** > **&#x200B; Origini dati &#x200B;**> **Integrazioni]**.
1. Fare clic su **[!UICONTROL Add Integration]**, che si trova sul lato destro della schermata.
1. Fare clic sull&#39;icona [!DNL Zendesk]. Verrà aperta la pagina delle credenziali [!DNL Zendesk].

## Recupera il token API [!DNL Zendesk] {#steptwo}

1. Nella finestra/scheda in cui hai effettuato l&#39;accesso all&#39;account [!DNL Zendesk], fai clic sull&#39;icona Impostazioni (ingranaggio) nell&#39;angolo in basso a sinistra dello schermo.
1. Quando viene visualizzato il menu `Settings`, individuare la sezione `Channels`. Fare clic su **[!UICONTROL API]** in questa sezione.
1. Nella sezione `Token Access` di questa pagina, fare clic sulla casella di controllo accanto a `Enabled`. Viene visualizzato un elenco dei token API attivi.
1. Fare clic su **[!UICONTROL Add New Token]**.
1. Quando richiesto, immetti un’etichetta per il token. Adobe consiglia di utilizzare `Commerce Intelligence`, in modo da sapere subito quale applicazione sta utilizzando il token.
1. Fare clic su **[!UICONTROL Create]**.
1. Viene creato un token API. Copia questo token, che verrà utilizzato nel passaggio successivo.

## Immetti le informazioni di accesso e il token API di [!DNL Zendesk] in [!DNL Commerce Intelligence] {#stepthree}

1. Immetti il prefisso del sito [!DNL Zendesk] e l&#39;indirizzo e-mail di accesso nella pagina delle credenziali [!DNL Zendesk] in [!DNL Commerce Intelligence].
1. Immetti il token API.
1. Fare clic su **[!UICONTROL Save & Connect]**. Se la connessione ha esito positivo, *Connessione riuscita.Il messaggio* viene visualizzato nella parte superiore dello schermo.

## Correlato:

* [Previsti [!DNL Zendesk] dati](../integrations/exp-zendesk-data.md)
* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=it)
