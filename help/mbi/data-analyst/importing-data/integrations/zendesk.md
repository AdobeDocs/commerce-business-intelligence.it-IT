---
title: Connetti Zendesk
description: Scopri come consolidare il reporting dell'helpdesk in [!DNL Commerce Intelligence].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/KBUuqTDD9s3qXDktcV3RzLx4zxtAFwAkKPbsQE2YGtI
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 261
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
* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
