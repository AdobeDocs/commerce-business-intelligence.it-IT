---
title: Dati Google Analytics previsti
description: Scopri come interagire con le metriche Google Analytics.
exl-id: db9fdaaa-47a9-4095-b1f8-9b6c74c25b7c
source-git-commit: 0e9d30155432a29cf67d29a10646a2971ea0382f
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Previsto [!DNL Google Analytics] dati

Dopo aver connesso un [!DNL Google Analytics] integrazione, è possibile interagire con [!DNL Google Analytics] metriche *immediatamente nel`Visual Report Builder`*. Quando si immette la variabile `Visual Report Builder`, se fai clic su **[!UICONTROL Add a Metric]**, una serie di metriche dal [!DNL Google Analytics] il profilo viene visualizzato in un menu a discesa immediatamente sotto le metriche nella Data Warehouse.

La [!DNL Google Analytics] integrazione *live* — questo significa che `Report Builder` richiede dati da [!DNL Google Analytics] *immediatamente* quando aggiungi una metrica al rapporto. Significa anche che le metriche a cui puoi accedere sono definite esattamente come sono in [!DNL Google Analytics]e che tali valori non sono *immagazzinato* nel tuo [!DNL MBI] account : viene visualizzato solo visivamente nei rapporti.

+++Metriche e Dimension supportati (Google Analytics 3 o Universal Analytics)

>[!NOTE]
>
>Il 1° luglio 2023, Universal Analytics standard ([!DNL Google Analytics] 3) le proprietà non elaboreranno più i dati. Potrai visualizzare i rapporti di Universal Analytics per un periodo di tempo successivo al 1° luglio 2023. Tuttavia, i nuovi dati entreranno solo in [!DNL Google Analytics] 4 proprietà.

