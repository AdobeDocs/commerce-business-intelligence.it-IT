---
title: Analisi dell’utilizzo dei coupon
description: Scopri come analizzare l’utilizzo dei coupon per l’acquisizione e la fidelizzazione dei clienti.
exl-id: d4d1393f-1695-43f2-980a-84525f84031e
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 2%

---

# Utilizzo coupon

Vi siete mai chiesti in che modo l&#39;offerta di coupon influisce sulla vostra attività? Vuoi sapere quali coupon aiutano o danneggiano le prestazioni? Questo argomento illustra le analisi che consentono di ottenere un quadro completo dell&#39;utilizzo dei coupon da parte dei clienti, rispondendo alle seguenti domande:

* Quanti clienti utilizzano i coupon?
* Quanti coupon vengono utilizzati?
* Qual è il vostro fatturato prima e dopo l&#39;applicazione dei coupon?
* Qual è il valore medio dell&#39;ordine prima e dopo l&#39;applicazione dei coupon?
* Che tipo di clienti ti attrae con i coupon?

## Metriche consigliate {#metrics}

Durante l’analisi dell’utilizzo dei coupon, considera l’utilizzo di ([o edificio](../../data-user/reports/ess-manage-data-metrics.md)) le metriche seguenti:

### Numero di ordini

Questa metrica mostra il numero di ordini con e senza coupon nel tempo. Questo mostra se e con quale frequenza i clienti utilizzano i coupon, e come questo cambia nel tempo.

### Entrate lorde

Questa metrica mostra i ricavi lordi che si ottengono dagli ordini che includono una particolare cedola. Le entrate lorde sono un calcolo del prezzo pieno degli articoli venduti, prima di eventuali sconti. Questo può aiutare a determinare quali coupon sono associati al ricavo lordo più alto e più basso.

### Sconti dai coupon

Questa metrica può mostrare l’importo totale dello sconto applicato dai coupon. È importante notare che questi ordini potrebbero non essersi verificati senza i coupon.

### Ricavi netti

Questa metrica mostra i ricavi netti ottenuti dagli ordini che includono un particolare coupon. Il reddito netto è un calcolo del prezzo degli articoli venduti dopo l&#39;applicazione di tutti gli sconti. Questo può aiutare a determinare quali coupon sono associati ai ricavi netti più alti e più bassi.

### Percentuale scontata

Questa mostra la quota di reddito lordo che viene compensata dagli sconti. Per i coupon che offrono uno sconto percentuale, questo valore è già noto (ad esempio, uno sconto del 10%). Nonostante ciò, questa misura fornisce informazioni approfondite e un metodo di confronto per le cedole che sono uno sconto fisso in dollari.

### Valore medio netto dell&#39;ordine

Questa misura mostra il valore medio dell&#39;ordine quando viene applicato un coupon. Puoi verificare se gli ordini con coupon hanno sempre un valore inferiore rispetto agli ordini senza coupon.

### Sconto medio su ordine

Questo mostra il valore medio in dollari scontato da ogni ordine in cui vengono applicati i coupon. In questo modo viene visualizzata la differenza tra il valore medio netto dell&#39;ordine e il valore medio lordo dell&#39;ordine.

### Acquirenti diversi

Questa metrica mostra il numero di acquirenti distinti che utilizzano un determinato coupon.

### Ricavi medi nel ciclo di vita

Questa metrica consente di valutare la fedeltà e i ricavi medi generati dai clienti che utilizzano un determinato coupon. Quando valuti se i clienti che utilizzano i coupon hanno un valore più alto rispetto ad altri, assicurati di tenere conto del numero di acquirenti distinti in ogni categoria per assicurarti di avere una dimensione campione significativa.

## Esempio {#example}

Ora che sai quali metriche esaminare, prendi un esempio che coinvolge tre diversi coupon: 10% di sconto, 20 dollari di sconto, 100 o più e 10 dollari di sconto.

| **Coupon** | **N. di ordini** | **Entrate lorde** | **Sconti lordi da cedole** | **Ricavi netti** | **Percentuale scontata** |
|-----|-----|-----|-----|-----|-----|
| **Sconto del 10%** | 79 | $19,757.02 | $1,975.70 | $17,781.32 | 10.00% |
| **$20 di sconto $100+** | 101 | $13,928.91 | $2,020.00 | $11,908.91 | 14.50% |
| **$10 di sconto** | 201 | $14,542.35 | $2,010.00 | $12,532.35 | 13.82% |

{style="table-layout:auto"}


| **Coupon** | **Media valore netto dell’ordine** | **Media sconto ordine** | **Acquirenti diversi** | **Media ricavi ciclo di vita** |
|-----|-----|-----|-----|-----|
| **Sconto del 10%** | $225.08 | $25.01 | 79 | $361.50 |
| **$20 di sconto $100+** | $117.91 | $20.00 | 95 | $218.76 |
| **$10 di sconto** | $62.35 | $10.00 | 199 | $84.27 |

