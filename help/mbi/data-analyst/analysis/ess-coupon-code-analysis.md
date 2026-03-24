---
title: Analisi codice coupon (base)
description: Scopri le prestazioni dei coupon nel tuo business, un modo interessante per segmentare gli ordini e comprendere meglio le abitudini dei clienti.
exl-id: 0d486259-b210-42ae-8f79-cd91cc15c2c2
role: Admin, User
feature: Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/Wr-Lx6N-regGfzW3olk2hya-AybetR0w4Z2yFTWHeDM
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 532
ht-degree: 0%

---

# Analisi codice coupon di base

Comprendere le prestazioni dei coupon della tua azienda è un modo interessante per segmentare gli ordini e comprendere meglio le abitudini dei clienti.

In questo argomento vengono documentati i passaggi necessari per creare questa analisi per comprendere le prestazioni dei clienti acquisiti con coupon, visualizzare le tendenze e tenere traccia dell’utilizzo del codice coupon individuale.

![Dashboard di analisi del codice coupon con metriche di utilizzo e prestazioni](../../assets/coupon_analysis_dash_720.png)<!--{: width="807" height="471"}-->

## Guida introduttiva

Innanzitutto, una nota su come viene tenuta traccia dei codici coupon. Se un cliente ha applicato un coupon a un ordine, possono verificarsi tre situazioni:

* Uno sconto si riflette nell&#39;importo `base_grand_total` (la metrica `Revenue` in Commerce Intelligence)
* Il codice coupon è memorizzato nel campo `coupon_code`. Se questo campo è NULL (vuoto), all&#39;ordine non è associato alcun coupon.
* L&#39;importo scontato è archiviato in `base_discount_amount`. A seconda della configurazione, questo valore può apparire negativo o positivo.

A partire dalla versione 2.4.7 di Commerce, un cliente può applicare più codici coupon a un ordine. In questo caso:

* Tutti i codici coupon applicati sono memorizzati nel campo `coupon_code` di `sales_order_coupons`. Il primo codice coupon applicato viene memorizzato anche nel campo `coupon_code` di `sales_order`. Se questo campo è NULL (vuoto), all&#39;ordine non è associato alcun coupon.

## Creazione di una metrica

Il primo passaggio consiste nel creare una nuova metrica con i passaggi seguenti:

* Passa a **[!UICONTROL Manage Data > Metrics > Create New Metric]**.

* Selezionare `sales_order`.
* Questa metrica esegue una **somma** nella colonna **base_discount_amount**, ordinata da **created_at**.
   * [!UICONTROL Filters]:
      * Aggiungi `Orders we count` (set di filtri salvato)
      * Aggiungi quanto segue:
         * `coupon_code`**IS NOT**`[NULL]`
      * Assegnare un nome alla metrica, ad esempio `Coupon discount amount`.

## Creazione del dashboard

* Una volta creata la metrica:
   * Passa a [!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
   * Assegna al dashboard un nome come `_Coupon Analysis_`.

* Qui puoi creare e aggiungere tutti i rapporti.

## Creazione di rapporti

* **Nuovi report:**

>[!NOTE]
>
>[!UICONTROL Time Period]** per ogni report è elencato come `All-time`. Puoi modificarlo in base alle tue esigenze di analisi. Adobe consiglia che tutti i rapporti in questo dashboard riguardino lo stesso periodo di tempo, ad esempio `All time`, `Year-to-date` o `Last 365 days`.

* **Ordini con coupon**
   * &#x200B;
     [!UICONTROL Metric]: `Orders`
      * Aggiungi filtro:
         * [`A`] `coupon_code` **NON È** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`

* **Ordini senza coupon**
   * &#x200B;
     [!UICONTROL Metric]: `Orders`
      * Aggiungi filtro:
         * [`A`] `coupon_code` **IS** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`

* **Ricavi netti da ordini con coupon**
   * &#x200B;
     [!UICONTROL Metric]: `Revenue`
      * Aggiungi filtro:
         * [`A`] `coupon_code` **NON È** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Sconti dai coupon**
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Ricavi medi vita: clienti acquisiti con coupon**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Aggiungi filtro:
         * [`A`] `Customer's first order's coupon_code` **NON È** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Ricavi medi vita: clienti acquisiti senza cedola**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Aggiungi filtro:
         * [A] `Customer's first order's coupon_code` **IS**`[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Dettagli sull&#39;utilizzo del coupon (nuovi ordini)**
   * Metrica `1`: `Orders`
      * Aggiungi filtro:
         * [`A`] `coupon_code` **NON È**`[NULL]`
         * [`B`] `Customer's order number` **Uguale a** `1`

   * Metrica `2`: `Revenue`
      * Aggiungi filtro:
         * [`A`] `coupon_code` **NON È**`[NULL]`
         * [`B`] `Customer's order number` **Uguale a** `1`

      * Rinomina: `Net revenue`

   * Metrica `3`: `Coupon discount amount`
      * Aggiungi filtro:
         * [`A`] `coupon_code` **NON È**`[NULL]`
         * [`B`] `Customer's order number` **Uguale a** `1`

   * Crea formula: `Gross revenue`
      * [!UICONTROL Formula]: `(B – C)`
      * &#x200B;
        [!UICONTROL Format]: `Currency`

   * Crea formula:**% scontato**
      * Formula: `(C / (B - C))`
      * &#x200B;
        [!UICONTROL Format]: `Percentage`

   * Crea formula: `Average order discount`
      * [!UICONTROL Formula]: `(C / A)`
      * &#x200B;
        [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Interval]: `None`
   * &#x200B;
     [!UICONTROL Tipo di grafico]: `Table`

* **Ricavi medi vita per coupon primo ordine**
   * [!UICONTROL Metric]:**Ricavi medi durata**
      * Aggiungi filtro:
         * [`A`] `coupon_code` **IS**`[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Dettagli sull&#39;utilizzo del coupon (nuovi ordini)**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Aggiungi filtro:
         * [`A`] `Customer's first order's coupon_code` **NON È** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Group by]: `Customer's first order's coupon_code`
   * &#x200B;
     [!UICONTROL Tipo di grafico]: **Column**

* **Nuovi clienti tramite acquisizione coupon/non coupon**
   * Metrica `1`: `New customers`
      * Aggiungi filtro:
         * [`A`] `Customer's first order's coupon_code` **NON È** `[NULL]`

      * [!UICONTROL Rename]: `Coupon acquisition customer`

   * Metrica `2`: `New customers`
      * Aggiungi filtro:
         * [`A`] `coupon_code` **IS**`[NULL]`

      * [!UICONTROL Rename]: `Non-coupon acquisition customer`

   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * [!UICONTROL Chart type]: `Stacked Column`

Dopo aver generato i rapporti, consulta l’immagine nella parte superiore di questo argomento per informazioni su come organizzare i rapporti sul dashboard.

>[!NOTE]
>
>A partire dalla versione 2.4.7 di Adobe Commerce, i clienti possono utilizzare le tabelle **quote_cedole** e **sales_order_cedole** per ottenere informazioni su come il cliente utilizza più cedole.

![Diagramma delle relazioni tra tabelle per l&#39;analisi con più coupon](../../assets/multicoupon_relationship_tables.png)
