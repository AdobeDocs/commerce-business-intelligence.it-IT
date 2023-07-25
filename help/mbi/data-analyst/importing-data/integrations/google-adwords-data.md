---
title: Previsti dati di Google Adwords
description: Scopri come utilizzare Data Warehouse Manager per tracciare facilmente i campi di dati rilevanti per l’analisi.
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# Previsto [!DNL Google Adwords] dati

Dopo [hai connesso il tuo [!DNL Google Adwords] account](../integrations/google-adwords.md), è possibile utilizzare [Gestione Date Warehouse](../../data-warehouse-mgr/tour-dwm.md) per tracciare facilmente i campi di dati rilevanti per l’analisi.

In questa pagina sono disponibili due tabelle per la replica nella Data Warehouse:

* `campaigns[account-id]`
* `adwords[account-id]`

Il `campaigns` tabella *deve essere utilizzato per impostazione predefinita*, in modo da poter iniziare sincronizzando tutti i campi rilevanti da quella tabella.

Il `adwords` la tabella contiene quattro colonne che non sono `campaigns` tabella:

1. `keyword`
1. `adContent`
1. `adDestinationUrl`
1. `adGroup`

Quando ti interessa eseguire un’analisi che considera questi attributi, devi utilizzare `adwords` tabella.

>[!IMPORTANT]
>
>Questa tabella esclude le righe in cui tutte e quattro queste colonne sono `null`.

Di seguito è riportato uno schema previsto per entrambe le tabelle.

## [!DNL Campaigns] tabella

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

## [!DNL AdWords] tabella

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

Utilizzando questi dati, puoi iniziare a creare [metriche](../../../data-user/reports/ess-manage-data-metrics.md) e [rapporti](../../../tutorials/using-visual-report-builder.md) in base ai dati di spesa e [uniscilo ai ricavi del tuo ciclo di vita per calcolare il ROI](../../analysis/roi-ad-camp.md).

## Tabelle consolidate

[!DNL Adobe] consiglia di creare un `consolidated ad spend` tabella per combinare i dati provenienti da tutte le diverse origini pubblicitarie in un’unica tabella. Questo consente di utilizzare un singolo set di metriche per l’analisi pubblicitaria.

Se non disponi di una tabella consolidata e costruisci una bella dashboard sul `adwords` tabella, devi replicare il reporting o creare metriche duplicate per confrontare tali dati con il tuo [!DNL Facebook Ads] dati. L’utilizzo di una tabella consolidata consente di incorporare facilmente [!DNL Facebook Ads] con i dati esistenti [!DNL Adwords] rapporti. Puoi anche segmentare per piattaforma di annunci.

Se hai già sincronizzato i campi qui sopra, [contattaci](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) per consolidare la spesa pubblicitaria.
