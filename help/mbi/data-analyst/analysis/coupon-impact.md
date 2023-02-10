---
title: Analisi dell'impatto del buono sconto
description: Scopri come analizzare l’impatto del coupon sull’acquisizione e la fidelizzazione dei clienti.
exl-id: b0619365-fa75-49b5-a393-87f3364a390f
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '1392'
ht-degree: 2%

---

# Impatto coupon

L’analisi del modo in cui i clienti utilizzano i tuoi coupon può fornire informazioni significative sulla tua attività. In particolare, analizzare come acquisire e mantenere i clienti tramite coupon. In questo articolo, esploriamo le analisi che possono aiutarti a rispondere ai seguenti tipi di domande:

* Quanti clienti acquisisci tramite coupon?
* I clienti con coupon acquisiti hanno maggiori probabilità di effettuare acquisti ripetuti rispetto ai clienti non acquisiti tramite coupon?
* In che modo i ricavi a vita media differiscono tra i clienti acquistati con coupon e i clienti non acquisiti tramite coupon?
* I clienti acquisiti da coupon effettuano acquisti ripetuti con coupon?

Per rispondere a queste domande ci concentriamo su [confronto tra clienti acquistati con cedole e clienti acquisiti con non coupon](#compare), [analisi dei dettagli del primo ordine dalle acquisizioni di cedole](#firstorder)e [gli attributi dei clienti che utilizzano i coupon nel loro primo ordine.](#attributes)

Cominciamo!

## Confronto tra i clienti acquistati con cedole e i clienti non acquistati con coupon {#compare}

Durante la creazione di analisi che esplorano l’acquisizione e la fidelizzazione dei coupon, considera l’utilizzo delle metriche seguenti:

### Numero di nuovi clienti

Questa metrica mostra il numero di clienti acquistati con coupon e di clienti acquisiti con non coupon in tutto il tempo. Questo può aiutarti a determinare il rapporto tra le acquisizioni dei clienti tramite coupon.

### Ricavi a vita media

Questa metrica mostra i ricavi medi del ciclo di vita dei clienti acquistati con coupon e senza coupon. Questo può aiutare a determinare se il valore del ciclo di vita di un cliente varia a seconda del tipo di acquisizione.

### Numero di ordini ripetuti

Questa metrica mostra il numero di ordini ripetuti effettuati da entrambi i tipi di acquisizioni dei clienti. Questo può aiutare a determinare se più ordini di follow-up sono effettuati da clienti acquistati o non coupon acquisiti.

### Numero e percentuale di ordini ripetuti con coupon

Mostra il numero di ordini ripetuti effettuati con un coupon applicato e la percentuale di ordini ripetuti effettuati con un coupon. Questo può aiutare a determinare se i clienti con coupon acquistati tendono a fare più ordini con un coupon rispetto ai clienti non coupon acquisiti e se i clienti con coupon acquisiti sono in modo sproporzionato utilizzando i coupon nei loro ordini di follow-up.

Vediamo alcuni dati di esempio per le metriche di acquisizione con coupon rispetto a quelle senza coupon:

| **Acquisizione da clienti** | **Numero di nuovi clienti** | **Ricavi a vita media** | **Numero di ordini ripetuti** | **Numero di ordini ripetuti con coupon** | **% di ordini ripetuti con cedola** |
|-----|-----|-----|-----|-----|-----|
| Coupon | 1,206 | $356.91 | 2,570 | 1,248 | 48.56% |
| Non coupon | 11,561 | $498.30 | 20,145 | 3,251 | 16.14% |

{style=&quot;table-layout:auto&quot;}

Cosa possiamo togliere da questo? Diamo un&#39;occhiata:

### Numero di nuovi clienti

Nell&#39;esempio precedente, vi è un numero molto più elevato di acquisizioni non coupon rispetto alle acquisizioni di cedole. Tuttavia, ci sono ancora 1.206 clienti acquistati tramite un coupon che altrimenti non sarebbero diventati clienti.

### Ricavi a vita media

In questo esempio, le acquisizioni non cedole hanno un ricavo medio più elevato rispetto alle acquisizioni di cedole. Ciò implica che le acquisizioni non coupon stanno effettuando acquisti ripetuti e/o stanno effettuando acquisti di valore più elevato.

### Numero di ordini ripetuti

Il numero di ordini ripetuti per acquisizioni non coupon è molto più elevato delle acquisizioni di cedole. Questo è previsto perché ci sono molti più clienti non coupon acquisiti.

### Numero di ordini ripetuti con coupon

Analogamente, il numero di ordini ripetuti effettuati con cedola è più elevato per le acquisizioni non coupon.

## #Percent of repeat order with coupon

I clienti non coupon acquisiti hanno una percentuale molto inferiore di ordini ripetuti con un coupon applicato rispetto ai clienti coupon acquisiti. Pertanto, per i clienti con cedola acquistata, quasi uno su due ordini ripetuti ha un coupon applicato. In questo esempio, i clienti con coupon acquistati tendono ad effettuare acquisti ripetuti con coupon.

## Analisi dei dettagli del primo ordine da acquisizioni di cedole {#firstorder}

In questa sezione ci concentriamo solo su **primi ordini da acquisizioni di cedole, segmentati per cedola.** utilizziamo queste metriche nella nostra analisi:

### Numero di ordini/clienti

Questa metrica mostra il numero di primi ordini per ogni coupon, o il numero di clienti che hanno utilizzato il coupon nel loro primo ordine. Questo può aiutare a determinare se una certa cedola incoraggia più acquisti di altri coupon prima volta.

### Entrate lorde

Questa metrica rivela i ricavi che ottieni da un particolare coupon utilizzato nel primo ordine di un cliente. Questo ricavo è un calcolo degli articoli venduti prima dell&#39;applicazione di eventuali sconti.

### Sconti dai coupon

Questa metrica mostra l’importo totale dello sconto applicato dai coupon.

### Entrate nette

Questa metrica rivela i ricavi che ottieni da un particolare coupon utilizzato nel primo ordine di un cliente. Questo ricavo è un calcolo degli articoli venduti dopo l&#39;applicazione di tutti gli sconti. è importante notare che le entrate nette potrebbero non essersi verificate senza i coupon.

### Valore medio dell&#39;ordine

Questa metrica rivela il valore medio dell’ordine per una particolare cedola.

### Numero medio di ordini nel ciclo di vita

Questa metrica consente di valutare la fedeltà e il numero medio di ordini generati dai clienti che utilizzano un certo coupon.

### Ricavi a vita media

Questa metrica aiuta a valutare la fedeltà e i ricavi medi generati dai clienti che utilizzano un certo coupon. Quando si valuta se i clienti che utilizzano i coupon hanno un valore superiore rispetto agli altri, è necessario tenere conto del numero di ordini in cui ogni coupon è stato utilizzato per assicurarsi di avere una dimensione significativa del campione.

Ora, vediamo un esempio che coinvolge tre diversi coupon utilizzati per il primo ordine dei clienti:

| **Coupon** | **Primi ordini (FTO)** | **Entrate lorde provenienti da FTO** | **Sconti applicati a FTO** | **Entrate nette da FTO** | **Valore medio dell&#39;ordine per FTO** |
|-----|-----|-----|-----|-----|-----|
| **25% di sconto su $100 o più** | 56 | $8,531.04 | $2,132.76 | $6,398.28 | $152.34 |
| **Sconto di 10 $** | 87 | $3,707.07 | $426.10 | $3,280.97 | $42.61 |
| **Sconto del 20%** | 145 | $10,975.05 | $2,195.01 | $8,780.04 | $75.69 |

{style=&quot;table-layout:auto&quot;}

Cosa possiamo togliere da questo? Primo, il coupon &quot;20% di sconto&quot; aveva il maggior numero di ordini prima volta. Tuttavia, il numero di ordini associati a ciascuna cedola può variare in base a diversi fattori, tra cui:

* l&#39;importo della pubblicità per ogni coupon.
* il periodo di tempo per il quale sono stati offerti i coupon.
* l&#39;ora del giorno/settimana/mese/anno i coupon sono stati offerti.
* la stagione i coupon sono stati offerti, a seconda del business.

   **Esempio:** il coupon &quot;20% di sconto&quot; è stato offerto durante i mesi estivi, ma l&#39;azienda vende abbigliamento invernale.
* le restrizioni sui coupon.

   **Esempio:** il coupon &quot;10% off&quot; è offerto solo ai clienti che acquistano un cappotto invernale nello stesso ordine.

La **entrate lorde** per il coupon &quot;25% di sconto di $100 o più&quot; è molto più alto del ricavo lordo per il coupon &quot;$10 off&quot;. Tuttavia, il coupon &quot;$10 off&quot; ha un molto più grande **numero di ordini**. Analisi delle **valore medio dell&#39;ordine** fornisce informazioni approfondite su queste differenze: anche se il coupon &quot;25% di sconto di $100 o più&quot; aveva un numero inferiore di ordini, il valore medio dell&#39;ordine è superiore al triplo di quello del coupon &quot;$10 off&quot;. Pertanto, un ricavo lordo più ampio è attribuito alla cedola &quot;25% di sconto di $100 o più&quot;.

La **sconti** e **entrate nette** per i coupon &quot;25% di sconto di $100 o più&quot; e &quot;20% di sconto&quot; sono di valore prossimo. Anche se il valore medio dell&#39;ordine per &quot;25% di sconto di $100 o più&quot; è vicino al doppio del valore medio dell&#39;ordine per &quot;20% di sconto&quot;, quest&#39;ultima cedola ha un po&#39; meno del triplo del numero di ordini.

## Attributi dei clienti che utilizzano i coupon nel loro primo ordine {#attributes}

Ora che abbiamo esaminato gli ordini stessi, diamo un&#39;occhiata ai clienti che usano i coupon nei loro primi ordini:

| **Coupon del primo ordine del cliente** | **Numero di clienti** | **Numero medio di ordini nel ciclo di vita** | **Ricavi a vita media** |
|-----|-----|-----|-----|
| **25% di sconto su $100 o più** | 56 | 2.8 | $554.54 |
| **Sconto di 10 $** | 87 | 1.9 | $115.50 |
| **Sconto del 20%** | 145 | 1.3 | $103.75 |

{style=&quot;table-layout:auto&quot;}

noterai che il numero dei primi ordini è lo stesso del numero di clienti per ogni coupon. Questo ha senso perché ogni cliente può avere un solo primo ordine.

Il maggior numero di clienti è stato acquistato con il buono sconto del 20%. Tuttavia, questi clienti hanno il minimo **numero medio di ordini** e **ricavo medio della vita**; in genere, la maggior parte dei clienti con coupon acquisiti non effettua ordini ripetuti. Inoltre, i clienti acquisiti attraverso il &quot;25% di sconto di $100 o più&quot; coupon drive più alto **numero medio di ordini** e, a sua volta, più **ricavo medio della vita**. Generalmente, gli utenti che sono stati acquisiti tramite questo coupon di solito torna e fare più acquisti ripetuti.

## Ritorno a capo {#wrapup}

È possibile creare una moltitudine di analisi per comprendere meglio come i clienti utilizzano i coupon. Hai mai pensato di analizzare come i tuoi clienti utilizzano i tuoi coupon o il tempo necessario per utilizzare i coupon? Cosa dire del trovare l&#39;importo di sconto ottimale - quale importo incoraggia gli acquirenti ripetuti, valore medio più alto dell&#39;ordine e ricavi a vita più elevati? Per assistenza con questi tipi di domande, [contattare il supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
