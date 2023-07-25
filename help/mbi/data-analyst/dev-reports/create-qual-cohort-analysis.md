---
title: Creare un’analisi qualitativa per coorte
description: Scopri cos’è una coorte qualitativa, perché potresti essere interessato a creare questa analisi e come crearla in Commerce Intelligence.
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# Creare un `Qualitative Cohort Analysis`

Sapete in che modo [!DNL Google Adwords]I segmenti di clienti acquisiti aumentano il proprio LTV rispetto ai clienti acquisiti tramite la ricerca organica? Hai mai pensato di eseguire una `cohort` analisi affiancata di segmenti cliente diversi nello stesso rapporto? In caso affermativo, una `qualitative cohort analysis` ti aiuta a rispondere a quelle domande.

Questo argomento analizza cosa sia una coorte qualitativa, perché potresti essere interessato a creare questa analisi e come crearla in [!DNL Commerce Intelligence].

## Cosa sono `qualitative cohorts`Comunque? {#whatare}

`Cohort` l’analisi può essere generalmente definita come l’analisi di gruppi di utenti che condividono caratteristiche simili nel corso del loro ciclo di vita. Consente di identificare le tendenze comportamentali tra diversi gruppi di utenti.

Consulta [analisi per coorte](https://www.cohortanalysis.com/).

Più `cohort` analisi in [!DNL Commerce Intelligence] raggruppa gli utenti in base a una data comune, ad esempio l’insieme di tutti i clienti che hanno effettuato il primo acquisto in un dato mese. A `qualitative cohort` è un po’ diverso: è un gruppo di utenti definito da una caratteristica che non è basata sul tempo. Alcuni esempi:

* Il set di tutti gli utenti acquisiti da una campagna pubblicitaria
* Il set di tutti gli utenti il cui primo acquisto includeva un coupon (o meno)
* Il set di tutti gli utenti che hanno una certa età

## Quali sono le differenze rispetto al normale `cohort` costruttore? {#different}

Il [`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md) è ottimizzato per raggruppare le coorti utilizzando una caratteristica basata sul tempo. Si tratta di un’ottima soluzione per le analisi che si concentrano su un segmento specifico di utenti (ad esempio, tutti gli utenti che sono stati acquisiti tramite una campagna di ricerca a pagamento). In `Cohort Analysis Builder`, è possibile (1) concentrarsi su quello specifico gruppo di utenti e (2) `cohort` in una data (come la data del primo ordine).

Tuttavia, se desideri analizzare il comportamento della coorte di più segmenti di utenti nello stesso rapporto sulla coorte (`paid` ricerca e `organic` ricerca e traffico diretto, ad esempio?), questa analisi più avanzata può essere costruita nel `Report Builder`.

## Quali informazioni devo inviare al supporto per configurare la mia analisi? {#support}

Creazione di un `qualitative cohort` rapporto in `Report Builder` coinvolge il team di analisti Adobi nella creazione di alcuni [colonne calcolate avanzate](../data-warehouse-mgr/creating-calculated-columns.md) sulle tabelle necessarie.

Per generarli, invia una [ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) (e fai riferimento a questo articolo!). Ecco cosa devi sapere:

* Il `metric` desideri eseguire l’analisi per coorte con e con quale tabella (ad esempio: `Revenue`, basato su `orders` tabella).

* Il `user segments` si desidera definire e la posizione di tali informazioni nel database (ad esempio, valori diversi di `User's referral source`, nativo del `users` e riposizionato in basso nella `orders`).

* Il `cohort date` desideri che l’analisi utilizzi (ad esempio: `User's first order date` timestamp). Questo esempio ci consentirebbe di esaminare ogni segmento e chiedere `How does a user's revenue grow in the months following their first order date?`.

* Il `time interval` per visualizzare l’analisi (ad esempio: `weeks`, `months`, o `quarters` dopo il `User's first order date`).

Una volta che il team di analisti Adobe risponderà a quanto sopra, avrai a disposizione un paio di nuove colonne calcolate avanzate per creare il tuo rapporto. A questo scopo, puoi seguire le istruzioni riportate di seguito.

## Creazione dell’analisi qualitativa per coorte {#create}

Innanzitutto, vuoi aggiungere la metrica che ti interessa nella coorte, una volta per ogni `cohort` stai analizzando. In questo esempio, vuoi visualizzare cumulativo `Revenue` nei mesi successivi al primo ordine di un cliente, segmentato da `User's referral source`. Ciò significa che, per ogni segmento, ne aggiungi uno `Revenue` metrica e filtro per il segmento specifico:

![](../../assets/qualcohort1.gif)

In secondo luogo, è necessario apportare due modifiche alle opzioni di tempo del rapporto:

1. Imposta il `time interval` a `None`. Questo perché alla fine si raggruppa in base all’intervallo di tempo come dimensione invece di utilizzare le solite opzioni di tempo.

1. Imposta il `time range` alla finestra di tempo che si desidera venga coperta dal rapporto.

In questo esempio, viene visualizzata una `all time` visualizzazione di `Revenue`. Dopo di che, dovresti finire con una serie di punti:

![](../../assets/qualcohort2.gif)

In terzo luogo, è necessario regolare per impostare `cohorts`. In base al `cohort date` e `time interval` hai specificato al team di analisti Adobe, hai una dimensione nel tuo account che esegue il `cohort` incontri. In questo esempio, la dimensione personalizzata è denominata `Months between this order and customer's first order date`. Utilizzando questa dimensione, è necessario:

* `Group by` la dimensione con `group by` opzione

* Seleziona tutti i valori del `dimension` cui sei interessato

* Con il `Show top/bottom option`, seleziona i primi X mesi a cui sei interessato e ordina in base al `Months between this order and customer's first order date` dimensione

Ora puoi vedere una riga per ogni `cohort` che hai specificato. Guardate l&#39;esempio ora, vedete la `Revenue` contributo degli utenti di ciascuna origine di riferimento, `grouped by` il numero di mesi tra il primo ordine e qualsiasi ordine successivo. Nell&#39;esempio è stata aggiunta anche una `Cumulative perspective` per visualizzare `cohorts'` crescita aggregata: per una maggiore granularità, consulta la tabella dei risultati.

Cosa ci dice questo? In questo caso, l’origine di riferimento specifica `Paid search` è prezioso nel primo mese della durata di acquisto di un cliente, ma non riesce a mantenere la sua base di clienti con ricavi ripetuti. Mentre `Direct Traffic` parte da un importo inferiore, le entrate nei mesi successivi si accumulano in realtà a un ritmo simile.

Non importa come te la canti, `cohort` l’analisi è uno strumento potente nella casella degli strumenti di analisi. Questo tipo di analisi può fornire alcune informazioni interessanti sulla tua attività che `time-based cohorts` potrebbe non farlo, consentendo di prendere decisioni migliori basate sui dati.
