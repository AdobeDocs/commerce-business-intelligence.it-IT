---
title: Formule
description: Scopri come utilizzare le formule.
exl-id: b6432d93-739f-410c-b732-e09a278f8dae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# Formule

Una formula combina più metriche e logica matematica per rispondere a una domanda. Ad esempio, quanto dei ricavi per prodotto durante le feste è stato generato dai nuovi clienti?

![Vendite festive nel dashboard](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## Passaggio 1: creare il rapporto di base

1. Nel menu, scegliere `Report Builder`.

1. Fare clic su **[!UICONTROL Add Metric]** e scegliere la prima metrica per il report.

   Per questo esempio, viene utilizzata la metrica `Revenue by products ordered`.

1. Fare di nuovo clic su **[!UICONTROL Add Metric]** e scegliere la seconda metrica per il report.

   Per questo esempio, viene utilizzata la metrica `New Customers`.

1. Nella barra laterale, fare clic su **[!UICONTROL Details]** per visualizzare informazioni su ciascuna metrica.

   ![Ricavi per prodotti ordinati](../../assets/magento-bi-report-builder-revenue-by-products.png)

1. Nella barra laterale, fai clic sul nome di ciascuna metrica per aprire la pagina delle impostazioni in una nuova scheda del browser. Scorri verso il basso per visualizzare ogni componente della metrica, incluse la query della metrica, il filtro e le dimensioni.

   ![Impostazioni metriche](../../assets/magento-bi-report-builder-revenue-by-products-metric-detail.png)

1. Per tornare al report, fai clic sulla scheda precedente del browser.

1. Nel grafico, posiziona il cursore del mouse su alcune coordinate su ciascuna linea per visualizzare le quantità associate a ciascuna metrica.

## Passaggio 2: aggiungere una formula

1. Nella parte superiore della barra laterale fare clic su **[!UICONTROL Add Formula]**.

   La casella della formula mostra le metriche come input disponibili `A` e `B` e include una casella di input in cui è possibile immettere la formula.

   Effettua le seguenti operazioni:

   * Nella casella di input `Enter your Formula` immettere `A/B`.

     Questo divide i ricavi per prodotti ordinati per il numero di nuovi clienti.

   * Imposta `Select format` su `123Number`.

   * Nella barra laterale sostituire `Untitled` con un nome per la formula.

   ![Impostazioni formula](../../assets/magento-bi-report-builder-revenue-by-products-add-formula-detail.png)

1. Al termine, fare clic su **[!UICONTROL Apply]**.

   Il report ora include una nuova riga per la formula, `New Customer Revenue`, e la barra laterale mostra l&#39;importo totale dei ricavi generati dai nuovi clienti.

   ![Report con formula](../../assets/magento-bi-report-builder-revenue-by-products-formula-report.png)

## Passaggio 3: aggiungere un intervallo di date

1. Fare clic su **[!UICONTROL Date Range]** nell&#39;angolo superiore destro.

1. Nella scheda `Fixed Date Range` eseguire le operazioni seguenti:

   * Scegliere l&#39;intervallo di date nei calendari.

     In questo esempio, la stagione festiva va da `November 1` a `December 31`.

   * In `Select Time Interval` scegliere `Day`.

     ![Intervallo date fisso](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range.png)

   * Al termine, fare clic su **[!UICONTROL Apply]**.

   Il rapporto è ora limitato al periodo festivo, con un punto dati per ogni giorno.

   ![Intervallo date fisso](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range-report.png)

## Passaggio 4: salvare il rapporto

In questo passaggio il rapporto verrà salvato come grafico e anche come tabella.

1. Fare clic su `Untitled Report` nella parte superiore della pagina e immettere un titolo descrittivo. In questo esempio, il titolo del report è `2017 Holiday Sales`.

   Quindi, effettua le seguenti operazioni:

   * Nell&#39;angolo superiore destro fare clic su **[!UICONTROL Save]**.

   * Per `Type`, accettare l&#39;impostazione predefinita `Chart`.

   * Scegliere `Dashboard` in cui il report deve essere disponibile.

   * Fare clic su **[!UICONTROL Save to Dashboard]**.

1. Fai clic sul titolo del rapporto e modifica il nome. In questo esempio, il titolo del report è stato modificato in `2017 Holiday Sales Data`.

   Quindi, effettua le seguenti operazioni:

   * Nell&#39;angolo superiore destro fare clic su **[!UICONTROL Save a Copy]**.

   * Imposta `Type` su `Table`.

   * Scegliere `Dashboard` in cui il report deve essere disponibile.

   * Fare clic su **[!UICONTROL Save a Copy to Dashboard]**.

1. Per visualizzare i rapporti nel dashboard, eseguire una delle operazioni seguenti:

   * Fare clic su **[!UICONTROL Go to Dashboard]** nel messaggio nella parte superiore della pagina.

   * Nel menu, scegliere **[!UICONTROL Dashboards]**. Fate clic sul nome del dashboard corrente per visualizzare l&#39;elenco. Quindi, fai clic sul nome della dashboard in cui è stato salvato il rapporto.
