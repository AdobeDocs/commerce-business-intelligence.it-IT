---
title: Dati Adwords di Google previsti
description: Scopri come utilizzare Data Warehouse Manager per monitorare facilmente i campi dati rilevanti ai fini dell’analisi.
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# Dati Adwords di Google previsti

Dopo [hai connesso il tuo [!DNL Google Adwords] account](../integrations/google-adwords.md), puoi utilizzare la [Data Warehouse Manager](../../data-warehouse-mgr/tour-dwm.md) per tenere traccia facilmente dei campi dati rilevanti ai fini dell’analisi.

In questo caso, si noteranno due tabelle disponibili per la replica nel data warehouse: `campaigns[account-id]` e `adwords[account-id]`.

La `campaigns` tabella *deve essere utilizzato per impostazione predefinita*, in modo da poter iniziare sincronizzando tutti i campi pertinenti da quella tabella.

La `adwords` La tabella contiene quattro colonne che non si trovano nella `campaigns` tabella:

* `keyword`
* `adContent`
* `adDestinationUrl`
* `adGroup`

Ogni volta che sei interessato a eseguire un’analisi che considera questi attributi, devi utilizzare il `adwords` tabella.

>[!IMPORTANT]
>
>Questa tabella escluderà le righe in cui tutte e quattro le colonne sono `null`.

Di seguito è riportato uno schema previsto per entrambe le tabelle:

## `Campaigns` tabella

La `campaigns` La tabella contiene le colonne seguenti:

| **Colonna** | **Descrizione** |
|-----|-----|
| `\_id` | Chiave primaria per la tabella |
| `accountId` | ID account |
| [`adClicks`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | Numero totale di clic per il giorno |
| [`adCost`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adcost) | Costo totale della campagna per il giorno |
| [`adwordsCampaignID`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] ID campagna |
| [`campaign`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | Nome della campagna (ad esempio, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=time&amp;jump=ga_date) | Data di esecuzione della campagna |
| [`impressions`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_impressions) | Numero di impression per il giorno |
| `profileId` | ID profilo |
| `profileName` | Nome del profilo |
| `\_updated\_at` | Data e ora dell’ultimo aggiornamento per questa riga |

{style=&quot;table-layout:auto&quot;}

## Tabella AdWords

La `adwords` La tabella contiene le colonne seguenti:

| **Colonna** | **Descrizione** |
|-----|-----|
| `\_id` | Chiave primaria per la tabella |
| `accountId` | ID account |
| [`adClicks`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | Numero totale di clic per il giorno |
| [`adCost`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adcost) | Costo totale della campagna per il giorno |
| [`adwordsCampaignID`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] ID campagna |
| [`campaign`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | Nome della campagna (ad esempio, [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=time&amp;jump=ga_date) | Data di esecuzione della campagna |
| [`impressions`](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&amp;group=adwords&amp;jump=ga_impressions) | Numero di impression per il giorno |
| `profileId` | ID profilo |
| `profileName` | Nome del profilo |
| `\_updated\_at` | Data e ora dell’ultimo aggiornamento per questa riga |
| `keyword` | Parola chiave della campagna |
| `adContent` | La prima riga del testo per la campagna online |
| `adDestinationUrl` | L’URL a cui [!DNL Adwords] annunci traffico riferito |
| `adGroup` | Nome della [!DNL Adwords] gruppo di annunci |

{style=&quot;table-layout:auto&quot;}

Utilizzando questi dati puoi iniziare a creare [metriche ](../../../data-user/reports/ess-manage-data-metrics.md) e [rapporti](../../../tutorials/using-visual-report-builder.md) in base ai dati di spesa e [sposarlo ai ricavi della tua vita per calcolare il ROI](../../analysis/roi-ad-camp.md).

## Tabelle consolidate

Consigliamo sempre di creare una `consolidated ad spend` per combinare i dati provenienti da tutte le origini pubblicitarie multiple in un’unica tabella. Questo consente di utilizzare un singolo set di metriche per l’analisi pubblicitaria.

Senza una tabella consolidata, se si crea una bella dashboard `adwords` per confrontare tali dati con il tuo [!DNL Facebook Ads] dati. L’utilizzo di una tabella consolidata consente di incorporare [!DNL Facebook Ads] con i dati esistenti [!DNL Adwords] rapporti. (Non ti preoccupare - hai la possibilità di segmentare anche per piattaforma di annunci!)

Se hai già sincronizzato i campi di cui sopra, contattaci per consolidare la spesa pubblicitaria.
