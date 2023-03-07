---
title: Analisi codice coupon (base)
description: Scopri le prestazioni dei coupon nel tuo business, un modo interessante per segmentare gli ordini e comprendere meglio le abitudini dei clienti.
exl-id: 0d486259-b210-42ae-8f79-cd91cc15c2c2
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# Analisi codice coupon di base

Comprendere le prestazioni dei coupon della tua azienda è un modo interessante per segmentare gli ordini e comprendere meglio le abitudini dei clienti.

Questo articolo illustra i passaggi necessari per creare questa analisi per comprendere le prestazioni dei clienti acquisiti con coupon, visualizzare le tendenze e tenere traccia dell’utilizzo del codice coupon individuale.

![](../../assets/coupon_analysis_dash_720.png)<!--{: width="807" height="471"}-->

## Guida introduttiva

Innanzitutto, una nota su come viene tenuta traccia dei codici coupon. Se un cliente ha applicato un coupon a un ordine, possono verificarsi tre situazioni:

* Uno sconto si riflette nel `base_grand_total` importo (il tuo `Revenue` in MBI)
* Il codice coupon viene memorizzato in `coupon_code` campo. Se questo campo è NULL (vuoto), all&#39;ordine non è associato alcun coupon.
* L&#39;importo scontato è memorizzato in `base_discount_amount`. A seconda della configurazione, questo valore può apparire negativo o positivo.

## Creazione di una metrica

Il primo passaggio consiste nel creare una nuova metrica con i passaggi seguenti:

* Accedi a **[!UICONTROL Manage Data > Metrics > Create New Metric]**.

* Seleziona la `sales_order`.
* Questa metrica esegue una **Somma** il **base_discount_amount** colonna, ordinata per **created_at**.
   * [!UICONTROL Filters]:
      * Aggiungi il `Orders we count` (Set di filtri salvato)
      * Aggiungi quanto segue:
         * `coupon_code`**NON È**`[NULL]`
      * Assegna un nome alla metrica, ad esempio `Coupon discount amount`.

## Creazione del dashboard

* Una volta creata la metrica:
   * Accedi a [!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
   * Assegna al dashboard un nome come `_Coupon Analysis_`.

* Qui puoi creare e aggiungere tutti i rapporti.

## Creazione di rapporti

* **Nuovi report:**

>[!NOTE]
>
>Il [!UICONTROL Time Period]** per ogni rapporto è elencato come `All-time`. Puoi modificarlo in base alle tue esigenze di analisi. L’Adobe consiglia che tutti i rapporti su questo dashboard riguardino lo stesso periodo di tempo, ad esempio `All time`, `Year-to-date`, o `Last 365 days`.

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
         * [`A`] `coupon_code` **È** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`


* **Ricavi netti da ordini con cedole**
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

* **Ricavi medi ciclo di vita: clienti con coupon acquisiti**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Aggiungi filtro:
         * [`A`] `Customer's first order's coupon_code` **NON È** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **Ricavi medi nel ciclo di vita: clienti acquisiti senza cedola**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Aggiungi filtro:
         * [A] `Customer's first order's coupon_code` **È**`[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **Dettagli sull’utilizzo del coupon (primi ordini)**
   * Metrica `1`: `Orders`
      * Aggiungi filtro:
         * [`A`] `coupon_code` **NON È**`[NULL]`
         * [`B`] `Customer's order number` **Uguale** `1`
   * Metrica `2`: `Revenue`
      * Aggiungi filtro:
         * [`A`] `coupon_code` **NON È**`[NULL]`
         * [`B`] `Customer's order number` **Uguale** `1`
      * Rinomina:  `Net revenue`
   * Metrica `3`: `Coupon discount amount`
      * Aggiungi filtro:
         * [`A`] `coupon_code` **NON È**`[NULL]`
         * [`B`] `Customer's order number` **Uguale** `1`
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








* **Ricavi medi ciclo di vita per cedola primo ordine**
   * [!UICONTROL Metric]:**Ricavi medi nel ciclo di vita**
      * Aggiungi filtro:
         * [`A`] `coupon_code` **È**`[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **Dettagli sull’utilizzo del coupon (primi ordini)**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Aggiungi filtro:
         * [`A`] `Customer's first order's coupon_code` **NON È** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Interval]: `None`
   * [!UICONTROL Group by]: `Customer's first order's coupon_code`
   * 

      [!UICONTROL Tipo di grafico]: **Column**


* **Nuovi clienti per acquisizione coupon/non coupon**
   * Metrica `1`: `New customers`
      * Aggiungi filtro:
         * [`A`] `Customer's first order's coupon_code` **NON È** `[NULL]`
      * [!UICONTROL Rename]: `Coupon acquisition customer`
   * Metrica `2`: `New customers`
      * Aggiungi filtro:
         * [`A`] `coupon_code` **È**`[NULL]`
      * [!UICONTROL Rename]: `Non-coupon acquisition customer`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * [!UICONTROL Chart type]: `Stacked Column`





Dopo aver generato i rapporti, consulta l’immagine nella parte superiore di questo argomento per informazioni su come organizzare i rapporti sul dashboard.
