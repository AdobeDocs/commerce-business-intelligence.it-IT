---
title: Filtri
description: Scopri come utilizzare i filtri.
exl-id: eb683dfe-9a90-400a-a0c0-3dc00d1f28b5
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# Filtri

È possibile aggiungere uno o più filtri per limitare i dati utilizzati per creare un rapporto. Ogni filtro è un’espressione che include una colonna della tabella associata, un operatore e un valore. Ad esempio, per includere solo i clienti ripetuti, puoi creare un filtro che includa solo i clienti che hanno effettuato più di un ordine. È possibile utilizzare più filtri con logica `AND/OR` per aggiungere logica al rapporto.

>[!TIP]
>
>Un rapporto può avere un massimo di 3.500 punti dati. Per ridurre il numero di punti dati, utilizza un filtro per ridurre la quantità di dati utilizzati per generare il rapporto.

MBI include una selezione di filtri che è possibile utilizzare &quot;out of the box (OOTB)&quot; o modificare in base alle tue esigenze. Non esiste un limite al numero di filtri che puoi creare.

## Per aggiungere un filtro:

1. Nel grafico, passa il puntatore del mouse su ciascun punto dati.

   In questo rapporto, ogni punto dati mostra il numero totale di clienti per il mese.

1. Nel pannello a sinistra, fai clic su Filtri (![](../../assets/magento-bi-btn-filter.png)).

   ![Aggiungi filtro](../../assets/magento-bi-report-builder-filter-add.png)

1. Fai clic su **[!UICONTROL Add Filter]**.

   I filtri sono numerati alfabeticamente e il primo è `[A]`. Le prime due parti del filtro sono opzioni a discesa e la terza parte è un valore.

   ![](../../assets/magento-bi-report-builder-filter-add-a.png)

   * Fai clic sulla prima parte del filtro e scegli la colonna che desideri utilizzare come oggetto dell’espressione.

      ![Scegli la prima parte del filtro](../../assets/magento-bi-report-builder-filter-part1.png)

   * Fai clic sulla seconda parte del filtro e scegli l’operatore .

      ![Scegli l’operatore](../../assets/magento-bi-report-builder-filter-part2.png)

   * Nella terza parte del filtro, immetti il valore necessario per completare l’espressione.

      ![Immetti il valore](../../assets/magento-bi-report-builder-filter-part3.png)

   * Al termine del filtro, fai clic su **[!UICONTROL Apply]**.

      Il rapporto ora include solo i clienti ripetuti e il numero di record dei clienti recuperati per il rapporto è stato ridotto da 33K a 12,6k.

      ![Rapporto filtrato](../../assets/magento-bi-report-builder-filter-report.png)<!--{: .zoom}-->

1. Nella barra laterale, fai clic sulla prospettiva ( ![](../../assets/magento-bi-btn-perspective.png)).

   ![Prospettiva](../../assets/magento-bi-report-builder-filter-perspective.png)<!--{: .zoom}-->

1. Nell’elenco delle impostazioni, scegli `Cumulative`. Quindi, fai clic su **[!UICONTROL Apply]**.

   ![Prospettiva cumulativa](../../assets/magento-bi-report-builder-filter-perspective-cumulative.png)

   La `Cumulative` La prospettiva distribuisce il cambiamento nel tempo, anziché mostrare i dati frastagliati su e giù per ogni mese.

1. Inserisci un `Title` per il rapporto e fai clic su **[!UICONTROL Save]** come `Chart` al dashboard.

   ![Salva nel dashboard](../../assets/magento-bi-report-builder-filter-perspective-cumulative-save.png)
