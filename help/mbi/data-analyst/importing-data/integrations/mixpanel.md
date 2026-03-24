---
title: Connetti Mixpanel
description: Scopri come analizzare il modo in cui gli utenti si spostano e utilizzano i tuoi siti web e le tue app.
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/ap-nWiPVnPSpvUT4uiimZ7iC4fiuKvKH0ZMVkOTDcK8
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
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 246
ht-degree: 0%

---

# Connetti [!DNL Mixpanel]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![Logo Mixpanel](../../../assets/Mixpanel_logo.png)

Con [!DNL Mixpanel] puoi analizzare il modo in cui gli utenti si spostano e utilizzano i tuoi siti Web e le tue app. Osservando da vicino i dati sul comportamento degli utenti, si ottengono decisioni di progettazione e sviluppo più intelligenti, il che significa un prodotto complessivamente migliore. La connessione di [!DNL Mixpanel] a [!DNL Commerce Intelligence] consente di analizzare il comportamento degli utenti e come questo comportamento si traduce in ricavi.

Collegare i dati di [!DNL Mixpanel] a [!DNL Commerce Intelligence] è un semplice processo in tre fasi:

1. [Apri la pagina delle credenziali  [!DNL Mixpanel]  in [!DNL Commerce Intelligence]](#stepone)
1. [Recupera le tue credenziali API  [!DNL Mixpanel] &#x200B;](#steptwo)
1. [Immetti le tue credenziali API  [!DNL Mixpanel]  in [!DNL Commerce Intelligence]](#stepthree)

Per completare il processo, è necessario aprire due finestre o schede del browser, una per [!DNL Commerce Intelligence] e l&#39;altra per l&#39;account [!DNL Mixpanel].

## Apertura della pagina delle credenziali di [!DNL Mixpanel] {#stepone}

Introduzione:

1. Passare alla pagina `Connections` in **[!DNL Manage Data** > **Connections]**.

1. Fare clic su **[!UICONTROL Add a New Source]**, che si trova sul lato destro della schermata sopra la tabella `Data Sources`.

1. Fare clic sull&#39;icona [!DNL Mixpanel] e aprire la pagina delle credenziali.

Lascia aperta questa pagina per il momento e passa alla finestra del browser con il tuo account [!DNL Mixpanel].

## Recupero credenziali API [!DNL Mixpanel] {#steptwo}

Se non hai ancora effettuato l&#39;accesso all&#39;account [!DNL Mixpanel], effettua questa operazione e quindi effettua le seguenti operazioni:

1. Fare clic su **[!UICONTROL Account]** nell&#39;angolo superiore destro.

1. Nella finestra di dialogo visualizzata, fare clic su **[!UICONTROL Projects]**.

1. Vengono visualizzate le credenziali API:

![Recupero credenziali API Mixpanel](../../../assets/Mixpanel_API_creds.png)

Tienilo aperto, ti serve per chiuderlo.

## Immissione delle credenziali API [!DNL Mixpanel] in [!DNL Commerce Intelligence] {#stepthree}

1. Copiare `API Key` e `Secret` nella pagina delle credenziali di [!DNL Mixpanel] in [!DNL Commerce Intelligence].
1. Fare clic su **[!UICONTROL Connect to Mixpanel]** per completare la configurazione.

Se la connessione ha esito positivo, _ha esito positivo.Il messaggio_ viene visualizzato nella parte superiore della pagina.

### Correlato

* [Previsti [!DNL Mixpanel] dati](../integrations/mixpanel-data.md)
* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