[!DNL Google Analytics] integrazioni in [!DNL MBI] utilizza [!DNL Google Analytics] [API di reportistica di base](https://developers.google.com/analytics/devguides/reporting/core/v3/)e supportano le metriche e le dimensioni seguenti.

>[!NOTE]
>
>Per evitare risultati imprevisti o insensati, verifica che tutte le dimensioni utilizzate siano compatibili con una o più metriche utilizzate nel `Report Builder`. Puoi controllare [qui](https://ga-dev-tools.google/dimensions-metrics-explorer/).

## Metriche supportate

| [!DNL MBI] Nome visualizzato | [!DNL Google Analytics] Nome/Formula |
| --- | --- |
| `Page Views` | `ga:pageviews` |
| `Total Time Spent On Page` | `ga:timeOnPage` |
| `Bounces (One Page Visits)` | `ga:bounces` |
| `Entrances` | `ga:entrances` |
| `Exits` | `ga:exits` |
| `Unique Pageviews` | `ga:uniquePageviews` |
| `Ad Clicks` | `ga:adClicks` |
| `Ad Cost` | `ga:adCost` |
| `Cost per Click (CPC)` | `ga:CPC` |
| `Cost per Thousand Impressions (CPM)` | `ga:CPM` |
| `Click-Through Rate (CTR)` | `ga:CTR` |
| `Impressions` | `ga:impressions` |
| `Product Revenue` | `ga:itemRevenue` |
| `Products Purchased` | `ga:itemQuantity` |
| `Revenue` | `ga:transactionRevenue` |
| `Transactions` | `ga:transactions` |
| `Shipping Revenue` | `ga:transactionShipping` |
| `Tax Revenue` | `ga:transactionTax` |
| `Unique Purchases` | `ga:uniquePurchases` |
| `Pageviews After Internal Search` | `ga:searchDepth` |
| `Visit Duration After Internal Search` | `ga:searchDuration` |
| `Exits After Internal Search` | `ga:searchExits` |
| `Internal Search Refinements` | `ga:searchRefinements` |
| `Unique Users Using Internal Search` | `ga:searchUniques` |
| `Bounce Rate` | `ga:visitBounceRate` |
| `Average Time on Page` | `ga:avgTimeOnPage` |
| `Average Session Length` | `ga:avgSessionDuration` |
| `All Goals Conversion Rate` | `ga:goalConversionRateAll` |
| `Total Events` | `ga:totalEvents` |
| `Unique Events` | `ga:uniqueEvents` |
| `Event Value` | `ga:eventValue` |
| `Average Domain Lookup Time` | `ga:avgDomainLookupTime` |
| `Average Page Download Time` | `ga:avgPageDownloadTime` |
| `Average Page Load Time` | `ga:avgPageLoadTime` |
| `Transactions Per Visit` | `ga:transactionsPerVisit` |
| `Sessions` | `ga:sessions` |
| `Users` | `ga:users` |
| `New Users | ga:newUsers` |
| `Sessions Where Internal Search Used` | `ga:searchSessions` |
| `Goal X Starts` | `ga:goal...Starts` |
| `Goal X Completions` | `ga:goal...Completions` |
| `Goal X Conversion Rate` | `ga:goal...ConversionRate` |
| `Goal X Total Value` | `ga:goal...Value` |
| `All Goal Starts` | `ga:goalStartsAll` |
| `All Goal Completions` | `ga:goalCompletionsAll` |
| `All Goals Conversion Rate` | `ga:goalConversionRateAll` |
| `Total Goal Value` | `ga:goal1ValueAll` |

{style="table-layout:auto"}

## Dimension supportati

| [!DNL MBI] Nome visualizzato | [!DNL Google Analytics] Nome/Formula | Raggruppabile? |
| --- | --- | --- |
| `Ad Content` | `ga:adContent` | `Yes` |
| `Ad Group` | `ga:adGroup` | `Yes` |
| `Matched Search Query` | `ga:adMatchedQuery` | `Yes` |
| `Placement Domain` | `ga:adPlacementDomain` | `Yes` |
| `Placement URL` | `ga:adPlacementUrl` | `Yes` |
| `Affiliation` | `ga:affiliation` | `Yes` |
| `Browser` | `ga:browser` | `Yes` |
| `Browser Version` | `ga:browserVersion` | `Yes` |
| `Campaign` | `ga:campaign` | `Yes` |
| `Continent` | `ga:continent` | `Yes` |
| `Custom Variable 2` | `ga:customVarValue2` | `Yes` |
| `Custom Variable 3` | `ga:customVarValue3` | `Yes` |
| `Custom Variable 5` | `ga:customVarValue5` | `Yes` |
| `Date` | `ga:date` | `No` |
| `Day` | `ga:day` | `No` |
| `Days Since Last Session` | `ga:daysSinceLastSession` | `Yes` |
| `Days Since Referring Campagin` | `ga:daysToTransaction` | `Yes` |
| `Device Category` | `ga:deviceCategory` | `Yes` |
| `Custom Dimension 10` | `ga:dimension10` | `Yes` |
| `Custom Dimension 12` | `ga:dimension12` | `Yes` |
| `Custom Dimension 13` | `ga:dimension13` | `Yes` |
| `Custom Dimension 18` | `ga:dimension18` | `Yes` |
| `Custom Dimension 2` | `ga:dimension2` | `Yes` |
| `Custom Dimension 20` | `ga:dimension20` | `Yes` |
| `Custom Dimension 3` | `ga:dimension3` | `Yes` |
| `Custom Dimension 4` | `ga:dimension4` | `Yes` |
| `Custom Dimension 5` | `ga:dimension5` | `Yes` |
| `Custom Dimension 8` | `ga:dimension8` | `Yes` |
| `Custom Dimension 9` | `ga:dimension9` | `Yes` |
| `Event Action` | `ga:eventAction` | `Yes` |
| `Event Category` | `ga:eventCategory` | `Yes` |
| `Event Label` | `ga:eventLabel` | `Yes` |
| `Exit Page Path` | `ga:exitPagePath` | `Yes` |
| `Flash Version Supported` | `ga:flashVersion` | `Yes` |
| `Hour` | `ga:hour` | `No` |
| `In-Market Segment` | `ga:interestInMarketCategory` | `Yes` |
| `Language` | `ga:language` | `Yes` |
| `Longitude` | `ga:longitude` | `No` |
| `Medium` | `ga:medium` | `Yes` |
| `Metro` | `ga:metro` | `Yes` |
| `Mobile Device Branding` | `ga:mobileDeviceBranding` | `Yes` |
| `Mobile Device Info` | `ga:mobileDeviceInfo` | `Yes` |
| `Month` | `ga:month` | `No` |
| `Operating System` | `ga:operatingSystem` | `Yes` |
| `Operating System Version` | `ga:operatingSystemVersion` | `Yes` |
| `Pages Viewed per Session` | `ga:pageDepth` | `Yes` |
| `Page Path` | `ga:pagePath` | `Yes` |
| `Product Category` | `ga:productCategory` | `Yes` |
| `Product Name` | `ga:productName` | `Yes` |
| `Referral URL` | `ga:referralPath` | `No` |
| `Region (State)` | `ga:region` | `Yes` |
| `Screen Colors` | `ga:screenColors` | `Yes` |
| `Screen Resolution` | `ga:screenResolution` | `Yes` |
| `Internal Search Category` | `ga:searchCategory` | `Yes` |
| `Internal Search Refined Keyword(s)` | `ga:searchKeywordRefinement` | `Yes` |
| `Internal Search Used?` | `ga:searchUsed` | `Yes` |
| `Second Page Path` | `ga:secondPagePath` | `Yes` |
| `Source` | `ga:source` | `Yes` |
| `Sub-Continent` | `ga:subContinent` | `Yes` |
| `Transaction ID` | `ga:transactionId` | `Yes` |
| `Custom (User Defined) Value` | `ga:userDefinedValue` | `Yes` |
| `Year` | `ga:year` | `No` |

{style="table-layout:auto"}

+++

+++Metriche e Dimension supportati (Google Analytics 4)

[!DNL Google Analytics] integrazioni in [!DNL MBI] utilizza [!DNL Google Analytics] [API dati v1 (GA4)](https://developers.google.com/analytics/devguides/reporting/data/v1).

>[!NOTE]
>
> MBI non supporta le dimensioni seguenti: `cohort`, `cohortNthDay`, `cohortNthMonth`e `cohortNthWeek`.
>
>Per evitare risultati imprevisti o insensati, verifica che tutte le dimensioni utilizzate siano compatibili con una o più metriche utilizzate nel `Visual Report Builder`. Puoi controllare la [Esplora Dimension e metriche GA4](https://ga-dev-tools.google/ga4/dimensions-metrics-explorer/).

+++
