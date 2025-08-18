---
title: ROI marketing
description: Scopri come impostare una dashboard che tenga traccia dell’analisi dei canali, incluso il ROI in forma aggregata e per campagna.
exl-id: 5de83998-e6cf-478d-bb6a-7a3dc77c2c0c
role: Admin,  User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# ROI marketing

>[!NOTE]
>
>Questo argomento contiene istruzioni per i client che utilizzano l&#39;architettura originale e la nuova architettura. Ti trovi nella [nuova architettura](../../administrator/account-management/new-architecture.md) se è disponibile la sezione &quot;Visualizzazioni di Data Warehouse&quot; dopo aver selezionato &quot;Gestisci dati&quot; nella barra degli strumenti principale.

Se stai spendendo soldi per la pubblicità online, vuoi tenere traccia del tuo ritorno su questa spesa e prendere decisioni basate sui dati su ulteriori investimenti. Questo argomento illustra come impostare una dashboard che tenga traccia dell’analisi dei canali, incluso il ROI in forma aggregata e per campagna.

![](../../assets/Marketing_dashboard_example.png)

Prima di iniziare, connettere gli account [[!DNL [Facebook Ads]]](../importing-data/integrations/facebook-ads.md), [[!DNL [Adwords]]](../importing-data/integrations/google-adwords.md) e [[!DNL [Google Ecommerce]]](../importing-data/integrations/google-ecommerce.md) e inserire eventuali dati aggiuntivi sulla spesa pubblicitaria online. Questa analisi contiene [colonne calcolate avanzate](../data-warehouse-mgr/adv-calc-columns.md).

## Tabelle consolidate

