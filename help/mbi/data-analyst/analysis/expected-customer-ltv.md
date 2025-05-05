---
title: Analisi del valore del ciclo di vita previsto (LTV) per Pro
description: Scopri come impostare una dashboard che ti aiuti a comprendere la crescita del valore del ciclo di vita del cliente e il valore atteso del ciclo di vita dei tuoi clienti.
exl-id: e353b92a-ff3b-466b-b519-4f86d054c0bc
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Analisi del valore del ciclo di vita previsto

In questo argomento viene illustrato come impostare una dashboard che consenta di comprendere la crescita del valore del ciclo di vita del cliente e il valore atteso del ciclo di vita dei clienti.

![](../../assets/exp-lifetim-value-anyalysis.png)

Questa analisi è disponibile solo per gli account Pro sulla nuova architettura. Se il tuo account ha accesso alla funzionalità `Persistent Views` nella barra laterale `Manage Data`, ti trovi nella nuova architettura e puoi seguire le istruzioni elencate qui per creare autonomamente questa analisi.

Prima di iniziare, acquisisci familiarità con [Report Builder coorte.](../dev-reports/cohort-rpt-bldr.md)

## Colonne calcolate

Colonne da creare nella tabella **orders** se si utilizzano **mesi di 30 giorni**:

* [!UICONTROL Column name]: `Months between first order and this order`
* [!UICONTROL Column type]: `Same Table`
* &#x200B;
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: A = `Seconds between customer's first order date and this order`
* &#x200B;
  [!UICONTROL Datatype]: `Integer`
* **Definizione:**`case when A is null then null when A <= 0 then '1'::int else (ceil(A)/2629800)::int end`

* [!UICONTROL Column name]: `Months since order`
* [!UICONTROL Column type]: `Same Table`
* &#x200B;
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: A = `created_at`
* &#x200B;
  [!UICONTROL Datatype]: `Integer`
* Definizione: `case when created_at is null then null else (ceil((extract(epoch from current_timestamp) - extract(epoch from created_at))/2629800))::int end`

Colonne da creare nella tabella **`orders`** se si utilizza **calendario** mesi:

* [!UICONTROL Column name]: `Calendar months between first order and this order`
* [!UICONTROL Column type]: `Same Table`
* &#x200B;
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column inputs]:
   * `A` = `created_at`
   * `B` = `Customer's first order date`

* &#x200B;
  [!UICONTROL Datatype]: `Integer`
* Definizione: `case when (A::date is null) or (B::date is null) then null else ((date_part('year',A::date) - date_part('year',B::date))*12 + date_part('month',A::date) - date_part('month',B::date))::int end`

* [!UICONTROL Column name]: `Calendar months since order`
* [!UICONTROL Column type]: `Same Table`
* &#x200B;
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: `A` = `created_at`
* &#x200B;
  [!UICONTROL Datatype]: `Integer`
* **Definizione:**`case when A is null then null else ((date_part('year',current_timestamp::date) - date_part('year',A::date))*12 + date_part('month',current_timestamp::date) - date_part('month',A::date))::int end`

* [!UICONTROL Column name]: `Is in current month? (Yes/No)`
* [!UICONTROL Column type]: `Same Table`
* &#x200B;
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: A = `created_at`
* &#x200B;
  [!UICONTROL Datatype]: `String`
* Definizione: `case when A is null then null when (date_trunc('month', current_timestamp::date))::varchar = (date_trunc('month', A::date))::varchar then 'Yes' else 'No' end`

## Metriche

### Istruzioni sulla metrica

Metriche da creare

* **Clienti distinti per data primo ordine**
   * Se si abilitano gli ordini degli ospiti, utilizzare `customer_email`

* Nella tabella **`orders`**
* Questa metrica esegue un **conteggio valori distinti**
* Nella colonna **`customer_id`**
* Ordinato per la marca temporale **`Customer's first order date`**

>[!NOTE]
>
>Assicurati di [aggiungere tutte le nuove colonne come dimensioni alle metriche](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.

## Rapporti

### Istruzioni per il rapporto

**Ricavi previsti per cliente per mese**

* Metrica `A`: `Revenue (hide)`
   * `Calendar months between first order and this order` `<= X` (Scegli un numero ragionevole per X, ad esempio, 24 mesi)
   * `Is in current month?` = `No`

* &#x200B;
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
* &#x200B;
  [!UICONTROL Format]: `Currency`

Altri dettagli grafico

* [!UICONTROL Time period]: `All time`
* Intervallo di tempo: `None`
* [!UICONTROL Group by]: `Calendar months between first order and this order` - mostra tutto
* Cambia `group by` per la metrica `All time customers` in Indipendente utilizzando l&#39;icona a forma di matita accanto a `group by`
* Modificare i campi `Show top/bottom` come segue:
   * [!UICONTROL Revenue]: `Top 24 sorted by Calendar months between first order and this order`
   * [!UICONTROL All time customers]: `Top 24 sorted by All time customers`
   * [!UICONTROL All time customers by month since first order]: `Top 24 sorted by All time customers by month since first order`

**Ricavi medi al mese per coorte**

* Metrica `A`: `Revenue`
* &#x200B;
  [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Average value per cohort member`

**Ricavi medi cumulati al mese per coorte**

* Metrica `A`: `Revenue`
* &#x200B;
  [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Cumulative average value per cohort member`

Dopo aver compilato tutti i rapporti, puoi organizzarli nel dashboard come desideri. Il risultato potrebbe essere simile all’immagine nella parte superiore della pagina.

Per qualsiasi domanda durante la creazione di questa analisi, o semplicemente per coinvolgere il team Professional Services, [contatta il supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
