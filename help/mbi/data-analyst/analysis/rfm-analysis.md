---
title: Recency, Frequenza, Analisi monetaria (RFM)
description: Scopri come impostare un dashboard che ti consenta di segmentare i clienti in base alla loro frequenza, recency e classificazione monetaria.
exl-id: 8f0f08fd-710b-4810-9faf-3d0c3cc0a25d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# Analisi RFM

In questo articolo, mostriamo come impostare un dashboard che ti consenta di segmentare i clienti in base alla loro recency, frequenza e classificazione monetaria. L’analisi RFM è una tecnica di marketing che prende in considerazione i comportamenti dei clienti per aiutarti a determinare la segmentazione per l’attività. Esso tiene conto di tre aspetti: Recente in quanto recentemente un cliente ha acquistato dal tuo negozio, frequenza in quanto spesso acquista da te, e monetario in quanto il cliente spende.

![](../../assets/blobid0.png)

L’analisi RFM può essere configurata solo se disponi della [!DNL MBI] Pianifica Pro sulla nuova architettura (ad esempio, se disponi dell’opzione &quot;Data Warehouse viste&quot; nel menu &quot;Gestisci dati&quot;). Queste colonne possono essere create dalla pagina &quot;Gestisci dati > Data Warehouse&quot;. Istruzioni dettagliate sono fornite di seguito.

## Introduzione

Devi prima caricare un file contenente solo una chiave primaria con il valore di uno. In questo modo sarà possibile creare alcune colonne calcolate necessarie per l’analisi.

Puoi sfruttare questo [articolo del centro di assistenza](../importing-data/connecting-data/using-file-uploader.md) e l&#39;immagine seguente per formattare il file.

## Colonne calcolate

Un&#39;ulteriore distinzione viene fatta se la vostra azienda permette gli ordini dei clienti. In tal caso, puoi ignorare tutti i passaggi della `customer_entity` tabella. Se gli ordini degli ospiti non sono consentiti, ignora tutti i passaggi per `sales_flat_order` tabella.

Colonne da creare

* **`Sales_flat_order/customer_entity`** tabella
* `Customer's last order date`
* [!UICONTROL Column type]: `Many to one > Max`
* [!UICONTROL Pat]: `sales_flat_order.customer_id > customer_entity.entity_id`
* Selezionati [!UICONTROL column]: `created_at`
* [!UICONTROL Filter]: `Orders we count`

* 

       Secondi dall’ultima data dell’ordine del cliente
   * [!UICONTROL Column type]: - &quot;Stessa tabella > Età
* Selezionati [!UICONTROL column]: `Customer's last order date`

* (input) Riferimento al conteggio
* [!UICONTROL Column type]: `Same table > Calculation`
* 
   [!UICONTROL Ingressi]: `entity_id`
* [!UICONTROL Calculation]: `**case when A is null then null else 1 end**`
* 

   [!UICONTROL Tipo di dati]: `Integer`

* **Riferimento conteggio** tabella (questo è il file appena caricato con il numero &quot;1&quot;)
* Numero di clienti
* [!UICONTROL Column type]: `Many to One > Count Distinct`
* [!UICONTROL Path]: `ales_flat_order.(input) reference > Count reference.Primary Key` O `customer_entity.(input)reference > Count Reference`. `Primary Key`
* Selezionati [!UICONTROL column]: `sales_flat_order.customer_email` O `customer_entity.entity_id`

* **Entità_cliente** tabella
* Numero di clienti
* [!UICONTROL Column type]: `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]: `customer_entity`.(input) riferimento > Concentrazione del cliente. `Primary Key`
* Selezionati [!UICONTROL column]: `Number of customers`

* (ingresso) `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's lifetime revenue`

* Classificazione in base ai ricavi della vita del cliente
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `case when A is null then null else (B-(A-1)) end`
* 

   [!UICONTROL Tipo di dati]: `Integer`

* Punteggio monetario del cliente (in percentuale)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* 

   [!UICONTROL Tipo di dati]: `Integer`

* (input) Classificazione per numero di ordini della durata del cliente
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's lifetime number of orders`

* Classificazione per numero di ordini della durata del cliente
* 
   [!UICONTROL Tipo di colonna]: – "Stessa tabella > Calcolo"
* [!UICONTROL Inputs]: - **(input) Classificazione per numero di ordini della durata del cliente**, **Numero di clienti**
* [!UICONTROL Calculation]: - **caso in cui A è nullo, null altro (B-(A-1)) end**
* [!UICONTROL Datatype]: - Intero

