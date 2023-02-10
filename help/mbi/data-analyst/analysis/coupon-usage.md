---
title: Analisi dell'utilizzo del coupon
description: Scopri come analizzare l’utilizzo dei coupon sull’acquisizione e la conservazione dei clienti.
exl-id: d4d1393f-1695-43f2-980a-84525f84031e
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 2%

---

# Utilizzo coupon

Vi siete mai chiesti come l&#39;offerta di coupon influenza il vostro business? Vuoi sapere quali coupon aiutano o danneggiano le prestazioni? In questo articolo, esploriamo le analisi che ti danno una buona immagine dell&#39;uso del coupon dei tuoi clienti rispondendo a queste domande:

* Quanti clienti stanno utilizzando dei coupon?
* Quanti coupon vengono utilizzati?
* Quali sono i ricavi prima e dopo l&#39;applicazione dei coupon?
* Qual è il valore medio dell&#39;ordine prima e dopo l&#39;applicazione dei coupon?
* Che tipo di clienti attrae con coupon?

Cominciamo!

## Metriche consigliate {#metrics}

Quando analizzi l&#39;utilizzo del coupon, considera l&#39;utilizzo di ([o edificio](../../data-user/reports/ess-manage-data-metrics.md)) queste metriche:

### Numero di ordini

Questa metrica mostra il numero di ordini con e senza coupon nel tempo. Questo mostra se e con quale frequenza i clienti utilizzano i tuoi coupon e come questo cambia nel tempo.

### Entrate lorde

Questa metrica rivela i ricavi lordi che ottieni dagli ordini che includono un particolare coupon. Il ricavo lordo è un calcolo dell&#39;intero prezzo degli articoli venduti, prima di applicare eventuali sconti. Questo può aiutare a determinare quali coupon sono associati al ricavo lordo più alto e più basso.

### Sconti dai coupon

Questa metrica può mostrare l’importo totale dello sconto applicato dai coupon. è importante notare che questi ordini potrebbero non essersi verificati senza i coupon.

### Entrate nette

Questa metrica mostra i ricavi netti ottenuti da ordini che includono un particolare coupon. Il ricavo netto è un calcolo del prezzo degli articoli venduti dopo l&#39;applicazione di tutti gli sconti. Questo può aiutare a determinare quali coupon sono associati ai ricavi netti più elevati e più bassi.

### Percentuale scontata

Mostra la quota dei ricavi lordi compensata da sconti. Per i coupon che offrono uno sconto percentuale, questo valore è già noto (ad esempio, 10% di sconto). Nonostante ciò, questa misura fornisce informazioni approfondite e un metodo di confronto per i coupon che sono uno sconto fisso in dollari.

### Valore medio netto dell’ordine

Questa misura mostra il valore medio dell&#39;ordine quando viene applicata una cedola. È possibile analizzare se gli ordini con coupon presentano in modo coerente un valore di ordine inferiore rispetto agli ordini senza coupon.

### Sconto medio degli ordini

Questo mostra il valore medio in dollari scontato da ogni ordine in cui vengono applicati i coupon. Viene visualizzata la differenza tra il valore medio netto dell&#39;ordine e il valore medio lordo dell&#39;ordine.

### Acquirenti distinti

Questa metrica mostra il numero di acquirenti distinti che utilizzano un certo coupon.

### Ricavi a vita media

Questa metrica aiuta a valutare la fedeltà e i ricavi medi generati dai clienti che utilizzano un certo coupon. Quando si valuta se i clienti che utilizzano i coupon hanno un valore superiore agli altri, è necessario tenere conto del numero di acquirenti distinti in ciascuna categoria per assicurarsi di disporre di un campione significativo.

## Esempio {#example}

Ora che sappiamo quali metriche esaminare, diamo un&#39;occhiata ad un esempio che coinvolge tre diversi coupon: uno sconto del 10%, uno sconto di 20 $ su 100 $ o più e uno sconto di 10 $.

| **Coupon** | **Numero di ordini** | **Entrate lorde** | **Sconti lordi da coupon** | **Entrate nette** | **Percentuale scontata** |
|-----|-----|-----|-----|-----|-----|
| **Sconto del 10%** | 79 | $19,757.02 | $1,975.70 | $17,781.32 | 10.00% |
| **$20 sconto $100+** | 101 | $13,928.91 | $2,020.00 | $11,908.91 | 14.50% |
| **Sconto di 10 $** | 201 | $14,542.35 | $2,010.00 | $12,532.35 | 13.82% |

{style=&quot;table-layout:auto&quot;}


| **Coupon** | **Media valore netto dell&#39;ordine** | **Media sconto ordine** | **Acquirenti distinti** | **Media ricavo a vita** |
|-----|-----|-----|-----|-----|
| **Sconto del 10%** | $225.08 | $25.01 | 79 | $361.50 |
| **$20 sconto $100+** | $117.91 | $20.00 | 95 | $218.76 |
| **Sconto di 10 $** | $62.35 | $10.00 | 199 | $84.27 |

