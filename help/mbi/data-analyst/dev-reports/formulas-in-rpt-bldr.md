---
title: Formule in Report Builder
description: Scopri come utilizzare le formule in Report Builder.
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/XxqMoKRPIKcRgh8HKa6z2IMp6WkiCVp2jhIbXFqcraU
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 544
ht-degree: 0%

---

# Formule in `Report Builder`

In [`Report Builder`](../../tutorials/using-visual-report-builder.md), puoi creare visualizzazioni efficaci utilizzando le [metriche definite](../../data-user/reports/ess-manage-data-metrics.md) nel tuo account. La combinazione di queste metriche in una formula consente di ottenere ulteriori informazioni dai dati. Questo argomento descrive come utilizzare le formule in `Report Builder`.

## Cos&#39;è un `formula`? {#what}

In `Report Builder`, un `formula` è solo una combinazione di una o più metriche basate su una logica matematica. Un esempio tipico è simile al seguente:

![Esempio di formula che mostra il calcolo in Report Builder](../../assets/formula-example.png)

In questo esempio si utilizzano `Number of orders metric (A)` e `Distinct buyers metric (B)` e l&#39;obiettivo è rispondere alla domanda: qual è il numero medio di ordini che i miei acquirenti effettuano ogni mese? I parametri della formula sono:

* `Definition`: applica la matematica alle metriche di input. In questo esempio, la divisione del numero di ordini per il numero di acquirenti distinti indica il numero medio di ordini. La definizione è (A/B).

* `Format`: la formula restituisce un numero, un periodo di tempo o un importo in valuta? Accanto alla definizione della formula è disponibile un elenco a discesa che consente di specificare il formato del risultato. In questo caso, è un numero.

* `Miscellaneous`: la marca temporale, i raggruppamenti, le prospettive e i filtri della formula sono tutti ereditati dalle relative metriche di input. Non c&#39;è niente da fare qui!

## Come posso usare `formulas` nei miei report? {#how}

Ora che hai trattato le nozioni di base, guarda alcuni esempi.

### Esempio: voglio scoprire quale percentuale delle mie entrate può essere attribuita a ordini nuovi.

![Utilizzo di formule per trovare la percentuale di ricavi attribuita a nuovi ordini](../../assets/first_time_orders.gif)

In questo esempio sono state utilizzate le metriche `Revenue` e `Revenue (first time orders)`. Dividendo la metrica `Revenue (first time orders)(B)` per `Revenue metric (A)` e impostando il formato di restituzione su `Percent`, è possibile trovare la percentuale di ricavi che può essere attribuita agli ordini delle prime volte.

### Esempio: voglio sapere qual è il ricavo medio per ordine quando effettuo e non offro `promo code`.

![Utilizzo di formule per trovare il ricavo medio per ordine con e senza codici promozionali](../../assets/promo_code.gif)

In questo esempio sono state utilizzate le metriche `Revenue` e `Number of orders`. La risposta a questa domanda prevede due passaggi: dividere `Revenue (A)` per `Number of orders (B)` e impostare il formato restituito su `Currency`. Successivamente, è stato consentito solo al risultato della formula (`Avg. Revenue per order`) di visualizzare e raggruppare i risultati per `Promo code`.

### Esempio: voglio conoscere la distribuzione delle sorgenti UTM dei miei nuovi clienti.

![Utilizzo di formule per trovare la distribuzione delle origini UTM dei nuovi clienti](../../assets/distro.gif)

La ricerca della risposta a questa domanda richiede alcuni passaggi:

1. È stata aggiunta la metrica `New Customers`, quindi raggruppata per `utm_source - all`. Metrica `A` o `New Customers (grouped)`.

1. Successivamente, hai duplicato la metrica `New Customers (grouped)` e l&#39;hai impostata per utilizzare una dimensione indipendente. La metrica `B` - `New customers (ungrouped)` - mostra il numero totale di nuovi clienti.

1. Dopo aver nascosto entrambe le metriche, impostare la definizione della formula su `A/B`. `New customers (grouped)` è diviso per `New Customers (ungrouped)`.

1. Impostare quindi il formato dei risultati su `Percent`.

In questo esempio è stata utilizzata la prospettiva `Stacked Columns` per visualizzare i risultati per mese. Questo ci permette di confrontare la distribuzione dei nuovi clienti su base mensile.

## Ritorno a capo {#wrapup}

Negli esempi precedenti è stato notato che le metriche di input della formula `timestamp`, `groupings`, `perspectives` e `filters` sono ereditate? Tieni presente che le formule possono essere utilizzate per utilizzare `perspectives` e [opzioni di tempo indipendenti](../../tutorials/time-options-visual-rpt-bldr.md){: target="_blank"}, proprio come le metriche.

Per ulteriori domande sull&#39;utilizzo delle formule in `Report Builder`, [contattare il supporto tecnico](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=it).
