---
title: Analisi del comportamento di riacquisto del cliente
description: Scopri come analizzare il comportamento del cliente nel reacquisto.
exl-id: 62666d08-5240-4f19-bf8e-e5b2d79a25c4
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 0%

---

# Comportamento di riacquisto del cliente

Se offri più di un prodotto, probabilmente ti chiedi in che modo i clienti che acquistano un prodotto specifico si comportano in modo diverso nel tempo rispetto ad altri clienti. In questo articolo, esploriamo le analisi che possono aiutarti a rispondere alle seguenti domande:

Tra i clienti che acquistano un *elemento specifico*,

* Qual è la probabilità che effettuino un altro acquisto?
* Quanto tempo ci vorrà per fare un altro acquisto?
* Qual è il numero medio di ordini che i clienti inseriscono nel breve/lungo periodo?
* Qual è il fatturato medio generato dai clienti nel breve/lungo periodo?

## Metriche consigliate

Quando si creano le analisi delle attività di riacquisto dei clienti, è consigliabile utilizzare le metriche seguenti:

### Probabilità ordine di ripetizione

Questa misura è definita come il numero totale di ordini ripetuti, in percentuale degli ordini totali. In altre parole, questa è la probabilità che un ordine venga seguito da un altro ordine. Questa misura identifica gli elementi che potrebbero indurre i clienti a tornare al tuo negozio.

### Numero medio di ordini inseriti

Questo espone il comportamento di acquisto dei clienti, in particolare quanti ordini i clienti hanno effettuato in un determinato periodo di tempo. Puoi scegliere di limitare questa misura per visualizzare il comportamento dei clienti a breve, medio o lungo termine. Alcuni prodotti possono incoraggiare i clienti ad effettuare acquisti frequenti nel breve periodo, mentre altri possono influenzare la fidelizzazione a lungo termine di un cliente. Se questo numero è più alto per un articolo rispetto ad altri, questo suggerirebbe che le persone che acquistano questo articolo sono quelle che ritornano al tuo negozio.

### Ricavo medio della vita del cliente

Questa metrica ti consente di capire se i clienti che acquistano articoli specifici hanno più valore nel corso della loro vita. Se questo numero è più alto per un articolo rispetto ad altri articoli a prezzi simili, ciò suggerirebbe che i clienti di maggior valore tendono ad acquistare questo articolo.

### Ora dell’ordine successivo

Questa misura mostra la frequenza di ordinazione del cliente o il tempo necessario al cliente per effettuare nuovamente l&#39;ordine. Se l&#39;orario per l&#39;ordine successivo è più breve per un articolo rispetto ad altri, ciò suggerirebbe che le persone che acquistano questo articolo tendono a tornare prima.

## Esempio di oggi: prodotti a base di caffè

Tenendo presenti le metriche precedenti, diamo un&#39;occhiata a un esempio che coinvolge i prodotti per il caffè.

| **Nome del prodotto** | **Probabilità ordine di ripetizione** | **Numero medio di ordini nel ciclo di vita** | **Ricavi in media a vita** | **Tempo medio in ordine successivo** |
|-----|-----|-----|-----|-----|
| Frigorifero da caffè a tazza singola | 94,98% | 7,92 | $549,82 | 57,01 giorni |
| Capsule di caffè | 93,82% | 8,68 | $479,98 | 63,48 giorni |
| Fagioli di caffè | 41,92% | 6,07 | $ 99,82 | 27,31 giorni |

{style=&quot;table-layout:auto&quot;}

Ora che abbiamo i nostri dati, diamo un&#39;occhiata a cosa potrebbe significare questo per ciascuna delle nostre metriche.

### Probabilità ordine di ripetizione

In questo esempio, la probabilità di ripetizione dell&#39;ordine - o la probabilità che un ordine sarà seguito da un altro ordine - è molto più alta per i produttori di caffè a tazza singola e le capsule di caffè che per i chicchi di caffè.

Dal momento che i clienti che acquistano il birrificio sono &quot;impegnati&quot; ad acquistare le capsule associate in futuro, questo ha senso. Allo stesso modo, i clienti che hanno acquistato le capsule hanno un birrificio compatibile con le capsule. Tuttavia, i chicchi di caffè non sono specifici per un particolare birrificio.

### Numero medio di ordini nel ciclo di vita

Sulla base dei dati di cui sopra, possiamo vedere che le persone che acquistano il birrificio o le capsule hanno fatto più acquisti nella loro vita, in media, rispetto ai clienti che hanno acquistato chicchi di caffè.

### Ricavo medio della vita del cliente

I clienti che acquistano il birrificio hanno i ricavi medi più elevati per tutta la vita; che ha senso, dato che il costo del birrificio è incluso in questa misura. Al contrario, i clienti che acquistano chicchi di caffè in genere acquistano solo articoli a basso costo.

### Ora dell’ordine successivo

Tra i clienti che hanno acquistato capsule di caffè, metà fare un ordine ripetuto in circa 2 mesi. Tuttavia, tra i clienti che hanno acquistato chicchi di caffè, metà fare un ordine ripetuto in circa 1 mese. Questo potrebbe essere perché le persone che ordinano capsule o (1) non bevono tanto caffè, o (2) fanno ordini in massa (per esempio, l&#39;acquisto di 2 mesi di caffè in un ordine).

## Quali altre analisi posso creare?

Utilizzando le metriche descritte in questo articolo, puoi anche creare altre utili analisi di riacquisto. Ad esempio, possiamo anche vedere in che modo i clienti riacquistano **stesso elemento** - ad esempio, se acquistano le ricariche regolarmente. Capsule e chicchi di caffè possono essere riacquistati regolarmente, ma sarebbe inaspettato vedere i clienti che fanno acquisti ripetuti del distributore di caffè. Se la tua attività si concentra su ricariche o ripopolamenti, questa analisi sarebbe estremamente utile.

Oltre ad analizzare il comportamento di riacquisto dei clienti, puoi anche creare analisi che tengano conto della fidelizzazione dei clienti. Valuta la possibilità di analizzare i pattern di abbandono dei clienti: dove si trovano i clienti che abbandonano il sito e non tornano? A che velocità sta avvenendo?

Una volta identificato il motivo per cui si verifica un’abbandono, puoi utilizzare l’analisi per creare un `reactivation` campagna. Utilizzando questi dati, puoi identificare gli utenti che sono diventati inattivi, quanto tempo è trascorso dalla loro ultima visita, qual è stato il loro ultimo acquisto e così via. Questo ti consentirà di prendere decisioni actionable che incoraggeranno i tuoi clienti a tornare.

Per informazioni sull’analisi, [contattare il supporto](../../guide-overview.md).
