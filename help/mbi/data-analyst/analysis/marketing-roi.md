---
title: ROI del marketing
description: Scopri come impostare un dashboard per monitorare l’analisi dei canali, compreso il ROI in aggregato e per campagna.
exl-id: 5de83998-e6cf-478d-bb6a-7a3dc77c2c0c
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# ROI del marketing

>[!NOTE]
>
>Questo articolo contiene istruzioni per i clienti che utilizzano l’architettura originale e la nuova architettura. Sei sul [nuova architettura](../../administrator/account-management/new-architecture.md) se hai la sezione &quot;Data Warehouse visualizzazioni&quot; disponibile dopo aver selezionato &quot;Gestisci dati&quot; dalla barra degli strumenti principale.

Se si spendono soldi per la pubblicità online, sarà inevitabile voler monitorare il proprio ritorno su questa spesa e prendere decisioni basate sui dati su ulteriori investimenti. In questo articolo, mostriamo come impostare un dashboard per monitorare l’analisi dei canali, compreso il ROI in aggregato e per campagna.

![](../../assets/Marketing_dashboard_example.png)

Prima di iniziare, è necessario collegare il [!DNL [Facebook Ads]](../importing-data/integrations/facebook-ads.md), [!DNL [Adwords]](../importing-data/integrations/google-adwords.md)e [!DNL [Google Ecommerce]](../importing-data/integrations/google-ecommerce.md) , nonché inserire eventuali dati aggiuntivi di spesa degli annunci online. Questa analisi contiene [colonne calcolate avanzate](../data-warehouse-mgr/adv-calc-columns.md).

## Tabelle consolidate

**Architettura originale:** Per riunire la spesa da varie fonti (come [!DNL Facebook Ads] o [!DNL Google Adwords]), è consigliabile creare una **tabella consolidata** di tutte le tue spese pubblicitarie. Sarà necessario un analista per completare questo passaggio. Se non lo hai già fatto, [presentare una richiesta di supporto](../../guide-overview.md) con l&#39;oggetto `[MARKETING ROI ANALYSIS]`e viene creata una tabella da un analista.

**Nuova architettura:** Puoi seguire l’esempio illustrato in [questa libreria di analisi](../../data-analyst/data-warehouse-mgr/create-dw-views.md) argomento. Le tabelle consolidate sono ora note come visualizzazioni Data Warehouse sulla nuova architettura.

## Colonne calcolate

Colonne da creare

* **`Consolidated Digital Ad Spend`** tabella
* **`Campaign name`** verrà creato da un analista come parte del **[ANALISI DEL ROI DI MARKETING]** biglietto

>[!NOTE]
>
>Vedi sopra per le nuove differenze di architettura.

**Architetture nuove e originali:**

* **`sales_flat_order`** tabella
   * **`Order's GA campaign`**
      * Seleziona una definizione: `Joined Column`
      * [!UICONTROL Create Path]:
      * 
         [!UICONTROL Many]: `sales_flat_order.increment_id`
      * 

         [!UICONTROL One]: `ecommerce####.transaction_id`

      * Seleziona una [!UICONTROL table]: `ecommerce####`
      * Seleziona una [!UICONTROL column]: `campaign`
      * [!UICONTROL Path]: `sales_flat_order.increment_id = ecommerce#####.transactionID`
   * **`Order's GA medium`**
      * Seleziona una definizione: Colonna unita
      * Seleziona una [!UICONTROL table]: `ecommerce####`
      * Seleziona una [!UICONTROL column]: `medium`
      * [!UICONTROL Path]: sales_flat_order.increment_id = ecommerce#####.transactionId
   * **`Order's GA source`**
      * Seleziona una definizione: Colonna unita
      * Seleziona una [!UICONTROL table]: `ecommerce####`
      * Seleziona una [!UICONTROL column]: `source`
      * [!UICONTROL Path]: sales_flat_order.increment_id = ecommerce#####.transactionId ^




* **`customer_entity`** tabella
* **`Customer's first order GA campaign`**
   * Seleziona una definizione: `Max`
   * Seleziona una [!UICONTROL table]: `sales_flat_order`
   * Seleziona una [!UICONTROL column]: `Order's GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA source`**
   * Seleziona una definizione: `Max`
   * Seleziona una [!UICONTROL table]: `sales_flat_order`
   * Seleziona una [!UICONTROL column]: `Order's GA source`
   * [!UICONTROL Path]: sales_flat_order.customer_id = customer_entity.entity_id
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA medium`**
   * Seleziona una definizione: `Max`
   * Seleziona una [!UICONTROL table]: `sales_flat_order`
   * Seleziona una [!UICONTROL column]: `Order's GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`sales_flat_order`** tabella
