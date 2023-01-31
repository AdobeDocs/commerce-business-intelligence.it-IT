---
title: Analisi degli ordini restituiti
description: Scopri come impostare un dashboard che fornisce un’analisi dettagliata dei rendimenti del tuo negozio.
exl-id: 6a948561-45b7-4813-9661-ab42197ca5bd
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# Ordini restituiti

In questo articolo, scopri come impostare un dashboard che fornisce un’analisi dettagliata dei rendimenti del tuo negozio.

![](../../assets/detailed-returns-dboard.png)

Prima di iniziare, devi essere un [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) cliente e assicurati che la tua azienda utilizzi `enterprise\_rma` tabella dei resi.

Questa analisi contiene [colonne calcolate avanzate](../data-warehouse-mgr/adv-calc-columns.md).

## Introduzione

Colonne da tracciare

* **`enterprise_rma`** o **`rma`** tabella
* **`entity_id`**
* **`status`**
* **`order_id`**
* **`customer_id`**
* **`date_requested`**

* **`enterprise_rma_item_entity`** o **`rma_item_entity`** tabella
* **`entity_id`**
* **`rma_entity_id`**
* **`qty_returned`**
* **`status`**
* **`order_item_id`**
* **`product_name`**
* **`product_sku`**

Filtrare i set da creare

* **`enterprise_rma`** tabella
* Nome set di filtri: `Returns we count`
* Logica set filtro:
   * Segnaposto - inserisci la logica personalizzata qui

* **`enterprise_rma_item_entity`** tabella
* Nome set di filtri: `Returns items we count`
* Logica set filtro:
   * Segnaposto - inserisci la logica personalizzata qui

### Colonne calcolate

Colonne da creare

* **`enterprise_rma`** tabella
* **`Order's created at`**
* Seleziona una definizione: `Joined Column`
* [!UICONTROL Create Path]:
* 
   [!UICONTROL Many]: `enterprise_rma.order_id`
* 

   [!UICONTROL One]: `sales_flat_order.entity_id`

* Seleziona una [!UICONTROL table]: `sales_flat_order`
* Seleziona una [!UICONTROL column]: `created_at`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's order number`**
* Seleziona una definizione: `Joined Column`
* Seleziona una [!UICONTROL table]: `sales_flat_order`
* Seleziona una [!UICONTROL column]: `Customer's order number`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Time between order's created_at and date_requested`** viene creato da un analista come parte del `[RETURNS ANALYSIS]` biglietto

* **`enterprise_rma_item_entity`** tabella
* **`return_date_requested`**
* Seleziona una definizione: `Joined Column`
* [!UICONTROL Create Path]:
   * 
      [!UICONTROL Many]: `enterprise_rma_item_entity.rma_entity_id`
   * 

      [!UICONTROL One]: `enterprise_rma.entity_id`

* Seleziona una [!UICONTROL table]: `enterprise_rma`
* Seleziona una [!UICONTROL column]: `date_requested`
   * `enterprise_rma_item_entity.rma_entity_id = enterprise_rma.entity_id`

* **`Return item total value (qty_returned * price)`** viene creato da un analista come parte del `[RETURNS ANALYSIS]` biglietto

* **`sales_flat_order`** tabella
* **`Order contains a return? (1=yes/0=No)`**
* Seleziona una definizione: `Exists`
* Seleziona una [!UICONTROL table]: `enterprise_rma`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's previous order number`** viene creato da un analista come parte del `[RETURNS ANALYSIS]` biglietto
* **`Customer's previous order contains return? (1=yes/0=no)`** viene creato da un analista come parte del `[RETURNS ANALYSIS]` biglietto

>[!NOTE]
>
>Se sei interessato ad analizzare solo le ore lavorative per secondi alla risoluzione o secondi alla prima risposta, informa l&#39;analista al momento della richiesta del ticket.

### Metriche

* **Restituisce**
* In **`enterprise_rma`** tabella
* Questa metrica esegue un **Conteggio**
* Sulla **`entity_id`** column
* Ordinato dal **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Articoli restituiti**
* In **`enterprise_rma_item_entity`** tabella
* Questa metrica esegue un **Somma**
* Sulla **`qty_approved`** column
* Ordinato dal **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Valore totale articolo restituito**
* In **`enterprise_rma_item_entity`** tabella
* Questa metrica esegue un **Somma**
* Sulla **`Returned item total value (qty_returned * price)`** column
* Ordinato dal **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Tempo medio tra ordine e reso**
* In **`enterprise_rma`** tabella
* Questa metrica esegue un **Media**
* Sulla **`Time between order's created_at and date_requested`** column
* Ordinato dal **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

>[!NOTE]
>
>Assicurati di [aggiungi tutte le nuove colonne come dimensioni alle metriche](../data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.

### Rapporti

* **Ripeti la probabilità dell&#39;ordine dopo un ritorno**
* Metrica `A`: `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is in current month? = No`

* Metrica `B`: `Non-last orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Is customer's last order? (1=yes/0=no) = 0`
   * `Order contains a return? (1=yes/0=No) = 1`

* Formula: Probabilità ordine di ripetizione
* [!UICONTROL Formula]: `B / A`
* 

   [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL intervallo]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* 
   [!UICONTROL Tipo di grafico]: `Bar`

* **Tempo medio di ritorno (tutto l&#39;ora)**
* Metrica `A`: `Avg time between order and return`
* [!UICONTROL Metric]: `Avg time between order and return`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL intervallo]: `None`
* 

   [!UICONTROL Tipo di grafico]: `Number`

* **Percentuale di ordini con un rendimento**
* Metrica `A`: `Number of orders`
* [!UICONTROL Metric]: `Number of orders`

* Metrica `B`: `Orders w/ return`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`

* Formula: % degli ordini con restituzione
* [!UICONTROL Formula]: `B / A`
* 

   [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL intervallo]: `None`
* [!UICONTROL Chart Type]: `Number - % of orders with return`

* **Ricavi restituiti dal mese**
* Metrica `A`: `Returned item total value`
* [!UICONTROL Metric]: `Returned item total value`

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By month`
* 

   [!UICONTROL Tipo di grafico]: `Line`

* **Clienti che hanno effettuato un ritorno e non hanno acquistato di nuovo**
* Metrica `A`: `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is customer's last order? (1=yes/0=no) = 1`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL intervallo]: `None`
* 
   [!UICONTROL Group by]: `Customer_email`
* 

   [!UICONTROL Tipo di grafico]: `Table`

* **Tasso di restituzione per articolo**
* Metrica `A`: `Returned items` (Nascondi)
* [!UICONTROL Metric]: Articoli restituiti

* Metrica `B`: `Items sold` (Nascondi)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:

* [!UICONTROL Formula]: `Return %`
* [!UICONTROL Formula]: `B / A`
* 

   [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL intervallo]: `None`
* [!UICONTROL Group by]: `product_sku AND/OR product_name`
* 
   [!UICONTROL Tipo di grafico]: `Table`

Dopo aver compilato tutti i rapporti, puoi organizzarli nel dashboard come desideri. Il risultato potrebbe assomigliare al dashboard di esempio riportato sopra.

In caso di domande durante la creazione di questa analisi o se desideri semplicemente coinvolgere il team Professional Services, [contattare il supporto](../../guide-overview.md).
