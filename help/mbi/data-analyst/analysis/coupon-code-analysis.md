---
title: Prestazioni coupon
description: Scopri come analizzare le prestazioni del coupon.
exl-id: f6565e33-18ee-4f85-ade0-fd361854475b
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 0%

---

# Analisi avanzata del codice coupon

Comprendere le prestazioni del coupon della vostra azienda è un modo interessante per segmentare i vostri ordini e anche meglio comprendere i vostri clienti. Questo articolo ti guiderà attraverso i passaggi per creare analisi per capire quali clienti si acquisiscono attraverso l&#39;uso di coupon, come essi eseguono e monitorare l&#39;uso generale di coupon.

![](../../assets/coupon_analysis_-_analysis_library.png)<!--{: width="800" height="375"}-->

Questa analisi contiene [colonne calcolate avanzate](../data-warehouse-mgr/adv-calc-columns.md).

## Introduzione

Come primo passo, assicurati che le colonne seguenti siano sincronizzate nella tua Data Warehouse. In caso contrario, continua a seguirli, scegliendo &quot;Gestisci dati&quot; > &quot;Data Warehouse&quot; e sincronizzando quanto segue:

* **sales\_flat\_order** tabella
* **coupon\_code**
* **base\_sconto\_importo**

## Colonne calcolate

Colonne da creare indipendentemente dai criteri degli ordini dei clienti:

* `sales\_flat\_order` tabella
* **L&#39;ordine ha il coupon applicato?**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `coupon\_code`
   * [!UICONTROL Datatype]: `String`
   * [!UICONTROL Calculation]: quando `A` è nullo `No coupon` else `Coupon` end


* **\[INPUT\] customer\_id - codice coupon**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `customer\_id`
      * `B`: `coupon\_code`
   * [!UICONTROL Datatype]: Stringa
   * [!UICONTROL Calculation]: `concat(A,' - ',B)`


* **Numero di ordini con questo coupon**
   * [!UICONTROL Column type]: `Same Table => EVENT\_NUMBER`
   * Proprietario evento:`INPUT customer_id - coupon code`
   * Classificazione evento: `created\_at`
   * [!UICONTROL Filters]: `Orders we count` set di filtri

Colonne aggiuntive da creare se gli ordini guest NON sono supportati:

* `customer\_entity` tabella
   * **Il primo ordine del cliente includeva un coupon? (Coupon/No coupon)**
   * [!UICONTROL Column type]: `Many to One => MAX`
   * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
   * Seleziona una [!UICONTROL column]: `Order has coupon applied? (Coupon/No coupon)`
   * [!UICONTROL Filters]:
      * `A`: `Orders we count`
      * `B`: `Customer's order number = 1`
   * **Coupon del primo ordine del cliente**
      * [!UICONTROL Column type]: `Many to One => MAX`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Seleziona una [!UICONTROL column]: `coupon\_code`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Customer's order number = 1`
   * **Numero di coupon utilizzati per il ciclo di vita del cliente**
      * [!UICONTROL Column type]: `Many to One => COUNT`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Order has coupon applied? (Coupon/No coupon) = Coupon`
   * **Acquisto di coupon cliente o non coupon acquisto cliente**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`
      * [!UICONTROL Datatype]: `String`
      * [!UICONTROL Calculation]: **caso in cui A=&#39;Coupon&#39; then &#39;Coupon acquisition customer&#39; else &#39;Non coupon acquisition customer&#39; end**
   * **Percentuale degli ordini del cliente con coupon**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `User's lifetime number of coupons used`
         * `B`: `User's lifetime number of orders`
      * [!UICONTROL Datatype]: `Decimal`
      * [!UICONTROL Calculation]: **caso in cui A è nullo o B è nullo o B=0 allora null altro A/B end**
   * **Utilizzo del coupon del cliente**
      * [!UICONTROL Column type]: `Same Table => Calculation`
      * [!UICONTROL Inputs]:
         * `A`: `Percent of customer's orders with coupon`
      * [!UICONTROL Datatype]: `String`
      * [!UICONTROL Calculation]: **caso in cui A è nullo allora nullo quando A=0 allora &#39;Coupon non utilizzato&#39; quando A&lt;0.5 allora &#39;Prezzo più pieno&#39; quando A=0.5 poi &#39;50/50&#39; quando A=1 poi &#39;Coupon solo&#39; quando A>0.5 poi &#39;Coupon più&#39; altro &#39;Fine indefinita&#39;**









