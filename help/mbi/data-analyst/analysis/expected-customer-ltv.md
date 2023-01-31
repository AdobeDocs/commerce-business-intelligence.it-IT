---
title: Analisi del valore del ciclo di vita previsto (LTV) per Pro
description: Scopri come impostare un dashboard che ti aiuterà a comprendere la crescita del valore del ciclo di vita del cliente e il valore del ciclo di vita previsto dei clienti.
exl-id: e353b92a-ff3b-466b-b519-4f86d054c0bc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# Analisi del valore del ciclo di vita prevista

In questo articolo, mostriamo come impostare un dashboard che ti aiuterà a comprendere la crescita del valore della vita del cliente e il valore della vita previsto dei tuoi clienti.

![](../../assets/exp-lifetim-value-anyalysis.png)

Questa analisi è disponibile solo per gli account clienti Pro sulla nuova architettura. Se il tuo account ha accesso a `Persistent Views` nella sezione `Manage Data` barra laterale, sei sulla nuova architettura e puoi seguire le istruzioni elencate qui per creare autonomamente questa analisi.

Prima di iniziare, vorrai acquisire familiarità con i nostri [generatore di report per coorte.](../dev-reports/cohort-rpt-bldr.md)

## Colonne calcolate

Colonne da creare nel **ordini** tabella se si utilizza **30 giorni**:

* [!UICONTROL Column name]: `Months between first order and this order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: A = `Seconds between customer's first order date and this order`
* 
   [!UICONTROL Datatype]: `Integer`
* **Definizione:**`case when A is null then null when A <= 0 then '1'::int else (ceil(A)/2629800)::int end`

* [!UICONTROL Column name]: `Months since order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: A = `created_at`
* 
   [!UICONTROL Datatype]: `Integer`
* Definizione: `case when created_at is null then null else (ceil((extract(epoch from current_timestamp) - extract(epoch from created_at))/2629800))::int end`

Colonne da creare nel **`orders`** tabella se si utilizza **calendario** mesi:

* [!UICONTROL Column name]: `Calendar months between first order and this order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column inputs]:
   * `A` = `created_at`
   * `B` = `Customer's first order date`

* 
   [!UICONTROL Datatype]: `Integer`
* Definizione: `case when (A::date is null) or (B::date is null) then null else ((date_part('year',A::date) - date_part('year',B::date))*12 + date_part('month',A::date) - date_part('month',B::date))::int end`

* [!UICONTROL Column name]: `Calendar months since order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: `A` = `created_at`
* 
   [!UICONTROL Datatype]: `Integer`
* **Definizione:**`case when A is null then null else ((date_part('year',current_timestamp::date) - date_part('year',A::date))*12 + date_part('month',current_timestamp::date) - date_part('month',A::date))::int end`

* [!UICONTROL Column name]: `Is in current month? (Yes/No)`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: A = `created_at`
* 
   [!UICONTROL Datatype]: `String`
* Definizione: `case when A is null then null when (date_trunc('month', current_timestamp::date))::varchar = (date_trunc('month', A::date))::varchar then 'Yes' else 'No' end`

## Metriche

### Istruzioni per la metrica

Metriche da creare

* **Clienti distinti per data del primo ordine**
   * Se abiliti gli ordini degli ospiti, utilizza `customer_email`

* In **`orders`** tabella
* Questa metrica esegue un **Conteggio valori distinti**
* Sulla **`customer_id`** column
* Ordinato dal **`Customer's first order date`** timestamp

>[!NOTE]
>
>Assicurati di [aggiungi tutte le nuove colonne come dimensioni alle metriche](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.

## Rapporti

### Istruzioni per i rapporti

**Entrate previste per cliente per mese**

* Metrica `A`: `Revenue (hide)`
   * `Calendar months between first order and this order` `<= X` (Scegli un numero ragionevole per X, ad esempio, 24 mesi)
   * `Is in current month?` = `No`

* 
   [!UICONTROL Metric]: `Revenue`
* [!UICONTROL Filter]:

* Metrica `B`: `All time customers (hide)`
   * `Is in current month?` = `No`

* [!UICONTROL Metric]: `New customers by first order date`
* [!UICONTROL Filter]:

* Metrica `C`: `All time customers by month since first order (hide)`
   * `Calendar months since order` `<= X`
   * `Is in current month?` = `No`

* [!UICONTROL Metric]: `New customers by first order date`
* [!UICONTROL Filter]:

* [!UICONTROL Formula]: `Expected revenue`
* [!UICONTROL Formula]: `A / (B - C)`
* 

   [!UICONTROL Format]: `Currency`

Altri dettagli del grafico

* [!UICONTROL Time period]: `All time`
* Intervallo di tempo: `None`
* [!UICONTROL Group by]: `Calendar months between first order and this order` - mostra tutto
* Modificare la `group by` per `All time customers` da Indipendente utilizzando l’icona a forma di matita accanto a `group by`
* Modifica le `Show top/bottom` campi come segue:
   * [!UICONTROL Revenue]: `Top 24 sorted by Calendar months between first order and this order`
   * [!UICONTROL All time customers]: `Top 24 sorted by All time customers`
   * [!UICONTROL All time customers by month since first order]: `Top 24 sorted by All time customers by month since first order`

**Entrate medie al mese per coorte**

* Metrica `A`: `Revenue`
* 
   [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Average value per cohort member`

**Ricavi medi cumulativi mensili per coorte**

* Metrica `A`: `Revenue`
* 
   [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Cumulative average value per cohort member`

Dopo aver compilato tutti i rapporti, puoi organizzarli nel dashboard come desideri. Il risultato finale potrebbe assomigliare all’immagine nella parte superiore della pagina.

In caso di domande durante la creazione di questa analisi, o se desideri semplicemente coinvolgere il nostro team di servizi professionali, [contattare il supporto](../../guide-overview.md).
