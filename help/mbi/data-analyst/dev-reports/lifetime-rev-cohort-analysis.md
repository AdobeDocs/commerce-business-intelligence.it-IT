---
title: Analisi per coorte dei ricavi del ciclo di vita
description: Scopri la potenza dell’analisi per coorte con Commerce Intelligence.
exl-id: f2b55745-d364-4ba6-9857-ce9cee05c3ae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 0%

---

# Analisi [!DNL Lifetime Revenue Cohort]

Esistono diversi modi per esaminare i dati in [!DNL Adobe Commerce Intelligence] e si sa che l&#39;interpretazione e la comprensione sono importanti quanto il calcolo e la visualizzazione. In questo argomento viene illustrata la potenza dell&#39;analisi [!DNL Commerce Intelligence] `cohort`.

## Cosa significa analisi `lifetime revenue cohort`?

Il grafico seguente mostra la spesa cumulativa per utente per un periodo di tempo dopo la sua acquisizione. `Cohorts` utenti sono suddivisi in base al mese di acquisizione.

Ad esempio, la riga arancione precedente mostra la media per gli utenti acquisiti a novembre 2011. Il primo punto dati indica che nel primo mese gli utenti acquisiti a novembre hanno trascorso in media circa `$200`. Il secondo punto dati indica che alla fine del secondo mese questi utenti avevano speso in media circa `$240`. La loro spesa media nel secondo mese è stata di circa `$40 (240 - 200)`. Le diverse linee rappresentano diverse coorti di utenti. La linea verde rappresenta gli utenti che sono stati acquisiti in dicembre, mentre la linea blu rappresenta gli utenti che sono stati acquisiti in ottobre.

## Perché è importante?

Questo tipo di analisi `cohort` può essere utile per diversi scopi, ma il vantaggio più immediato è spesso quello di migliori decisioni di acquisizione dei clienti. Molte aziende limitano la spesa di marketing ai canali che producono redditività al primo acquisto di un cliente. Queste aziende pagano per acquisire i clienti attraverso un determinato canale, purché il loro primo acquisto medio renda più di `gross margin` del costo per acquisirli.

Il problema di questo approccio è che spesso si traduce in un sottoinvestimento nella crescita. Se i tuoi concorrenti fanno marketing basandosi su una comprensione più profonda del comportamento d&#39;acquisto, la tua crescita è superiore. L&#39;analisi di `lifetime revenue cohort` ti aiuta a comprendere le conseguenze dell&#39;espansione delle spese di acquisizione dei clienti e offre un modo semplice per trasmettere questo messaggio al resto del tuo team. Se i clienti futuri si comportano come clienti esistenti, l’acquisizione di clienti per un CPA più elevato determina un periodo di recupero del capitale investito prevedibile. A seconda della situazione di cassa dell&#39;azienda, è possibile definire il periodo di recupero desiderato, trovare il punto pertinente nel grafico e spendere di conseguenza.

Inoltre, puoi utilizzare questa analisi per vedere se stai migliorando l’onboarding, il coinvolgimento e la generazione di ricavi dagli utenti acquisiti. Ad esempio, questa analisi `cohort` è un ottimo modo per vedere se una promozione di spedizione gratuita per i nuovi utenti ha prodotto acquirenti ripetuti o acquirenti occasionali che non tornano mai più.

## Quali saranno le differenze tra i diversi modelli di business?

Per la maggior parte delle aziende, il grafico di analisi `lifetime revenue cohort` mostrerà una grande quantità di spesa nel periodo iniziale e quindi aumenterà più lentamente nel tempo. Questo picco iniziale è dovuto al fatto che è più probabile che i clienti effettuino il primo acquisto subito dopo l’acquisizione che in qualsiasi altro momento. Nei casi in cui l’evento di acquisizione stesso è un acquisto, il 100% dei clienti effettua un acquisto nel primo periodo. Nei casi in cui la registrazione può avvenire prima degli acquisti, questo effetto è meno drastico.

Ad esempio, [!DNL Groupon] potrebbe avere un salto iniziale molto più basso rispetto a [!DNL Amazon], perché molte delle persone iscritte a [!DNL Groupon] non effettuano subito un acquisto. A meno che non ci sia un numero elevato di rimborsi, questo grafico inclinerà verso l&#39;alto e verso destra dopo il salto iniziale. Il tasso di crescita tende a diminuire nel tempo perché i clienti sono più attivi al momento della prima iscrizione. Questo causa un calo della media perché il numero di persone nella coorte rimane costante, indipendentemente da quante tornano per acquistarne di più. Nelle aziende che sottoscrivono abbonamenti, la pendenza decadrà in modo meno aggressivo rispetto alle aziende in cui le persone effettuano acquisti una tantum.

A volte, un’attività di abbonamento ha in realtà una pendenza che aumenta nel tempo. È raro vederlo, ma è un ottimo segnale per l&#39;azienda quando succede. Ciò non significa che non vi siano clienti abituali, ma piuttosto che gli aggiornamenti per i clienti che rimangono più che compensare i clienti che se ne vanno.

## Come si calcola?

Esistono due semplici input per questo calcolo: il numero di membri presenti in `cohort` (che non cambia mai) e la quantità di ricavi generati da tali membri nel periodo specificato. Per determinare i membri in `cohort`, si conta il numero di utenti acquisiti nel periodo in questione. Un&#39;acquisizione può essere un primo acquisto, la creazione di un account, l&#39;iscrizione a una newsletter o un altro evento. Il calcolo di `revenue` è un po&#39; più complicato. Si desidera sommare i ricavi per gli ordini emessi dai membri di `cohort` e eseguiti in un periodo di tempo fisso a partire dalla data di acquisizione, ad esempio i primi tre mesi. Infine, dividi i ricavi per il numero di membri in `cohort` per ogni periodo di tempo nel grafico e aggiungi questo valore cumulativamente nel tempo.

## Quali sono le varianti di questo grafico?

Esistono molti tipi diversi di utili analisi `cohort`. La variante più comune è [filtro per origine di acquisizione utente](../analysis/most-value-source-channel.md). Ad esempio, potrebbe essere utile esaminare questo grafico per i clienti provenienti da `organic` ricerca, `paid` ricerca o da un programma di affiliazione. Questo ti aiuta a capire se i clienti di un&#39;origine di acquisizione sono più fedeli o importanti di un&#39;altra. Puoi anche filtrare in base ai dati demografici o ad altri attributi utente.

Un altro modo per esaminare i dati consiste nell’utilizzare una prospettiva incrementale, anziché cumulativa, dei dati. Mostra la quantità incrementale spesa da un utente medio in ogni mese dopo l’acquisizione. Ciò è utile per prevedere il numero di acquisti ripetuti che si ottiene dagli utenti esistenti. Questo si può vedere anche con altre cose oltre ai ricavi. Alcuni esempi includono metriche di margine e non finanziarie come inviti, voti o messaggi.