* `sales\_flat\_order` tabella
   * **Il primo ordine del cliente incluso coupon? (Coupon/No coupon)**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Seleziona una [!UICONTROL column]: `Customer's first order included a coupon? (Coupon/No coupon)`
^
   * **Coupon del primo ordine del cliente**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Seleziona una [!UICONTROL column]: `Customer's first order coupon?`


Colonne aggiuntive da creare se gli ordini guest NON sono supportati:

* `sales\_flat\_order` tabella
   * **Il primo ordine del cliente includeva un coupon? (Coupon/No coupon)** **-** creato da analista come parte del ticket \[COUPON ANALYSIS\]
   * **Coupon del primo ordine del cliente**{:}**-** creato da analista come parte del ticket \[COUPON ANALYSIS\]

* **Numero di coupon utilizzati per il ciclo di vita del cliente**{:}**-** creato da analista come parte del ticket \[COUPON ANALYSIS\]
* **Acquisto di coupon cliente o non coupon acquisto cliente**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`
   * [!UICONTROL Datatype]: `String`
   * [!UICONTROL Calculation]: **caso in cui A=&#39;Coupon&#39; then &#39;Coupon acquisition customer&#39; else &#39;Non coupon acquisition customer&#39; end**


* **Percentuale degli ordini del cliente con coupon**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `User's lifetime number of coupons used`
      * `B`: `User's lifetime number of orders`
   * [!UICONTROL Datatype]: `Decimal`
   * [!UICONTROL Calculation]: **caso in cui A è nullo o B è nullo o B=0 allora null altro A/B end**


* **Utilizzo del coupon del cliente**
   * [!UICONTROL Column type]: `Same Table => Calculation`
   * [!UICONTROL Inputs]:
      * `A`: `Percent of customer's orders with coupon`
   * [!UICONTROL Datatype]: `String`
   * [!UICONTROL Calculation]: **caso in cui A è nullo allora nullo quando A=0 allora &#39;Coupon non utilizzato&#39; quando A&lt;0.5 allora &#39;Prezzo più pieno&#39; quando A=0.5 poi &#39;50/50&#39; quando A=1 poi &#39;Coupon solo&#39; quando A>0.5 poi &#39;Coupon più&#39; altro &#39;Fine indefinita&#39;**


## Metriche

* **Importo sconto coupon**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* In `sales\_flat\_order` tabella
* Questa metrica esegue un **Somma**
* Sulla `discount\_amount` column
* Ordinato dal `created\_at` timestamp
* [!UICONTROL Filter]:

* **Numero di coupon utilizzati**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* In `sales\_flat\_order` tabella
* Questa metrica esegue un **Conteggio**
* Sulla `entity\_id` column
* Ordinato dal `created\_at` timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>Assicurati di [aggiungi tutte le nuove colonne come dimensioni alle metriche](../data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.

## Rapporti

* **% dei clienti con cedola acquistata e non acquisita**
   * [!UICONTROL Metric]: `New customers`

* Metrica `A`: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL intervallo]: `None`
* [!UICONTROL Group by]: `Coupon acquisitions customer` o `Non coupon acquisition customer`
* 

   [!UICONTROL Tipo di grafico]: `Pie`

* **Numero di clienti con cedola acquistata e non acquisita**
   * [!UICONTROL Metric]: `New customers`

* Metrica A: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Coupon acquisitions customer` o `Non coupon acquisition customer`
* [!UICONTROL Chart type]: `Stacked column`

* **Ricavo medio della vita: Acq. coupon (90+ giorni)**
   * [!UICONTROL Metric]: `Average lifetime revenue`
   * [!UICONTROL Filter]:
      * Il primo ordine del cliente includeva un coupon (Coupon/No Coupon) = Coupon

* Metrica `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
   [!UICONTROL intervallo]: `None`
* 

   [!UICONTROL Tipo di grafico]: `Scalar`

* **Ricavo medio della vita: Acq. non coupon (90+ giorni)**
   * [!UICONTROL Metric]: Ricavi a vita media
   * [!UICONTROL Filter]:
      * Il primo ordine del cliente includeva un coupon (Coupon/No Coupon) = Nessun coupon

