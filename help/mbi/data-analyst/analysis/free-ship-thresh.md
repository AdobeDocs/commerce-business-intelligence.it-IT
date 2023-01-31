---
title: Soglia di spedizione gratuita
description: Scopri come impostare un dashboard che tenga traccia delle prestazioni della soglia di spedizione gratuita.
exl-id: a90ad89b-96d3-41f4-bfc4-f8c223957113
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---

# Spedizione gratuita

>[!NOTE]
>
>Questo articolo contiene istruzioni per i clienti che utilizzano l’architettura originale e la nuova architettura. Se hai la sezione &quot;Viste Date Warehouse&quot; disponibile dopo aver selezionato &quot;Gestisci dati&quot; dalla barra degli strumenti principale, accedi alla nuova architettura.

In questo articolo, mostriamo come impostare un dashboard che tenga traccia delle prestazioni della soglia di spedizione gratuita. Questo dashboard, mostrato di seguito, è un ottimo modo per testare A/B due diverse soglie di spedizione gratuita. Ad esempio, la tua azienda potrebbe non essere sicura di dover offrire la spedizione gratuita a $ 50 o $ 100. È necessario eseguire un test A/B di due sottoinsiemi casuali dei clienti ed eseguire l&#39;analisi in [!DNL MBI].

Prima di iniziare, vuoi identificare due periodi di tempo separati in cui hai avuto valori diversi per la soglia di spedizione gratuita del tuo negozio.

![](../../assets/free_shipping_threshold.png)

Questa analisi contiene [colonne calcolate avanzate](../data-warehouse-mgr/adv-calc-columns.md).

## Colonne calcolate

Se ti trovi nell’architettura originale (ad esempio, se non hai la `Data Warehouse Views` nella sezione `Manage Data` menu), sarà necessario contattare il nostro team di supporto per creare le colonne seguenti. Nella nuova architettura, queste colonne possono essere create dalla `Manage Data > Data Warehouse` pagina. Istruzioni dettagliate sono fornite di seguito.

* **`sales_flat_order`** tabella
   * Questo calcolo crea blocchi in incrementi relativi alle dimensioni del carrello tipiche. Questo può variare da incrementi, compresi, 5, 10, 50, 100

* **`Order subtotal (buckets)`** Architettura originale: verrà creato da un analista come parte del `[FREE SHIPPING ANALYSIS]` biglietto
* **`Order subtotal (buckets)`** Nuova architettura:
   * Come accennato sopra, questo calcolo crea secchi in incrementi rispetto alle dimensioni del carrello tipiche. Se si dispone di una colonna del subtotale nativo, ad esempio `base_subtotal`, che può essere utilizzato come base di questa nuova colonna. In caso contrario, può essere una colonna calcolata che esclude la spedizione e gli sconti dai ricavi.
   >[!NOTE]
   >
   >Le dimensioni &quot;bucket&quot; dipenderanno da ciò che è appropriato per voi come cliente. Puoi iniziare con il tuo `average order value` e creare un certo numero di secchi minori e maggiori di tale quantità. Nel calcolo seguente viene illustrato come copiare facilmente parte della query, modificarla e creare altri blocchi. L&#39;esempio viene fatto con incrementi di 50.

   * `Column type - Same table, Column definition - Calculation, Column Inputs-` `base_subtotal`oppure `calculated column`, `Datatype`: `Integer`
   * [!UICONTROL Calculation]: `case when A >= 0 and A<=200 then 0 - 200`
quando `A< 200` e `A <= 250` then `201 - 250`
quando `A<251` e `A<= 300` then `251 - 300`
quando `A<301` e `A<= 350` then `301 - 350`
quando `A<351` e `A<=400` then `351 - 400`
quando `A<401` e `A<=450` then `401 - 450`
altro &#39;oltre 450&#39; fine



## Metriche

Nessuna nuova metrica!!!

>[!NOTE]
>
>Assicurati di [aggiungi tutte le nuove colonne come dimensioni alle metriche](../data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.

## Rapporti

* **Valore medio dell&#39;ordine con la regola di spedizione A**
   * [!UICONTROL Metric]: `Average order value`

* Metrica `A`: `Average Order Value`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **Numero di ordini per periodi fissi subtotali con regola di spedizione A**
   * [!UICONTROL Metric]: `Number of orders`

   >[!NOTE]
   >
   >È possibile tagliare la coda di fine mostrando la parte superiore `X` `sorted by` `Order subtotal` (secchi) nel `Show top/bottom`.

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
      [!UICONTROL Group by]: `Independent`
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

      [!UICONTROL Group by]: `Independent`

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


Ripetere i passaggi e i rapporti precedenti per la spedizione B e il periodo di tempo con la regola di spedizione B.

Dopo aver compilato tutti i rapporti, puoi organizzarli nel dashboard come desideri. Il risultato finale potrebbe assomigliare all&#39;immagine nella parte superiore della pagina.
