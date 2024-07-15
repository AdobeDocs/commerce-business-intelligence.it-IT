---
title: Analisi dell’impatto dei coupon
description: Scopri come analizzare l’impatto dei coupon sull’acquisizione e la fidelizzazione dei clienti.
exl-id: b0619365-fa75-49b5-a393-87f3364a390f
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 1%

---

# Impatto coupon

L’analisi del modo in cui i clienti utilizzano i coupon può fornire informazioni significative sulla tua attività. In particolare, analizzando come acquisire e fidelizzare i clienti tramite coupon. In questo argomento vengono illustrate le analisi che consentono di rispondere ai seguenti tipi di domande:

* Quanti clienti acquisisci tramite coupon?
* I clienti acquisiti con coupon hanno più probabilità di effettuare acquisti ripetuti rispetto ai clienti non acquisiti con coupon?
* In che modo i ricavi medi nel ciclo di vita differiscono tra i clienti acquisiti con coupon e i clienti non acquisiti con coupon?
* I clienti acquisiti da coupon effettuano acquisti ripetuti con coupon?

Rispondi a queste domande concentrandoti su [confronto tra clienti acquisiti con coupon e clienti non acquisiti con coupon](#compare), [analisi dei dettagli del primo ordine da acquisizioni con coupon](#firstorder) e [analisi degli attributi dei clienti che utilizzano i coupon nel primo ordine.](#attributes)

Inizia.

## Confronto tra clienti acquisiti con cedola e clienti acquisiti senza cedola {#compare}

Quando crei analisi che esplorano l’acquisizione e la conservazione dei coupon, considera l’utilizzo delle metriche seguenti:

### Numero di nuovi clienti

Questa metrica mostra il numero di clienti acquisiti con coupon e di clienti non acquisiti con coupon in tutto il tempo. Questo può aiutarti a determinare il rapporto di acquisizioni dei clienti tramite coupon.

### Ricavi medi nel ciclo di vita

Questa metrica mostra i ricavi medi generati da clienti acquisiti con cedola e senza cedola nel corso del ciclo di vita. Questo può aiutare a determinare se il valore del ciclo di vita di un cliente varia a seconda del tipo di acquisizione.

### Numero di ordini ripetuti

Questa metrica mostra il numero di ordini ripetuti effettuati da entrambi i tipi di acquisizioni cliente. Questo può aiutare a determinare se più ordini di follow-up sono effettuati da clienti acquisiti con coupon o non acquistati con coupon.

### Numero e percentuale di ordini ripetuti con coupon

Mostra il numero di ordini ripetuti eseguiti con un coupon applicato e la percentuale di ordini ripetuti con un coupon. Questo può aiutarti a determinare se i clienti acquisiti con coupon tendono ad effettuare più ordini ripetuti con un coupon rispetto ai clienti acquisiti senza coupon e se i clienti acquisiti con coupon utilizzano in modo sproporzionato i coupon nei loro ordini di follow-up.

Osserva alcuni dati di esempio per le metriche di acquisizione di cedole e non cedole:

| **Acquisizione cliente** | **Numero di nuovi clienti** | **Ricavi medi nel corso della vita** | **Numero di ordini ripetuti** | **Numero di ordini ripetuti con coupon** | **% di ordini ripetuti con coupon** |
|-----|-----|-----|-----|-----|-----|
| Coupon | 1.206 | 356,91 $ | 2.570 | 1.248 | 48,56% |
| Non cedola | 11.561 | 498,30 $ | 20.145 | 3.251 | 16,14% |

{style="table-layout:auto"}

Osserva cosa puoi portare con te:

### Numero di nuovi clienti

Nell’esempio precedente, vi è un numero molto maggiore di acquisizioni senza cedola rispetto alle acquisizioni con cedola. Tuttavia, ci sono ancora 1.206 clienti acquisiti tramite un coupon che altrimenti potrebbero non essere diventati clienti.

### Ricavi medi nel ciclo di vita

In questo esempio, le acquisizioni senza cedola hanno un ricavo medio nel ciclo di vita più elevato rispetto alle acquisizioni con cedola. Ciò implica che le acquisizioni senza cedola stanno effettuando più acquisti ripetuti e/o stanno effettuando acquisti di valore più elevato.

### Numero di ordini ripetuti

Il numero di ordini ripetuti per le acquisizioni senza cedola è molto più elevato delle acquisizioni con cedola. Questo è previsto perché ci sono molti più clienti acquisiti non coupon.

### Numero di ordini ripetuti con coupon

Analogamente, il numero di ordini ripetuti con una cedola è più elevato per le acquisizioni non cedolare.

## Percentuale di ordini ripetuti con coupon

I clienti acquisiti senza cedola hanno una percentuale molto inferiore di ordini ripetuti con una cedola applicata rispetto ai clienti acquisiti con cedola. Pertanto, per i clienti acquisiti con coupon, quasi la metà degli ordini ripetuti ha un coupon applicato. In questo esempio, i clienti con coupon acquistati tendono a effettuare acquisti ripetuti con coupon.

## Analisi dei dettagli del primo ordine dalle acquisizioni di coupon {#firstorder}

Questa sezione si concentra solo su **primi ordini da acquisizioni di cedole, segmentati per cedola.** Utilizza queste metriche nell&#39;analisi:

### Numero di ordini/clienti

Questa metrica mostra il numero di ordini di prima volta per ogni coupon o il numero di clienti che hanno utilizzato quel coupon nel loro primo ordine. Questo può aiutare a determinare se un determinato coupon incoraggia più nuovi acquisti rispetto ad altri coupon.

### Entrate lorde

Questa metrica rivela i ricavi ottenuti da un particolare coupon utilizzato nel primo ordine di un cliente. Questi ricavi sono un calcolo degli articoli venduti prima dell&#39;applicazione di eventuali sconti.

### Sconti dai coupon

Questa metrica mostra l’importo totale dello sconto applicato dai coupon.

### Ricavi netti

Questa metrica rivela i ricavi ottenuti da un particolare coupon utilizzato nel primo ordine di un cliente. Questo ricavo è un calcolo degli articoli venduti dopo l&#39;applicazione di tutti gli sconti. È importante notare che il reddito netto potrebbe non essersi verificato senza le cedole.

### Valore medio dell’ordine

Questa metrica mostra il valore medio dell’ordine per una particolare cedola.

### Numero medio di ordini nel ciclo di vita

Questa metrica consente di valutare la fedeltà e il numero medio di ordini generati dai clienti che utilizzano un determinato coupon.

### Ricavi medi nel ciclo di vita

Questa metrica consente di valutare la fedeltà e i ricavi medi generati dai clienti che utilizzano un determinato coupon. Nel valutare se i clienti che utilizzano i coupon hanno un valore superiore rispetto ad altri, assicurati di tenere conto del numero di ordini in cui è stato utilizzato ogni coupon per garantire una dimensione campione significativa.

Ora, guarda un esempio che coinvolge tre diversi coupon utilizzati per il primo ordine dei clienti:

| **Coupon** | **Nuovi ordini (FTO)** | **Ricavi lordi da FTO** | **Sconti applicati a FTO** | **Entrate nette da FTO** | **Valore medio ordine per FTO** |
|-----|-----|-----|-----|-----|-----|
| **25% di sconto di $100 o più** | 56 | 8.531,04 $ | 2.132,76 $ | 6.398,28 $ | 152,34 $ |
| **$10 di sconto** | 87 | 3.707,07 $ | 426,10 $ | 3.280,97 $ | 42,61 $ |
| **20% di sconto** | 145 | 10.975,05 $ | 2.195,01 $ | 8.780,04 $ | 75,69 $ |

{style="table-layout:auto"}

Cosa si può ricavare da questo? In primo luogo, il coupon &quot;20% off&quot; ha avuto il maggior numero di ordini di prima volta. Tuttavia, il numero di ordini associati a ciascuna cedola può variare in base a diversi fattori, tra cui:

* l&#39;importo pubblicitario per ogni cedola.
* il periodo di tempo per il quale i buoni sono stati offerti.
* l’ora del giorno/settimana/mese/anno in cui sono stati offerti i coupon.
* la stagione in cui sono stati offerti i coupon, a seconda dell&#39;azienda.

  **Esempio:** il coupon &quot;20% di sconto&quot; è stato offerto durante i mesi estivi, ma l&#39;azienda vende abbigliamento invernale.
* le restrizioni sulle cedole.

  **Esempio:** il coupon &quot;10% di sconto&quot; è offerto solo ai clienti che acquistano un cappotto invernale nello stesso ordine.

Il **ricavo lordo** per la cedola &quot;25% di sconto di 100 o più dollari&quot; è molto più alto del ricavo lordo per la cedola &quot;10 dollari di sconto&quot;. Tuttavia, il coupon &quot;$10 off&quot; ha un **numero di ordini** molto più grande. L&#39;analisi del **valore medio dell&#39;ordine** fornisce informazioni approfondite su queste differenze. Anche se il coupon &quot;25% off $100 o più&quot; aveva un numero inferiore di ordini, il valore medio dell&#39;ordine è più del triplo rispetto al coupon &quot;off$10&quot;. Pertanto, un maggiore ricavo lordo è attribuito alla cedola &quot;25% off $100 o più&quot;.

I **sconti** e **ricavi netti** per i coupon &quot;25% di sconto pari o superiore a 100 dollari&quot; e &quot;20% di sconto&quot; hanno un valore vicino. Anche se il valore medio dell&#39;ordine per &quot;25% di sconto di $100 o più&quot; è vicino al doppio del valore medio dell&#39;ordine per &quot;20% di sconto&quot;, quest&#39;ultimo coupon ha un poco meno del triplo del numero di ordini.

## Attributi dei clienti che utilizzano i coupon per il primo ordine {#attributes}

Dopo aver esaminato gli ordini, esaminare i clienti che utilizzano i coupon nei loro primi ordini:

| **Buono sconto primo cliente** | **Numero di clienti** | **Numero medio di ordini nel ciclo di vita** | **Ricavi medi nel corso della vita** |
|-----|-----|-----|-----|
| **25% di sconto di $100 o più** | 56 | 2,8 | 554,54 $ |
| **$10 di sconto** | 87 | 1,9 | 115,50 $ |
| **20% di sconto** | 145 | 1,3 | 103,75 $ |

{style="table-layout:auto"}

Noterai che il numero di nuovi ordini corrisponde al numero di clienti per ogni coupon. Questo è utile perché ogni cliente può avere un solo primo ordine.

Il maggior numero di clienti è stato acquisito attraverso il coupon &quot;20% di sconto&quot;. Tuttavia, questi clienti hanno il **numero medio di ordini nel ciclo di vita** e il **reddito medio nel ciclo di vita** più basso; in genere, la maggior parte dei clienti acquisiti con coupon non effettua ordini ripetuti. Inoltre, i clienti hanno acquisito tramite l&#39;unità coupon &quot;25% off $100 o più&quot; un numero di ordini superiore a **numero di ordini con durata media** e, a sua volta, un numero superiore a **ricavi con durata media**. In genere, gli utenti che sono stati acquistati tramite questo coupon di solito tornano e fanno più acquisti ripetuti.

## Ritorno a capo {#wrapup}

Sono disponibili numerose analisi che puoi creare per comprendere meglio come i tuoi clienti utilizzano i coupon. Hai mai pensato di analizzare in che modo i tuoi clienti utilizzano i coupon o il tempo necessario per utilizzarli? E per quanto riguarda la ricerca dell&#39;importo di sconto ottimale: quale importo incoraggia gli acquirenti ripetuti, un valore medio più alto dell&#39;ordine e maggiori ricavi nel corso della vita? Per informazioni su questi tipi di domande, [contatta l&#39;assistenza](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