* **`Customer's first order GA campaign`**
   * Seleziona una definizione: `Joined Column`
   * Seleziona una [!UICONTROL table]: `customer_entity`
   * Seleziona una [!UICONTROL column]: `Customer's first order GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA source`**
   * Seleziona una definizione: Colonna unita
   * Seleziona una [!UICONTROL table]: `customer_entity`
   * Seleziona una [!UICONTROL column]: `Customer's first order GA source`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA medium`**
   * Seleziona una definizione: `Joined Column`
   * Seleziona una [!UICONTROL table]: `customer_entity`
   * Seleziona una [!UICONTROL column]: `Customer's first order GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

## Metriche

* **Spesa pubblicitaria**
* In **`Consolidated Digital Ad Spend`** tabella
* Questa metrica esegue un **Somma**
* Sulla **`adCost`** column
* Ordinato dal **`date`** timestamp

* **Impressioni dell&#39;annuncio**
* In **`Consolidated Digital Ad Spend`** tabella
* Questa metrica esegue un **Somma**
* Sulla **`Impressions`** column
* Ordinato dal **`Month`** timestamp

* **Clic sugli annunci**
* In **`Consolidated Digital Ad Spend`** tabella
* Questa metrica esegue un **Somma**
* Sulla **`adClicks`** column
* Ordinato dal **`Month`** timestamp

>[!NOTE]
>
>Assicurati di [aggiungi tutte le nuove colonne come dimensioni alle metriche](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.

## Rapporti

* **Spesa dell&#39;annuncio (tutto il tempo)**
   * [!UICONTROL Metric]: Spesa annuncio

* Metrica `A`: Spesa annuncio
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL intervallo]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **Acquisizioni di clienti annunci (sempre)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logica del filtro: ([`A`] O [`B`] O [`C`]) E [`D`]

* Metrica `A`: `Ad customer acquisitions`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL intervallo]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **Ad ROI**
   * [!UICONTROL Metric]: Spesa annuncio

   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logica del filtro: ([`A`] O [`B`] O [`C`]) E [`D`]
   * [!UICONTROL Metric]: Ricavi a vita media
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logica del filtro: ([`A`] O [`B`] O [`C`]) E [`D`]
   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * 

      [!UICONTROL Format]: `Percentage`



* Metrica `A`: `Ad Spend (hide)`
* Metrica `B`: `Ad customer acquisitions (hide)`
* Metrica `C`: `Average LTV (hide)`
* [!UICONTROL Formula]: `Ads ROI`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL intervallo]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **Ordini per mezzo di ga**
   * 

      [!UICONTROL Metric]: `Orders`

* Metrica `A`: `Orders`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Order's medium`
* 

   [!UICONTROL Chart Type]: `Area`

* **ROI dell’annuncio per campagna**
   * [!UICONTROL Metric]: `Ad Spend`

   * [!UICONTROL Metric]:`New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logica del filtro: ([`A`] O [`B`] O [`C`]) E [`D`]
   * [!UICONTROL Metric]: Ricavi a vita media
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logica del filtro: ([`A`] O [`B`] O [`C`]) E [`D`]
   * [!UICONTROL Metric]: Numero medio di ordini nel ciclo di vita
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Logica del filtro: ([`A`] O [`B`] O [`C`]) E [`D`]
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




* Metrica `A`: `Ad Spend` (nascondere)
* Metrica `B`: `Ad customer acquisitions`
* Metrica `C`: `Average LTV`
* Metrica `D`: `Average lifetime # of orders`
* 
   [!Formula UICONTROL]: `CAC`
* [!UICONTROL Formula]: `Avg return`
* [!UICONTROL Formula]: `Ads ROI`
* Metrica `H`: `adClicks`
* Metrica `I`: `Impressions`
* 
   [!Formula UICONTROL]: `CTR`
* 
   [!Formula UICONTROL]: `CPC`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL intervallo]: `None`
* 
   [!UICONTROL Group by]: `campaign` (Utilizza la campagna &quot;del primo ordine del cliente&quot; per le metriche delle tabelle di spesa non pubblicitarie)
* 

   [!UICONTROL Chart Type]: `Table`

In caso di domande durante la creazione di questa analisi, o se desideri semplicemente coinvolgere il nostro team di servizi professionali, [contattare il supporto](../../guide-overview.md).

### Correlati

* [Tecniche consigliate per l’assegnazione di tag UTM in [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
* [Come funziona [!DNL Google Analytics] L’attribuzione UTM funziona?](../analysis/utm-attributes.md)
