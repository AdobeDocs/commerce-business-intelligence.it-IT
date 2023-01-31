---
title: Formule nel Report Builder
description: Scopri come utilizzare le formule nel Report Builder.
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---

# Formule nel `Report Builder`

In [`Report Builder`](../../tutorials/using-visual-report-builder.md), puoi creare visualizzazioni potenti utilizzando [metriche definite](../../data-user/reports/ess-manage-data-metrics.md) nel tuo account. Combinare queste metriche in una formula ti consente di ottenere ulteriori informazioni dai tuoi dati. In questo articolo, approfondiamo il modo in cui le formule possono essere utilizzate nel `Report Builder` - saltiamo dentro!

## Cosa è un `formula`? {#what}

In `Report Builder`, `formula` è solo una combinazione di una o più metriche basate su una logica matematica. Esempio tipico:

![](../../assets/formula-example.png)

In questo esempio, utilizziamo un `Number of orders metric (A)` e `Distinct buyers metric (B)`e il nostro obiettivo è quello di rispondere alla domanda: qual è il numero medio di ordini che i miei acquirenti fanno ogni mese? I parametri della formula sono:

* `Definition`: In questo caso, puoi applicare la matematica alle metriche di input. In questo esempio, la suddivisione del numero di ordini per il numero di acquirenti distinti indicherà il numero medio di ordini. Pertanto, la definizione è (A/B).

* `Format`: La formula restituisce un numero, un periodo di tempo o un importo in valuta? Accanto alla definizione della formula è disponibile un menu a discesa, che consente di specificare il formato della restituzione. In questo caso, è un numero.

* `Miscellaneous`: La marca temporale, i raggruppamenti, le prospettive e i filtri della formula sono tutti ereditati dalle relative metriche di input. Non c&#39;è niente da fare qui!

## Come posso utilizzare `formulas` nei miei rapporti? {#how}

Ora che abbiamo trattato le basi, diamo un&#39;occhiata ad alcuni esempi.

### Esempio: Voglio scoprire quale percentuale delle mie entrate può essere attribuita agli ordini della prima volta.

![Utilizzo di formule per trovare la percentuale di ricavi attribuiti agli ordini nuovi](../../assets/first_time_orders.gif)

In questo esempio, abbiamo utilizzato il `Revenue` e `Revenue (first time orders)` metriche. Dividendo la `Revenue (first time orders)(B)` metrica per `Revenue metric (A)` e l&#39;impostazione del formato di ritorno su `Percent`, possiamo trovare la percentuale di ricavi che possono essere attribuiti ai primi ordini.

### Esempio: Voglio sapere qual è il ricavo medio per ordine quando faccio e non offro un `promo code`.

![Utilizzo di formule per trovare i ricavi medi per ordine con e senza codici promozionali](../../assets/promo_code.gif)

In questo esempio, abbiamo utilizzato il `Revenue` e `Number of orders` metriche. La risposta a questa domanda si articola in due fasi: `Revenue (A)` dal `Number of orders (B)` e l&#39;impostazione del formato di ritorno su `Currency`. Successivamente, è stato consentito solo il risultato della formula (`Avg. Revenue per order`) per mostrare e raggruppare i risultati per `Promo code`.

### Esempio: Voglio conoscere la distribuzione delle fonti UTM dei miei nuovi clienti.

![Utilizzo di formule per trovare la distribuzione delle fonti UTM dei nuovi clienti](../../assets/distro.gif)

Per trovare la risposta a questa domanda sono necessari alcuni passaggi:

1. Prima abbiamo aggiunto il `New Customers` e quindi raggruppati per `utm_source - all`. Questa è metrica `A`oppure `New Customers (grouped)`.

1. Successivamente, abbiamo duplicato il `New Customers (grouped)` e impostalo per l’utilizzo di una dimensione indipendente. Metrica `B` - `New customers (ungrouped)` - mostra il numero totale di nuovi clienti.

1. Dopo aver nascosto entrambe le metriche, imposta la definizione della formula su `A/B`. Questo divide il `New customers (grouped)` dal `New Customers (ungrouped)`.

1. Quindi, imposta il formato dei risultati su `Percent`.

Nel nostro esempio, abbiamo utilizzato il `Stacked Columns` prospettiva per visualizzare i risultati per mese. Questo ci consente di confrontare la distribuzione dei nuovi clienti su base mensile.

## Ritorno a capo {#wrapup}

Avete notato negli esempi sopra che la formula è `timestamp`, `groupings`, `perspectives`e `filters` sono ereditate dalle relative metriche di input? Tenere presente che le formule possono essere utilizzate `perspectives` e [opzioni di tempo indipendenti](../../tutorials/time-options-visual-rpt-bldr.md){: target=&quot;_blank&quot;}, proprio come possono fare le metriche.

Se hai ulteriori domande sull&#39;utilizzo delle formule nel `Report Builder`, [contattare il supporto](../../guide-overview.md).
