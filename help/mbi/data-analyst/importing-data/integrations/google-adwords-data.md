---
title: Previsti dati di Google Adwords
description: Scopri come utilizzare Data Warehouse Manager per tracciare facilmente i campi di dati rilevanti per l’analisi.
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# Previsti dati di Google Adwords

Dopo [hai connesso il tuo [!DNL Google Adwords] account](../integrations/google-adwords.md), è possibile utilizzare [Gestione Date Warehouse](../../data-warehouse-mgr/tour-dwm.md) per tracciare facilmente i campi di dati rilevanti per l’analisi.

In questa pagina sono disponibili due tabelle per la replica nella Data Warehouse: `campaigns[account-id]` e `adwords[account-id]`.

Il `campaigns` tabella *deve essere utilizzato per impostazione predefinita*, in modo da poter iniziare sincronizzando tutti i campi rilevanti da quella tabella.

Il `adwords` la tabella contiene quattro colonne che non sono `campaigns` tabella:

* `keyword`
* `adContent`
* `adDestinationUrl`
* `adGroup`

Quando ti interessa eseguire un’analisi che considera questi attributi, devi utilizzare `adwords` tabella.

>[!IMPORTANT]
>
>Questa tabella esclude le righe in cui tutte e quattro queste colonne sono `null`.

Ecco uno schema previsto per entrambe le tabelle:

## `Campaigns` tabella

Il `campaigns` la tabella contiene le colonne seguenti:

| **Colonna** | **Descrizione** |
|-----|-----|
| `\_id` | Chiave primaria per la tabella |
| `accountId` | ID account |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | Numero totale di clic per il giorno |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | Costo totale della campagna per il giorno |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] ID campagna |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | Nome della campagna (ad esempio, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | Data di esecuzione della campagna |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | Numero di impression per il giorno |
| `profileId` | ID profilo |
| `profileName` | Nome del profilo |
| `\_updated\_at` | Data e ora dell&#39;ultimo aggiornamento per questa riga |

{style="table-layout:auto"}

## Tabella AdWords

Il `adwords` la tabella contiene le colonne seguenti:

| **Colonna** | **Descrizione** |
|-----|-----|
| `\_id` | Chiave primaria per la tabella |
| `accountId` | ID account |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | Numero totale di clic per il giorno |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | Costo totale della campagna per il giorno |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] ID campagna |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | Nome della campagna (ad esempio, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | Data di esecuzione della campagna |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | Numero di impression per il giorno |
| `profileId` | ID profilo |
| `profileName` | Nome del profilo |
| `\_updated\_at` | Data e ora dell&#39;ultimo aggiornamento per questa riga |
| `keyword` | Parola chiave della campagna |
| `adContent` | Prima riga di testo per la campagna online |
| `adDestinationUrl` | L&#39;URL al quale [!DNL Adwords] traffico di annunci indirizzato |
| `adGroup` | Il nome del [!DNL Adwords] gruppo di annunci |

{style="table-layout:auto"}

Utilizzando questi dati, puoi iniziare a creare [metriche ](../../../data-user/reports/ess-manage-data-metrics.md) e [rapporti](../../../tutorials/using-visual-report-builder.md) in base ai dati di spesa e [uniscilo ai ricavi del tuo ciclo di vita per calcolare il ROI](../../analysis/roi-ad-camp.md).

## Tabelle consolidate

L’Adobe consiglia di creare un `consolidated ad spend` tabella per combinare i dati provenienti da tutte le diverse origini pubblicitarie in un’unica tabella. Questo consente di utilizzare un singolo set di metriche per l’analisi pubblicitaria.

Senza una tabella consolidata, se crei una dashboard bella sul `adwords` tabella, devi replicare il reporting o creare metriche duplicate per confrontare tali dati con il tuo [!DNL Facebook Ads] dati. L’utilizzo di una tabella consolidata consente di incorporare facilmente [!DNL Facebook Ads] con i dati esistenti [!DNL Adwords] rapporti. Puoi anche segmentare per piattaforma di annunci.

Se hai già sincronizzato i campi di cui sopra, contattaci per consolidare la spesa pubblicitaria.
