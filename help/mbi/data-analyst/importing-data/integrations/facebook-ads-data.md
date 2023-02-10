---
title: Dati previsti di Facebook Ads
description: Scopri una breve panoramica delle tabelle consigliate per la sincronizzazione con il data warehouse
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# Previsto [!DNL Facebook Ads] dati

![](../../../assets/Facebook_Logo.png)

Dopo aver [ha collegato [!DNL Facebook Ads] account](../integrations/facebook-ads.md), puoi utilizzare la [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) per tenere traccia facilmente dei campi dati rilevanti ai fini dell’analisi.

In questo articolo, ti offriamo una breve panoramica delle tabelle che ti consigliamo di sincronizzare con il data warehouse. Questo non è un elenco completo, dato che ci sono un bel po &#39;di sottotabelle. Stiamo solo evidenziando le tabelle principali.

## Tabelle delle campagne pubblicitarie core

Queste tabelle contengono dati sui componenti principali delle campagne pubblicitarie.

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/reference/ads-api/adcampaign/)

Questa tabella è la tabella principale delle campagne in una [!DNL Facebook Ads] conto. Colonne incluse `campaign id`, `name`, `status (active/paused)`, `objective`.

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

I record di questa tabella sono la tabella principale di [!DNL Facebook Ads] Imposta in un [!DNL Facebook Ads] conto. Le colonne includono l’annuncio `Campaign id/name` il set di annunci appartiene a, le informazioni sul budget, il tipo di offerta, la pianificazione e il targeting del pubblico.

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/reference/ads-api/adgroup/)

Questa tabella registra tutti gli annunci in una [!DNL Facebook Ads] conto. Le colonne includono le informazioni sull’annuncio, compresi il set di annunci e la campagna di annunci a cui appartiene, le offerte di annunci, il targeting degli annunci e il riferimento a specifici contenuti creativi (immagine/testo) utilizzati dall’annuncio.

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/reference/ads-api/adcreative/)

Questa tabella registra tutti i creativi utilizzati in [!DNL Facebook Ads]. Includono nome creativo, descrizione e URL immagine pertinenti, se appropriato.

## Tabelle di campagne segmentate

Le tabelle seguenti contengono una voce per ogni campagna/set/ad combinato per ogni giorno, segmentata per dimensioni quali età, genere e paese.

### `facebook _ads insights_ (account-id)`

Questa tabella include una voce per ogni combinazione campagna/set/ad per ogni giorno, insieme a statistiche quali impression, clic, costo, cpc, cpm, cpp, ctr, reach, social reach e spesa.

### `facebook _ads insights_ (account-id)_~\_actions`

Questa è una sottotabella del `facebook_ads_insights_{account_id}` tabella. Include i dati di conversione per le azioni che avvengono in base a campagne diverse.

### `facebook _ads insights country_ (account-id)`

Questa tabella include le stesse informazioni della `facebook_ads_insights_{account_id}` e la segmenta per paese.

### `facebook ads insights age and gender (account-id)`

Questa tabella include le stesse informazioni della `facebook_ads_insights_{account_id}` e la segmenta per età e genere.

## Correlati

* [Collegamento [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [Riautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
