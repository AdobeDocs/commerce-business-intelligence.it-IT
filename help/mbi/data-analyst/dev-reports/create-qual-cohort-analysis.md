---
title: Creare un’analisi qualitativa per coorte
description: Scopri cos’è una coorte qualitativa, perché potresti essere interessato a creare questa analisi e come crearla in Commerce Intelligence.
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 0%

---

# Crea un `Qualitative Cohort Analysis`

Sapete in che modo i segmenti di clienti acquisiti da [!DNL Google Adwords] aumentano l&#39;LTV rispetto ai clienti acquisiti da ricerca organica? Hai mai pensato di eseguire un&#39;analisi `cohort` affiancata su diversi segmenti di clienti nello stesso rapporto? In caso affermativo, `qualitative cohort analysis` ti aiuta a rispondere a tali domande.

In questo argomento vengono illustrate le caratteristiche di una coorte qualitativa, le ragioni per cui potrebbe essere utile creare l&#39;analisi e le modalità di creazione in [!DNL Commerce Intelligence].

## Cosa sono `qualitative cohorts`? {#whatare}

L&#39;analisi di `Cohort` in generale può essere definita come l&#39;analisi di gruppi di utenti che condividono caratteristiche simili nel corso dei loro cicli di vita. Consente di identificare le tendenze comportamentali tra diversi gruppi di utenti.

Vedi [analisi per coorte](https://www.cohortanalysis.com/).

La maggior parte delle analisi di `cohort` in [!DNL Commerce Intelligence] raggruppa gli utenti in base a una data comune, ad esempio il set di tutti i clienti che hanno effettuato il primo acquisto in un dato mese. `qualitative cohort` è un gruppo di utenti definito da una caratteristica non basata sul tempo. Alcuni esempi:

* Il set di tutti gli utenti acquisiti da una campagna pubblicitaria
* Il set di tutti gli utenti il cui primo acquisto includeva un coupon (o meno)
* Il set di tutti gli utenti che hanno una certa età

## Quali sono le differenze rispetto al normale generatore `cohort`? {#different}

[`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md) è ottimizzato per il raggruppamento di coorti utilizzando una caratteristica basata sul tempo. Si tratta di un’ottima soluzione per le analisi che si concentrano su un segmento specifico di utenti (ad esempio, tutti gli utenti che sono stati acquisiti tramite una campagna di ricerca a pagamento). In `Cohort Analysis Builder`, puoi (1) concentrarti su quel gruppo di utenti specifico e (2) `cohort` su una data (come la data del loro primo ordine).

Tuttavia, se desideri analizzare il comportamento della coorte di più segmenti utente nello stesso rapporto di coorte (`paid` ricerca rispetto a `organic` ricerca rispetto al traffico diretto, ad esempio?), questa analisi più avanzata può essere costruita in `Report Builder`.

## Quali informazioni devo inviare al supporto per configurare la mia analisi? {#support}

La creazione di un report `qualitative cohort` in `Report Builder` implica che il team di analisti Adobe crei alcune [colonne calcolate avanzate](../data-warehouse-mgr/creating-calculated-columns.md) nelle tabelle necessarie.

Per generare questi elementi, invia un [ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=it) (e fai riferimento a questo articolo!). Ecco cosa devi sapere:

* `metric` con cui eseguire l&#39;analisi della coorte e la tabella utilizzata (ad esempio: `Revenue`, basata sulla tabella `orders`).

* I `user segments` che si desidera definire e la posizione in cui si trovano le informazioni nel database (ad esempio, valori diversi di `User's referral source`, nativi della tabella `users` e trasferiti in `orders`).

* I `cohort date` che desideri che l&#39;analisi utilizzi (ad esempio: il timestamp `User's first order date`). Questo esempio ci consentirebbe di esaminare ogni segmento e chiedere a `How does a user's revenue grow in the months following their first order date?`.

* `time interval` per cui si desidera visualizzare l&#39;analisi (ad esempio: `weeks`, `months` o `quarters` dopo `User's first order date`).

Una volta che il team di analisti di Adobe risponderà a quanto sopra, avrai a disposizione un paio di nuove colonne calcolate avanzate per creare il tuo rapporto. A questo scopo, puoi seguire le istruzioni riportate di seguito.

## Creazione dell’analisi qualitativa per coorte {#create}

Innanzitutto, aggiungere la metrica che si è interessati a raggruppare, una volta per ogni `cohort` che si sta analizzando. In questo esempio, vuoi visualizzare i `Revenue` cumulativi effettuati nei mesi successivi al primo ordine di un cliente, segmentati da `User's referral source`. Ciò significa che, per ogni segmento, aggiungi una metrica `Revenue` e un filtro per il segmento specifico:

![Dimostrazione animata della creazione di un&#39;analisi qualitativa per coorte](../../assets/qualcohort1.gif)

In secondo luogo, è necessario apportare due modifiche alle opzioni di tempo del rapporto:

1. Imposta `time interval` su `None`. Questo perché alla fine si raggruppa in base all’intervallo di tempo come dimensione invece di utilizzare le solite opzioni di tempo.

1. Impostare `time range` sulla finestra di tempo che si desidera venga coperta dal report.

In questo esempio, si esamina una visualizzazione `all time` di `Revenue`. Dopo di che, dovresti finire con una serie di punti:

![Dimostrazione animata delle opzioni di raggruppamento e analisi per coorte](../../assets/qualcohort2.gif)

In terzo luogo, si esegue la regolazione per impostare `cohorts`. In base a `cohort date` e `time interval` specificati per il team di analisti Adobe, hai una dimensione nel tuo account che esegue la data `cohort`. In questo esempio, la dimensione personalizzata è denominata `Months between this order and customer's first order date`. Utilizzando questa dimensione, è necessario:

* `Group by` la dimensione con l&#39;opzione `group by`

* Seleziona tutti i valori di `dimension` a cui sei interessato

* Con `Show top/bottom option`, seleziona i primi X mesi che ti interessano e ordina per la dimensione `Months between this order and customer's first order date`

Ora è possibile visualizzare una riga per ogni `cohort` specificato. Consulta l&#39;esempio ora. Viene visualizzato il contributo di `Revenue` da parte degli utenti di ogni origine di riferimento, `grouped by` il numero di mesi tra il primo ordine e qualsiasi ordine successivo. Nell&#39;esempio è stato aggiunto anche un `Cumulative perspective` per visualizzare la crescita aggregata `cohorts'`. Per una maggiore granularità, vedere la tabella dei risultati.

Cosa ci dice questo? In questo caso, l&#39;origine di riferimento specifica `Paid search` è utile nel primo mese della durata di acquisto di un cliente, ma non riesce a mantenere la sua base clienti con ricavi ripetuti. Mentre `Direct Traffic` inizia con un importo inferiore, nei mesi successivi le entrate si accumulano a un ritmo simile.

Indipendentemente dal modo in cui viene tagliata, l&#39;analisi `cohort` è uno strumento potente nella casella degli strumenti di analisi. Questo tipo di analisi consente di ottenere informazioni interessanti sull&#39;azienda, che potrebbero non essere disponibili nel `time-based cohorts` tradizionale, consentendo di prendere decisioni più mirate in base ai dati.
