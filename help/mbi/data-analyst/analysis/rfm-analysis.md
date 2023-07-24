---
title: Recency, frequenza, analisi monetaria (RFM)
description: Scopri come impostare una dashboard che consenta di segmentare i clienti in base all’attualità, alla frequenza e alle classificazioni monetarie.
exl-id: 8f0f08fd-710b-4810-9faf-3d0c3cc0a25d
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# Analisi RFM

Questo argomento illustra come impostare una dashboard che consenta di segmentare i clienti in base all’attualità, alla frequenza e alle classificazioni monetarie. L’analisi RFM è una tecnica di marketing che prende in considerazione i comportamenti dei clienti per aiutarti a determinare la segmentazione per l’estensione. Essa tiene conto di tre aspetti:

1. Recency in quanto recentemente un cliente ha acquistato dal tuo negozio
1. Frequenza di acquisto
1. Quante spese spende il cliente

![](../../assets/blobid0.png)

L&#39;analisi RFM può essere configurata solo se si dispone di [!DNL Adobe Commerce Intelligence] Pro pianifica la nuova architettura (ad esempio, se disponi del `Data Warehouse Views` opzione sotto `Manage Data` menu). Queste colonne possono essere create da **[!DNL Manage Data > Data Warehouse]** pagina. Istruzioni dettagliate sono fornite di seguito.

## Guida introduttiva

Devi innanzitutto caricare un file contenente solo una chiave primaria con il valore di una. Ciò consente di creare alcune colonne calcolate necessarie per l’analisi.

Puoi utilizzare questo [articolo](../importing-data/connecting-data/using-file-uploader.md) e l&#39;immagine seguente per formattare il file.

## Colonne calcolate

Un&#39;ulteriore distinzione viene fatta se la vostra azienda consente gli ordini degli ospiti. In tal caso, puoi ignorare tutti i passaggi per `customer_entity` tabella. Se gli ordini degli ospiti non sono consentiti, ignora tutti i passaggi per `sales_flat_order` tabella.

Colonne da creare

* **`Sales_flat_order/customer_entity`** tabella
* `Customer's last order date`
* [!UICONTROL Column type]: `Many to one > Max`
* [!UICONTROL Pat]: `sales_flat_order.customer_id > customer_entity.entity_id`
* Selezionato [!UICONTROL column]: `created_at`
* [!UICONTROL Filter]: `Orders we count`

* 
      Secondi trascorsi dall&#39;ultima data dell&#39;ordine del cliente
  * [!UICONTROL Column type]: - &quot;Stessa tabella > Età
* Selezionato [!UICONTROL column]: `Customer's last order date`

* (input) Riferimento conteggio
* [!UICONTROL Column type]: `Same table > Calculation`
* 
  [!UICONTROL Input]: `entity_id`
* [!UICONTROL Calculation]: `**case when A is null then null else 1 end**`
* 
  [!UICONTROL Datatype]: `Integer`

* **Riferimento conteggio** tabella (file caricato con il numero &quot;1&quot;)
* Numero di clienti
* [!UICONTROL Column type]: `Many to One > Count Distinct`
* [!UICONTROL Path]: `ales_flat_order.(input) reference > Count reference.Primary Key` OPPURE `customer_entity.(input)reference > Count Reference`. `Primary Key`
* Selezionato [!UICONTROL column]: `sales_flat_order.customer_email` OPPURE `customer_entity.entity_id`

* **Customer_entity** tabella
* Numero di clienti
* [!UICONTROL Column type]: `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]: `customer_entity`.(input) reference > Customer Concentration (Concentrazione cliente). `Primary Key`
* Selezionato [!UICONTROL column]: `Number of customers`

* (ingresso) `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's lifetime revenue`

* Classificazione per ricavi ciclo di vita cliente
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `case when A is null then null else (B-(A-1)) end`
* 
  [!UICONTROL Datatype]: `Integer`

* Punteggio monetario del cliente (in percentili)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* 
  [!UICONTROL Datatype]: `Integer`

* (input) Classificazione per numero di ordini del ciclo di vita del cliente
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's lifetime number of orders`

* Classificazione in base al numero di ordini del ciclo di vita del cliente
* 
  [!UICONTROL Tipo di colonna]: – "Stessa tabella > Calcolo"
* [!UICONTROL Inputs]: - **(input) Classificazione per numero di ordini del ciclo di vita del cliente**, **Numero di clienti**
* [!UICONTROL Calculation]: - **caso in cui A è nullo e quindi nullo; altrimenti (B-(A-1))**
* [!UICONTROL Datatype]: - Intero

