---
title: Generazione di rapporti su un calendario al dettaglio
description: Scopri come impostare la struttura per utilizzare un calendario retail 4-5-4 all’interno del tuo [!DNL MBI] conto.
exl-id: 3754151c-4b0f-4238-87f2-134b8409e32b
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 0%

---

# Generazione di rapporti su un calendario al dettaglio

In questo articolo, mostriamo come impostare la struttura per utilizzare un [Calendario retail 4-5-4](https://nrf.com/resources/4-5-4-calendar) all&#39;interno della [!DNL MBI] conto. Il generatore di report video fornisce intervalli di tempo, intervalli e impostazioni indipendenti incredibilmente flessibili. Il nostro team è anche in grado di aiutarti a cambiare il giorno di inizio della settimana per allinearti con le tue preferenze commerciali. Tuttavia, tutte queste impostazioni funzionano con il calendario mensile tradizionale in vigore.

Poiché molti dei nostri clienti modificano il proprio calendario in modo da utilizzare le date di vendita al dettaglio o di contabilità, i passaggi seguenti illustrano come lavorare con i tuoi dati e creare report utilizzando le date di vendita al dettaglio. Sebbene le istruzioni riportate di seguito facciano riferimento al calendario 4-5-4 Retail, è possibile modificarle per qualsiasi calendario specifico utilizzato dal team, sia che si tratti di un calendario finanziario o personalizzato.

Prima di iniziare, vuoi acquisire familiarità con [File Uploader](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) e assicurati di aver allungato il `.csv` in modo che le date coprano tutti i tuoi dati storici e trasmettano le date nel futuro.

Questa analisi contiene [colonne calcolate avanzate](../data-warehouse-mgr/adv-calc-columns.md).

## Introduzione

È possibile [scaricare](../../assets/454-calendar.csv) a `.csv` versione del calendario retail 4-5-4 per gli anni al dettaglio dal 2014 al 2017. Tieni presente che potrebbe essere necessario regolare questo file in base al calendario della vendita interno e estendere l’intervallo di date per supportare l’intervallo di tempo storico e corrente. Dopo aver scaricato il file, utilizza File Uploader per creare una tabella Retail Calendar (Calendario vendite al dettaglio) nel tuo [!DNL MBI] data warehouse. Se utilizzi una versione inalterata del calendario della vendita al dettaglio 4-5-4, assicurati che la struttura e i tipi di dati dei campi in questa tabella corrispondano ai seguenti elementi:

| Nome colonna | Tipo di dati colonna | Chiave principale |
| --- | --- | --- |
| `Date Retail` | `Date & Time` | `Yes` |
| `Year Retail` | `Whole Number` | `No` |
| `Quarter Retail` | `Whole Number` | `No` |
| `Month Number Retail` | `Whole Number` | `No` |
| `Week Retail` | `Whole Number` | `No` |
| `Month Name Retail` | `Text` (Fino a 255 caratteri) | `No` |
| `Week Number of Month Retail` | `Whole Number` | `No` |

{style=&quot;table-layout:auto&quot;}

## Colonne da creare

* **sales\_order** tabella
   * `INPUT` `created\_at` (aaaa-mm-gg 00:00:00)
      * [!UICONTROL Column type]: – `Same table > Calculation`
      * [!UICONTROL Inputs]: – `created\_at`
      * [!UICONTROL Datatype]: – `Datetime`
      * [!UICONTROL Calculation]: - ` case when A is null then null else to\_char(A, 'YYYY-MM-DD 00:00:00') end`

* **Calendario al dettaglio** tabella di caricamento file
   * **Data corrente**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]: `Date Retail`
      * 
         [!UICONTROL Tipo di dati]: `Datetime`
      * [!UICONTROL Calculation]: `case when A is null then null else to\_char(now(), 'YYYY-MM-DD 00:00:00') end`

         >[!NOTE]
         >
         >La `now()` la funzione precedente è specifica di PostgreSQL. Nonostante la maggior parte [!DNL MBI] i data warehouse sono ospitati su PostgreSQL, alcuni potrebbero essere ospitati su Redshift. Se il calcolo di cui sopra restituisce un errore, potrebbe essere necessario utilizzare la funzione Redshift `getdate()` anziché `now()`.
   * **Anno al dettaglio corrente** (Deve essere creato da analista di supporto)
      * [!UICONTROL Column type]: E`vent Counter`
      * [!UICONTROL Local Key]: `Current date`
      * [!UICONTROL Remote Key]: `Retail calendar.Date Retail`
      * 
         [!UICONTROL Operation]: `Max`
      * [!UICONTROL Operation value]: `Year Retail`
   * **Incluso nell&#39;anno al dettaglio in corso? (Sì/No)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
         [!UICONTROL Tipo di dati]: `String`
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when A = B then 'Yes' else 'No' end`
   * **Incluso nell&#39;anno precedente? (Sì/No)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
         [!UICONTROL Tipo di dati]: String
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when (A = (B-1)) then 'Yes' else 'No' end`


