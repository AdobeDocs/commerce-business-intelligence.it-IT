---
title: Dati previsti di Facebook Ads
description: Breve panoramica delle tabelle che si consiglia di sincronizzare con la Data Warehouse
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# Previsti [!DNL Facebook Ads] dati

Dopo aver [connesso il tuo [!DNL Facebook Ads] account](../integrations/facebook-ads.md), puoi utilizzare [Gestione Date Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) per tenere traccia facilmente dei campi di dati rilevanti per l&#39;analisi.

Questo argomento offre una breve panoramica delle tabelle. L&#39;Adobe consiglia di eseguire la sincronizzazione con la Data Warehouse. Questo evidenzia solo le tabelle principali, in quanto sono presenti alcune sottotabelle.

## Tabelle core per campagne pubblicitarie

Queste tabelle contengono dati sui componenti core di ad campaign.

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)

Questa tabella è la tabella principale delle campagne in un account [!DNL Facebook Ads]. Le colonne includono `campaign id`, `name`, `status (active/paused)`, `objective`.

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

Questo record di tabella è la tabella principale di [!DNL Facebook Ads] set in un account [!DNL Facebook Ads]. Le colonne includono l&#39;annuncio `Campaign id/name` a cui appartiene il set di annunci, il budget, il tipo di offerta, la pianificazione e le informazioni sul targeting del pubblico.

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/adgroup)

Questa tabella registra tutti gli annunci in un account [!DNL Facebook Ads]. Le colonne includono le informazioni sull’annuncio, tra cui il set di annunci e la campagna pubblicitaria a cui appartiene, l’offerta pubblicitaria, il targeting degli annunci e il riferimento a specifici contenuti creativi (immagine/testo) utilizzati dall’annuncio.

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-creative)

Questa tabella registra le creatività utilizzate in [!DNL Facebook Ads]. I creativi includono il nome della creatività, la descrizione e gli URL immagine pertinenti, se del caso.

## Tabelle di campagne segmentate

Le tabelle seguenti contengono una voce per ogni combinazione di campagna/set/annunci per ogni giorno, segmentata per dimensioni quali età, genere e paese.

### `facebook _ads insights_ (account-id)`

Questa tabella include una voce per ogni combinazione di campagna/set/annunci per ogni giorno, oltre a statistiche quali impression, clic, costo, cpc, cpm, cpp, ctr, portata, portata social e spesa.

### `facebook _ads insights_ (account-id)_~\_actions`

Sottotabella della tabella `facebook_ads_insights_{account_id}`. Include i dati di conversione per le azioni che si verificano in base a campagne diverse.

### `facebook _ads insights country_ (account-id)`

Questa tabella include le stesse informazioni della tabella `facebook_ads_insights_{account_id}` e le segmenta per paese.

### `facebook ads insights age and gender (account-id)`

Questa tabella include le stesse informazioni della tabella `facebook_ads_insights_{account_id}` e le segmenta per età e genere.

## Correlato

* [Connessione in corso  [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
