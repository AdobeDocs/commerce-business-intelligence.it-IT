---
title: Analisi del codice coupon (base)
description: Scopri le prestazioni del coupon della tua azienda è un modo interessante per segmentare i tuoi ordini e capire meglio le abitudini dei clienti.
exl-id: 0d486259-b210-42ae-8f79-cd91cc15c2c2
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# Analisi codice coupon di base

Comprendere le prestazioni del coupon della tua attività è un modo interessante per segmentare i tuoi ordini e capire meglio le abitudini dei clienti.

Abbiamo documentato i passaggi necessari per creare questa analisi per capire come si comportano i clienti con coupon acquisiti, vedere le tendenze e tenere traccia dell’utilizzo del codice coupon individuale.

![](../../assets/coupon_analysis_dash_720.png)<!--{: width="807" height="471"}-->

## Introduzione

In primo luogo, una nota su come vengono tracciati i codici coupon. Se un cliente ha applicato un coupon a un ordine, si verificano tre cose:

* Uno sconto è riflesso nel `base_grand_total` importo `Revenue` metrica in MBI)
* Il codice del coupon è memorizzato nel `coupon_code` campo . Se questo campo è NULL (vuoto), all’ordine non è associato un coupon.
* L&#39;importo scontato viene memorizzato in `base_discount_amount`. A seconda della configurazione, questo valore può apparire negativo o positivo.

## Creazione di una metrica

Il primo passaggio consiste nel creare una nuova metrica con i seguenti passaggi:

* Passa a **[!UICONTROL Manage Data > Metrics > Create New Metric]**.

* Seleziona la `sales_order`.
* Questa metrica esegue un **Somma** sulla **base_discount_amount** colonna, ordinata da **created_at**.
   * [!UICONTROL Filters]:
      * Aggiungi il `Orders we count` (Set di filtri salvati)
      * Aggiungi quanto segue:
         * `coupon_code`**NON**`[NULL]`
      * Assegna un nome alla metrica, ad esempio `Coupon discount amount`.

## Creazione del dashboard

* Una volta creata la metrica:
   * Passa a [!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**
   * Assegna al dashboard un nome come `_Coupon Analysis_`.

* In questo caso creeremo e aggiungeremo tutti i rapporti.

## Creazione di report

* **Nuovi rapporti:**

>[!NOTE]
>
>La [!UICONTROL Time Period]** per ogni rapporto è elencato come `All-time`. Sentitevi liberi di modificarlo per soddisfare le vostre esigenze di analisi. È consigliabile che tutti i rapporti di questo dashboard coprano lo stesso periodo di tempo, ad esempio `All time`, `Year-to-date`oppure `Last 365 days`.

* **Ordini con coupon**
   * 
      [!UICONTROL Metric]: `Orders`
      * Aggiungi filtro:
         * [`A`] `coupon_code` **NON** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL intervallo]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`


* **Ordini senza coupon**
   * 
      [!UICONTROL Metric]: `Orders`
      * Aggiungi filtro:
         * [`A`] `coupon_code` **IS** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL intervallo]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`


* **Entrate nette da ordini con coupon**
   * 
      [!UICONTROL Metric]: `Revenue`
      * Aggiungi filtro:
         * [`A`] `coupon_code` **NON** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL intervallo]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **Sconti dai coupon**
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL intervallo]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Ricavo medio della vita: Clienti acquistati con coupon**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Aggiungi filtro:
         * [`A`] `Customer's first order's coupon_code` **NON** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL intervallo]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **Ricavo medio della vita: Clienti non coupon acquisiti**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Aggiungi filtro:
         * [A] `Customer's first order's coupon_code` **IS**`[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL intervallo]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **Dettagli di utilizzo del coupon (primi ordini)**
   * Metrica `1`: `Orders`
      * Aggiungi filtro:
         * [`A`] `coupon_code` **NON**`[NULL]`
         * [`B`] `Customer's order number` **Uguale a** `1`
   * Metrica `2`: `Revenue`
      * Aggiungi filtro:
         * [`A`] `coupon_code` **NON**`[NULL]`
         * [`B`] `Customer's order number` **Uguale a** `1`
      * Rinomina:  `Net revenue`
   * Metrica `3`: `Coupon discount amount`
      * Aggiungi filtro:
         * [`A`] `coupon_code` **NON**`[NULL]`
         * [`B`] `Customer's order number` **Uguale a** `1`
   * Crea nuova formula: `Gross revenue`
      * [!UICONTROL Formula]: `(B – C)`
      * 
         [!UICONTROL Format]: `Currency`
   * Crea nuova formula:**% scontato**
      * Formula: `(C / (B - C))`
      * 
         [!UICONTROL Format]: `Percentage`
   * Crea nuova formula: `Average order discount`
      * [!UICONTROL Formula]: `(C / A)`
      * 
         [!UICONTROL Format]: `Percentage`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL intervallo]: `None`
   * 

      [!UICONTROL Tipo di grafico]: `Table`








* **Ricavi medi a vita per cedola al primo ordine**
   * [!UICONTROL Metric]:**Ricavi in media a vita**
      * Aggiungi filtro:
         * [`A`] `coupon_code` **IS**`[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL intervallo]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **Dettagli di utilizzo del coupon (primi ordini)**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Aggiungi filtro:
         * [`A`] `Customer's first order's coupon_code` **NON** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL intervallo]: `None`
   * [!UICONTROL Group by]: `Customer's first order's coupon_code`
   * 

      [!UICONTROL Tipo di grafico]: **Column**


* **Nuovi clienti con coupon / acquisizione senza coupon**
   * Metrica `1`: `New customers`
      * Aggiungi filtro:
         * [`A`] `Customer's first order's coupon_code` **NON** `[NULL]`
      * [!UICONTROL Rename]: `Coupon acquisition customer`
   * Metrica `2`: `New customers`
      * Aggiungi filtro:
         * [`A`] `coupon_code` **IS**`[NULL]`
      * [!UICONTROL Rename]: `Non-coupon acquisition customer`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * [!UICONTROL Chart type]: `Stacked Column`





Dopo aver creato i rapporti, fai riferimento all’immagine nella parte superiore di questo argomento per scoprire come organizzare i rapporti sul dashboard.
