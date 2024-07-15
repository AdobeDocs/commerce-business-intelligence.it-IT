---
title: Soglia spedizione gratuita
description: Scopri come impostare una dashboard che tenga traccia delle prestazioni della soglia di spedizione gratuita.
exl-id: a90ad89b-96d3-41f4-bfc4-f8c223957113
role: Admin,  User
feature: Data Warehouse Manager, Dashboards, Reports
source-git-commit: 6bdbdbcc652d476fa2a22589ac99678d5855e6fe
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# Spedizione gratuita

>[!NOTE]
>
>Questo argomento contiene istruzioni per i client che utilizzano l&#39;architettura originale e la nuova architettura. La nuova architettura è attiva se è disponibile la sezione `Data Warehouse Views` dopo aver selezionato `Manage Data` dalla barra degli strumenti principale.

In questo argomento viene illustrato come impostare un dashboard che tenga traccia delle prestazioni della soglia di spedizione gratuita. Questa dashboard, mostrata di seguito, è un ottimo modo per testare A/B due soglie di spedizione gratuite. Ad esempio, la tua azienda potrebbe non essere sicura di dover offrire la spedizione gratuita a $50 o $100. È necessario eseguire un test A/B di due sottoinsiemi casuali dei clienti ed eseguire l&#39;analisi in [!DNL Commerce Intelligence].

Prima di iniziare, si desidera identificare due periodi di tempo separati in cui si sono avuti valori diversi per la soglia di spedizione gratuita del negozio.

![](../../assets/free_shipping_threshold.png)

Questa analisi contiene [colonne calcolate avanzate](../data-warehouse-mgr/adv-calc-columns.md).

## Colonne calcolate

Se si utilizza l&#39;architettura originale (ad esempio, se non si dispone dell&#39;opzione `Data Warehouse Views` nel menu `Manage Data`), contattare il team di supporto per creare le colonne seguenti. Nella nuova architettura, è possibile creare queste colonne dalla pagina `Manage Data > Data Warehouse`. Di seguito sono riportate istruzioni dettagliate.

* Tabella **`sales_flat_order`**
   * Questo calcolo crea dei bucket in incrementi relativi alle dimensioni tipiche del carrello. Può essere incrementato da 5, 10, 50, 100

* Architettura originale **`Order subtotal (buckets)`**: creata da un analista come parte del ticket `[FREE SHIPPING ANALYSIS]`
* **`Order subtotal (buckets)`** Nuova architettura:
   * Come accennato in precedenza, questo calcolo crea periodi fissi con incrementi relativi alle dimensioni tipiche del carrello. Se si dispone di una colonna del subtotale nativa come `base_subtotal`, è possibile utilizzarla come base per questa nuova colonna. In caso contrario, può essere una colonna calcolata che esclude la spedizione e gli sconti dai ricavi.

  >[!NOTE]
  >
  >Le dimensioni del &quot;bucket&quot; dipendono da ciò che è appropriato per te come client. Puoi iniziare con `average order value` e creare alcuni bucket inferiori e superiori a tale importo. Osservando il calcolo riportato di seguito, è possibile copiare facilmente una parte della query, modificarla e creare contenitori aggiuntivi. L&#39;esempio viene eseguito con incrementi di 50.

   * `Column type - Same table, Column definition - Calculation, Column Inputs-` `base_subtotal` o `calculated column`, `Datatype`: `Integer`
   * [!UICONTROL Calculation]: `case when A >= 0 and A<=200 then 0 - 200`
quando `A< 200` e `A <= 250` quindi `201 - 250`
quando `A<251` e `A<= 300` quindi `251 - 300`
quando `A<301` e `A<= 350` quindi `301 - 350`
quando `A<351` e `A<=400` quindi `351 - 400`
quando `A<401` e `A<=450` quindi `401 - 450`
other &#39;oltre 450&#39;
fine


## Metriche

Nessuna nuova metrica!!!

>[!NOTE]
>
>Assicurati di [aggiungere tutte le nuove colonne come dimensioni alle metriche](../data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.

## Rapporti

* **Valore medio ordine con regola di spedizione A**
   * [!UICONTROL Metric]: `Average order value`

* Metrica `A`: `Average Order Value`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart Type]: `Scalar`

* **Numero di ordini per bucket di subtotale con regola di spedizione A**
   * [!UICONTROL Metric]: `Number of orders`

  >[!NOTE]
  >
  >È possibile tagliare l&#39;estremità finale mostrando i primi `X` `sorted by` `Order subtotal` (bucket) in `Show top/bottom`.

* Metrica `A`: `Number of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 
  [!UICONTROL Chart Type]: `Column`

* **Percentuale di ordini per subtotale con regola di spedizione A**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * 
     [!UICONTROL Raggruppa per]: `Independent`
   * [!UICONTROL Formula]: `(A / B)`
   * 
     [!UICONTROL Format]: `%`

* Metrica `A`: `Number of orders by subtotal (hide)`
* Metrica `B`: `Total number of orders (hide)`
* [!UICONTROL Formula]: `% of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 
  [!UICONTROL Chart Type]: `Line`

* **Percentuale di ordini con subtotale superiore alla regola di spedizione A**
   * [!UICONTROL Metric]: `Number of orders`
   * 
     [!UICONTROL Perspective]: `Cumulative`

   * [!UICONTROL Metric]: `Number of orders`
   * 
     [!UICONTROL Raggruppa per]: `Independent`

   * [!UICONTROL Formula]: `1- (A / B)`
   * 
     [!UICONTROL Format]: `%`

* Metrica `A`: `Number of orders by subtotal`
* Metrica `B`: `Total number of orders (hide)`
* [!UICONTROL Formula]: `% of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 
  [!UICONTROL Chart Type]: `Line`


Ripetere i passaggi e i rapporti sopra indicati per la spedizione B e il periodo di tempo con la regola di spedizione B.

Dopo aver compilato tutti i rapporti, puoi organizzarli nel dashboard come desideri. Il risultato potrebbe essere simile all’immagine nella parte superiore della pagina.
