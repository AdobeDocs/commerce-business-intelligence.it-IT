---
title: Creare un’analisi qualitativa per coorte
description: Scopri cos’è una coorte qualitativa, perché potresti essere interessato a creare questa analisi e come crearla in [!DNL MBI].
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 0%

---

# Crea un `Qualitative Cohort Analysis`

Lei sa come la sua [!DNL Adwords]I segmenti di clienti acquisiti aumentano i loro LTV rispetto a quei clienti acquisiti dalla ricerca organica? Hai mai pensato di esibirti in un `cohort` analisi affiancata di diversi segmenti di clienti nello stesso rapporto? In caso affermativo, un `qualitative cohort analysis` Ti aiuterà a rispondere a quelle domande.

In questo articolo, ci soffermiamo su cosa sia una coorte qualitativa, perché potrebbe interessarti costruire questa analisi e come crearla [!DNL MBI].

## Cosa sono `qualitative cohorts`Comunque? {#whatare}

`Cohort` l&#39;analisi può essere generalmente definita come l&#39;analisi di gruppi di utenti che condividono caratteristiche simili nel corso del loro ciclo di vita. Ti consente di identificare le tendenze comportamentali tra diversi gruppi di utenti.

Vedi [analisi per coorte](https://www.cohortanalysis.com/) - ci abbiamo scritto il sito!

Più `cohort` analizza [!DNL MBI] raggruppare gli utenti in base a una data comune (ad esempio, l’insieme di tutti i clienti che hanno effettuato il loro primo acquisto in un dato mese). A `qualitative cohort` è un po&#39; diverso: è un gruppo di utenti definito da una caratteristica che non è basata sul tempo. Alcuni esempi includono:

* Set di tutti gli utenti acquisiti da una campagna pubblicitaria
* L&#39;insieme di tutti gli utenti il cui primo acquisto includeva un coupon (o no)
* Set di tutti gli utenti che hanno una certa età

## Come differisce dal normale `cohort` costruttore? {#different}

La [`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md) è ottimizzato per raggruppare le coorti utilizzando una caratteristica basata sul tempo. Questo è ottimo per le analisi incentrate su un segmento specifico di utenti (ad esempio, tutti gli utenti che sono stati acquisiti tramite una campagna di ricerca a pagamento). In `Cohort Analysis Builder`, puoi (1) concentrarti su quel gruppo di utenti specifico e (2) `cohort` in una data (come la data del primo ordine).

Tuttavia, se desideri analizzare il comportamento della coorte di più segmenti di utenti nello stesso rapporto di coorte (`paid` ricerca e confronto `organic` ricerca e traffico diretto, forse?), questa analisi più avanzata può essere realizzata nel `Report Builder`.

## Quali informazioni devo inviare al supporto per impostare la mia analisi? {#support}

Creazione di una `qualitative cohort` nella `Report Builder` coinvolge il nostro team di analisti nella creazione di [colonne calcolate avanzate](../data-warehouse-mgr/creating-calculated-columns.md) sulle tabelle necessarie.

Per creare questi elementi, invia un [biglietto di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) (e fai riferimento a questo articolo!). Ecco cosa dobbiamo sapere:

* La `metric` desideri eseguire l’analisi per coorte con e con quale tabella utilizza (esempio: `Revenue`, basato su `orders` tabella).

* La `user segments` definire e dove si trovano le informazioni nel database (esempio: diversi valori di `User's referral source`, nativo di `users` tabella e riposizionata verso il basso `orders`).

* La `cohort date` desideri utilizzare l’analisi (ad esempio: la `User's first order date` timestamp). Questo esempio ci consentirebbe di esaminare ogni segmento e di chiedere `How does a user's revenue grow in the months following their first order date?`.

* La `time interval` per cui desideri visualizzare l’analisi (esempio: `weeks`, `months`oppure `quarters` dopo il `User's first order date`).

Una volta che il nostro team di analisti avrà risposto a quanto sopra, avrai a disposizione un paio di nuove colonne calcolate avanzate per creare il tuo report! Quindi sarà in grado di seguire le seguenti indicazioni per fare questo.

## Creazione di un’analisi qualitativa della coorte {#create}

Innanzitutto, aggiungi la metrica a cui sei interessato nella coorte, una volta per ogni `cohort` sta analizzando. In questo esempio, vogliamo vedere cumulativo `Revenue` effettuato nei mesi successivi al primo ordine di un cliente, segmentato dal `User's referral source`. Ciò significa che, per ogni segmento, ne aggiungeremo uno `Revenue` metrica e filtro per il segmento specifico:

![](../../assets/qualcohort1.gif)

In secondo luogo, è necessario apportare due modifiche alle opzioni di tempo del rapporto:

1. Imposta la `time interval` a `None`. Questo perché alla fine raggruppiamo come dimensione l’intervallo di tempo anziché le consuete opzioni di tempo.

1. Imposta la `time range` nella finestra di tempo in cui desideri che il rapporto venga trattato.

Nel nostro esempio, osserviamo un `all time` vista `Revenue`. Dopo questo, dovresti finire con una serie di punti:

![](../../assets/qualcohort2.gif)

In terzo luogo, effettuerete una regolazione per impostare effettivamente il `cohorts`. In base ai `cohort date` e `time interval` hai specificato al nostro team di analisti, nel tuo account sarà presente una dimensione che eseguirà la `cohort` incontri. In questo esempio, la dimensione personalizzata viene denominata `Months between this order and customer's first order date`. Utilizzando questa dimensione, devi:

* `Group by` la dimensione con `group by` opzione

* Seleziona tutti i valori del `dimension` di cui sei interessato

* Con la `Show top/bottom option`, seleziona i primi X mesi che ti interessano e ordina in base al `Months between this order and customer's first order date` dimension

Ora puoi vedere una riga per ogni `cohort` che hai specificato. Dai un&#39;occhiata al nostro esempio: vediamo il `Revenue` contributi degli utenti di ciascuna origine di riferimento, `grouped by` il numero di mesi tra il primo ordine e l&#39;ordine successivo. Abbiamo aggiunto anche un `Cumulative perspective` per visualizzare `cohorts'` crescita aggregata - date un&#39;occhiata alla tabella dei risultati per una maggiore granularità.

Cosa ci dice questo? Qui, l&#39;origine di riferimento specifica `Paid search` è molto utile nel primo mese della vita di acquisto di un cliente, ma non riesce a mantenere la sua base clienti con ricavi ripetuti. Quando `Direct Traffic` inizia con un importo più basso, i ricavi nei mesi successivi si accumulano a un ritmo simile.

Non importa come lo dice, `cohort` analysis è uno strumento potente nella tua casella degli strumenti di analisi. Questo tipo di analisi può fornire alcuni spunti molto interessanti sul tuo business che tradizionali `time-based cohorts` potrebbe non essere possibile, consentendo di prendere decisioni migliori basate sui dati.
