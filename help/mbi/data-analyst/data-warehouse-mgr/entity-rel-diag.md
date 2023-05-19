---
title: Diagrammi di relazione entità
description: Scopri alcuni diagrammi ER per visualizzare la relazione tra una serie di tabelle di database di Commerce comuni.
exl-id: de7d419f-efbe-4d0c-95a8-155a12aa93f3
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# Diagramma relazione entità

Che cos’è un’ **[!UICONTROL entity relationship (ER) diagram]**? Un [!UICONTROL ER] Il diagramma è una visualizzazione delle tabelle all’interno di un database e del modo in cui si relazionano tra loro. Questo argomento contiene alcuni [!UICONTROL ER] diagrammi per aiutarti a visualizzare la relazione tra alcune tabelle di database comuni di Adobe Commerce.

>[!NOTE]
>
>In questo argomento vengono visualizzate le parole **unire**, **relazione**, e **percorso**. Queste parole vengono utilizzate per descrivere la connessione tra due tabelle.

## Commerce core [!UICONTROL ER] Diagramma

![4_DB_Chart](../../assets/4_DB_Chart.png)

Questo `ER` rappresenta le relazioni tra le tabelle principali di un database Commerce. Visualizzando più relazioni contemporaneamente, è possibile vedere in che modo i dati si relazionano tra più tabelle.

Le sezioni seguenti contengono `ER` diagrammi specifici di due tabelle alla volta. Per visualizzare un diagramma e la relativa descrizione, fare clic sull&#39;intestazione di tale sezione.

## `customer\_entity & sales\_flat\_order`

![Un cliente molti ordini](../../assets/2_OneCustomerManyOrders.png)

Un cliente può effettuare molti ordini. La relazione tra queste due tabelle è `customer\_entity.entity\_id = sales\_flat\_order.customer\_id`

>[!IMPORTANT]
>
>`customer\_entity.entity\_id` non è uguale a `sales\_flat\_order.entity\_id`. Il primo può essere considerato come un `customer\_id` e il secondo può essere considerato come un `order\_id.`

Entro [!DNL Commerce Intelligence], se il percorso tra queste due tabelle non esiste, è possibile [creare il percorso](../data-warehouse-mgr/create-paths-calc-columns.md) nella scheda Data Warehouse. Quando siete pronti a creare il percorso, questo viene definito come segue:

![](../../assets/SFO___CE_path.png)

## `sales\_flat\_order & sales\_flat\_order\_item`

![1_OneOrderManyItems](../../assets/1_OneOrderManyItems.png)

Un ordine può contenere molti elementi. La relazione tra queste due tabelle è `sales\_flat\_order.entity\_id = sales\_flat\_order\_item.order\_id`.

Entro [!DNL Commerce Intelligence], se il percorso tra queste due tabelle non esiste, è possibile [creare il percorso](../data-warehouse-mgr/create-paths-calc-columns.md) nella scheda Data Warehouse. Quando siete pronti a creare il percorso, definite il percorso come mostrato di seguito.

![](../../assets/SFOI___SFO_path.png)

## `catalog\_product\_entity & sales\_flat\_order\_item`

![3_OneProductManyTimes](../../assets/3_OneProductManyTimes.png)

Un prodotto può essere acquistato in molti articoli. La relazione tra queste due tabelle è `catalog\_product\_entity.entity\_id = sales\_flat\_order\_item.product`.

Entro [!DNL Commerce Intelligence], se il percorso tra queste due tabelle non esiste, è possibile [creare il percorso](../data-warehouse-mgr/create-paths-calc-columns.md) nella scheda Data Warehouse. Quando siete pronti a creare il percorso, definite il percorso come mostrato di seguito.

![](../../assets/SFOI___CPE_path.png)