* Punteggio di frequenza del cliente (in percentuale)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime number of orders`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* 

   [!UICONTROL Tipo di dati]: `Integer`

* Classificazione in secondi dalla data dell’ultimo ordine del cliente
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Seconds since customer's last order date`

* Punteggio di aggiornamento del cliente (in percentuale)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime number of orders`, `Number of customers`
* [!UICONTROL Calculation]: `Case when (A * 100/B,0) <= 20 then 5 when (A * 100/B,0) <= 40 then 4 when (A * 100/B,0) <= 60 then 3 when (A * 100/B,0) <= 80 then 2 when (A * 100/B,0) <= 100 then 1 else 0 end`
* 

   [!UICONTROL Tipo di dati]: `Integer`

* Punteggio di aggiornamento del cliente (in percentuale)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `Customer's recency score (by percentiles)`, `Customer's frequency score (by percentiles)`, `Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]: `case when (A IS NULL or B IS NULL or C IS NULL) then null else concat(A,B,C) end`
* 

   [!UICONTROL Tipo di dati]: String

* **Riferimento conteggio** tabella
* [!UICONTROL Number of customers]: `(RFM > 0)`
* [!UICONTROL Column type]: `Many to One > Count Distinct`
* [!UICONTROL Path]: `sales_flat_order.(input) reference > Customer Concentration. Primary Key` O `customer_entity.(input)reference > Customer Concentration.Primary Key`
* Selezionati [!UICONTROL column]: `sales_flat_order.customer_email` O `customer_entity.entity_id`
* [!UICONTROL Filter]: `Customer's RFM score (by percentile)` Uguale A 000

* **Entità_cliente** tabella
* [!UICONTROL Number of customers]: `(RFM > 0)`
* [!UICONTROL Column type]: `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]: `customer_entity.(input) reference > Customer Concentration.Primary Key`
* Selezionati [!UICONTROL column]: - `Number of customers`

* Punteggio di aggiornamento del cliente `(R+F+M)`
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: - `Customer's recency score (by percentiles)`, `Customer's frequency score (by percentiles)`, `Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]: `case when (A IS NULL or B IS NULL or C IS NULL) then null else A+B+C end`
* 

   [!UICONTROL Tipo di dati]: `Integer`

* (input) Classificazione in base al punteggio RFM complessivo del cliente
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's recency score (R+F+M)`
* [!UICONTROL Filter]: `Customer's RFM score (by percentile)` Uguale A 000

* Classificazione in base al punteggio RFM complessivo del cliente
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer's overall RFM score`, `Number of customers (RFM > 0)`
* [!UICONTROL Calculation]: `case when A is null then null else (B-(A-1)) end`
* 

   [!UICONTROL Tipo di dati]: `Integer`

* Gruppo RFM del cliente
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round(A * 100/B,0) <= 20 then '5. copper' when round(A * 100/B,0) <= 40 then '4. bronze' when round(A * 100/B,0) <= 60 then '3. silver' when round(A * 100/B,0)<= 80 then '2. gold' else '1. Platinum' end`
* 

   [!UICONTROL Tipo di dati]: `Integer`

>[!NOTE]
>
>I percentili utilizzati sono anche suddivisioni di clienti (ad esempio, 20% di bucket per restituire 1-5). Se hai un modo personalizzato per ponderarli, fai sapere all&#39;analista quando invii il biglietto.

## Metriche

Nessuna nuova metrica!

**Nota**: Assicurati di [aggiungi tutte le nuove colonne come dimensioni alle metriche](../data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.

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
   [!UICONTROL Group by]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **Clienti con 5 punteggi recenti**
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
   [!UICONTROL Group by]: `Email`
* [!UICONTROL Group by]: `Customer's RFM score (R+F+M)`
* 

   [!UICONTROL Chart type]: `Table`

* **Clienti con 1 punteggio recente**
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
   [!UICONTROL Group by]: `Email`
* [!UICONTROL Group by]: `Customer's RFM score (R+F+M)`
* 

   [!UICONTROL Chart type]: `Table`

Dopo aver compilato tutti i rapporti, puoi organizzarli nel dashboard come desideri. Il risultato finale potrebbe assomigliare al dashboard di esempio riportato sopra, ma le tre tabelle generate sono solo esempi dei tipi di segmentazione del cliente che puoi eseguire.