* **sales\_order** tabella
   * **Creato\_at (anno di vendita)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Percorso -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * Seleziona una [!UICONTROL table]: `Retail Calendar`
      * Seleziona una [!UICONTROL column]: `Year Retail`
   * **Creato\_at (settimana di vendita al dettaglio)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Percorso -
         * [!UICONTROL Many]:sales\_order.\[INPUT\] creato\_at (aaaa-mm-gg 00:00:00
         * [!UICONTROL One]:Retail Calendar.Date Reti
      * Seleziona una [!UICONTROL table]: `Retail Calendar`
      * Seleziona una [!UICONTROL column]: `Week Retail`
   * **Creato\_at (mese di vendita al dettaglio)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Percorso
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * Seleziona una [!UICONTROL table]: `Retail Calendar`
      * Seleziona una [!UICONTROL column]: `Month Number Retail`
   * **Includere nell&#39;anno precedente? (Sì/No)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Percorso -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: Retail `Calendar.Date Retail`
      * Seleziona una [!UICONTROL table]: `Retail Calendar`
      * Seleziona una [!UICONTROL column]: `Include in previous retail year? (Yes/No)`
   * **Includi nell&#39;anno di vendita corrente? (Sì/No)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Percorso -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: Retail `Calendar.Date Retail`
      * Seleziona una [!UICONTROL table]: `Retail Calendar`
      * Seleziona una [!UICONTROL column]: `Include in current retail year? (Yes/No)`

## Metriche

Nota: Per questa analisi non sono necessarie nuove metriche. Tuttavia, assicurati di [aggiungi le nuove colonne create nella tabella sales\_order come dimensioni](../data-warehouse-mgr/manage-data-dimensions-metrics.md) per tutte le metriche nella tabella sales\_order prima di continuare con i rapporti.

## Rapporti

* **Ordini settimanali - calendario al dettaglio (anno)**
   * Metrica `A`: `2017`
      * [!UICONTROL Metric]: Numero di ordini
      * [!UICONTROL Filter]:
         * Creato\_at (anno al dettaglio) = 2017
   * Metrica `B`: `2016`
      * [!UICONTROL Metric]: Numero di ordini
      * [!UICONTROL Filter]:
         * Creato\_at (anno al dettaglio) = 2016
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

* **Panoramica del calendario retail (anno al dettaglio corrente per mese)**
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

* **Panoramica del calendario retail (anno di vendita precedente per mese)**
   * Metrica `A`: `Revenue`
      * 
         [!UICONTROL Metric]: `Revenue`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * Metrica `B`: `Orders`
      * [!UICONTROL Metric]: Numero di ordini
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

Quanto sopra descrive come configurare un calendario per la vendita al dettaglio in modo che sia compatibile con qualsiasi metrica creata sul tuo `sales\_order` tabella (ad esempio,`Revenue` e `Orders`), ma puoi anche estenderlo per supportare il calendario della vendita al dettaglio per le metriche create su qualsiasi tabella. L’unico requisito consiste nel fatto che questa tabella dispone di un campo datetime valido che può essere utilizzato per aggiungere alla tabella Retail Calendar (Calendario vendite al dettaglio).

Ad esempio, per visualizzare le metriche a livello di cliente in un calendario di vendita al dettaglio 4-5-4, crea una nuova `Same Table` calcolo `customer\_entity` tabella, simile a `\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)` descritto sopra. Puoi quindi utilizzare questa colonna per riprodurre tutti gli elementi `One to Many` calcoli JOINED\_COLUMN `Created_at (retail year)` e `Include in previous retail year? (Yes/No)` unendo `customer\_entity` della tabella `Retail Calendar` tabella.

Non dimenticare di [aggiungi tutte le nuove colonne come dimensioni alle metriche](../data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.
