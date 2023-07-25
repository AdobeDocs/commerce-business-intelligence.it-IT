---
title: Formule nel Report Builder
description: Scopri come utilizzare le formule nel Report Builder.
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# Formule in `Report Builder`

In [`Report Builder`](../../tutorials/using-visual-report-builder.md), puoi creare visualizzazioni efficaci utilizzando [metriche definite](../../data-user/reports/ess-manage-data-metrics.md) nel tuo account. La combinazione di queste metriche in una formula consente di ottenere ulteriori informazioni dai dati. Questo argomento descrive come utilizzare le formule nel `Report Builder` - saltiamo dentro!

## Cos’è un `formula`? {#what}

In `Report Builder`, a `formula` è solo una combinazione di una o più metriche basate su una logica matematica. Un esempio tipico è simile al seguente:

![](../../assets/formula-example.png)

In questo esempio, utilizzi un’ `Number of orders metric (A)` e un `Distinct buyers metric (B)`e l&#39;obiettivo è quello di rispondere alla domanda: qual è il numero medio di ordini che i miei acquirenti fanno ogni mese? I parametri della formula sono:

* `Definition`: in questo caso, puoi applicare la matematica alle metriche di input. In questo esempio, la divisione del numero di ordini per il numero di acquirenti distinti indica il numero medio di ordini. La definizione è (A/B).

* `Format`: la formula restituisce un numero, un periodo di tempo o un importo in valuta? Accanto alla definizione della formula è disponibile un elenco a discesa che consente di specificare il formato del risultato. In questo caso, è un numero.

* `Miscellaneous`: la marca temporale, i raggruppamenti, le prospettive e i filtri della formula sono tutti ereditati dalle relative metriche di input. Non c&#39;è niente da fare qui!

## Come posso utilizzare `formulas` nei miei rapporti? {#how}

Ora che hai trattato le nozioni di base, guarda alcuni esempi.

### Esempio: voglio scoprire quale percentuale delle mie entrate può essere attribuita a ordini nuovi.

![Utilizzo di formule per trovare la percentuale di ricavi attribuita a ordini nuovi](../../assets/first_time_orders.gif)

In questo esempio hai utilizzato `Revenue` e `Revenue (first time orders)` metriche. Dividendo il `Revenue (first time orders)(B)` metrica per `Revenue metric (A)` e l&#39;impostazione del formato di ritorno su `Percent`, è possibile trovare la percentuale di ricavi che può essere attribuita agli ordini di prima volta.

### Esempio: voglio sapere qual è il ricavo medio per ordine quando effettuo e non offro un `promo code`.

![Utilizzo di formule per trovare il ricavo medio per ordine con e senza codici promozionali](../../assets/promo_code.gif)

In questo esempio hai utilizzato `Revenue` e `Number of orders` metriche. La risposta a questa domanda prevede due passaggi: `Revenue (A)` da `Number of orders (B)` e l&#39;impostazione del formato di ritorno su `Currency`. Successivamente, è stato consentito solo il risultato della formula (`Avg. Revenue per order`) per mostrare e raggruppare i risultati per `Promo code`.

### Esempio: voglio conoscere la distribuzione delle sorgenti UTM dei miei nuovi clienti.

![Utilizzo di formule per trovare la distribuzione delle origini UTM dei nuovi clienti](../../assets/distro.gif)

La ricerca della risposta a questa domanda richiede alcuni passaggi:

1. Prima hai aggiunto il `New Customers` metrica e quindi raggruppata per `utm_source - all`. Questa è una metrica `A`, o `New Customers (grouped)`.

1. Successivamente, hai duplicato `New Customers (grouped)` e impostarla per utilizzare una dimensione indipendente. Metrica `B` - `New customers (ungrouped)` - mostra il numero totale di nuovi clienti.

1. Dopo aver nascosto entrambe le metriche, imposta la definizione della formula su `A/B`. Questo divide il `New customers (grouped)` da `New Customers (ungrouped)`.

1. Quindi, si imposta il formato dei risultati su `Percent`.

In questo esempio hai utilizzato `Stacked Columns` per visualizzare i risultati per mese. Questo ci permette di confrontare la distribuzione dei nuovi clienti su base mensile.

## Ritorno a capo {#wrapup}

Hai notato negli esempi precedenti che la formula è `timestamp`, `groupings`, `perspectives`, e `filters` vengono ereditati dalle relative metriche di input? È possibile utilizzare le formule `perspectives` e [opzioni di tempo indipendenti](../../tutorials/time-options-visual-rpt-bldr.md){: target=&quot;_blank&quot;}, proprio come le metriche.

Per ulteriori domande sull&#39;utilizzo delle formule in `Report Builder`, [contatta l’assistenza](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
