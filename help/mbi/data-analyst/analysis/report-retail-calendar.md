---
title: Generazione di rapporti su un calendario di vendita al dettaglio
description: Scopri come impostare la struttura per utilizzare un calendario 4-5-4 per la vendita al dettaglio all’interno del [!DNL Commerce Intelligence] account.
exl-id: 3754151c-4b0f-4238-87f2-134b8409e32b
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---

# Generazione di rapporti su un calendario di vendita al dettaglio

In questo argomento viene illustrato come impostare la struttura per l&#39;utilizzo di [4-5-4 calendario vendite al dettaglio](https://nrf.com/resources/4-5-4-calendar) all&#39;interno del [!DNL Adobe Commerce Intelligence] account. Il generatore di rapporti visivi fornisce intervalli di tempo, intervalli e impostazioni indipendenti incredibilmente flessibili. Tuttavia, tutte queste impostazioni funzionano con il calendario mensile tradizionale attivo.

Poiché molti clienti modificano il calendario per utilizzare date di vendita al dettaglio o contabili, i passaggi seguenti illustrano come lavorare con i dati e creare rapporti utilizzando date di vendita al dettaglio. Anche se le istruzioni seguenti fanno riferimento al calendario 4-5-4 Retail, è possibile modificarle per qualsiasi calendario specifico utilizzato dal team, che si tratti di calendario finanziario o semplicemente di un intervallo di tempo personalizzato.

Prima di iniziare, rivedi [Caricamento file](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) e assicurarsi di aver allungato la `.csv` file. In questo modo le date coprono tutti i dati storici e li spingono nel futuro.

Questa analisi contiene [colonne calcolate avanzate](../data-warehouse-mgr/adv-calc-columns.md).

## Guida introduttiva

È possibile [scaricare](../../assets/454-calendar.csv) a `.csv` versione del calendario 4-5-4 delle vendite al dettaglio per gli anni dal 2014 al 2017. Potrebbe essere necessario regolare questo file in base al calendario interno della vendita al dettaglio ed estendere l’intervallo di date per supportare l’intervallo di tempo storico e corrente. Dopo aver scaricato il file, utilizza lo strumento di caricamento file per creare una tabella del calendario di vendita al dettaglio nel tuo [!DNL Commerce Intelligence] Data Warehouse. Se utilizzi una versione inalterata del calendario 4-5-4 per la vendita al dettaglio, assicurati che la struttura e i tipi di dati dei campi in questa tabella corrispondano ai seguenti:

| Nome colonna | Tipo di dati colonna | Chiave primaria |
| --- | --- | --- |
| `Date Retail` | `Date & Time` | `Yes` |
| `Year Retail` | `Whole Number` | `No` |
| `Quarter Retail` | `Whole Number` | `No` |
| `Month Number Retail` | `Whole Number` | `No` |
| `Week Retail` | `Whole Number` | `No` |
| `Month Name Retail` | `Text` (Fino a 255 caratteri) | `No` |
| `Week Number of Month Retail` | `Whole Number` | `No` |

{style="table-layout:auto"}

## Colonne da creare

* **sales\_order** tabella
   * `INPUT` `created\_at` (aaaa-mm-gg 00:00:00)
      * [!UICONTROL Column type]: – `Same table > Calculation`
      * [!UICONTROL Inputs]: – `created\_at`
      * [!UICONTROL Datatype]: – `Datetime`
      * [!UICONTROL Calculation]: - ` case when A is null then null else to\_char(A, 'YYYY-MM-DD 00:00:00') end`

* **Calendario vendita al dettaglio** tabella di caricamento file
   * **Data corrente**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]: `Date Retail`
      * 
        [!UICONTROL Datatype]: `Datetime`
      * [!UICONTROL Calculation]: `case when A is null then null else to\_char(now(), 'YYYY-MM-DD 00:00:00') end`

        >[!NOTE]
        >
        >Il `now()` La funzione precedente è specifica di PostgreSQL. Anche se la maggior parte [!DNL Commerce Intelligence] I data warehouse sono ospitati su PostgreSQL, alcuni possono essere ospitati su Redshift. Se il calcolo precedente restituisce un errore, potrebbe essere necessario utilizzare la funzione Redshift `getdate()` invece di `now()`.

   * **Anno corrente di vendita al dettaglio** (Deve essere creato dall’analista del supporto tecnico)
      * [!UICONTROL Column type]: E`vent Counter`
      * [!UICONTROL Local Key]: `Current date`
      * [!UICONTROL Remote Key]: `Retail calendar.Date Retail`
      * 
        [!UICONTROL Operation]: `Max`
      * [!UICONTROL Operation value]: `Year Retail`
   * **Incluso nell&#39;anno corrente di vendita al dettaglio? (Sì/No)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
        [!UICONTROL Datatype]: `String`
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when A = B then 'Yes' else 'No' end`
   * **Incluso nell&#39;anno precedente? (Sì/No)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
        [!UICONTROL Datatype]: String
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when (A = (B-1)) then 'Yes' else 'No' end`

