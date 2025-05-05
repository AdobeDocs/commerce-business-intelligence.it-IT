---
title: Analisi del comportamento di riacquisto del cliente
description: Scopri come analizzare il comportamento di riacquisto dei clienti.
exl-id: 62666d08-5240-4f19-bf8e-e5b2d79a25c4
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# Comportamento di riacquisto del cliente

Se offri più di un prodotto, probabilmente ti chiedi in che modo i clienti che acquistano un prodotto specifico si comportano in modo diverso nel tempo rispetto ad altri clienti. Questo argomento illustra le analisi che possono aiutarti a rispondere alle seguenti domande.

Tra i clienti che acquistano un *elemento specifico*,

* Qual è la probabilità che effettuino un altro acquisto?
* Quanto tempo ci vuole per effettuare un altro acquisto?
* Qual è il numero medio di ordini che i clienti effettuano a breve/lungo termine?
* Qual è il reddito medio generato dai clienti nel breve/lungo termine?

## Metriche consigliate

Durante la creazione di analisi delle attività di riacquisto dei clienti, Adobe consiglia di utilizzare le metriche seguenti:

### Probabilità di ripetizione ordine

Questa misura è definita come il numero totale di ordini ripetuti, espresso come percentuale del totale degli ordini. In altre parole, questa è la probabilità che un ordine sia seguito da un altro ordine. Questa misura identifica gli articoli che potrebbero indurre i clienti a tornare al negozio.

### Numero medio di ordini effettuati

Questo mostra il comportamento di acquisto dei tuoi clienti, in particolare quanti ordini hanno effettuato i tuoi clienti in un dato periodo di tempo. Puoi scegliere di limitare questa misura per vedere il comportamento dei clienti a breve, medio o lungo termine. Alcuni prodotti possono incoraggiare i clienti ad effettuare acquisti frequenti nel breve termine, mentre altri possono influenzare la fedeltà a lungo termine di un cliente. Se questo numero è superiore per un articolo rispetto ad altri, ciò potrebbe indicare che le persone che acquistano questo articolo sono quelle che tornano al tuo negozio.

### Ricavi medi del ciclo di vita del cliente

Questa metrica consente di capire se i clienti che acquistano articoli specifici hanno più valore nel corso della loro vita. Se questo numero è più alto per un articolo rispetto ad altri articoli con prezzi simili, questo suggerirebbe che i clienti di valore più alto tendono ad acquistare questo articolo.

### Tempo all&#39;ordine successivo

Questa misura mostra la frequenza di ordinazione del cliente o il tempo necessario affinché il cliente riordini. Se il tempo per l&#39;ordine successivo è più breve per un articolo rispetto ad altri, questo suggerirebbe che le persone che acquistano questo articolo tendono a tornare prima.

## Esempio attuale: prodotti a base di caffè

Tenendo conto delle metriche di cui sopra, osserva un esempio che coinvolge prodotti a base di caffè.

| **Nome prodotto** | **Probabilità di ripetizione ordine** | **Numero medio di ordini nel ciclo di vita** | **Ricavi medi nel ciclo di vita** | **Tempo mediano all&#39;ordine successivo** |
|-----|-----|-----|-----|-----|
| Produttore di caffè monodose | 94,98% | 7,92 | 549,82 $ | 57,01 giorni |
| Capsule di caffè | 93,82% | 8,68 | 479,98 $ | 63,48 giorni |
| Semi di caffè | 41,92% | 6,07 | 99,82 $ | 27,31 giorni |

{style="table-layout:auto"}

Ora che disponi dei tuoi dati, cosa significa questo per ciascuna delle tue metriche?

### Probabilità di ripetizione ordine

In questo esempio, la probabilità di ripetizione dell’ordine - o la probabilità che un ordine sia seguito da un altro - è molto più elevata per i caffè e le capsule di caffè monodose rispetto ai chicchi di caffè.

Dal momento che i clienti che acquistano il produttore si sono &quot;impegnati&quot; ad acquistare le capsule associate in futuro, questo ha senso. Analogamente, i clienti che hanno acquistato le capsule hanno un produttore di birra compatibile con le capsule. Tuttavia, i chicchi di caffè non sono specifici per qualsiasi produttore particolare.

### Numero medio di ordini nel ciclo di vita

Sulla base dei dati di cui sopra, puoi vedere che le persone che acquistano il produttore di birra o le capsule hanno fatto più acquisti nel corso della loro vita, in media, rispetto ai clienti che hanno acquistato chicchi di caffè.

### Ricavi medi del ciclo di vita del cliente

I clienti che acquistano il produttore di birra ottengono i maggiori ricavi medi nel corso della vita, il che è logico, dato che il costo del produttore è incluso in questa misura. Al contrario, i clienti che acquistano chicchi di caffè in genere acquistano solo articoli a basso costo.

### Tempo all&#39;ordine successivo

Tra i clienti che hanno acquistato capsule di caffè, la metà fare un ordine ripetuto in circa due mesi. Tuttavia, tra i clienti che hanno acquistato chicchi di caffè, metà fanno un ordine ripetuto in circa un mese. Ciò potrebbe essere dovuto al fatto che le persone che ordinano le capsule (1) non bevono molto caffè o (2) effettuano gli ordini alla rinfusa (ad esempio, acquistando due mesi di caffè in un ordine).

## Quali altre analisi posso creare?

Utilizzando le metriche descritte in questo argomento, puoi anche creare altre utili analisi di riacquisto. Ad esempio, puoi anche vedere in che modo i clienti riacquistano **lo stesso articolo**, ad esempio se acquistano regolarmente le ricariche. Le capsule e i chicchi di caffè possono essere riacquistati regolarmente, ma sarebbe inaspettato vedere i clienti fare acquisti ripetuti della caffettiera. Questa analisi è utile se l&#39;azienda si concentra sulla ricarica o sul ripopolamento.

Oltre ad analizzare il comportamento di riacquisto dei clienti, puoi anche creare analisi che considerano la loro fedeltà. Valuta l’analisi dei pattern di customer churn: dove sono i clienti che lasciano il tuo sito e non tornano? A che velocità si verifica?

Dopo aver identificato il motivo dell&#39;abbandono, è possibile utilizzare l&#39;analisi per creare una campagna `reactivation`. Utilizzando questi dati, puoi identificare gli utenti che non sono più attivi, il periodo di tempo trascorso dall’ultima visita, l’ultimo acquisto e così via. Questo consente di prendere decisioni fruibili che incitano i clienti a tornare.

Per assistenza sull&#39;analisi, [contatta il supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=it).