* Metrica `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
   [!UICONTROL intervallo]: `None`
* 

   [!UICONTROL Tipo di grafico]: `Scalar`

* **Ricavi medi a vita per cedola al primo ordine**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* Metrica `A`: `Average lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL intervallo]: `None`
* [!UICONTROL Group by]: `Customer's first order's coupon`
* 

   [!UICONTROL Tipo di grafico]: `Column`

>[!NOTE]
>
>Se hai un gran numero di codici coupon, come molti dei nostri clienti fanno, si desidera applicare un Top/Bottom come Top 10 ordinato per Avg lifetime ricavo

* **Probabilità ordine ripetuto: Acquisizioni di cedole**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Il primo ordine del cliente includeva un coupon (Coupon/No Coupon) = Coupon
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Il primo ordine del cliente includeva un coupon (Coupon/No Coupon) = Coupon
      * L&#39;ultimo ordine del cliente? = No
   * 
      [!Formula UICONTROL]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * Seleziona un numero statisticamente significativo da `Customer's by lifetime orders` grafico. Quando si guarda il grafico, come buona regola in genere cerchiamo i numeri d&#39;ordine con 30 o più clienti nel bucket. A seconda del set di dati, questo può essere un numero grande in modo da poter aggiungere 1-10.


* Metrica `A`: `Number of orders`
* Metrica `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL intervallo]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **Probabilità ordine ripetuto: Acquisizioni non cedole**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Il primo ordine del cliente include un coupon (Coupon/No Coupon) = No Coupon
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Il primo ordine del cliente include un coupon (Coupon/No Coupon) = No Coupon
      * L&#39;ultimo ordine del cliente? = No
   * 
      [!Formula UICONTROL]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * Seleziona un numero statisticamente significativo da `Customer's by lifetime orders` grafico o 1-5.



* Metrica `A`: `Number of orders`
* Metrica `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL intervallo]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **Tasso di utilizzo del coupon acquistato dai clienti (ordini ripetuti)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * Acquisto di cedola cliente o non coupon acquirente = Acquisto di cedola
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Numero ordine del cliente > 1
      * Il primo ordine del cliente includeva un coupon? (Coupon/No coupon) = Coupon
   * [!UICONTROL Metric]:`Number of orders`
   * [!UICONTROL Filter]:
      * Numero ordine del cliente > 1
      * Il primo ordine del cliente includeva un coupon? (Coupon/No coupon) = Coupon
      * L&#39;ordine ha il coupon applicato? (Coupon/No coupon) = Coupon
   * 
      [!Formula UICONTROL]: `C/B`
   * [!UICONTROL Format]: `Percentage %`




* Metrica `A`: `Coupon-acquired customers`
* Metrica `B`: `Number of repeat orders`
* Metrica `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL intervallo]: `None`
* 

   [!UICONTROL Tipo di grafico]: `Table` (può trasporre questa tabella per una visualizzazione migliore)

* **Tasso di utilizzo della cedola dei clienti non acquisiti con coupon (ordini ripetuti)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * Acquisto di cedola cliente o non coupon acquirente = Acquisizione non coupon
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Numero ordine del cliente > 1
      * Il primo ordine del cliente includeva un coupon? (Coupon/No coupon) = Nessun coupon
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Numero ordine del cliente > 1
      * Il primo ordine del cliente includeva un coupon? (Coupon/No coupon) = Nessun coupon
      * L&#39;ordine ha il coupon applicato? (Coupon/No coupon) = Coupon
   * 
      [!Formula UICONTROL]: `C/B`
   * [!UICONTROL Format]: `Percentage %`




* Metrica `A`: `Non-coupon-acquired customers`
* Metrica `B`: `Number of repeat orders`
* Metrica `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL intervallo]: `None`
* 

   [!UICONTROL Tipo di grafico]: `Table` (può trasporre questa tabella per una visualizzazione migliore)

* **Dettagli di utilizzo del coupon (primi ordini)**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Numero dell&#39;ordine del cliente = 1
      * Numero di ordini con questa cedola > 10
   * 
      [!UICONTROL Metric]: `Revenue`
   * [!UICONTROL Filter]:
      * Numero dell&#39;ordine del cliente = 1
      * Numero di ordini con questa cedola > 10
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * Numero dell&#39;ordine del cliente = 1
      * Numero di ordini con questa cedola > 10
   * [!UICONTROL Formula]: `B-C` (se C è negativo); B+C (se C è positivo)
   * 

      [!UICONTROL Format]: `Currency`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * Numero dell&#39;ordine del cliente = 1
      * Numero di ordini con questa cedola > 10




* Metrica `A`: `First time orders (FTO)`
* Metrica `B`: `Revenue from FTO`
* Metrica `C`: `Discounts applied to FTO`
* [!UICONTROL Formula]: `Gross revenue from FTO`
* Metrica `E`: `Average order value for FTO`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL intervallo]: `None`
* [!UICONTROL Group by]: `coupon code`
* 

   [!UICONTROL Tipo di grafico]: `Table`
>[!NOTE]
>
>La quantità di 10 per &quot;Numero di ordini con questo coupon&quot; è arbitraria. Puoi usare la quantità più appropriata per questo filtro.

* **Numero di ordini con coupon (tutti i tempi)**
   * [!UICONTROL Metric]: `Number of coupons used`

* Metrica `A`: `Number or orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL intervallo]: `None`
* 

   [!UICONTROL Tipo di grafico]: `Scalar`

