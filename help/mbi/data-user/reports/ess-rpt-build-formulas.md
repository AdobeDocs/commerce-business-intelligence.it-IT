---
title: Formule
description: Scopri come utilizzare le formule.
exl-id: b6432d93-739f-410c-b732-e09a278f8dae
source-git-commit: df81d2b036d00cd53274ec1ae22031dbf06cc948
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# Formule

Una formula combina più metriche e logica matematica per rispondere a una domanda. Ad esempio, quanto dei ricavi per prodotto durante le feste è stato generato dai nuovi clienti?

![Vendite festive nel dashboard](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## Passaggio 1: creare il rapporto di base

1. Nel menu, scegli `Report Builder`.

1. Clic **[!UICONTROL Add Metric]** e scegli la prima metrica per il rapporto.

   Per questo esempio, il `Revenue by products ordered` viene utilizzata la metrica.

1. Clic **[!UICONTROL Add Metric]** e scegli la seconda metrica per il rapporto.

   Per questo esempio, il `New Customers` viene utilizzata la metrica.

1. Nella barra laterale, fai clic su **[!UICONTROL Details]** per visualizzare informazioni su ciascuna metrica.

   ![Ricavi per prodotti ordinati](../../assets/magento-bi-report-builder-revenue-by-products.png)

1. Nella barra laterale, fai clic sul nome di ciascuna metrica per aprire la pagina delle impostazioni in una nuova scheda del browser. Scorri verso il basso per visualizzare ogni componente della metrica, incluse la query della metrica, il filtro e le dimensioni.

   ![Impostazioni delle metriche](../../assets/magento-bi-report-builder-revenue-by-products-metric-detail.png)

1. Per tornare al report, fai clic sulla scheda precedente del browser.

1. Nel grafico, posiziona il cursore del mouse su alcune coordinate su ciascuna linea per visualizzare le quantità associate a ciascuna metrica.

## Passaggio 2: aggiungere una formula

1. Nella parte superiore della barra laterale, fai clic su **[!UICONTROL Add Formula]**.

   La casella della formula mostra le metriche come input disponibili `A` e `B`e include una casella di input in cui è possibile immettere la formula.

   Effettua le seguenti operazioni:

   * In `Enter your Formula` casella di input, immetti `A/B`.

      Questo divide i ricavi per prodotti ordinati per il numero di nuovi clienti.

   * Imposta `Select format` a `123Number`.

   * Nella barra laterale, sostituisci `Untitled` con un nome per la formula.

   ![Impostazioni formula](../../assets/magento-bi-report-builder-revenue-by-products-add-formula-detail.png)

1. Al termine, fai clic su **[!UICONTROL Apply]**.

   Il rapporto ora contiene una nuova riga per la formula, `New Customer Revenue`e la barra laterale mostra l’importo totale dei ricavi generati dai nuovi clienti.

   ![Rapporto con formula](../../assets/magento-bi-report-builder-revenue-by-products-formula-report.png)

## Passaggio 3: aggiungere un intervallo di date

1. Clic **[!UICONTROL Date Range]** nell’angolo superiore destro.

1. Il giorno `Fixed Date Range` , eseguire le operazioni seguenti:

   * Scegliere l&#39;intervallo di date nei calendari.

      Per questo esempio, la stagione festiva è da `November 1` da a `December 31`.

   * Sotto `Select Time Interval`, scegli `Day`.

      ![Intervallo date fisso](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range.png)

   * Al termine, fai clic su **[!UICONTROL Apply]**.

   Il rapporto è ora limitato al periodo festivo, con un punto dati per ogni giorno.

   ![Intervallo date fisso](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range-report.png)

## Passaggio 4: salvare il rapporto

In questo passaggio il rapporto verrà salvato come grafico e anche come tabella.

1. Clic `Untitled Report` nella parte superiore della pagina e inserisci un titolo descrittivo. In questo esempio, il titolo del rapporto è `2017 Holiday Sales`.

   Quindi, effettua le seguenti operazioni:

   * Nell’angolo superiore destro, fai clic su **[!UICONTROL Save]**.

   * Per `Type`, accetta il valore predefinito `Chart` impostazione.

   * Scegli la `Dashboard` dove la relazione deve essere disponibile.

   * Clic **[!UICONTROL Save to Dashboard]**.

1. Fai clic sul titolo del rapporto e modifica il nome. In questo esempio, il titolo del rapporto viene modificato in `2017 Holiday Sales Data`.

   Quindi, effettua le seguenti operazioni:

   * Nell’angolo superiore destro, fai clic su **[!UICONTROL Save a Copy]**.

   * Imposta `Type` a `Table`.

   * Scegli la `Dashboard` dove la relazione deve essere disponibile.

   * Clic **[!UICONTROL Save a Copy to Dashboard]**.

1. Per visualizzare i rapporti nel dashboard, eseguire una delle operazioni seguenti:

   * Clic **[!UICONTROL Go to Dashboard]** nel messaggio nella parte superiore della pagina.

   * Nel menu, scegli **[!UICONTROL Dashboards]**. Fate clic sul nome del dashboard corrente per visualizzare l&#39;elenco. Quindi, fai clic sul nome della dashboard in cui è stato salvato il rapporto.