* Punteggio di frequenza del cliente (in percentili)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime number of orders`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* 
  [!UICONTROL Datatype]: `Integer`

* Classificazione per secondi dalla data dell&#39;ultimo ordine del cliente
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Seconds since customer's last order date`

* Punteggio di recency del cliente (in percentili)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime number of orders`, `Number of customers`
* [!UICONTROL Calculation]: `Case when (A * 100/B,0) <= 20 then 5 when (A * 100/B,0) <= 40 then 4 when (A * 100/B,0) <= 60 then 3 when (A * 100/B,0) <= 80 then 2 when (A * 100/B,0) <= 100 then 1 else 0 end`
* 
  [!UICONTROL Datatype]: `Integer`

* Punteggio di recency del cliente (in percentili)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `Customer's recency score (by percentiles)`, `Customer's frequency score (by percentiles)`, `Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]: `case when (A IS NULL or B IS NULL or C IS NULL) then null else concat(A,B,C) end`
* 
  [!UICONTROL Datatype]: String

* **Riferimento conteggio** tabella
* [!UICONTROL Number of customers]: `(RFM > 0)`
* [!UICONTROL Column type]: `Many to One > Count Distinct`
* [!UICONTROL Path]: `sales_flat_order.(input) reference > Customer Concentration. Primary Key` OPPURE `customer_entity.(input)reference > Customer Concentration.Primary Key`
* Selezionato [!UICONTROL column]: `sales_flat_order.customer_email` OPPURE `customer_entity.entity_id`
* [!UICONTROL Filter]: `Customer's RFM score (by percentile)` Diverso da 000

* **Customer_entity** tabella
* [!UICONTROL Number of customers]: `(RFM > 0)`
* [!UICONTROL Column type]: `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]: `customer_entity.(input) reference > Customer Concentration.Primary Key`
* Selezionato [!UICONTROL column]: - `Number of customers`

* Punteggio di recency del cliente `(R+F+M)`
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: – `Customer's recency score (by percentiles)`, `Customer's frequency score (by percentiles)`, `Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]: `case when (A IS NULL or B IS NULL or C IS NULL) then null else A+B+C end`
* 
  [!UICONTROL Datatype]: `Integer`

* (input) Classificazione per punteggio RFM complessivo del cliente
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's recency score (R+F+M)`
* [!UICONTROL Filter]: `Customer's RFM score (by percentile)` Diverso da 000

* Classificazione in base al punteggio RFM complessivo del cliente
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer's overall RFM score`, `Number of customers (RFM > 0)`
* [!UICONTROL Calculation]: `case when A is null then null else (B-(A-1)) end`
* 
  [!UICONTROL Datatype]: `Integer`

* Gruppo RFM del cliente
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round(A * 100/B,0) <= 20 then '5. copper' when round(A * 100/B,0) <= 40 then '4. bronze' when round(A * 100/B,0) <= 60 then '3. silver' when round(A * 100/B,0)<= 80 then '2. gold' else '1. Platinum' end`
* 
  [!UICONTROL Datatype]: `Integer`

>[!NOTE]
>
>I percentili utilizzati sono anche frazioni di clienti (ad esempio, 20% di bucket per restituire 1-5). Se desideri ponderare questi elementi in modo personalizzato, informa l’analista quando invii il ticket.

## Metriche

Nessuna nuova metrica.

>[!NOTE]
>
>Assicurati di [aggiungere tutte le nuove colonne come dimensioni alle metriche](../data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.

## Rapporti

* **Clienti per raggruppamento RFM**
* Metrica `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's RFM score (by percentiles) Not Equal to 000`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* Nascondi grafico
* [!UICONTROL Group by]: `Customer's RFM group`
* 
  [!UICONTROL Raggruppa per]: `Email`
* 
  [!UICONTROL Chart type]: `Table`

* **Clienti con cinque punteggi di attualità**
* Metrica `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's recency score (by percentiles) Equal to 5`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart Type]: `Scalar`
* Nascondi grafico
* 
  [!UICONTROL Raggruppa per]: `Email`
* [!UICONTROL Group by]: `Customer's RFM score (R+F+M)`
* 
  [!UICONTROL Chart type]: `Table`

* **Clienti con un punteggio di recency**
* Metrica `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's recency score (by percentiles) Equal to 1`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart Type]: `Scalar`
* Nascondi grafico
* 
  [!UICONTROL Raggruppa per]: `Email`
* [!UICONTROL Group by]: `Customer's RFM score (R+F+M)`
* 
  [!UICONTROL Chart type]: `Table`

Dopo aver compilato tutti i rapporti, puoi organizzarli nel dashboard come desideri. Il risultato potrebbe essere simile al dashboard di esempio riportato sopra, ma le tre tabelle generate sono solo esempi dei tipi di segmentazione dei clienti che è possibile eseguire.