* **Entrate nette da ordini con coupon (tutti i tempi)**
   * 
      [!UICONTROL Metric]: `Revenue`
   * [!UICONTROL Filter]:
      * L&#39;ordine ha il coupon applicato? (Coupon/No coupon) = Coupon

* Metrica `A`: `Net revenue from orders with coupons`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL intervallo]: `None`
* 

   [!UICONTROL Tipo di grafico]: `Scalar`

* **Sconti da coupon (tutti i tempi)**
   * [!UICONTROL Metric]: `Number of coupons used`

* Metrica `A`: `Coupon discount amount`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL intervallo]: `None`
* 

   [!UICONTROL Tipo di grafico]: `Scalar`

* **Numero di ordini con e senza coupon**
   * [!UICONTROL Metric]: `Number of orders`

* Metrica `A`: `Number of orders`
* [!UICONTROL Time period]: `Last 24 months`
* 
   [!UICONTROL intervallo]: `None`
* [!UICONTROL Group by]: `Order has coupon applied? (Coupon/No coupon)`
* [!UICONTROL Chart type]: `Stacked column`

* **Utilizzo del coupon tra utenti ripetuti**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * Numero di ordini per tutta la durata del cliente > 1

* Metrica `A`: `New customers`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL intervallo]: `None`
* [!UICONTROL Group by]: `Customer's coupon usage`
* 

   [!UICONTROL Tipo di grafico]: `Pie`

* **Dettagli utilizzo coupon**
   * [!UICONTROL Metric]: `Number of orders with coupon`
   * [!UICONTROL Filter]:
      * Numero di ordini con questa cedola > 10
   * 
      [!UICONTROL Metric]: `Revenue`
   * [!UICONTROL Filter]:
      * Numero di ordini con questa cedola > 10
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * Numero di ordini con questa cedola > 10
   * [!UICONTROL Formula]: `B-C` (se `C` è negativo); `B+C` (se `C` è positivo)
   * 

      [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `C/(B-C)` (se `C` è negativo); `C/(B+C)` (se `C` è positivo)
   * 

      [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * Numero di ordini con questa cedola > 10
   * 
      [!Formula UICONTROL]: `C/A`
   * 

      [!UICONTROL Format]: `Currency`

   * [!UICONTROL Metric]: `Distinct buyers`
   * [!UICONTROL Filter]:
      * Numero di ordini con questa cedola > 10





* Metrica `A`: `Number of orders`
* Metrica `B`: `Net revenue from orders`
* Metrica `C`: `Total discounts applied`
* [!UICONTROL Formula]: `Gross revenue`
* [!UICONTROL Formula]: `% discounted`
* Metrica `F`: `Average net order value`
* [!UICONTROL Formula]: `Average order discount`
* Metrica `H`: `Distinct buyers`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL intervallo]: `None`
* [!UICONTROL Group by]: `coupon code`
* 
   [!UICONTROL Tipo di grafico]: `Table`

>[!NOTE]
>
>La quantità di 10 per &quot;Numero di ordini con questo coupon&quot; è arbitraria. Puoi usare la quantità più appropriata per questo filtro.

Dopo aver compilato tutti i rapporti, puoi organizzarli nel dashboard come desideri. Il risultato finale potrebbe assomigliare all’immagine nella parte superiore della pagina.

In caso di domande durante la creazione di questa analisi, o se desideri semplicemente coinvolgere il nostro team di servizi professionali, [contattare il supporto](../../guide-overview.md).