**Architettura originale:** Per riunire le spese da varie origini, come [!DNL Facebook Ads] o [!DNL Google Adwords], Adobe consiglia di creare una **tabella consolidata** di tutte le spese pubblicitarie. Per completare questo passaggio è necessario un analista. In caso contrario, [invia una richiesta di supporto](../../guide-overview.md#Submitting-a-Support-Ticket) con l&#39;oggetto `[MARKETING ROI ANALYSIS]` e un analista crea questa tabella.

**Nuova architettura:** Puoi seguire l&#39;esempio riportato nell&#39;argomento [questa libreria di analisi](../../data-analyst/data-warehouse-mgr/create-dw-views.md). Le tabelle consolidate sono ora note come visualizzazioni di Data Warehouse sulla nuova architettura.

## Colonne calcolate

Colonne da creare

* Tabella **`Consolidated Digital Ad Spend`**
* **`Campaign name`** è stato creato da un analista Adobe come parte del ticket di **[ANALISI ROI MARKETING]**

**Architetture originali e nuove:**

* Tabella **`sales_flat_order`**
   * **`Order's GA campaign`**
      * Selezionare una definizione: `Joined Column`
      * [!UICONTROL Create Path]:
      * &#x200B;
        [!UICONTROL Many]: `sales_flat_order.increment_id`
      * &#x200B;
        [!UICONTROL One]: `ecommerce####.transaction_id`

      * Seleziona [!UICONTROL table]: `ecommerce####`
      * Seleziona [!UICONTROL column]: `campaign`
      * [!UICONTROL Path]: `sales_flat_order.increment_id = ecommerce#####.transactionID`

   * **`Order's GA medium`**
      * Seleziona una definizione: Colonna unita
      * Seleziona [!UICONTROL table]: `ecommerce####`
      * Seleziona [!UICONTROL column]: `medium`
      * [!UICONTROL Path]: sales_flat_order.increment_id = ecommerce####.transactionId

   * **`Order's GA source`**
      * Seleziona una definizione: Colonna unita
      * Seleziona [!UICONTROL table]: `ecommerce####`
      * Seleziona [!UICONTROL column]: `source`
      * [!UICONTROL Path]: sales_flat_order.increment_id = ecommerce####.transactionId
^

* Tabella **`customer_entity`**
* **`Customer's first order GA campaign`**
   * Selezionare una definizione: `Max`
   * Seleziona [!UICONTROL table]: `sales_flat_order`
   * Seleziona [!UICONTROL column]: `Order's GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA source`**
   * Selezionare una definizione: `Max`
   * Seleziona [!UICONTROL table]: `sales_flat_order`
   * Seleziona [!UICONTROL column]: `Order's GA source`
   * [!UICONTROL Path]: sales_flat_order.customer_id = customer_entity.entity_id
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA medium`**
   * Selezionare una definizione: `Max`
   * Seleziona [!UICONTROL table]: `sales_flat_order`
   * Seleziona [!UICONTROL column]: `Order's GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* Tabella **`sales_flat_order`**
* **`Customer's first order GA campaign`**
   * Selezionare una definizione: `Joined Column`
   * Seleziona [!UICONTROL table]: `customer_entity`
   * Seleziona [!UICONTROL column]: `Customer's first order GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA source`**
   * Seleziona una definizione: Colonna unita
   * Seleziona [!UICONTROL table]: `customer_entity`
   * Seleziona [!UICONTROL column]: `Customer's first order GA source`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA medium`**
   * Selezionare una definizione: `Joined Column`
   * Seleziona [!UICONTROL table]: `customer_entity`
   * Seleziona [!UICONTROL column]: `Customer's first order GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

## Metriche

* **Spesa annuncio**
* Nella tabella **`Consolidated Digital Ad Spend`**
* Questa metrica esegue una **somma**
* Nella colonna **`adCost`**
* Ordinato per la marca temporale **`date`**

* **Impression annuncio**
* Nella tabella **`Consolidated Digital Ad Spend`**
* Questa metrica esegue una **somma**
* Nella colonna **`Impressions`**
* Ordinato per la marca temporale **`Month`**

* **Clic sull&#39;annuncio**
* Nella tabella **`Consolidated Digital Ad Spend`**
* Questa metrica esegue una **somma**
* Nella colonna **`adClicks`**
* Ordinato per la marca temporale **`Month`**

>[!NOTE]
>
>Assicurati di [aggiungere tutte le nuove colonne come dimensioni alle metriche](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.

## Rapporti

* **Annuncio (tutto il tempo)**
   * [!UICONTROL Metric]: spesa annuncio

* Metrica `A`: spesa annuncio
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`

* **Acquisizioni di clienti annuncio (in qualsiasi momento)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logica filtro: ([`A`] O [`B`] O [`C`]) E [`D`]

* Metrica `A`: `Ad customer acquisitions`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`

* **ROI annuncio**
   * [!UICONTROL Metric]: spesa annuncio

   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logica filtro: ([`A`] O [`B`] O [`C`]) E [`D`]

   * [!UICONTROL Metric]: Ricavi medi nel ciclo di vita
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logica filtro: ([`A`] O [`B`] O [`C`]) E [`D`]

   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * &#x200B;
     [!UICONTROL Format]: `Percentage`

* Metrica `A`: `Ad Spend (hide)`
* Metrica `B`: `Ad customer acquisitions (hide)`
* Metrica `C`: `Average LTV (hide)`
* [!UICONTROL Formula]: `Ads ROI`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`

* **Ordini per mezzo ga**
   * &#x200B;
     [!UICONTROL Metric]: `Orders`

* Metrica `A`: `Orders`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Order's medium`
* &#x200B;
  [!UICONTROL Chart Type]: `Area`

* **ROI annuncio per campagna**
   * [!UICONTROL Metric]: `Ad Spend`

   * [!UICONTROL Metric]:`New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logica filtro: ([`A`] O [`B`] O [`C`]) E [`D`]

   * [!UICONTROL Metric]: Ricavi medi nel ciclo di vita
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logica filtro: ([`A`] O [`B`] O [`C`]) E [`D`]

   * [!UICONTROL Metric]: numero medio di ordini nel ciclo di vita
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logica filtro: ([`A`] O [`B`] O [`C`]) E [`D`]

   * [!UICONTROL Formula]: `(A / B)`
   * &#x200B;
     [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `(C - (A / B))`
   * &#x200B;
     [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * &#x200B;
     [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Metric]: `Ad Clicks`

   * [!UICONTROL Metric]: `Ad Impressions`

   * [!UICONTROL Formula]: `(H / I)`
   * &#x200B;
     [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Formula]: `(A / H)`
   * &#x200B;
     [!UICONTROL Format]: `Currency`

* Metrica `A`: `Ad Spend` (nascondere)
* Metrica `B`: `Ad customer acquisitions`
* Metrica `C`: `Average LTV`
* Metrica `D`: `Average lifetime # of orders`
* &#x200B;
  [!UICONTROL Formula]: `CAC`
* [!UICONTROL Formula]: `Avg return`
* [!UICONTROL Formula]: `Ads ROI`
* Metrica `H`: `adClicks`
* Metrica `I`: `Impressions`
* &#x200B;
  [!UICONTROL Formula]: `CTR`
* &#x200B;
  [!UICONTROL Formula]: `CPC`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Raggruppa per]: `campaign` (Utilizza la campagna &quot;Customer&#39;s first order&#39;s&quot; per le metriche della tabella di spesa non relative agli annunci)
* &#x200B;
  [!UICONTROL Chart Type]: `Table`

Per qualsiasi domanda durante la creazione di questa analisi, o semplicemente per coinvolgere il team Professional Services, [contatta il supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=it).

### Correlato

* [Best practice per l&#39;assegnazione di tag UTM in [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
* [Come funziona l&#39;attribuzione  [!DNL Google Analytics] UTM?](../analysis/utm-attributes.md)
