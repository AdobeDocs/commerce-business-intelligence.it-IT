---
title: Analisi dei livelli di magazzino
description: Scopri come analizzare i livelli di inventario.
exl-id: 620156c5-7bea-4b36-84c7-e0cb4b5cc8be
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Analizza livelli scorte

In questo argomento viene illustrato come impostare un dashboard che fornisca informazioni approfondite sull&#39;inventario corrente e contenga istruzioni per i client sia sull&#39;architettura legacy che sulla nuova architettura. Se non disponi della funzionalità **[!UICONTROL Data Warehouse Views]** opzione sotto **[!UICONTROL Manage Data]** menu. Se ti trovi nell’architettura legacy, invia una [nuova richiesta di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) con l&#39;oggetto **[!UICONTROL INVENTORY ANALYSIS]** una volta raggiunta la sezione designata nel _Colonne calcolate_ istruzioni di seguito.

## Colonne da tracciare:

### Colonne per tenere traccia delle istruzioni

* **[!UICONTROL cataloginventory_stock_item]** tabella:
   * **`item_id`**
   * **`product_id`**
   * **`qty`**

* **[!UICONTROL catalog_product_entity]** tabella:
   * **`entity_id`**
   * **`sku`**
   * **`created_at`**

## Colonne calcolate:

+++ Nuova architettura

* **[!UICONTROL catalog_product_entity]** tabella:
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Seleziona un [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Seleziona un [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * 
        [!UICONTROL Column equation]: `AGE`
      * Seleziona [!UICONTROL DATETIME column]: `Product's most recent order date`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Seleziona un [!UICONTROL column]: `qty_ordered`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `Same Table`
      * 
        [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] input:
         * R: `Product's lifetime number of items sold`
         * B: `Product's first order date`
      * 
        [!UICONTROL Datatype]: `Decimal`
      * Definizione:
         * caso in cui A è nullo o B è nullo allora null altro round(A::decimal/(extract(epoch from (current_timestamp - B))::decimal/604800.0),2) end

* **[!UICONTROL cataloginventory_stock_item]** tabella:
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Seleziona un [!UICONTROL column]: `sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Seleziona un [!UICONTROL column]: `Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Seleziona un [!UICONTROL column]: `Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Seleziona un [!UICONTROL column]: `Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * [!UICONTROL Column type]: `Same Table`
      * 
        [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] input:
         * R: `qty`
         * B: `Avg products sold per week (all time)`
      * 
        [!UICONTROL Datatype]: `Decimal`
      * Definizione:
         * caso in cui A è null o B è null o B = 0.0, quindi null altro round(A::decimal/B,2) end

+++
+++ Architettura legacy

* **[!UICONTROL catalog_product_entity]** tabella:
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Seleziona un [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Seleziona un [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * 
        [!UICONTROL Column equation]: `AGE`
      * Selezionare la colonna DATETIME: **`Product's most recent order date`**

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: **`sales_order_item.product_id => catalog_product_entity.entity_id`**
      * Seleziona un [!UICONTROL column]: **`qty_ordered`**
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * Creato da un analista quando si invia il file **[ANALISI INVENTARIO]** richiesta di supporto

* **[!UICONTROL cataloginventory_stock_item]** tabella:
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Seleziona un [!UICONTROL column]: `sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Seleziona un [!UICONTROL column]: `Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Seleziona un [!UICONTROL column]: `Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Seleziona un [!UICONTROL column]: `Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * Creato da un analista quando si invia il file **[!UICONTROL INVENTORY ANALYSIS]** richiesta di supporto

+++

## Metriche

### Istruzioni sulle metriche

* **[!UICONTROL cataloginventory_stock_item]** tabella:
   * **`Inventory on hand`**: questa metrica esegue una
      * **Somma** il
      * **`qty`** colonna ordinata da
      * [Nessuno] colonna

## Rapporti

### Istruzioni per il rapporto

* **`Inventory on hand by sku`**
   * [!UICONTROL Metric]: `Inventory on hand`
   * [!UICONTROL Time period]: `All time`
   * Intervallo di tempo: `None`
   * [!UICONTROL Group by]:
      * `Sku`
      * `Weeks on hand`
   * 
     [!UICONTROL Chart type]: `Table`

* **`Inventory with less than 2 weeks on hand (order now)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `< 2`

   * [!UICONTROL Time period]: `All time`
   * Intervallo di tempo: `None`
   * 
     [!UICONTROL Raggruppa per]: `Sku`
   * 
     [!UICONTROL Chart type]: `Table`

* **`Inventory with more than 26 weeks on hand (put on sale)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `> 26`

   * [!UICONTROL Time period]: `All time`
   * Intervallo di tempo: `None`
   * 
     [!UICONTROL Raggruppa per]: `Sku`
   * 
     [!UICONTROL Chart type]: `Table`

In caso di domande durante la creazione di questa analisi, o se desideri semplicemente coinvolgere il team Professional Services, [contatta l’assistenza](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
