---
title: Analisi degli ordini restituiti
description: Scopri come impostare una dashboard che fornisca un’analisi dettagliata dei resi del tuo negozio.
exl-id: 6a948561-45b7-4813-9661-ab42197ca5bd
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# Ordini restituiti

In questo argomento viene illustrato come impostare una dashboard che fornisca un&#39;analisi dettagliata dei resi del negozio.

![](../../assets/detailed-returns-dboard.png)

Prima di iniziare, devi essere un [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) e devono assicurarsi che la tua azienda utilizzi il `enterprise\_rma` tabella per i resi.

Questa analisi contiene [colonne calcolate avanzate](../data-warehouse-mgr/adv-calc-columns.md).

## Guida introduttiva

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

Set di filtri da creare

* **`enterprise_rma`** tabella
* Nome set di filtri: `Returns we count`
* Logica set di filtri:
   * Segnaposto: immetti qui la logica personalizzata

* **`enterprise_rma_item_entity`** tabella
* Nome set di filtri: `Returns items we count`
* Logica set di filtri:
   * Segnaposto: immetti qui la logica personalizzata

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

* Seleziona un [!UICONTROL table]: `sales_flat_order`
* Seleziona un [!UICONTROL column]: `created_at`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's order number`**
* Seleziona una definizione: `Joined Column`
* Seleziona un [!UICONTROL table]: `sales_flat_order`
* Seleziona un [!UICONTROL column]: `Customer's order number`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Time between order's created_at and date_requested`** viene creato da un analista come parte del `[RETURNS ANALYSIS]` ticket

* **`enterprise_rma_item_entity`** tabella
* **`return_date_requested`**
* Seleziona una definizione: `Joined Column`
* [!UICONTROL Create Path]:
   * 
     [!UICONTROL Many]: `enterprise_rma_item_entity.rma_entity_id`
   * 
     [!UICONTROL One]: `enterprise_rma.entity_id`

* Seleziona un [!UICONTROL table]: `enterprise_rma`
* Seleziona un [!UICONTROL column]: `date_requested`
   * `enterprise_rma_item_entity.rma_entity_id = enterprise_rma.entity_id`

* **`Return item total value (qty_returned * price)`** viene creato da un analista come parte del `[RETURNS ANALYSIS]` ticket

* **`sales_flat_order`** tabella
* **`Order contains a return? (1=yes/0=No)`**
* Seleziona una definizione: `Exists`
* Seleziona un [!UICONTROL table]: `enterprise_rma`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's previous order number`** viene creato da un analista come parte del `[RETURNS ANALYSIS]` ticket
* **`Customer's previous order contains return? (1=yes/0=no)`** viene creato da un analista come parte del `[RETURNS ANALYSIS]` ticket

>[!NOTE]
>
>Se ti interessa analizzare solo l’orario di lavoro per i secondi di risoluzione o i secondi di prima risposta, informa l’analista quando richiedi il ticket.

### Metriche

* **Restituisce**
* In **`enterprise_rma`** tabella
* Questa metrica esegue una **Conteggio**
* Il giorno **`entity_id`** colonna
* Ordinato da **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Elementi restituiti**
* In **`enterprise_rma_item_entity`** tabella
* Questa metrica esegue una **Somma**
* Il giorno **`qty_approved`** colonna
* Ordinato da **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Valore totale dell&#39;articolo restituito**
* In **`enterprise_rma_item_entity`** tabella
* Questa metrica esegue una **Somma**
* Il giorno **`Returned item total value (qty_returned * price)`** colonna
* Ordinato da **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Tempo medio tra ordine e restituzione**
* In **`enterprise_rma`** tabella
* Questa metrica esegue un **Media**
* Il giorno **`Time between order's created_at and date_requested`** colonna
* Ordinato da **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

>[!NOTE]
>
>Assicurati di [aggiungere tutte le nuove colonne come dimensioni alle metriche](../data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.

### Rapporti

* **Probabilità di ripetizione ordine dopo aver effettuato un reso**
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

* Formula: probabilità ordine ripetuto
* [!UICONTROL Formula]: `B / A`
* 
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* 
  [!UICONTROL Chart Type]: `Bar`

* **Tempo medio di ritorno (tutto il tempo)**
* Metrica `A`: `Avg time between order and return`
* [!UICONTROL Metric]: `Avg time between order and return`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart Type]: `Number`

* **Percentuale di ordini con una restituzione**
* Metrica `A`: `Number of orders`
* [!UICONTROL Metric]: `Number of orders`

* Metrica `B`: `Orders w/ return`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`

* Formula: % di ordini con restituzione
* [!UICONTROL Formula]: `B / A`
* 
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Chart Type]: `Number - % of orders with return`

* **Ricavi restituiti per mese**
* Metrica `A`: `Returned item total value`
* [!UICONTROL Metric]: `Returned item total value`

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By month`
* 
  [!UICONTROL Chart Type]: `Line`

* **Clienti che hanno effettuato una restituzione e non hanno acquistato nuovamente**
* Metrica `A`: `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is customer's last order? (1=yes/0=no) = 1`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Raggruppa per]: `Customer_email`
* 
  [!UICONTROL Chart Type]: `Table`

* **Tasso di rendimento per articolo**
* Metrica `A`: `Returned items` (Nascondi)
* [!UICONTROL Metric]: elementi restituiti

* Metrica `B`: `Items sold` (Nascondi)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:

* [!UICONTROL Formula]: `Return %`
* [!UICONTROL Formula]: `B / A`
* 
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `product_sku AND/OR product_name`
* 
  [!UICONTROL Chart Type]: `Table`

Dopo aver compilato tutti i rapporti, puoi organizzarli nel dashboard come desideri. Il risultato potrebbe essere simile al dashboard di esempio riportato sopra.

In caso di domande durante la creazione di questa analisi o se desideri coinvolgere il team Professional Services, [contatta l’assistenza](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