{style=&quot;table-layout:auto&quot;}

## Cosa possiamo togliere da questo?

Circa 80 ordini sono stati effettuati con il coupon &quot;10% di sconto&quot;, 100 ordini con il coupon &quot;$20 off $100 o più&quot; e 200 ordini con il coupon &quot;$10 off&quot;. La **numero di ordini** associato a ciascuna cedola può variare in base a diversi fattori, tra cui:

* il periodo di tempo per il quale sono stati offerti i coupon.
* l&#39;ora del giorno/settimana/mese/anno i coupon sono stati offerti.
* la stagione i coupon sono stati offerti, a seconda del business. Ad esempio:
* Il coupon &quot;10% di sconto&quot; è stato offerto durante i mesi estivi, ma l&#39;azienda vende abbigliamento invernale.

* le restrizioni sui coupon. Ad esempio:
* Il coupon &quot;$10 off&quot; è offerto solo ai nuovi clienti.
* Il coupon &quot;10% off&quot; è offerto solo ai clienti che acquistano un cappotto invernale nello stesso ordine.

* il tipico comportamento di acquisto del cliente.

Mentre il **sconti lordi** per tutti e tre i coupon sono molto simili (circa $2.000), il numero di ordini per ogni coupon è significativamente diverso. L&#39;analisi degli sconti in base all&#39;ordine aiuta a spiegare le ragioni di questi numeri contrastanti. La cedola &quot;10% off&quot; ha il minor numero di ordini, ma **sconto ordine medio** di circa 25 dollari. Anche se questa cedola ha un numero basso di ordini, il suo alto valore medio di sconto fa sì che il suo importo lordo di sconto si avvicini a $2.000.

**Entrate lorde e nette** fornire un&#39;idea generale del valore completo degli ordini associati a ciascuna cedola. Tuttavia, questo quadro generale non fornisce una comprensione dei diversi comportamenti relativi a ciascun coupon. Una volta che si guarda una base per ordine, si può vedere che il coupon &quot;10% off&quot; ha un molto alto **ordine netto medio** che, a sua volta, porta al suo valore elevato **entrate nette**.

D&#39;altra parte, la cedola &quot;10% off&quot; ha un valore di sconto medio molto alto ($25,01), ma il più basso **percentuale scontata**. Questo ha senso quando si prende in considerazione il suo valore medio netto dell&#39;ordine di $225.08. Il coupon &quot;10% di sconto&quot; ha un piccolo sconto percentuale di un grande valore medio dell&#39;ordine netto, quindi lo sconto medio dell&#39;ordine è un grande importo.

Diamo un&#39;occhiata al **acquirenti distinti** e **ricavo medio della vita** per ogni coupon. La cedola &quot;10% di sconto&quot; ha lo stesso numero di ordini degli acquirenti distinti. Questo potrebbe essere il risultato del fatto che ogni cliente è limitato a un coupon. D&#39;altro canto, i coupon &quot;$20 off $100 o più&quot; e &quot;$10 off&quot; hanno meno acquirenti distinti rispetto al numero di ordini, il che implica che alcuni clienti hanno utilizzato questi coupon più volte.

Per i ricavi medi a vita, puoi vedere che il ricavo medio a vita per ogni coupon è maggiore del rispettivo **ordine netto medio** valore. Ciò implica che o i clienti hanno effettuato acquisti ripetuti e/o che il loro valore dell&#39;ordine è stato molto superiore al valore medio netto dell&#39;ordine.

## Che altro posso analizzare? {#otheranalyses}

Le analisi di cui abbiamo parlato in questo articolo possono fornire informazioni utili su come i tuoi clienti utilizzano i tuoi coupon, ma ci sono una moltitudine di altre analisi che ti permettono di approfondire un po&#39;.

**Puoi analizzare le acquisizioni dei tuoi clienti da coupon.**

Quali coupon incoraggiano i clienti ad effettuare ordini? Questi coupon attraggono acquirenti unici o incoraggiano la fedeltà dei clienti (in altre parole, clienti che effettuano acquisti ripetuti)?

**Puoi analizzare il tempo necessario ai tuoi clienti per utilizzare i tuoi coupon.**

I vostri coupon sono utilizzati il giorno in cui vengono rilasciati o trascorrono una settimana o due anni prima che la maggior parte dei vostri clienti li utilizzano?

**Puoi scoprire l’importo ottimale dello sconto che aumenta la fedeltà dei clienti e il valore complessivo.**

Quale importo di sconto incoraggerà gli acquirenti ripetuti, un valore medio più alto dell&#39;ordine e ricavi a vita più elevati?

La risposta a queste domande ti fornirà informazioni sui tuoi clienti, sul loro comportamento e sui coupon che forniscono il massimo valore alla tua attività.
