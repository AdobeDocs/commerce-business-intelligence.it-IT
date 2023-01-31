---
title: Definire la concentrazione del cliente
description: Scopri come impostare un dashboard che ti aiuterà a misurare come i ricavi totali vengono distribuiti tra la base di clienti.
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Concentrazione sui clienti

In questo articolo mostriamo come impostare un dashboard che ti aiuti a misurare la distribuzione dei ricavi totali tra la base clienti. Scopri la percentuale di clienti che contribuiscono alla percentuale di ricavi e crea elenchi segmentati per migliorare il mercato e mantenere i tuoi clienti che contribuiscono maggiormente.

Questa analisi contiene [colonne calcolate avanzate](../data-warehouse-mgr/adv-calc-columns.md).

## Introduzione

Devi prima caricare un file contenente solo una chiave primaria con il valore di uno. In questo modo sarà possibile creare alcune colonne calcolate necessarie per l’analisi.

Puoi sfruttare [caricatore di file](../importing-data/connecting-data/using-file-uploader.md) e l&#39;immagine seguente per formattare il file.

## Colonne calcolate

Se ti trovi nell’architettura originale (ad esempio, se non hai la `Data Warehouse Views` nella sezione `Manage Data` menu), sarà necessario contattare il nostro team di supporto per creare le colonne seguenti. Nella nuova architettura, queste colonne possono essere create dalla `Manage Data > Data Warehouse` pagina. Istruzioni dettagliate sono fornite di seguito.

Un&#39;ulteriore distinzione viene fatta se la vostra azienda permette gli ordini dei clienti. In tal caso, puoi ignorare tutti i passaggi della `customer_entity` tabella. Se gli ordini degli ospiti non sono consentiti, ignora tutti i passaggi per `sales_flat_order` tabella.

Colonne da creare

* `Sales_flat_order/customer_entity` tabella
* (ingresso) `reference`
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `entity_id`
* [!UICONTROL Calculation]: - **se A è nullo, allora null&#39;altro 1 end**
* [!UICONTROL Datatype]: - `Integer`

* `Customer concentration` tabella (questo è il file appena caricato con il numero) `1`)
* Numero di clienti
* [!UICONTROL Column type]: - `Many to One > Count Distinct`
* Percorso - `sales_flat_order.(input) reference > Customer Concentration.Primary Key` O `customer_entity.(input)reference > Customer Concentration.Primary Key`
* Colonna selezionata - `sales_flat_order.customer_email` O `customer_entity.entity_id`

* `customer_entity` tabella
* Numero di clienti
* [!UICONTROL Column type]: - `One to Many > JOINED_COLUMN`
* Percorso - `customer_entity.(input) reference > Customer Concentration. Primary Key`
* Colonna selezionata - `Number of customers`

* (ingresso) `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: - `Same table > Event Number`
* Proprietario dell&#39;evento - `Number of customers`
* Classificazione evento - `Customer's lifetime revenue`

* percentile dei ricavi del cliente
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: - **caso in cui A è nullo e null&#39;altro (A/B)* 100 **
* [!UICONTROL Datatype]: - `Decimal`

* `Sales_flat_order` tabella
* Numero di clienti
* [!UICONTROL Column type]: - `One to Many > JOINED_COLUMN`
* Percorso - `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* Colonna selezionata - `Number of customers`

* Classificazione in base ai ricavi per tutta la vita del cliente
* [!UICONTROL Column type]: - `Same table > Event Number`
* Proprietario dell&#39;evento - `Number of customers`
* Classificazione evento - `Customer's lifetime revenue`
* Filtro - `Customer's order number = 1`

* percentile dei ricavi del cliente
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: - **caso in cui A è nullo e null&#39;altro (A/B)* 100 **
* [!UICONTROL Datatype]: - `Decimal`

>[!NOTE]
>
>I percentili utilizzati sono anche suddivisioni di clienti, che rappresentano il Xesimo percentile della base cliente. Ogni cliente sarà associato a un numero intero compreso tra 1 e 100, che può essere considerato come il loro fatturato a vita. *rango*. Ad esempio, se il percentile dei ricavi del cliente per un cliente specifico è **5**, questo cliente si trova nella ***5° percentile*** di tutti i clienti in termini di fatturato a vita.

## Metriche

* **Valore totale del ciclo di vita del cliente**
* In `customer_entity` tabella
* Questa metrica esegue un **Somma**
* Sulla `Customer's lifetime revenue` column
* Ordinato dal `Customer's first order date` timestamp

## Rapporti

* **Concentrazione dei clienti**
* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* 
   [!UICONTROL Group by]: `Independent`
* Metrica `A`: `Total customer lifetime revenue by percentile`
* Metrica `B`: `Total customer lifetime revenue (ungrouped)`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's revenue percentile`
* Mostra superiore/inferiore: `100% of Customer's revenue percentile Name`
* 

   [!UICONTROL Chart type]: `Line`

* **concentrazione massima del 10%**
* [!UICONTROL Filter]: `Customer's revenue percentile <= 10`

* Metrica `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* Nascondi grafico
* 
   [!UICONTROL Group by]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **Concentrazione inferiore del 50% con un solo acquisto**

* Metrica `A`: `Total customer lifetime revenue`
* `Customer's revenue percentile <= 50`
* `Customer's lifetime number of orders = 1`
* [!UICONTROL Filter]:

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* Nascondi grafico
* 
   [!UICONTROL Group by]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **Concentrazione inferiore del 10%**
* [!UICONTROL Filter]: `Customer's revenue percentile > 90`

* Metrica `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* Nascondi grafico
* 
   [!UICONTROL Group by]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

Dopo aver compilato tutti i rapporti, puoi organizzarli nel dashboard come desideri. Il risultato finale potrebbe assomigliare al dashboard di esempio riportato sopra.

In caso di domande durante la creazione di questa analisi, o se desideri semplicemente coinvolgere il nostro team di servizi professionali, [contattare il supporto](../../guide-overview.md).
