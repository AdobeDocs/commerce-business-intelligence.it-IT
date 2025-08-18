---
title: Ordinare i dati utilizzando la funzione Mostra superiore/inferiore
description: Scopri come ordinare i dati utilizzando la funzione Mostra superiore/inferiore.
exl-id: d47119f4-cdc5-4fa7-a606-d4b8555a8843
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---

# Ordinamento dei dati tramite la funzionalità `Show Top/Bottom`

In `Visual Report Builder` è possibile fare di più che creare analisi con tale tendenza nel tempo. Ad esempio, puoi creare un rapporto per mostrare quanto sono preziosi i tuoi canali di acquisizione e marketing, ma puoi anche creare un rapporto che mostra solo i primi cinque esecutori. Allo stesso modo, puoi riorientare le attività di marketing creando un rapporto che mostra quali stati generano il maggior numero di ricavi.

Questo tipo di ordinamento dei dati può essere eseguito nei report che utilizzano sia `Group By` che `Time Interval of None`. Quando entrambi questi elementi si trovano in un report, la funzionalità `Show Top/Bottom` viene visualizzata sopra l&#39;anteprima del grafico. Questa funzione consente di visualizzare i punti di dati superiori (dal più alto al più basso) e inferiori (dal più basso al più alto) in base ai parametri impostati.

![Mostra funzionalità superiore/inferiore in Visual Report Builder.](../../assets/Show_Top_Bottom.png)

## Come si utilizza? {#how}

Fare clic su **[!UICONTROL Show Top/Bottom link]** per impostare i parametri di visualizzazione e ordinamento. Il numero nella casella di testo può essere un numero intero (come `5`) o `ALL`. Successivamente, puoi scegliere di ordinare il rapporto in base alla metrica OPPURE in base al raggruppamento.

Ad esempio, per visualizzare le cinque origini di riferimento che hanno generato il maggior numero di ricavi, effettua le seguenti operazioni:

1. Aggiungi la metrica `Revenue` al rapporto.

1. Aggiungi `Group By` per segmentare la metrica per origine riferimento.

1. Imposta `Time Interval` su `None`.

1. Nelle impostazioni di `Show Top/Bottom`, imposta la visualizzazione su `5` in modo che nel rapporto vengano incluse solo le origini di riferimento con i primi cinque importi totali delle entrate.

>[!NOTE]
>
>Poiché il report non ha un `Time Interval`, i valori, in questo caso le prime cinque origini di riferimento, possono cambiare nel tempo. Se un&#39;origine di riferimento supera un&#39;altra in termini di ricavi, l&#39;ordine di visualizzazione delle origini cambia.

## E l’utilizzo di più metriche? {#multiplemetrics}

L’utilizzo di questa funzione si complica quando un rapporto contiene più di una metrica, perché ogni metrica può essere ordinata solo in base a se stessa o a uno dei raggruppamenti.

Si supponga di aver creato un report con entrambe le metriche `Revenue` e `Number of orders`, raggruppate per origine di riferimento. `Revenue` può essere ordinato solo in base a `Revenue` o all&#39;origine di riferimento e `Number of orders` può essere ordinato solo in base a `Number of orders` o all&#39;origine di riferimento.

Ciò significa che mentre è possibile visualizzare `Revenue` solo dalle prime `5` origini di riferimento che generano ricavi, non è possibile visualizzare il numero di ordini anche dalle prime `5` origini di riferimento che generano ricavi. In parole povere: quando sono presenti più metriche, la cosa migliore è ordinare ciascuna metrica in base al raggruppamento.

Di seguito è riportato un esempio di grafico che ha ordinato la metrica `Revenue` in base a se stessa invece che in base al raggruppamento. Come puoi notare, il fatto di non ordinare la metrica per raggruppamento ha creato un rapporto strano (e in ultima analisi non utile):

![Risultati del report insoliti e inutili.](../../assets/strange-report-results.png)

Se avessi ordinato entrambe le metriche in base al raggruppamento, il grafico si presenterebbe così:

![Ordinamento di entrambe le metriche in base al raggruppamento.](../../assets/sort-metrics-by-grouping.png)

## Come vengono ordinati i valori per impostazione predefinita? {#defaultsorting}

Quando in un report con `Group by` e `Time Interval` di `None` è inclusa una sola metrica, l&#39;ordine predefinito in `Visual Report Builder` consiste nel mostrare i primi valori basati sulla metrica. In questa istanza, la funzionalità `Show Top/Bottom` potrebbe non essere necessaria se soddisfa le tue esigenze.

In questo esempio viene esaminato il numero di opportunità chiuse dagli agenti di vendita. Questa tabella viene ordinata automaticamente dal valore più alto a quello più basso in base alla metrica, in questo caso `Won Opportunities`.

![Ordinamento in base alla metrica.](../../assets/Ordered_by_metric.png)

Tuttavia, quando viene aggiunta una seconda metrica, l’impostazione predefinita consiste nell’ordinare la parte superiore in base al raggruppamento. Con l’aggiunta delle metriche e dei raggruppamenti, l’ordinamento predefinito si basa sul primo raggruppamento, quindi sul secondo e così via.

![Ordinamento in base al raggruppamento.](../../assets/Ordered_by_grouping.png)

## Ritorno a capo {#wrapup}

Anche se alcune funzioni di base sono trattate qui, questa funzione ha molti utilizzi interessanti.

Pensa all’esempio precedente di rappresentante di vendita e opportunità. La rimozione di `Time Interval`, l&#39;applicazione di `Group By` e l&#39;ordinamento dei dati in base al raggruppamento ci hanno permesso di ottenere un quadro dettagliato del numero di opportunità realizzate da ogni rappresentante. Inoltre, l&#39;utilizzo della funzionalità `Show Top/Bottom` consente di individuare i migliori esecutori.
