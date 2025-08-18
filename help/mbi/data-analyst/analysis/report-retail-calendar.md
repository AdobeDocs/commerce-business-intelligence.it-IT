---
title: Generazione di rapporti su un calendario di vendita al dettaglio
description: Scopri come impostare la struttura per utilizzare un calendario 4-5-4 per la vendita al dettaglio nel tuo account  [!DNL Commerce Intelligence] .
exl-id: 3754151c-4b0f-4238-87f2-134b8409e32b
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---

# Generazione di rapporti su un calendario di vendita al dettaglio

In questo argomento viene illustrato come impostare la struttura per l&#39;utilizzo di un calendario [4-5-4 per la vendita al dettaglio](https://nrf.com/resources/4-5-4-calendar) nell&#39;account [!DNL Adobe Commerce Intelligence]. Il generatore di rapporti visivi fornisce intervalli di tempo, intervalli e impostazioni indipendenti incredibilmente flessibili. Tuttavia, tutte queste impostazioni funzionano con il calendario mensile tradizionale attivo.

Poiché molti clienti modificano il calendario per utilizzare date di vendita al dettaglio o contabili, i passaggi seguenti illustrano come lavorare con i dati e creare rapporti utilizzando date di vendita al dettaglio. Anche se le istruzioni seguenti fanno riferimento al calendario 4-5-4 Retail, è possibile modificarle per qualsiasi calendario specifico utilizzato dal team, che si tratti di calendario finanziario o semplicemente di un intervallo di tempo personalizzato.

Prima di iniziare, è necessario rivedere [lo strumento di caricamento file](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) e assicurarsi di aver allungato il file `.csv`. In questo modo le date coprono tutti i dati storici e li spingono nel futuro.

Questa analisi contiene [colonne calcolate avanzate](../data-warehouse-mgr/adv-calc-columns.md).

## Guida introduttiva

Puoi [scaricare](../../assets/454-calendar.csv) una versione `.csv` del calendario 4-5-4 per la vendita al dettaglio dal 2014 al 2017. Potrebbe essere necessario regolare questo file in base al calendario interno della vendita al dettaglio ed estendere l’intervallo di date per supportare l’intervallo di tempo storico e corrente. Dopo aver scaricato il file, utilizzare lo strumento Caricamento file per creare una tabella Calendario vendita al dettaglio nel Data Warehouse [!DNL Commerce Intelligence]. Se utilizzi una versione inalterata del calendario 4-5-4 per la vendita al dettaglio, assicurati che la struttura e i tipi di dati dei campi in questa tabella corrispondano ai seguenti:

| Nome colonna | Tipo di dati colonna | Chiave primaria |
| --- | --- | --- |
| `Date Retail` | `Date & Time` | `Yes` |
| `Year Retail` | `Whole Number` | `No` |
| `Quarter Retail` | `Whole Number` | `No` |
| `Month Number Retail` | `Whole Number` | `No` |
| `Week Retail` | `Whole Number` | `No` |
| `Month Name Retail` | `Text` (fino a 255 caratteri) | `No` |
| `Week Number of Month Retail` | `Whole Number` | `No` |

{style="table-layout:auto"}

## Colonne da creare

* Tabella **sales\_order**
   * `INPUT` `created\_at` (aaaa-mm-gg 00:00:00)
      * [!UICONTROL Column type]: - `Same table > Calculation`
      * [!UICONTROL Inputs]: - `created\_at`
      * [!UICONTROL Datatype]: - `Datetime`
      * [!UICONTROL Calculation]: - ` case when A is null then null else to\_char(A, 'YYYY-MM-DD 00:00:00') end`

