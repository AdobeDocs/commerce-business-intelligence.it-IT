---
title: Connetti Mixpanel
description: Scopri come analizzare il modo in cui gli utenti si spostano e utilizzano i tuoi siti web e le tue app.
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# Connetti [!DNL Mixpanel]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![](../../../assets/Mixpanel_logo.png)

Con [!DNL Mixpanel] puoi analizzare il modo in cui gli utenti si spostano e utilizzano i tuoi siti Web e le tue app. Osservando da vicino i dati sul comportamento degli utenti, si ottengono decisioni di progettazione e sviluppo più intelligenti, il che significa un prodotto complessivamente migliore. La connessione di [!DNL Mixpanel] a [!DNL Commerce Intelligence] consente di analizzare il comportamento degli utenti e come questo comportamento si traduce in ricavi.

Collegare i dati di [!DNL Mixpanel] a [!DNL Commerce Intelligence] è un semplice processo in tre fasi:

1. [Apri la pagina delle credenziali  [!DNL Mixpanel]  in [!DNL Commerce Intelligence]](#stepone)
1. [Recupera le tue credenziali API  [!DNL Mixpanel] ](#steptwo)
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
* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=it)
