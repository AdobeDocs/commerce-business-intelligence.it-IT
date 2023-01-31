---
title: Creare metriche
description: Scopri come utilizzare le metriche per creare grafici.
exl-id: d4c25546-3c51-4d32-b9d8-c424ec103be5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---

# Creare metriche

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../administrator/user-management/user-management.md).

In parole povere, una metrica è una misura. Nelle strutture di SQL e database, una metrica è come una query memorizzata in un periodo di tempo variabile.

In [!DNL MBI], puoi utilizzare le metriche per [creare grafici](../../data-user/reports/ess-rpt-build-visual.md). Ad esempio, la metrica `revenue` è l&#39;importo totale degli ordini. La metrica `average customer revenue per order` è ciò che il cliente medio spende per ordine.

Quando vengono utilizzati nei rapporti, le metriche possono essere analizzate in un determinato periodo di tempo e [filtrato o segmentato](../../best-practices/segment-filter.md) per categorie diverse. Prendi in considerazione l’analisi delle entrate medie dei clienti raggruppate per genere - in questo caso, `average customer revenue per order` è la metrica e il genere è il raggruppamento.

## Definizione della metrica {#define}

1. Per creare una nuova metrica, fai clic su **[!UICONTROL Data** > **Metrics]**.

1. Fai clic su **[!UICONTROL Create New Metric]**.

1. Dal menu a discesa, fai clic sulla tabella che include la colonna nativa o calcolata che desideri utilizzare per la metrica.

1. Denomina la metrica.

   Consigliamo un nome che, a colpo d&#39;occhio, ti dica qual è la metrica. Ad esempio: `Average Order Revenue`.

1. Il passaggio successivo consiste nel definire il funzionamento della metrica. Mediante i menu a discesa, definisci il funzionamento della metrica e il `operation` e una `date` dimensione:

   * Scegli un&#39;operazione:
      * `Count` - Questa operazione conta il numero di righe in una tabella di dati
      * `Max` - Max restituisce il valore massimo di una colonna di dati specifica
      * `Min` - Min restituisce il valore minimo di una colonna di dati specifica
      * `Sum` - Questa operazione somma i valori di una colonna di dati specifica
      * `Average` - Questa operazione calcola la media dei valori delle colonne di dati
      * `Count Distinct Value` - Questo conta il numero univoco di valori in una colonna di dati specifica
      * `Median` - Questa operazione calcola la mediana dei valori delle colonne di dati
      * `First and Third Quartiles` - Queste operazioni calcolano rispettivamente il 25° e il 75° percentile dei valori delle colonne di dati
      * `Tenth and Ninetieth Percentiles` - Queste operazioni calcolano rispettivamente il decimo e il novantesimo percentile dei valori delle colonne di dati
   * Scegliere una colonna su cui eseguire l&#39;operazione. Ad esempio, per trovare i ricavi totali, esegui un’operazione di somma sul `order total` colonna.

      Se modifichi una metrica esistente, puoi anche [modificare la tabella operativa della metrica](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) in questa sezione.

   * Scegli una dimensione di data che può essere utilizzata per tendere la metrica. Ad esempio: `order date`.


## Aggiunta di filtri {#filters}

La `Filter` consente di creare un nuovo filtro o di applicare un [set di filtri salvato](../../data-user/reports/ess-manage-data-filters.md) alla metrica.

Per il nostro `average order revenue` Metrica, non vogliamo includere ordini di test che potrebbero essere stati fatti durante la configurazione del nostro negozio - questo ci darebbe un risultato impreciso. È possibile applicare un set di filtri per rimuovere tali ordini dal set di dati. Dopo la creazione, il filtro verrà applicato a tutti i grafici generati utilizzando questa metrica.

La `Filter Logic` è la sezione in cui puoi definire ulteriormente il comportamento di una metrica.

* &quot;\[`A`\] o \[`B`\]&quot; consentirà qualsiasi dato che soddisfi i filtri \[`A`\] O \[`B`\]
* &quot;\[`A`\] e \[`B`\]&quot; consentirà solo i dati che soddisfano entrambi i filtri \[`A`\] e \[`B`\]
* &quot;(\[`A`\] e \[`B`\]) O \[`C`\]&quot; consentirà solo i dati che soddisfano entrambi i filtri \[`A`\] e \[`B`\] o soddisfa il filtro \[`C`\] da solo

## Aggiunta di Dimension {#dimensions}

La [`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) la sezione mostra tutte le dimensioni dati disponibili per il filtraggio o il raggruppamento; per impostazione predefinita, tutte le colonne di dati disponibili sono elencate come dimensioni. Continuando il nostro esempio, se volessimo segmentare le entrate per fonte referenziale, potremmo farlo qui.

Oltre a elencare tutte le colonne di dati disponibili come dimensioni, [!DNL MBI] inoltre, supporrà quali colonne possono essere raggruppate. *Segmentazione o raggruppamento dei dati nei rapporti*, le colonne devono essere contrassegnate come raggruppabili.

## Completamento {#finish}

Oltre a definire il comportamento della metrica, puoi anche impostare i livelli di autorizzazione nella `User Rights` sezione . Quando `Admin` gli utenti hanno accesso a tutte le metriche. Devi indicare gli utenti che possono utilizzare questa metrica selezionando la casella accanto al gruppo appropriato.

Se modifichi una metrica esistente, puoi visualizzare un elenco di grafici (e relativi proprietari) che utilizzano tale metrica nel `Dependent Charts` sezione .

Le modifiche vengono salvate automaticamente e la metrica è ora pronta per l’uso.