* **Tabella caricamento file calendario vendita al dettaglio**
   * **Data corrente**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]: `Date Retail`
      * &#x200B;
        [!UICONTROL Datatype]: `Datetime`
      * [!UICONTROL Calculation]: `case when A is null then null else to\_char(now(), 'YYYY-MM-DD 00:00:00') end`

        >[!NOTE]
        >
        >La funzione `now()` sopra è specifica per PostgreSQL. Sebbene la maggior parte dei data warehouse [!DNL Commerce Intelligence] sia ospitata su PostgreSQL, alcuni potrebbero essere ospitati su Redshift. Se il calcolo precedente restituisce un errore, potrebbe essere necessario utilizzare la funzione Redshift `getdate()` anziché `now()`.

   * **Anno corrente** (deve essere creato dall&#39;analista del supporto tecnico)
      * [!UICONTROL Column type]: E`vent Counter`
      * [!UICONTROL Local Key]: `Current date`
      * [!UICONTROL Remote Key]: `Retail calendar.Date Retail`
      * &#x200B;
        [!UICONTROL Operation]: `Max`
      * [!UICONTROL Operation value]: `Year Retail`
   * **Incluso nell&#39;anno corrente? (Sì/No)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * &#x200B;
        [!UICONTROL Datatype]: `String`
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when A = B then 'Yes' else 'No' end`
   * **Incluso nell&#39;anno di vendita precedente? (Sì/No)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * &#x200B;
        [!UICONTROL Datatype]: String
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when (A = (B-1)) then 'Yes' else 'No' end`

* Tabella **sales\_order**
   * **Creato\_at (anno vendita al dettaglio)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Percorso -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * Seleziona [!UICONTROL table]: `Retail Calendar`
      * Seleziona [!UICONTROL column]: `Year Retail`
   * **Creato\_alle (settimana vendita al dettaglio)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Percorso -
         * [!UICONTROL Many]: sales\_order.\[INPUT\] creato\_at (aaaa-mm-gg 00:00:00
         * [!UICONTROL One]: Retail Calendar.Date Retail
      * Seleziona [!UICONTROL table]: `Retail Calendar`
      * Seleziona [!UICONTROL column]: `Week Retail`
   * **Creato\_alle (mese vendita al dettaglio)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Percorso
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * Seleziona [!UICONTROL table]: `Retail Calendar`
      * Seleziona [!UICONTROL column]: `Month Number Retail`
   * **Includere nell&#39;anno di vendita al dettaglio precedente? (Sì/No)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Percorso -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: vendita al dettaglio `Calendar.Date Retail`
      * Seleziona [!UICONTROL table]: `Retail Calendar`
      * Seleziona [!UICONTROL column]: `Include in previous retail year? (Yes/No)`
   * **Includere nell&#39;anno di vendita al dettaglio corrente? (Sì/No)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Percorso -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: vendita al dettaglio `Calendar.Date Retail`
      * Seleziona [!UICONTROL table]: `Retail Calendar`
      * Seleziona [!UICONTROL column]: `Include in current retail year? (Yes/No)`

## Metriche

Nota: non sono necessarie nuove metriche per questa analisi. Tuttavia, assicurati di [aggiungere le nuove colonne create nella tabella sales\_order come dimensioni](../data-warehouse-mgr/manage-data-dimensions-metrics.md) per tutte le metriche nella tabella sales\_order prima di continuare con i rapporti.

## Rapporti

* **Ordini settimanali - Calendario vendite al dettaglio (YoY)**
   * Metrica `A`: `2017`
      * [!UICONTROL Metric]: numero di ordini
      * [!UICONTROL Filter]:
         * Creato\_at (anno vendita al dettaglio) = 2017
   * Metrica `B`: `2016`
      * [!UICONTROL Metric]: numero di ordini
      * [!UICONTROL Filter]:
         * Creato\_at (anno vendita al dettaglio) = 2016
   * Metrica `C`: `2015`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * `Created\_at (retail Year) = 2015`
   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Interval]: `None`
   * &#x200B;
     [!UICONTROL Group by]: `Created\_at` (retail week)
   * &#x200B;
     [!UICONTROL Chart type]: `Line`
      * Disattiva `multiple Y-axes`

* **Panoramica calendario vendite al dettaglio (anno vendita al dettaglio corrente per mese)**
   * Metrica `A`: `Revenue`
      * &#x200B;
        [!UICONTROL Metric]: `Revenue`
      * [!UICONTROL Filter]:
         * &#x200B;
           [!UICONTROL Include current retail year?]: `Yes`
   * Metrica `B`: `Orders`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * &#x200B;
           [!UICONTROL Include current retail year?]: `Yes`
   * Metrica `C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * &#x200B;
           [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Interval]: `None`
   * &#x200B;
     [!UICONTROL Group by]: `Created\_at` (retail month)
   * &#x200B;
     [!UICONTROL Chart type]: `Line`

* **Panoramica calendario vendite al dettaglio (anno precedente vendite al dettaglio per mese)**
   * Metrica `A`: `Revenue`
      * &#x200B;
        [!UICONTROL Metric]: `Revenue`
      * [!UICONTROL Filter]:
         * &#x200B;
           [!UICONTROL Include current retail year?]: `Yes`
   * Metrica `B`: `Orders`
      * [!UICONTROL Metric]: numero di ordini
      * [!UICONTROL Filter]:
         * &#x200B;
           [!UICONTROL Include current retail year?]: `Yes`
   * Metrica `C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * &#x200B;
           [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Interval]: `None`
   * &#x200B;
     [!UICONTROL Group by]: `Created\_at` (retail month)
   * &#x200B;
     [!UICONTROL Chart type]: `Line`

## Passaggi successivi

Quanto sopra descrive come configurare un calendario di vendita al dettaglio in modo che sia compatibile con qualsiasi metrica generata nella tabella `sales\_order` (ad esempio `Revenue` o `Orders`). Puoi anche estendere questo periodo per supportare il calendario delle vendite al dettaglio per le metriche basate su qualsiasi tabella. L&#39;unico requisito è che questa tabella abbia un campo datetime valido che possa essere utilizzato per il join alla tabella Retail Calendar (Calendario vendite al dettaglio).

Ad esempio, per visualizzare le metriche a livello di cliente in un calendario 4-5-4 per la vendita al dettaglio, creare un calcolo `Same Table` nella tabella `customer\_entity`, simile a `\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)` descritto in precedenza. È quindi possibile utilizzare questa colonna per riprodurre i calcoli `One to Many` JOIN\_COLUMN (come `Created_at (retail year)`) e `Include in previous retail year? (Yes/No)` unendo la tabella `customer\_entity` alla tabella `Retail Calendar`.

Non dimenticare di [aggiungere tutte le nuove colonne come dimensioni alle metriche](../data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.
