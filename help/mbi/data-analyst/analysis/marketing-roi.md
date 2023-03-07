---
title: ROI marketing
description: Scopri come impostare una dashboard che tenga traccia dell’analisi dei canali, incluso il ROI in forma aggregata e per campagna.
exl-id: 5de83998-e6cf-478d-bb6a-7a3dc77c2c0c
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---

# ROI marketing

>[!NOTE]
>
>Questo articolo contiene istruzioni per i client che utilizzano l’architettura originale e la nuova architettura. Sei sul [nuova architettura](../../administrator/account-management/new-architecture.md) se è disponibile la sezione &quot;Data Warehouse visualizzazioni&quot; dopo aver selezionato &quot;Gestisci dati&quot; nella barra degli strumenti principale.

Se stai spendendo soldi per la pubblicità online, vuoi tenere traccia del tuo ritorno su questa spesa e prendere decisioni basate sui dati su ulteriori investimenti. Questo articolo illustra come impostare una dashboard che tenga traccia dell’analisi dei canali, incluso il ROI in forma aggregata e per campagna.

![](../../assets/Marketing_dashboard_example.png)

Prima di iniziare, è necessario connettere il [!DNL [Facebook Ads]](../importing-data/integrations/facebook-ads.md), [!DNL [Adwords]](../importing-data/integrations/google-adwords.md), e [!DNL [Google Ecommerce]](../importing-data/integrations/google-ecommerce.md) e inserire eventuali dati aggiuntivi sulla spesa pubblicitaria online. Questa analisi contiene [colonne calcolate avanzate](../data-warehouse-mgr/adv-calc-columns.md).

## Tabelle consolidate

**Architettura originale:** Per riunire le spese da varie fonti (come [!DNL Facebook Ads] o [!DNL Google Adwords]), l’Adobe consiglia di creare un **tabella consolidata** di tutte le spese pubblicitarie. Per completare questo passaggio è necessario un analista. In caso contrario, [invia una richiesta di supporto](../../guide-overview.md) con l&#39;oggetto `[MARKETING ROI ANALYSIS]`e un analista crea questa tabella.

**Nuova architettura:** Puoi seguire l’esempio in [questa libreria di analisi](../../data-analyst/data-warehouse-mgr/create-dw-views.md) argomento. Le tabelle consolidate sono ora note come visualizzazioni Date Warehouse sulla nuova architettura.

## Colonne calcolate

Colonne da creare

* **`Consolidated Digital Ad Spend`** tabella
* **`Campaign name`** viene creato da un analista come parte del **[ANALISI DEL ROI DI MARKETING]** ticket

>[!NOTE]
>
>Per le nuove differenze a livello di architettura, vedi sopra.

**Architetture nuove e originali:**

* **`sales_flat_order`** tabella
   * **`Order's GA campaign`**
      * Seleziona una definizione: `Joined Column`
      * [!UICONTROL Create Path]:
      * 
         [!UICONTROL Many]: `sales_flat_order.increment_id`
      * 

         [!UICONTROL One]: `ecommerce####.transaction_id`

      * Seleziona un [!UICONTROL table]: `ecommerce####`
      * Seleziona un [!UICONTROL column]: `campaign`
      * [!UICONTROL Path]: `sales_flat_order.increment_id = ecommerce#####.transactionID`
   * **`Order's GA medium`**
      * Seleziona una definizione: Colonna unita
      * Seleziona un [!UICONTROL table]: `ecommerce####`
      * Seleziona un [!UICONTROL column]: `medium`
      * [!UICONTROL Path]: sales_flat_order.increment_id = ecommerce####.transactionId
   * **`Order's GA source`**
      * Seleziona una definizione: Colonna unita
      * Seleziona un [!UICONTROL table]: `ecommerce####`
      * Seleziona un [!UICONTROL column]: `source`
      * [!UICONTROL Path]: sales_flat_order.increment_id = ecommerce#####.transactionId ^




* **`customer_entity`** tabella
* **`Customer's first order GA campaign`**
   * Seleziona una definizione: `Max`
   * Seleziona un [!UICONTROL table]: `sales_flat_order`
   * Seleziona un [!UICONTROL column]: `Order's GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA source`**
   * Seleziona una definizione: `Max`
   * Seleziona un [!UICONTROL table]: `sales_flat_order`
   * Seleziona un [!UICONTROL column]: `Order's GA source`
   * [!UICONTROL Path]: sales_flat_order.customer_id = customer_entity.entity_id
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA medium`**
   * Seleziona una definizione: `Max`
   * Seleziona un [!UICONTROL table]: `sales_flat_order`
   * Seleziona un [!UICONTROL column]: `Order's GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`sales_flat_order`** tabella
