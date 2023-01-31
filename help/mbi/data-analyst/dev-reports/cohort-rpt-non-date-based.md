---
title: Report Builder di coorti per coorti non basati su date
description: Scopri come raggruppare gli utenti in base a un’attività o un attributo simile.
exl-id: c7b85ce9-113c-4ffc-855f-3d53fe2347d8
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 0%

---

# `Cohort Report Builder for Non-Date-Based Cohorts`

Nostro [`Cohort Report Builder`](../dev-reports/cohort-rpt-bldr.md) è stato bravo ad aiutare i commercianti a studiare come si comportano nel tempo diversi sottoinsiemi di utenti. In passato, il `Cohort Report Builder` è stato principalmente ottimizzato per raggruppare gli utenti in base a un comune `cohort date` (ad esempio, l’insieme di tutti i clienti che hanno effettuato il loro primo acquisto in un dato mese). La `Non-Date Based Cohort` ora offre la possibilità di raggruppare gli utenti in base a un’attività o un attributo simile. Scopri alcuni casi d’uso per questa funzione.

## Casi d&#39;uso

Questo non è un elenco completo, ma sono disponibili alcune analisi potenziali che possono essere eseguite con questa funzione:

* Esame dei ricavi dei clienti acquisiti da [!DNL Google] contro [!DNL Facebook]
* Analisi dei clienti il cui primo acquisto è stato effettuato negli Stati Uniti rispetto al Canada
* Osservare il comportamento dei clienti acquisiti da varie campagne pubblicitarie

## Come creare l’analisi

1. Fai clic su **[!UICONTROL Report Builder]** nella scheda a sinistra o **[!UICONTROL Add Report** > **Create Report]** in qualsiasi dashboard.

1. In `Report Builder Selection` schermata, fai clic su **[!UICONTROL Create Report]** accanto al `Visual Report Builder` opzione .

### Aggiunta di una metrica

Ora che siamo nel `Report Builder`, aggiungiamo la metrica su cui desideri eseguire l’analisi (ad esempio: `Revenue` o `Orders`).

>[!NOTE]
>
>Nativo [!DNL Google Analytics] le metriche non sono compatibili con `Cohort Report Builder`. Il nostro obiettivo per questo esempio è quello di esaminare i ricavi nel tempo per i clienti di primo ordine che sono stati acquisiti tramite diverse fonti GA.

### Attiva/disattiva `Metric View` a `Cohort`

![Visualizzazione metrica da 1 a coorte](../../assets/1-toggle-metric-view-to-cohort.png)

Viene visualizzata una nuova finestra in cui è possibile configurare i dettagli del rapporto coorte.

Sono necessarie cinque specifiche per la creazione di una relazione Cohort:

1. Come raggruppare le coorti
1. Selezione delle coorti
1. Timestamp azione azione
1. Intervallo di tempo della prima azione per coorte
1. Intervallo di tempo dopo l’occorrenza di una coorte

![gruppi di coorte](../../assets/2-cohort-groups.png){: width=&quot;200&quot; height=&quot;224&quot;}

![coorte-first-action-range](../../assets/3-cohort-first-action-time-range.png){: width=&quot;400&quot; height=&quot;554&quot;}

#### 1. Raggruppamento `cohorts`

`Cohorts` sono raggruppati per una caratteristica di comportamento, in questo esempio `Customer's first order GA source`. Le opzioni disponibili sono colonne già designate come `groupable` per la metrica.

#### 2. Selezione delle coorti

È possibile mostrare tutti i risultati per la caratteristica specificata. Poiché ciò può comportare un numero elevato di `cohorts`, puoi selezionare le `cohorts` (che corrispondono ai vari valori disponibili per `Customer's first order GA source`) di cui hai bisogno.

![gruppi di coorte](../../assets/4-cohort-groups.png)<!--{: width="300" height="338"}-->

#### 3. `Action timestamp`

Questo ti consente di scegliere una colonna basata su data diversa dalla colonna in cui viene creata la metrica. Di seguito, esaminiamo la selezione dell’intervallo di tempo applicabile al dato `action timestamp`.

#### 4. `Cohort first action time range`

Qui puoi selezionare l’intervallo di date che contiene il `cohorts action timestamp` (quindi, i clienti che hanno effettuato il primo ordine da novembre 2017 a ottobre 2018). Può trattarsi di un intervallo di date mobile o fisso.

#### 5. `Time range after cohort occurrence`

Vuoi vedere il `cohorts` nel tempo per mese, settimana o anno? Qui puoi effettuare le selezioni. Sotto quella sezione, selezioni la `time range` dopo il `cohort action timestamp` si è verificato. Ad esempio, questo ti mostrerà dodici mesi di dati per i clienti che hanno effettuato il primo ordine durante l’intervallo di tempo dell’azione.

![coorte-first-action-range](../../assets/5-cohort-first-action-time-range.png)<!--{: width="400" height="557"}-->

### Altre note

* [!UICONTROL Filters]: applicati alle metriche rimangono intatti quando si passa da `Standard` e `Cohort` visualizzazioni
* Vedi [`Perspectives`](../../data-analyst/dev-reports/cohort-rpt-bldr.md).
