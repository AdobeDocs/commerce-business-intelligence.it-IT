---
title: Analisi per coorte di ricavi per ciclo di vita
description: Esplorare la potenza di [!DNL MBI] analisi per coorte.
exl-id: f2b55745-d364-4ba6-9857-ce9cee05c3ae
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 0%

---

# `Lifetime Revenue Cohort` Analisi

Ci sono molti modi diversi per guardare i tuoi dati in [!DNL MBI]E sappiamo che l&#39;interpretazione e la comprensione sono importanti quanto il calcolo e la visualizzazione. Questo articolo esplorerà il potere di [!DNL MBI] `cohort` analisi.

## Cosa fa? `lifetime revenue cohort` analisi?

Il grafico seguente mostra la spesa cumulativa per utente per un periodo di tempo dopo l’acquisizione. `Cohorts` Gli utenti sono suddivisi per il mese di acquisizione.

Ad esempio, la linea arancione sopra mostra la media per gli utenti acquisiti nel novembre 2011. Il primo punto dati indica che nel primo mese gli utenti acquisiti a novembre hanno speso in media circa `$200`. Il secondo punto dati significa che alla fine del secondo mese gli utenti avevano speso una media di circa `$240`. La loro spesa media nel mese due è stata approssimativamente `$40 (240 - 200)`. Le diverse righe rappresentano diverse coorti di utenti. La linea verde rappresenta gli utenti acquisiti in dicembre, mentre quella blu è un utente acquisito in ottobre.

## Perché questo è importante?

Questo tipo di `cohort` L’analisi può essere utile per diversi scopi, ma il vantaggio più immediato è spesso rappresentato da decisioni di acquisizione migliori per i clienti. Molte aziende limitano la spesa di marketing ai canali che producono redditività sul primo acquisto di un cliente. Queste società pagheranno per acquisire clienti attraverso un determinato canale a condizione che il loro rendimento medio di primo acquisto sia più elevato `gross margin` di quanto costi acquisirli.

Il problema di questo approccio è che spesso si traduce in un sottoinvestimento nella crescita. Se i tuoi concorrenti si basano su una comprensione più profonda del comportamento di acquisto, ti supereranno. La `lifetime revenue cohort` L’analisi ti aiuta a comprendere le conseguenze dell’aumento delle spese per l’acquisizione dei clienti e offre un modo semplice per trasmetterle al resto del team. Se i clienti futuri si comportano come clienti esistenti, l&#39;acquisizione di clienti per un CPA più elevato comporterà un periodo di rimborso prevedibile. A seconda della posizione di cassa dell&#39;azienda, è possibile definire con quale periodo di rimborso si è a proprio agio, trovare il punto pertinente sul grafico, e spendere di conseguenza.

Inoltre, puoi utilizzare questa analisi per vedere se stai migliorando l’onboarding, il coinvolgimento e la generazione di ricavi dagli utenti che acquisisci.  Ad esempio, questo `cohort` L&#39;analisi è un ottimo modo per vedere se una promozione di spedizione gratuita per i nuovi utenti ha portato a nuovi acquirenti o acquirenti unici che non ritornano mai.

## Quali sono le differenze tra i diversi modelli di business?

Per la maggior parte delle aziende, il `lifetime revenue cohort` il grafico di analisi mostrerà un elevato ammontare di spesa nel periodo iniziale e quindi aumenterà più lentamente nel tempo. Questo picco iniziale è dovuto al fatto che i clienti hanno più probabilità di effettuare il loro primo acquisto subito dopo l’acquisizione rispetto a qualsiasi altro momento. Nei casi in cui l&#39;evento di acquisizione stesso è un acquisto, il 100% dei clienti effettua un acquisto nel primo periodo. Nei casi in cui la registrazione può avvenire prima degli acquisti, questo effetto è meno drastico.

Ad esempio, [!DNL Groupon] avrebbe probabilmente un salto iniziale molto più basso di [!DNL Amazon], perché molte delle persone che si iscrivono [!DNL Groupon] non effettuare un acquisto immediatamente. A meno che non ci sia un elevato numero di rimborsi, questo grafico salirà verso l&#39;alto e verso destra dopo il salto iniziale. Il tasso di crescita tende a diminuire nel tempo perché i clienti sono solitamente più attivi quando si iscrivono per la prima volta. Questo fa sì che la media diminuisca perché il numero di persone nella coorte rimane costante, indipendentemente da quanti tornano a comprare di più. Nelle aziende di abbonamento, la pendenza diminuirà meno aggressivamente che nelle aziende in cui le persone effettuano acquisti una tantum.

A volte, un business di abbonamento avrà in realtà una pendenza che aumenta nel tempo. Raramente si vede, ma è un ottimo segnale per l&#39;azienda quando succede. Questo non significa che ci sono clienti senza fiato, ma piuttosto che gli aggiornamenti per i clienti che rimangono più che compensare i clienti che lasciano.

## Come viene calcolato?

Ci sono due semplici input per questo calcolo: quanti membri ci sono nel `cohort` (che non cambia mai) e quanti ricavi hanno generato i membri nel periodo specificato. Per determinare i membri nel `cohort`, contiamo il numero di utenti acquisiti nel periodo in questione. Un&#39;acquisizione può essere un primo acquisto, una creazione di un account, una registrazione a una newsletter o un altro evento. La `revenue` Il calcolo è un po&#39; più complicato. Vogliamo sommare i ricavi per gli ordini che sono stati inseriti dai membri di questo `cohort` ed è avvenuta entro un periodo di tempo fisso a partire dalla data di acquisizione (ad esempio, i primi tre mesi). Infine, dividiamo le entrate per il numero di membri nel `cohort` per ogni periodo di tempo nel grafico e aggiungi questo valore cumulativamente nel tempo.

## Quali sono le varianti di questo grafico?

Ci sono molti tipi diversi di utili `cohort` analisi.  La variazione più comune è [filtraggio per origine di acquisizione utente](../analysis/most-value-source-channel.md). Ad esempio, è possibile esaminare questo grafico per i clienti provenienti da `organic` ricerca, `paid` o un programma di affiliazione. Questo ti aiuterà a capire se i clienti di un&#39;origine di acquisizione sono più fedeli o preziosi di un&#39;altra. Naturalmente, puoi anche filtrare in base alla demografia o ad altri attributi utente.

Un altro modo per guardare i dati è con una prospettiva di dati incrementale, anziché cumulativa.  Questo mostra l’importo incrementale che un utente medio spende in ogni mese dopo l’acquisizione.  Questo è utile per prevedere la quantità di acquisti ripetuti che riceverai da utenti esistenti. Possiamo analizzarlo con altre cose oltre alle entrate. Alcuni esempi includono metriche di margine e non finanziarie come inviti, voti o messaggi.
