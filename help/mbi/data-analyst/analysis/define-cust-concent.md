---
title: Definire la concentrazione del cliente
description: Scopri come impostare una dashboard che ti aiuti a misurare come vengono distribuiti i ricavi totali nella base clienti.
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
role: Admin, Developer, User
feature: Data Warehouse Manager, Reports, Dashboards
TQID: https://experienceleague.adobe.com/kayq-ci-AiHHgNoaX09h6dqKQX14MudLvEqFmos3hQE
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 472
ht-degree: 0%

---

# Concentrazione dei clienti

In questo argomento viene illustrato come impostare una dashboard che consenta di misurare la distribuzione dei ricavi totali nella base clienti. Scopri la percentuale di clienti che contribuisce al fatturato e crea elenchi segmentati per ottimizzare il mercato e mantenere i clienti con un contributo elevato.

Questa analisi contiene [colonne calcolate avanzate](../data-warehouse-mgr/adv-calc-columns.md).

## Guida introduttiva

Devi innanzitutto caricare un file contenente solo una chiave primaria con il valore di una. Ciò consente di creare alcune colonne calcolate necessarie per l’analisi.

Per formattare il file è possibile utilizzare [lo strumento di caricamento file](../importing-data/connecting-data/using-file-uploader.md) e l&#39;immagine seguente.

## Colonne calcolate

Se si utilizza l&#39;architettura originale (ad esempio, se non si dispone dell&#39;opzione `Data Warehouse Views` nel menu `Manage Data`), contattare il team di supporto per creare le colonne seguenti. Nella nuova architettura, è possibile creare queste colonne dalla pagina `Manage Data > Data Warehouse`. Di seguito sono riportate istruzioni dettagliate.

Un&#39;ulteriore distinzione viene fatta se la vostra azienda consente gli ordini degli ospiti. In tal caso, è possibile ignorare tutti i passaggi per la tabella `customer_entity`. Se gli ordini guest non sono consentiti, ignorare tutti i passaggi per la tabella `sales_flat_order`.

Colonne da creare

* Tabella `Sales_flat_order/customer_entity`
* (input) `reference`
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `entity_id`
* [!UICONTROL Calculation]: - **caso in cui A è null quindi null altrimenti 1 fine**
* [!UICONTROL Datatype]: - `Integer`

* Tabella `Customer concentration` (file caricato con il numero `1`)
* Numero di clienti
* [!UICONTROL Column type]: - `Many to One > Count Distinct`
* Percorso - `sales_flat_order.(input) reference > Customer Concentration.Primary Key` O `customer_entity.(input)reference > Customer Concentration.Primary Key`
* Colonna selezionata - `sales_flat_order.customer_email` O `customer_entity.entity_id`

* Tabella `customer_entity`
* Numero di clienti
* [!UICONTROL Column type]: - `One to Many > JOINED_COLUMN`
* Percorso - `customer_entity.(input) reference > Customer Concentration. Primary Key`
* Colonna selezionata - `Number of customers`

* (input) `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: - `Same table > Event Number`
* Proprietario evento - `Number of customers`
* Classifica eventi - `Customer's lifetime revenue`

* Percentile di ricavi del cliente
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: - **se A è null, allora null else (A/B)* 100 end &#x200B;**
* [!UICONTROL Datatype]: - `Decimal`

* Tabella `Sales_flat_order`
* Numero di clienti
* [!UICONTROL Column type]: - `One to Many > JOINED_COLUMN`
* Percorso - `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* Colonna selezionata - `Number of customers`

* (input) Classificazione per ricavi ciclo di vita cliente
* [!UICONTROL Column type]: - `Same table > Event Number`
* Proprietario evento - `Number of customers`
* Classificazione evento - `Customer's lifetime revenue`
* Filtro - `Customer's order number = 1`

* Percentile di ricavi del cliente
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: - **se A è null, allora null else (A/B)* 100 end &#x200B;**
* [!UICONTROL Datatype]: - `Decimal`

>[!NOTE]
>
>I percentili utilizzati sono anche frazioni di clienti, che rappresentano il X percentile della base clienti. Ogni cliente è associato a un numero intero compreso tra 1 e 100, che può essere considerato come il ricavo del ciclo di vita *rank*. Ad esempio, se il percentile dei ricavi del Cliente per un cliente specifico è **5**, il cliente si trova nel ***quinto percentile*** di tutti i clienti in termini di ricavi relativi al ciclo di vita.

## Metriche

* **Valore totale durata cliente**
* Nella tabella `customer_entity`
* Questa metrica esegue una **somma**
* Nella colonna `Customer's lifetime revenue`
* Ordinato per la marca temporale `Customer's first order date`

## Rapporti

* **Concentrazione cliente**
* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* &#x200B;
  [!UICONTROL Raggruppa per]: `Independent`
* Metrica `A`: `Total customer lifetime revenue by percentile`
* Metrica `B`: `Total customer lifetime revenue (ungrouped)`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's revenue percentile`
* Mostra superiore/inferiore: `100% of Customer's revenue percentile Name`
* &#x200B;
  [!UICONTROL Chart type]: `Line`

* **Primi 10% di concentrazione**
* [!UICONTROL Filter]: `Customer's revenue percentile <= 10`

* Metrica `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* Nascondi grafico
* &#x200B;
  [!UICONTROL Raggruppa per]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

* **Ultima concentrazione del 50% con un solo acquisto**

* Metrica `A`: `Total customer lifetime revenue`
* `Customer's revenue percentile <= 50`
* `Customer's lifetime number of orders = 1`
* [!UICONTROL Filter]:

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* Nascondi grafico
* &#x200B;
  [!UICONTROL Raggruppa per]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

* **Concentrazione inferiore del 10%**
* [!UICONTROL Filter]: `Customer's revenue percentile > 90`

* Metrica `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* Nascondi grafico
* &#x200B;
  [!UICONTROL Raggruppa per]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

Dopo aver compilato tutti i rapporti, puoi organizzarli nel dashboard come desideri. Il risultato potrebbe essere simile al dashboard di esempio riportato sopra.

Per qualsiasi domanda durante la creazione di questa analisi, o semplicemente per coinvolgere il team Professional Services, [contatta il supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
