---
title: Connetti Mixpanel
description: Scopri come analizzare il modo in cui gli utenti si spostano e utilizzano i tuoi siti web e le tue app.
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
source-git-commit: 8de036e2717aedef95a8bb908898fd9b9bc9c3fa
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# Connetti [!DNL Mixpanel]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![](../../../assets/Mixpanel_logo.png)

Con [!DNL Mixpanel], puoi analizzare il modo in cui gli utenti si spostano e utilizzano i tuoi siti web e le tue app. Osservando da vicino i dati sul comportamento degli utenti, si ottengono decisioni di progettazione e sviluppo più intelligenti, il che significa un prodotto complessivamente migliore. Connessione [!DNL Mixpanel] a [!DNL MBI] consente di analizzare il comportamento degli utenti e come questo comportamento si traduce in ricavi.

Collegamento [!DNL Mixpanel] dati a [!DNL MBI] un semplice processo in tre fasi:

1. [Apri [!DNL Mixpanel] pagina delle credenziali in [!DNL MBI]](#stepone)
1. [Recupera [!DNL Mixpanel] Credenziali API](#steptwo)
1. [Immetti il [!DNL Mixpanel] Credenziali API in MBI](#stepthree)

Per completare questa procedura, devi aprire due finestre o schede del browser: una per [!DNL MBI], l&#39;altro per [!DNL Mixpanel] account.

## Apertura di [!DNL Mixpanel] pagina delle credenziali {#stepone}

Introduzione:

1. Vai a `Connections` pagina in **[!DNL Manage Data** > **Connections]**.
1. Clic **[!UICONTROL Add a New Source]**, situato sul lato destro dello schermo sopra la `Data Sources` tabella.
1. Fai clic su [!DNL Mixpanel] e viene aperta la pagina delle credenziali.

Lascia aperta questa pagina per il momento e passa alla finestra del browser con il tuo [!DNL Mixpanel] account.

## Recupero del [!DNL Mixpanel] Credenziali API {#steptwo}

Se non hai effettuato l’accesso a [!DNL Mixpanel] account, eseguire questa operazione e quindi eseguire le operazioni seguenti:

1. Clic **[!UICONTROL Account]** in alto a destra.
1. Nella finestra di dialogo visualizzata, fai clic su **[!UICONTROL Projects]**.
1. Vengono visualizzate le credenziali API:

![Recupero credenziali API Mixpanel](../../../assets/Mixpanel_API_creds.png)

Tienilo aperto, ti serve per chiuderlo.

## Inserimento di [!DNL Mixpanel] Credenziali API in [!DNL MBI] {#stepthree}

1. Copia il `API Key` e `Secret` in [!DNL Mixpanel] pagina delle credenziali in [!DNL MBI].
1. Clic **[!UICONTROL Connect to Mixpanel]** per completare la configurazione.

Tutto qui! Se la connessione ha esito positivo, viene visualizzata una _Operazione completata._ viene visualizzato nella parte superiore della pagina.

### Correlato

* [Previsto [!DNL Mixpanel] dati](../integrations/mixpanel-data.md)
* [Reautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
