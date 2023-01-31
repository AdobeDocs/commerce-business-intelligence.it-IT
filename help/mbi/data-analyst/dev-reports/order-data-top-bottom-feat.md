---
title: Ordinare i dati utilizzando la funzione Mostra in alto/in basso
description: Scopri come ordinare i dati utilizzando la funzione Mostra in alto/in basso.
exl-id: d47119f4-cdc5-4fa7-a606-d4b8555a8843
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# Ordinamento dei dati tramite `Show Top/Bottom` caratteristica

Puoi fare di più in `Visual Report Builder` anziché creare analizza tale tendenza nel tempo. Ad esempio, puoi creare un rapporto per mostrare quanto sono preziosi i tuoi canali di acquisizione e marketing, ma puoi anche creare un rapporto che mostra solo i primi cinque esecutori. Allo stesso modo, puoi concentrare nuovamente le tue attività di marketing creando un rapporto che ti mostra quali stati generano il maggior numero di ricavi.

Questo tipo di ordinamento e ordinamento dei dati può essere eseguito nei rapporti che utilizzano sia `Group By` e `Time Interval of None`. Quando entrambi questi elementi si trovano in un rapporto, il `Show Top/Bottom` viene visualizzata sopra l’anteprima del grafico. Questa funzione ti consente di visualizzare i punti di dati principali (dal più alto al più basso) e inferiori (dal più basso al più alto) in base ai parametri impostati.

![Mostra la funzione In alto/In basso nel Report Builder visivo.](../../assets/Show_Top_Bottom.png)

## Come lo utilizzo? {#how}

Dopo aver fatto clic sul pulsante **[!UICONTROL Show Top/Bottom link]**, viene visualizzata una finestra in cui puoi impostare i parametri di visualizzazione e ordinamento. Il numero nella casella di testo può essere un numero intero (come `5`) o `ALL`. Successivamente, puoi scegliere di ordinare il rapporto in base alla metrica O al raggruppamento.

Ad esempio, se vogliamo visualizzare le cinque fonti di riferimento che hanno generato maggiori ricavi, questo è il modo in cui lo facciamo:

1. Aggiungi il `Revenue` al rapporto.

1. Aggiungi un `Group By` segmentare la metrica per origine di riferimento.

1. Imposta `Time Interval` a `None`.

1. In `Show Top/Bottom` impostazioni, imposta la visualizzazione su `5` pertanto, nel rapporto sono incluse solo le fonti di riferimento con i primi cinque importi di ricavi totali.

>[!NOTE]
>
>Poiché il report non ha un `Time Interval`, i valori - in questo caso, le prime cinque origini di riferimento - possono cambiare nel tempo. Se un&#39;origine di riferimento supera un&#39;altra in termini di ricavi, l&#39;ordine in cui vengono visualizzate le origini cambierà.

## E l’utilizzo di più metriche? {#multiplemetrics}

L’utilizzo di questa funzione si complica quando si trovano più metriche in un rapporto, in quanto ogni metrica può essere ordinata solo da sola o da uno dei raggruppamenti.

Diciamo che abbiamo elaborato una relazione con entrambe le `Revenue` e `Number of orders` metriche, raggruppate per origine di riferimento. `Revenue` può essere ordinato solo per `Revenue` o sorgente di riferimento e `Number of orders` può essere ordinato solo per `Number of orders` o sorgente di riferimento.

Ciò significa che, mentre possiamo mostrare `Revenue` solo dall&#39;alto `5` ricavi che generano fonti di riferimento, non possiamo mostrare il numero di ordini anche dai più alti `5` ricavi che generano origini di riferimento. Inserisci semplicemente: in presenza di più metriche, la scommessa migliore è quella di ordinare ogni metrica in base al raggruppamento.

Ecco un esempio di grafico in cui abbiamo ordinato il `Revenue` metrica di per sé invece del raggruppamento. Come puoi vedere, non ordinando la metrica dal raggruppamento è stato creato un rapporto strano (e, in ultima analisi, inutile):

![Risultati dei rapporti strani e inutili.](../../assets/strange-report-results.png)

Se avessimo ordinato entrambe le metriche per il raggruppamento, il grafico sarebbe simile al seguente:

![Ordinamento di entrambe le metriche in base al raggruppamento.](../../assets/sort-metrics-by-grouping.png)

## Come vengono ordinati i valori per impostazione predefinita? {#defaultsorting}

Quando una sola metrica viene inclusa in un rapporto con una `Group by` e `Time Interval` di `None`, l&#39;ordine predefinito nel `Visual Report Builder` mostra i valori principali in base alla metrica. In questo caso, il `Show Top/Bottom` potrebbe non essere necessaria se soddisfa le tue esigenze.

In questo esempio, esaminiamo quante opportunità hanno chiuso i nostri rappresentanti commerciali. Questa tabella viene ordinata automaticamente dal più alto al più basso in base alla metrica, in questo caso `Won Opportunities`.

![Ordinamento in base alla metrica.](../../assets/Ordered_by_metric.png)

Tuttavia, quando viene aggiunta una seconda metrica, l’impostazione predefinita consiste nell’ordinare la parte superiore in base al raggruppamento. Con l’aggiunta di metriche e raggruppamenti, l’ordinamento predefinito sarà basato sul primo raggruppamento, sul secondo raggruppamento e così via.

![Ordinamento in base al raggruppamento.](../../assets/Ordered_by_grouping.png)

## Ritorno a capo {#wrapup}

L&#39;abbiamo menzionato all&#39;inizio dell&#39;articolo, ma lo ripetiamo ancora: mentre abbiamo trattato alcuni esempi di base, questa funzione ha molti usi interessanti.

Pensate al nostro precedente rappresentante commerciale ed esempio di opportunità. Rimozione di `Time Interval`, applicando un `Group By`, e l&#39;ordinamento dei dati in base al raggruppamento ci ha permesso di ottenere un quadro dettagliato del numero di opportunità di ogni rappresentante. Inoltre, utilizzando `Show Top/Bottom` Scopriamo chi sono i migliori esecutori.
