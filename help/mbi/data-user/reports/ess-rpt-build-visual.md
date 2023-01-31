---
title: Report Builder visivo
description: Scopri come utilizzare Visual Report Builder.
exl-id: 1101f43d-e014-4df2-be21-12d90a9d8a56
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---

# `Visual Report Builder`

`Visual Report Builder` consente di creare rapporti rapidi basati su metriche predefinite. Ogni metrica include una query che definisce il set di dati per il rapporto.

L’esempio seguente mostra come creare un report semplice, raggruppare i dati per una dimensione aggiuntiva, impostare la data e l’intervallo di tempo, modificare il tipo di grafico e salvare il report in un dashboard.

## Per creare un rapporto semplice:

1. In [!DNL MBI] menu, fai clic su **[!UICONTROL Report Builder]**.

1. Sotto `Visual Report Builder`, fai clic su **[!UICONTROL Create Report]** e procedi come segue:

   * Fai clic su **[!UICONTROL Add Metric]**.

      Le metriche disponibili possono essere elencate in ordine alfabetico o per tabella.

      ![Report Builder visivo](../../assets/magento-bi-visual-report-builder-add-metric.png)

   * Scegli la [metrica](../../data-user/reports/ess-manage-data-metrics.md) descrive il set di dati da utilizzare per il rapporto.

      La `New Customers` La metrica utilizzata in questo esempio conta tutti i clienti e ordina l’elenco in base alla data in cui il cliente si è iscritto a un account. Il rapporto iniziale include un grafico a linee semplice seguito dalla tabella dei dati.

      Il riepilogo a sinistra mostra il nome della metrica corrente, seguito dal risultato di eventuali calcoli sui dati di colonna specificati nella metrica. In questo esempio, il riepilogo visualizza il conteggio totale dei clienti.

      ![Report Builder visivo](../../assets/magento-bi-report-builder-untitled.png)

1. Nel grafico, passa il cursore del mouse su ciascun punto dati della riga. Ogni punto dati mostra il numero totale di nuovi clienti che hanno effettuato l’iscrizione durante quel mese.

1. Segui queste istruzioni per raggruppare i dati, modificare l’intervallo di date e il tipo di grafico.

   **`Group By`**

   La `Group By` consente di aggiungere più dimensioni per gruppo o segmento. I Dimension sono colonne della tabella che possono essere utilizzate per raggruppare i dati.

   * Scegli una delle dimensioni disponibili dall’elenco di `Group By` opzioni.

      Per questo esempio, il sistema ha trovato cinque codici coupon che sono stati utilizzati dai clienti durante il posizionamento del loro primo ordine.

      ![Raggruppa per](../../assets/magento-bi-report-builder-group-by-dimensions.png)

      La `Group By` nel dettaglio sono elencate tutte le cedole utilizzate dai clienti. I coupon utilizzati per inserire l’ordine iniziale sono contrassegnati da una casella di controllo. Il grafico ora presenta più linee colorate che rappresentano ogni coupon utilizzato per un primo ordine. La legenda è codificata in base al colore per corrispondere a ogni riga di dati.

   * Fai clic su **[!UICONTROL Apply]** per chiudere il gruppo per dettagli.

      ![Dimension multipli](../../assets/magento-bi-report-builder-group-by-dimension-detail.png)

   * Passa il puntatore del mouse sopra alcuni punti di dati su ogni riga per vedere il numero di clienti durante il mese che hanno utilizzato quel coupon durante il posizionamento del loro primo ordine.

   * La tabella di dati ora presenta una dimensione aggiuntiva, con una colonna per ogni mese e una riga per ogni codice coupon.

      ![Raggruppa per dati di tabella](../../assets/magento-bi-report-builder-group-by-table-data.png)

   * Fai clic su Trasponi (![](../../assets/magento-bi-btn-transpose.png)) nell’angolo in alto a destra della tabella per modificare l’orientamento dei dati.

      L’asse dei dati viene capovolto e la tabella ora include una colonna per ogni codice coupon e una riga per ogni mese. Questo orientamento potrebbe essere più leggibile.

      ![Dati tradotti](../../assets/magento-bi-report-builder-group-by-table-data-transposed.png)
   **`Date Range`**

   La `Date Range` mostra l&#39;intervallo di date e l&#39;intervallo di tempo correnti e si trova appena sopra il grafico a destra.

   * Fai clic sul pulsante `Date Range` che in questo esempio è impostato su `All-Time by Month`.

      ![Intervallo date](../../assets/magento-bi-report-builder-date-range.png)

   * Apporta le seguenti modifiche:

      * Per ingrandire una visualizzazione più vicina, modifica l’intervallo di date in `Last Full Quarter`.
      * Sotto `Select Time Interval`, scegli `Week`.
      * Al termine, fai clic su **[!UICONTROL Save]**.

      Il rapporto ora include solo i dati dell’ultimo trimestre, per settimana.

      ![Rapporto per ultimo trimestre per settimana](../../assets/magento-bi-report-builder-date-range-quarter-by-week-chart.png)
   **Tipo di grafico**

   * Fai clic sui controlli nell’angolo in alto a destra per trovare il grafico migliore per i dati.

      Alcuni tipi di grafico non sono compatibili con i dati multidimensionali.

      |  |  |
      |-----|-----|
      | ![](../../assets/magento-bi-btn-chart-line.png) | Grafico a linee |
      | ![](../../assets/magento-bi-btn-chart-horz-bar.png) | Barre orizzontali |
      | ![](../../assets/magento-bi-btn-chart-horz-stacked-bar.png) | Barre orizzontali sovrapposte |
      | ![](../../assets/magento-bi-btn-chart-vert-bar.png) | Barre verticali |
      | ![](../../assets/magento-bi-btn-chart-vert-stacked-bar.png) | Barre sovrapposte verticali |
      | ![](../../assets/magento-bi-btn-chart-pie.png) | Torta |
      | ![](../../assets/magento-bi-btn-chart-area.png) | Area |
      | ![](../../assets/magento-bi-btn-chart-funnel.png) | Funnel |

      {style=&quot;table-layout:auto&quot;}




1. Per assegnare al rapporto un `title`, sostituisci `Untitled Report` testo nella parte superiore della pagina con un titolo descrittivo.

1. Nell&#39;angolo in alto a destra, fai clic su **[!UICONTROL Save]** e procedi come segue:

   * Per `Type`, accetta l&#39;impostazione predefinita, `Chart`.

   * Scegli la `Dashboard` dove la relazione deve essere disponibile.

   * Fai clic su **[!UICONTROL Save to Dashboard]**.

      ![Salva nel dashboard](../../assets/magento-bi-report-builder-save-to-dashboard.png)

1. Per visualizzare il grafico in un dashboard, effettuare una delle seguenti operazioni:

   * Fai clic su **[!UICONTROL Go to Dashboard]** nel messaggio nella parte superiore della pagina.

   * Nel menu , scegli `Dashboards` e fare clic sul nome del dashboard corrente per visualizzare l&#39;elenco. Quindi, fai clic sul nome del dashboard in cui è stato salvato il rapporto.

      ![Report nel dashboard](../../assets/magento-bi-report-builder-my-dashboard.png)
