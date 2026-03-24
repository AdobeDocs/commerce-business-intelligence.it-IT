---
title: Diagrammi di relazione entità
description: Scopri alcuni diagrammi ER per visualizzare la relazione tra alcune tabelle di database comuni di Commerce.
exl-id: de7d419f-efbe-4d0c-95a8-155a12aa93f3
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/pWd5aVoaq2TPkGr37cNeF8CEZ63fItwCEez61eEgGBo
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 346
ht-degree: 0%

---

# Diagramma relazione entità

Cos&#39;è un **[!UICONTROL entity relationship (ER) diagram]**? Un diagramma [!UICONTROL ER] è una visualizzazione delle tabelle all&#39;interno di un database e del modo in cui si relazionano tra loro. Questo argomento contiene alcuni diagrammi di [!UICONTROL ER] che consentono di visualizzare la relazione tra alcune tabelle di database Adobe Commerce comuni.

>[!NOTE]
>
>In questo argomento vengono visualizzate le parole **join**, **relationship** e **path**. Queste parole vengono utilizzate per descrivere la connessione tra due tabelle.

## Diagramma core [!UICONTROL ER] di Commerce

![4_DB_Chart](../../assets/4_DB_Chart.png)

Questo diagramma `ER` rappresenta le relazioni tra le tabelle principali di un database Commerce. Visualizzando più relazioni contemporaneamente, è possibile vedere in che modo i dati si relazionano tra più tabelle.

Le sezioni seguenti contengono `ER` diagrammi specifici per due tabelle alla volta. Per visualizzare un diagramma e la relativa descrizione, fare clic sull&#39;intestazione di tale sezione.

## `customer\_entity & sales\_flat\_order`

![Un Cliente Molti Ordini](../../assets/2_OneCustomerManyOrders.png)

Un cliente può effettuare molti ordini. La relazione tra queste due tabelle è `customer\_entity.entity\_id = sales\_flat\_order.customer\_id`

>[!IMPORTANT]
>
>`customer\_entity.entity\_id` non è uguale a `sales\_flat\_order.entity\_id`. Il primo può essere considerato come `customer\_id` e il secondo come `order\_id.`

All&#39;interno di [!DNL Commerce Intelligence], se il percorso tra queste due tabelle non esiste, è possibile [creare il percorso](../data-warehouse-mgr/create-paths-calc-columns.md) nella scheda Data Warehouse. Quando siete pronti a creare il percorso, questo viene definito come segue:

![Diagramma relazioni entità che mostra il percorso da sales_flat_order a customer_entity](../../assets/SFO___CE_path.png)

## `sales\_flat\_order & sales\_flat\_order\_item`

![1_OneOrderManyItems](../../assets/1_OneOrderManyItems.png)

Un ordine può contenere molti elementi. La relazione tra queste due tabelle è `sales\_flat\_order.entity\_id = sales\_flat\_order\_item.order\_id`.

All&#39;interno di [!DNL Commerce Intelligence], se il percorso tra queste due tabelle non esiste, è possibile [creare il percorso](../data-warehouse-mgr/create-paths-calc-columns.md) nella scheda Data Warehouse. Quando siete pronti a creare il percorso, definite il percorso come mostrato di seguito.

![Diagramma relazioni entità che mostra il percorso da sales_flat_order_item a sales_flat_order](../../assets/SFOI___SFO_path.png)

## `catalog\_product\_entity & sales\_flat\_order\_item`

![3_OneProductManyTimes](../../assets/3_OneProductManyTimes.png)

Un prodotto può essere acquistato in molti articoli. La relazione tra queste due tabelle è `catalog\_product\_entity.entity\_id = sales\_flat\_order\_item.product`.

All&#39;interno di [!DNL Commerce Intelligence], se il percorso tra queste due tabelle non esiste, è possibile [creare il percorso](../data-warehouse-mgr/create-paths-calc-columns.md) nella scheda Data Warehouse. Quando siete pronti a creare il percorso, definite il percorso come mostrato di seguito.

![Diagramma relazioni entità che mostra il percorso da sales_flat_order_item a catalog_product_entity](../../assets/SFOI___CPE_path.png)