* **sales\_order** tabella
   * **Creato\_at (anno vendita al dettaglio)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Percorso -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * Seleziona un [!UICONTROL table]: `Retail Calendar`
      * Seleziona un [!UICONTROL column]: `Year Retail`
   * **Creato\_at (settimana vendita al dettaglio)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Percorso -
         * [!UICONTROL Many]: sales\_order.\[INPUT\] creato\_at (aaaa-mm-gg 00:00:00
         * [!UICONTROL One]: Retail Calendar.Date Retail
      * Seleziona un [!UICONTROL table]: `Retail Calendar`
      * Seleziona un [!UICONTROL column]: `Week Retail`
   * **Creato\_at (mese vendita al dettaglio)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Percorso
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * Seleziona un [!UICONTROL table]: `Retail Calendar`
      * Seleziona un [!UICONTROL column]: `Month Number Retail`
   * **Includere nell&#39;anno di vendita al dettaglio precedente? (Sì/No)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Percorso -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: vendita al dettaglio `Calendar.Date Retail`
      * Seleziona un [!UICONTROL table]: `Retail Calendar`
      * Seleziona un [!UICONTROL column]: `Include in previous retail year? (Yes/No)`
   * **Includere nell&#39;anno di vendita al dettaglio corrente? (Sì/No)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Percorso -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: vendita al dettaglio `Calendar.Date Retail`
      * Seleziona un [!UICONTROL table]: `Retail Calendar`
      * Seleziona un [!UICONTROL column]: `Include in current retail year? (Yes/No)`

## Metriche

Nota: non sono necessarie nuove metriche per questa analisi. Tuttavia, assicurati di [aggiungi le nuove colonne create nella tabella sales\_order come dimensioni](../data-warehouse-mgr/manage-data-dimensions-metrics.md) per tutte le metriche della tabella sales\_order prima di continuare con i rapporti.

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
   * 
     [!UICONTROL Interval]: `None`
   * 
     [!UICONTROL Group by]: `Created\_at` (retail week)
   * 
     [!UICONTROL Chart type]: `Line`
      * Disattiva `multiple Y-axes`

* **Panoramica calendario vendita al dettaglio (anno vendita al dettaglio corrente per mese)**
   * Metrica `A`: `Revenue`
      * 
        [!UICONTROL Metric]: `Revenue`
      * [!UICONTROL Filter]:
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * Metrica `B`: `Orders`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * Metrica `C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * 
     [!UICONTROL Group by]: `Created\_at` (retail month)
   * 
     [!UICONTROL Chart type]: `Line`

* **Panoramica calendario vendite al dettaglio (anno precedente vendite al dettaglio per mese)**
   * Metrica `A`: `Revenue`
      * 
        [!UICONTROL Metric]: `Revenue`
      * [!UICONTROL Filter]:
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * Metrica `B`: `Orders`
      * [!UICONTROL Metric]: numero di ordini
      * [!UICONTROL Filter]:
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * Metrica `C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * 
     [!UICONTROL Group by]: `Created\_at` (retail month)
   * 
     [!UICONTROL Chart type]: `Line`

## Passaggi successivi

Quanto riportato sopra descrive come configurare un calendario per la vendita al dettaglio in modo che sia compatibile con qualsiasi metrica generata sul `sales\_order` tabella (ad esempio `Revenue` o `Orders`). Puoi anche estendere questo periodo per supportare il calendario delle vendite al dettaglio per le metriche basate su qualsiasi tabella. L&#39;unico requisito è che questa tabella abbia un campo datetime valido che possa essere utilizzato per il join alla tabella Retail Calendar (Calendario vendite al dettaglio).

Ad esempio, per visualizzare le metriche a livello di cliente in un calendario 4-5-4 per la vendita al dettaglio, crea un `Same Table` calcolo in `customer\_entity` tabella, simile a `\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)` descritto in precedenza. È quindi possibile utilizzare questa colonna per riprodurre `One to Many` Calcoli JOIN\_COLUMN (come `Created_at (retail year)`) e `Include in previous retail year? (Yes/No)` unendo `customer\_entity` tabella al `Retail Calendar` tabella.

Non dimenticare di [aggiungere tutte le nuove colonne come dimensioni alle metriche](../data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.
