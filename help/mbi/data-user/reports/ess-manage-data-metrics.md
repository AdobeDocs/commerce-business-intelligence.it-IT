---
title: Creare metriche
description: Scopri come utilizzare le metriche per creare i grafici.
exl-id: d4c25546-3c51-4d32-b9d8-c424ec103be5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---

# Creare metriche

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../administrator/user-management/user-management.md).

Una metrica è una misurazione. Nelle strutture di SQL e database, una metrica è simile a una query memorizzata su un periodo di variabile.

In [!DNL Commerce Intelligence] è possibile utilizzare le metriche per [creare grafici](../../data-user/reports/ess-rpt-build-visual.md). Ad esempio, la metrica `revenue` è il numero totale di ordini. La metrica `average customer revenue per order` è la spesa media del cliente per ordine.

Se utilizzate nei rapporti, le metriche possono essere analizzate in un periodo di tempo specificato e [filtrate o segmentate](../../best-practices/segment-filter.md) da categorie diverse. Valuta l&#39;analisi dei ricavi medi dei clienti raggruppati per genere: in questo caso, `average customer revenue per order` è la metrica e il genere è il raggruppamento.

## Definizione della metrica {#define}

1. Per creare una metrica, fare clic su **[!UICONTROL Data** > **Metrics]**.

1. Fare clic su **[!UICONTROL Create New Metric]**.

1. Dal menu a discesa, fai clic sulla tabella che include la colonna nativa o calcolata che desideri utilizzare per la metrica.

1. Denomina la metrica.

   Adobe consiglia un nome che, a colpo d’occhio, indichi qual è la metrica. Esempio: `Average Order Revenue`.

1. Il passaggio successivo consiste nel definire il ruolo della metrica. Utilizzando i menu a discesa, definisci l’operazione della metrica, la colonna `operation` e una dimensione `date`:

   * Scegliere un&#39;operazione:
      * `Count` - Questa operazione conta il numero di righe in una tabella dati
      * `Max` - Max restituisce il valore massimo di una colonna di dati specifica
      * `Min` - Min restituisce il valore minimo di una colonna di dati specifica
      * `Sum` - Questa operazione somma i valori di una colonna di dati specifica
      * `Average` - Questa operazione calcola la media dei valori delle colonne di dati
      * `Count Distinct Value` - Conta il numero univoco di valori in una colonna di dati specifica
      * `Median` - Questa operazione calcola la mediana dei valori delle colonne di dati
      * `First and Third Quartiles` - Queste operazioni calcolano rispettivamente il 25° e il 75° percentile dei valori delle colonne di dati
      * `Tenth and Ninetieth Percentiles` - Queste operazioni calcolano rispettivamente il 10° e il 90° percentile dei valori delle colonne di dati

   * Scegliere una colonna su cui eseguire l&#39;operazione. Ad esempio, per trovare i ricavi totali, eseguire un&#39;operazione di somma sulla colonna `order total`.

     Se stai modificando una metrica esistente, puoi anche [modificare la tabella operativa della metrica](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) in questa sezione.

   * Scegli una dimensione di data che può essere utilizzata per generare la tendenza della metrica. Ad esempio, `order date`.

## Aggiunta di filtri {#filters}

La sezione `Filter` ti consente di creare un filtro o di applicare alla metrica un [set di filtri salvato](../../data-user/reports/ess-manage-data-filters.md).

Per la metrica `average order revenue`, non includere eventuali ordini di test eseguiti durante la configurazione dell&#39;archivio. Si otterrebbe un risultato non accurato. Può applicare un set di filtri per rimuovere tali ordini dal set di dati. Dopo la creazione, il filtro verrà applicato a tutti i grafici generati utilizzando questa metrica.

Nella sezione `Filter Logic` è possibile definire ulteriormente il comportamento di una metrica.

* &quot;\[`A`\] o \[`B`\]&quot; consente tutti i dati che soddisfano i filtri \[`A`\] O \[`B`\]
* &quot;\[`A`\] e \[`B`\]&quot; consente solo i dati che soddisfano entrambi i filtri \[`A`\] e \[`B`\]
* &quot;(\[`A`\] e \[`B`\]) OPPURE \[`C`\]&quot; consente solo i dati che soddisfano entrambi i filtri \[`A`\] e \[`B`\] oppure soddisfano solo il filtro \[`C`\]

## Aggiunta di dimensioni {#dimensions}

La sezione [`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) mostra tutte le dimensioni dati disponibili per il filtraggio o il raggruppamento. Per impostazione predefinita, tutte le colonne dati disponibili sono elencate come dimensioni. Continuando l’esempio, se desideri segmentare i ricavi per origine di riferimento, puoi farlo qui.

Oltre a elencare tutte le colonne di dati disponibili come dimensioni, [!DNL Commerce Intelligence] indovina le colonne raggruppabili. *Per segmentare o raggruppare i dati nei report*, le colonne devono essere contrassegnate come raggruppabili.

## Completamento {#finish}

Oltre a definire il comportamento della metrica, è possibile impostare i livelli di autorizzazione nella sezione `User Rights`. Sebbene `Admin` utenti abbiano accesso a tutte le metriche, è necessario indicare gli utenti che possono utilizzare questa metrica selezionando la casella accanto al gruppo appropriato.

Se stai modificando una metrica esistente, puoi visualizzare un elenco di grafici (e del relativo proprietario) che utilizzano questa metrica nella sezione `Dependent Charts`.

Le modifiche vengono salvate automaticamente e la metrica è ora valida.
