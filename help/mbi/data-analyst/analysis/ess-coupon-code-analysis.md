---
title: Analisi codice coupon (base)
description: Scopri le prestazioni dei coupon nel tuo business, un modo interessante per segmentare gli ordini e comprendere meglio le abitudini dei clienti.
exl-id: 0d486259-b210-42ae-8f79-cd91cc15c2c2
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: d8fc96a58b72c601a5700f35ea1f3dc982d76571
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# Analisi codice coupon di base

Comprendere le prestazioni dei coupon della tua azienda è un modo interessante per segmentare gli ordini e comprendere meglio le abitudini dei clienti.

In questo argomento vengono documentati i passaggi necessari per creare questa analisi per comprendere le prestazioni dei clienti acquisiti con coupon, visualizzare le tendenze e tenere traccia dell’utilizzo del codice coupon individuale.

![](../../assets/coupon_analysis_dash_720.png)<!--{: width="807" height="471"}-->

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
   * 
     [!UICONTROL Metric]: `Orders`
      * Aggiungi filtro:
         * [`A`] `coupon_code` **NON È** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`

* **Ordini senza coupon**
   * 
     [!UICONTROL Metric]: `Orders`
      * Aggiungi filtro:
         * [`A`] `coupon_code` **IS** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`

* **Ricavi netti da ordini con coupon**
   * 
     [!UICONTROL Metric]: `Revenue`
      * Aggiungi filtro:
         * [`A`] `coupon_code` **NON È** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Sconti dai coupon**
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Ricavi medi vita: clienti acquisiti con coupon**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Aggiungi filtro:
         * [`A`] `Customer's first order's coupon_code` **NON È** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Ricavi medi vita: clienti acquisiti senza cedola**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Aggiungi filtro:
         * [A] `Customer's first order's coupon_code` **IS**`[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
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
      * 
        [!UICONTROL Format]: `Currency`

   * Crea formula:**% scontato**
      * Formula: `(C / (B - C))`
      * 
        [!UICONTROL Format]: `Percentage`

   * Crea formula: `Average order discount`
      * [!UICONTROL Formula]: `(C / A)`
      * 
        [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * 
     [!UICONTROL Tipo di grafico]: `Table`

* **Ricavi medi vita per coupon primo ordine**
   * [!UICONTROL Metric]:**Ricavi medi durata**
      * Aggiungi filtro:
         * [`A`] `coupon_code` **IS**`[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Dettagli sull&#39;utilizzo del coupon (nuovi ordini)**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Aggiungi filtro:
         * [`A`] `Customer's first order's coupon_code` **NON È** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Group by]: `Customer's first order's coupon_code`
   * 
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

![](../../assets/multicoupon_relationship_tables.png)