* **`Customer's first order GA campaign`**
   * Seleziona una definizione: `Joined Column`
   * Seleziona un [!UICONTROL table]: `customer_entity`
   * Seleziona un [!UICONTROL column]: `Customer's first order GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA source`**
   * Seleziona una definizione: Colonna unita
   * Seleziona un [!UICONTROL table]: `customer_entity`
   * Seleziona un [!UICONTROL column]: `Customer's first order GA source`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA medium`**
   * Seleziona una definizione: `Joined Column`
   * Seleziona un [!UICONTROL table]: `customer_entity`
   * Seleziona un [!UICONTROL column]: `Customer's first order GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

## Metriche

* **Spesa annuncio**
* In **`Consolidated Digital Ad Spend`** tabella
* Questa metrica esegue una **Somma**
* Il giorno **`adCost`** colonna
* Ordinato da **`date`** timestamp

* **Impression degli annunci**
* In **`Consolidated Digital Ad Spend`** tabella
* Questa metrica esegue una **Somma**
* Il giorno **`Impressions`** colonna
* Ordinato da **`Month`** timestamp

* **Clic sull’annuncio**
* In **`Consolidated Digital Ad Spend`** tabella
* Questa metrica esegue una **Somma**
* Il giorno **`adClicks`** colonna
* Ordinato da **`Month`** timestamp

>[!NOTE]
>
>Assicurati di [aggiungere tutte le nuove colonne come dimensioni alle metriche](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.

## Rapporti

* **Spesa annuncio (tutto il tempo)**
   * [!UICONTROL Metric]: Spesa annuncio

* Metrica `A`: Spesa annuncio
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **Acquisizioni di clienti di annunci (in qualsiasi momento)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logica di filtro: ([`A`] OPPURE [`B`] OPPURE [`C`]) E [`D`]

* Metrica `A`: `Ad customer acquisitions`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **ROI annuncio**
   * [!UICONTROL Metric]: Spesa annuncio

   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logica di filtro: ([`A`] OPPURE [`B`] OPPURE [`C`]) E [`D`]
   * [!UICONTROL Metric]: Ricavi medi nel ciclo di vita
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logica di filtro: ([`A`] OPPURE [`B`] OPPURE [`C`]) E [`D`]
   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * 

      [!UICONTROL Format]: `Percentage`



* Metrica `A`: `Ad Spend (hide)`
* Metrica `B`: `Ad customer acquisitions (hide)`
* Metrica `C`: `Average LTV (hide)`
* [!UICONTROL Formula]: `Ads ROI`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **Ordini per mezzo ga**
   * 

      [!UICONTROL Metric]: `Orders`

* Metrica `A`: `Orders`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Order's medium`
* 

   [!UICONTROL Chart Type]: `Area`

* **ROI annuncio per campagna**
   * [!UICONTROL Metric]: `Ad Spend`

   * [!UICONTROL Metric]:`New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logica di filtro: ([`A`] OPPURE [`B`] OPPURE [`C`]) E [`D`]
   * [!UICONTROL Metric]: Ricavi medi nel ciclo di vita
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logica di filtro: ([`A`] OPPURE [`B`] OPPURE [`C`]) E [`D`]
   * [!UICONTROL Metric]: numero medio di ordini nel ciclo di vita
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logica di filtro: ([`A`] OPPURE [`B`] OPPURE [`C`]) E [`D`]
   * [!UICONTROL Formula]: `(A / B)`
   * 

      [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `(C - (A / B))`
   * 

      [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * 

      [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Metric]: `Ad Clicks`

   * [!UICONTROL Metric]: `Ad Impressions`

   * [!UICONTROL Formula]: `(H / I)`
   * 

      [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Formula]: `(A / H)`
   * 

      [!UICONTROL Format]: `Currency`




* Metrica `A`: `Ad Spend` (nascondi)
* Metrica `B`: `Ad customer acquisitions`
* Metrica `C`: `Average LTV`
* Metrica `D`: `Average lifetime # of orders`
* 
   [!UICONTROL Formula]: `CAC`
* [!UICONTROL Formula]: `Avg return`
* [!UICONTROL Formula]: `Ads ROI`
* Metrica `H`: `adClicks`
* Metrica `I`: `Impressions`
* 
   [!UICONTROL Formula]: `CTR`
* 
   [!UICONTROL Formula]: `CPC`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 
   [!UICONTROL Raggruppa per]: `campaign` (Utilizza la campagna &quot;Customer&#39;s first order&#39;s&quot; per le metriche della tabella di spesa non relative agli annunci)
* 

   [!UICONTROL Chart Type]: `Table`

In caso di domande durante la creazione di questa analisi, o se desideri semplicemente coinvolgere il team Professional Services, [contatta l’assistenza](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

### Correlato

* [Tecniche consigliate per l’assegnazione tag UTM in [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
* [In che modo [!DNL Google Analytics] Lavoro di attribuzione UTM?](../analysis/utm-attributes.md)
