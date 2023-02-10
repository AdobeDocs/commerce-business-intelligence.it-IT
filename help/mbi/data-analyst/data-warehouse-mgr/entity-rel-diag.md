---
title: Diagrammi di relazione entità
description: Scopri alcuni diagrammi ER per visualizzare la relazione tra una manciata di tabelle di database Commerce comuni.
exl-id: de7d419f-efbe-4d0c-95a8-155a12aa93f3
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# Diagramma relazione entità

Cosa è un **[!UICONTROL entity relationship (ER) diagram]**? Un `ER` diagramma è una visualizzazione delle tabelle all’interno di un database e del modo in cui si relazionano tra loro. Questo articolo contiene alcuni diagrammi ER per aiutarti a visualizzare la relazione tra una manciata di tabelle di database Commerce comuni.

>[!NOTE]
>
>In questo articolo vedrai le parole **join**, **relazione** e **path**. Queste parole sono tutte utilizzate per descrivere come due tabelle sono collegate.

## Commerce di base `ER` Diagramma

![4_DB_Chart](../../assets/4_DB_Chart.png)

Questo `ER` il diagramma rappresenta le relazioni tra le tabelle principali di un database Commerce. Visualizzando più relazioni contemporaneamente, è possibile vedere come i dati si rapportano tra più tabelle.

Le sezioni seguenti contengono `ER` diagrammi specifici per due tabelle alla volta. Per visualizzare un diagramma e la relativa descrizione, fai clic sull’intestazione della sezione.

## `customer\_entity & sales\_flat\_order`

![Un cliente molti ordini](../../assets/2_OneCustomerManyOrders.png)

Un cliente può effettuare molti ordini. La relazione tra queste due tabelle è `customer\_entity.entity\_id = sales\_flat\_order.customer\_id`

>[!IMPORTANT]
>
>`customer\_entity.entity\_id` è diverso da `sales\_flat\_order.entity\_id`. Il primo può essere pensato come un `customer\_id` e il secondo può essere considerato come un `order\_id.`

Within [!DNL MBI], se il percorso tra queste due tabelle non esiste già, puoi [creare il percorso](../data-warehouse-mgr/create-paths-calc-columns.md) nella scheda Data Warehouse. Quando sei pronto a creare il percorso, verrà definito come segue:

![](../../assets/SFO___CE_path.png)

## `sales\_flat\_order & sales\_flat\_order\_item`

![1_OneOrderManyItems](../../assets/1_OneOrderManyItems.png)

Un ordine può contenere molti elementi. La relazione tra queste due tabelle è `sales\_flat\_order.entity\_id = sales\_flat\_order\_item.order\_id`.

Within [!DNL MBI], se il percorso tra queste due tabelle non esiste già, puoi [creare il percorso](../data-warehouse-mgr/create-paths-calc-columns.md) nella scheda Data Warehouse. Quando sei pronto a creare il percorso, verrà definito come segue:

![](../../assets/SFOI___SFO_path.png)

## `catalog\_product\_entity & sales\_flat\_order\_item`

![3_OneProductManyTimes](../../assets/3_OneProductManyTimes.png)

Un prodotto può essere acquistato molti articoli. La relazione tra queste due tabelle è `catalog\_product\_entity.entity\_id = sales\_flat\_order\_item.product`.

Within [!DNL MBI], se il percorso tra queste due tabelle non esiste già, puoi [creare il percorso](../data-warehouse-mgr/create-paths-calc-columns.md) nella scheda Data Warehouse. Quando sei pronto a creare il percorso, verrà definito come segue:

![](../../assets/SFOI___CPE_path.png)