{style="table-layout:auto"}

## Cosa puoi portare via da questo?

Circa 80 ordini sono stati effettuati con il coupon &quot;10% di sconto&quot;, 100 ordini con il coupon &quot;20 dollari di sconto di 100 dollari o più&quot; e 200 ordini con il coupon &quot;10 dollari di sconto&quot;. Il **numero di ordini** associato a ciascuna cedola può variare in base a diversi fattori, tra cui:

* il periodo di tempo per il quale i buoni sono stati offerti.
* l’ora del giorno/settimana/mese/anno in cui sono stati offerti i coupon.
* la stagione in cui sono stati offerti i coupon, a seconda dell&#39;azienda. Ad esempio:
* Il coupon &quot;10% di sconto&quot; è stato offerto durante i mesi estivi, ma l&#39;azienda vende abbigliamento invernale.

* le restrizioni sulle cedole. Ad esempio:
* Il coupon &quot;$10 off&quot; è offerto solo ai nuovi clienti.
* Il coupon &quot;10% di sconto&quot; è offerto solo ai clienti che acquistano un cappotto invernale nello stesso ordine.

* il comportamento d&#39;acquisto tipico del cliente.

Mentre il **sconti lordi** per tutti e tre i coupon sono simili (circa $ 2.000), il numero di ordini per ogni coupon è diverso. L&#39;analisi degli sconti per ordine consente di spiegare le ragioni di questi numeri contrastanti. Il coupon &quot;10% di sconto&quot; ha il minor numero di ordini, ma un **sconto medio ordine** di circa 25 dollari. Anche se questo coupon ha un basso numero di ordini, il suo alto valore di sconto medio fa sì che il suo importo di sconto lordo si avvicini a $ 2.000.

**Entrate lorde e nette** fornisci un’idea generale del valore completo degli ordini associati a ciascun coupon. Tuttavia, questo quadro generale non fornisce una comprensione dei diversi comportamenti correlati a ciascun coupon. Se si considera una base di ordine, è possibile notare che il coupon &quot;10% di sconto&quot; ha un valore elevato **ordine netto medio** valore, che a sua volta porta al suo elevato **ricavi netti**.

D&#39;altra parte, la cedola &quot;10% di sconto&quot; ha un valore di sconto medio alto ($25.01), ma il più basso **percentuale attualizzata**. Ciò ha senso quando si tiene conto del suo valore netto medio di ordine di $ 225,08. La cedola &quot;10% di sconto&quot; ha un piccolo sconto percentuale di un grande valore medio netto dell&#39;ordine, quindi lo sconto medio dell&#39;ordine è un grande importo.

Osserva la **acquirenti distinti** e **reddito medio nel ciclo di vita** per ogni cedola. Il coupon &quot;10% di sconto&quot; ha lo stesso numero di ordini come acquirenti distinti. Ciò potrebbe essere dovuto al fatto che ogni cliente è limitato a un solo coupon. D&#39;altra parte, i coupon da &quot;$20 off $100 o più&quot; e &quot;$10 off&quot; hanno meno acquirenti distinti rispetto al numero di ordini, il che implica che alcuni clienti hanno utilizzato questi coupon più volte.

Per i ricavi medi nel ciclo di vita, puoi notare che i ricavi medi nel ciclo di vita di ogni coupon sono superiori ai rispettivi **ordine netto medio** valore. Ciò implica che i clienti hanno effettuato acquisti ripetuti e/o che il loro valore dell’ordine era molto più alto del valore netto medio dell’ordine.

## Che altro posso analizzare? {#otheranalyses}

Le analisi menzionate in questo argomento possono fornirti informazioni utili su come i tuoi clienti utilizzano i coupon, ma sono disponibili molte altre analisi che ti consentono di approfondire un po’.

**Puoi analizzare le acquisizioni dei clienti dai coupon.**

Quali coupon incoraggiano i clienti a effettuare ordini? Questi coupon attirano acquirenti occasionali o incoraggiano la fedeltà dei clienti (in altre parole, clienti che effettuano acquisti ripetuti)?

**Puoi analizzare il tempo necessario ai clienti per utilizzare i coupon.**

I coupon vengono utilizzati il giorno in cui vengono rilasciati o trascorrono una settimana o due prima che la maggior parte dei clienti li utilizzi?

**Puoi scoprire l’importo dello sconto ottimale che aumenta la fedeltà dei clienti e il valore complessivo.**

Quale importo di sconto incoraggia gli acquirenti abituali, un valore medio più alto per l&#39;ordine e maggiori ricavi nel corso del ciclo di vita?

Le risposte a queste domande forniscono informazioni approfondite sui clienti, sul loro comportamento e sui coupon che forniscono il massimo valore alla tua attività.
