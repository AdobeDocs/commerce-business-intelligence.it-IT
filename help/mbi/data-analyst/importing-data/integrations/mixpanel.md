---
title: Connetti pannello multiplo
description: Scopri come analizzare come gli utenti navigano e utilizzano i tuoi siti web e le tue app.
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Connetti [!DNL Mixpanel]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![](../../../assets/Mixpanel_logo.png)

Con [!DNL Mixpanel], puoi analizzare il modo in cui gli utenti navigano e utilizzano i tuoi siti web e le tue app. Osservare da vicino i dati sul comportamento degli utenti porta a decisioni di progettazione e sviluppo più intelligenti, il che significa un prodotto migliore in generale. Collegamento [!DNL Mixpanel] a [!DNL MBI] ti consente di analizzare il comportamento degli utenti e il modo in cui tale comportamento si traduce in entrate.

Collegamento del [!DNL Mixpanel] dati a [!DNL MBI] un semplice processo in tre fasi:

1. [Apri [!DNL Mixpanel] pagina delle credenziali in [!DNL MBI]](#stepone)
1. [Recupera il tuo [!DNL Mixpanel] Credenziali API](#steptwo)
1. [Inserisci il tuo [!DNL Mixpanel] Credenziali API in MBI](#stepthree)

Per completare questo processo, dovrai aprire due finestre o schede del browser, una per [!DNL MBI], l&#39;altro per il tuo [!DNL Mixpanel] conto.

## Apertura [!DNL Mixpanel] pagina delle credenziali {#stepone}

Cominciamo:

1. Vai a `Connections` pagina sotto **[!DNL Manage Data** > **Connections]**.
1. Fai clic su **[!UICONTROL Add a New Source]**, situato sul lato destro dello schermo sopra il `Data Sources` tabella.
1. Fai clic sul pulsante [!DNL Mixpanel] Viene visualizzata la pagina delle credenziali.

Lascia aperta questa pagina per il momento e passa alla finestra del browser con il tuo [!DNL Mixpanel] conto.

## Recupero [!DNL Mixpanel] Credenziali API {#steptwo}

Se non hai effettuato l’accesso al tuo [!DNL Mixpanel] tuttavia, esegui questa operazione e procedi come segue:

1. Fai clic su **[!UICONTROL Account]** nell&#39;angolo in alto a destra.
1. Nella finestra di dialogo visualizzata, fai clic su **[!UICONTROL Projects]**.
1. Verranno visualizzate le credenziali API:

![Recupero delle credenziali API di Mixpanel](../../../assets/Mixpanel_API_creds.png)

Tenete questo aperto - abbiamo bisogno che lo richiami.

## Inserimento del [!DNL Mixpanel] Credenziali API in [!DNL MBI] {#stepthree}

1. Copia il `API Key` e `Secret` nel [!DNL Mixpanel] pagina delle credenziali in [!DNL MBI].
1. Fai clic su **[!UICONTROL Connect to Mixpanel]** per completare la configurazione.

Tutto qui! Se la connessione ha esito positivo, un _Successo!_ il messaggio viene visualizzato nella parte superiore della pagina.

### Correlati

* [Previsto [!DNL Mixpanel] dati](../integrations/mixpanel-data.md)
* [Riautenticazione delle integrazioni](https://support.magento.com/hc/en-us/articles/360016733151)
