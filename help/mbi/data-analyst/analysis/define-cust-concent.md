---
title: Definire la concentrazione del cliente
description: Scopri come impostare una dashboard che ti aiuti a misurare come vengono distribuiti i ricavi totali nella base clienti.
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# Concentrazione dei clienti

Questo articolo illustra come impostare una dashboard che ti aiuti a misurare come vengono distribuiti i ricavi totali nella base clienti. Scopri la percentuale di clienti che contribuisce al fatturato e crea elenchi segmentati per ottimizzare il mercato e mantenere i clienti con un contributo elevato.

Questa analisi contiene [colonne calcolate avanzate](../data-warehouse-mgr/adv-calc-columns.md).

## Guida introduttiva

Devi innanzitutto caricare un file contenente solo una chiave primaria con il valore di una. Ciò consente di creare alcune colonne calcolate necessarie per l’analisi.

È possibile utilizzare [caricatore di file](../importing-data/connecting-data/using-file-uploader.md) e l&#39;immagine seguente per formattare il file.

## Colonne calcolate

Se utilizzi l’architettura originale (ad esempio, se non disponi del `Data Warehouse Views` opzione sotto `Manage Data` ), desideri contattare il team di supporto per creare le colonne seguenti. Nella nuova architettura, queste colonne possono essere create dal `Manage Data > Data Warehouse` pagina. Di seguito sono riportate istruzioni dettagliate.

Un&#39;ulteriore distinzione viene fatta se la vostra azienda consente gli ordini degli ospiti. In tal caso, puoi ignorare tutti i passaggi per `customer_entity` tabella. Se gli ordini degli ospiti non sono consentiti, ignora tutti i passaggi per `sales_flat_order` tabella.

Colonne da creare

* `Sales_flat_order/customer_entity` tabella
* (ingresso) `reference`
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `entity_id`
* [!UICONTROL Calculation]: - **caso in cui A è null then null else 1 end**
* [!UICONTROL Datatype]: – `Integer`

* `Customer concentration` tabella (file caricato con il numero `1`)
* Numero di clienti
* [!UICONTROL Column type]: – `Many to One > Count Distinct`
* Percorso - `sales_flat_order.(input) reference > Customer Concentration.Primary Key` OPPURE `customer_entity.(input)reference > Customer Concentration.Primary Key`
* Colonna selezionata - `sales_flat_order.customer_email` OPPURE `customer_entity.entity_id`

* `customer_entity` tabella
* Numero di clienti
* [!UICONTROL Column type]: – `One to Many > JOINED_COLUMN`
* Percorso - `customer_entity.(input) reference > Customer Concentration. Primary Key`
* Colonna selezionata - `Number of customers`

* (ingresso) `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: – `Same table > Event Number`
* Proprietario evento - `Number of customers`
* Classifica eventi - `Customer's lifetime revenue`

* Percentile di ricavi del cliente
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]IT: - **caso in cui A è null e quindi null else (A/B)* 100 end **
* [!UICONTROL Datatype]: – `Decimal`

* `Sales_flat_order` tabella
* Numero di clienti
* [!UICONTROL Column type]: – `One to Many > JOINED_COLUMN`
* Percorso - `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* Colonna selezionata - `Number of customers`

* (input) Classificazione per ricavi ciclo di vita cliente
* [!UICONTROL Column type]: – `Same table > Event Number`
* Proprietario evento - `Number of customers`
* Classifica eventi - `Customer's lifetime revenue`
* Filtro - `Customer's order number = 1`

* Percentile di ricavi del cliente
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]IT: - **caso in cui A è null e quindi null else (A/B)* 100 end **
* [!UICONTROL Datatype]: - `Decimal`

>[!NOTE]
>
>I percentili utilizzati sono anche frazioni di clienti, che rappresentano il X percentile della base clienti. Ogni cliente è associato a un numero intero compreso tra 1 e 100, che può essere considerato come il ricavo del ciclo di vita *rango*. Ad esempio, se il percentile dei ricavi del cliente per un cliente specifico è **5**, questo cliente si trova in ***quinto percentile*** di tutti i clienti in termini di fatturato nel ciclo di vita.

## Metriche

* **Valore &quot;lifetime&quot; del ciclo di vita totale del cliente**
* In `customer_entity` tabella
* Questa metrica esegue una **Somma**
* Il giorno `Customer's lifetime revenue` colonna
* Ordinato da `Customer's first order date` timestamp

## Rapporti

* **Concentrazione dei clienti**
* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* 
   [!UICONTROL Raggruppa per]: `Independent`
* Metrica `A`: `Total customer lifetime revenue by percentile`
* Metrica `B`: `Total customer lifetime revenue (ungrouped)`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's revenue percentile`
* Mostra superiore/inferiore: `100% of Customer's revenue percentile Name`
* 

   [!UICONTROL Chart type]: `Line`

* **Massima concentrazione del 10%**
* [!UICONTROL Filter]: `Customer's revenue percentile <= 10`

* Metrica `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* Nascondi grafico
* 
   [!UICONTROL Raggruppa per]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **Concentrazione minima del 50% con un solo acquisto**

* Metrica `A`: `Total customer lifetime revenue`
* `Customer's revenue percentile <= 50`
* `Customer's lifetime number of orders = 1`
* [!UICONTROL Filter]:

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* Nascondi grafico
* 
   [!UICONTROL Raggruppa per]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **Concentrazione minima del 10%**
* [!UICONTROL Filter]: `Customer's revenue percentile > 90`

* Metrica `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* Nascondi grafico
* 
   [!UICONTROL Raggruppa per]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

Dopo aver compilato tutti i rapporti, puoi organizzarli nel dashboard come desideri. Il risultato potrebbe essere simile al dashboard di esempio riportato sopra.

In caso di domande durante la creazione di questa analisi, o se desideri semplicemente coinvolgere il team Professional Services, [contatta l’assistenza](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
