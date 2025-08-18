---
title: Analisi degli ordini restituiti
description: Scopri come impostare una dashboard che fornisca un’analisi dettagliata dei resi del tuo negozio.
exl-id: 6a948561-45b7-4813-9661-ab42197ca5bd
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Ordini restituiti

In questo argomento viene illustrato come impostare una dashboard che fornisca un&#39;analisi dettagliata dei resi del negozio.

![](../../assets/detailed-returns-dboard.png)

Prima di iniziare, devi essere un cliente di [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) e assicurarti che la tua azienda utilizzi la tabella `enterprise\_rma` per le restituzioni.

Questa analisi contiene [colonne calcolate avanzate](../data-warehouse-mgr/adv-calc-columns.md).

## Guida introduttiva

Colonne da tracciare

* Tabella **`enterprise_rma`** o **`rma`**
* **`entity_id`**
* **`status`**
* **`order_id`**
* **`customer_id`**
* **`date_requested`**

* Tabella **`enterprise_rma_item_entity`** o **`rma_item_entity`**
* **`entity_id`**
* **`rma_entity_id`**
* **`qty_returned`**
* **`status`**
* **`order_item_id`**
* **`product_name`**
* **`product_sku`**

Set di filtri da creare

* Tabella **`enterprise_rma`**
* Nome set di filtri: `Returns we count`
* Logica set di filtri:
   * Segnaposto: immetti qui la logica personalizzata

* Tabella **`enterprise_rma_item_entity`**
* Nome set di filtri: `Returns items we count`
* Logica set di filtri:
   * Segnaposto: immetti qui la logica personalizzata

### Colonne calcolate

Colonne da creare

* Tabella **`enterprise_rma`**
* **`Order's created at`**
* Selezionare una definizione: `Joined Column`
* [!UICONTROL Create Path]:
* &#x200B;
  [!UICONTROL Many]: `enterprise_rma.order_id`
* &#x200B;
  [!UICONTROL One]: `sales_flat_order.entity_id`

* Seleziona [!UICONTROL table]: `sales_flat_order`
* Seleziona [!UICONTROL column]: `created_at`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's order number`**
* Selezionare una definizione: `Joined Column`
* Seleziona [!UICONTROL table]: `sales_flat_order`
* Seleziona [!UICONTROL column]: `Customer's order number`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Time between order's created_at and date_requested`** è stato creato da un analista come parte del tuo ticket `[RETURNS ANALYSIS]`

* Tabella **`enterprise_rma_item_entity`**
* **`return_date_requested`**
* Selezionare una definizione: `Joined Column`
* [!UICONTROL Create Path]:
   * &#x200B;
     [!UICONTROL Many]: `enterprise_rma_item_entity.rma_entity_id`
   * &#x200B;
     [!UICONTROL One]: `enterprise_rma.entity_id`

* Seleziona [!UICONTROL table]: `enterprise_rma`
* Seleziona [!UICONTROL column]: `date_requested`
   * `enterprise_rma_item_entity.rma_entity_id = enterprise_rma.entity_id`

* **`Return item total value (qty_returned * price)`** è stato creato da un analista come parte del tuo ticket `[RETURNS ANALYSIS]`

* Tabella **`sales_flat_order`**
* **`Order contains a return? (1=yes/0=No)`**
* Selezionare una definizione: `Exists`
* Seleziona [!UICONTROL table]: `enterprise_rma`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's previous order number`** è stato creato da un analista come parte del tuo ticket `[RETURNS ANALYSIS]`
* **`Customer's previous order contains return? (1=yes/0=no)`** è stato creato da un analista come parte del tuo ticket `[RETURNS ANALYSIS]`

>[!NOTE]
>
>Se ti interessa analizzare solo l’orario di lavoro per i secondi di risoluzione o i secondi di prima risposta, informa l’analista quando richiedi il ticket.

### Metriche

* **Restituisce**
* Nella tabella **`enterprise_rma`**
* Questa metrica esegue **Count**
* Nella colonna **`entity_id`**
* Ordinato da **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Elementi restituiti**
* Nella tabella **`enterprise_rma_item_entity`**
* Questa metrica esegue una **somma**
* Nella colonna **`qty_approved`**
* Ordinato da **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Valore totale restituito**
* Nella tabella **`enterprise_rma_item_entity`**
* Questa metrica esegue una **somma**
* Nella colonna **`Returned item total value (qty_returned * price)`**
* Ordinato da **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Tempo medio tra l&#39;ordine e la restituzione**
* Nella tabella **`enterprise_rma`**
* Questa metrica esegue una **media**
* Nella colonna **`Time between order's created_at and date_requested`**
* Ordinato da **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

>[!NOTE]
>
>Assicurati di [aggiungere tutte le nuove colonne come dimensioni alle metriche](../data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.

### Rapporti

* **Probabilità di ripetere l&#39;ordine dopo aver effettuato una restituzione**
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
* &#x200B;
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* &#x200B;
  [!UICONTROL Chart Type]: `Bar`

* **Tempo medio per il ritorno (tutti i tempi)**
* Metrica `A`: `Avg time between order and return`
* [!UICONTROL Metric]: `Avg time between order and return`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Number`

* **Percentuale di ordini con restituzione**
* Metrica `A`: `Number of orders`
* [!UICONTROL Metric]: `Number of orders`

* Metrica `B`: `Orders w/ return`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`

* Formula: % di ordini con restituzione
* [!UICONTROL Formula]: `B / A`
* &#x200B;
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Chart Type]: `Number - % of orders with return`

* **Entrate restituite entro il mese**
* Metrica `A`: `Returned item total value`
* [!UICONTROL Metric]: `Returned item total value`

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By month`
* &#x200B;
  [!UICONTROL Chart Type]: `Line`

* **Clienti che hanno effettuato una restituzione e non hanno acquistato nuovamente**
* Metrica `A`: `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is customer's last order? (1=yes/0=no) = 1`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Raggruppa per]: `Customer_email`
* &#x200B;
  [!UICONTROL Chart Type]: `Table`

* **Percentuale di reso per elemento**
* Metrica `A`: `Returned items` (Nascondi)
* [!UICONTROL Metric]: elementi restituiti

* Metrica `B`: `Items sold` (Nascondi)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:

* [!UICONTROL Formula]: `Return %`
* [!UICONTROL Formula]: `B / A`
* &#x200B;
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `product_sku AND/OR product_name`
* &#x200B;
  [!UICONTROL Chart Type]: `Table`

Dopo aver compilato tutti i rapporti, puoi organizzarli nel dashboard come desideri. Il risultato potrebbe essere simile al dashboard di esempio riportato sopra.

In caso di domande durante la creazione di questa analisi o se desideri coinvolgere il team Professional Services, [contatta il supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
