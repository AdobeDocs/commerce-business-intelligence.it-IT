---
title: Ottimizzazione del database per l'analisi
description: Scopri come ottimizzare il database per l’analisi.
exl-id: e73e1a1e-c933-476d-97bc-bd8f52bb2fa1
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 0%

---

# Ottimizzare il database

Il principale vantaggio dell&#39;utilizzo di una banca dati operativa per le informazioni aziendali è che non è necessario creare o modificare nulla per raccogliere i dati. Sono già disponibili informazioni preziose; tutto quello che devi fare è sbloccarlo.

Questo argomento contiene alcuni consigli che consentono di ottimizzare il database per l’analisi e trarre informazioni utili dai dati non elaborati.

## Non eliminare i dati

>[!TIP]
>
>Le leggi locali e internazionali che influenzano la tua attività (e i tuoi termini di servizio) possono influenzare i tipi di dati che puoi conservare e per quanto tempo puoi conservarli. Il rispetto di queste leggi dovrebbe essere la tua priorità assoluta.

Quando un ordine viene annullato, un utente disattiva il proprio account o un prodotto viene interrotto, si potrebbe tentare di eliminare le informazioni associate nel database. Le tavole crescono ed eliminano il disordine sembra un&#39;idea prudente. Tuttavia, eliminare le righe significa che queste informazioni vengono perse per sempre o che sarà necessario scavare attraverso i vecchi backup per trovarle.

È invece possibile aggiungere alla tabella una colonna di stato che indica quando la riga non è più attiva o rilevante. Si consiglia inoltre di aggiungere una colonna in cui memorizzare la data di modifica apportata oppure di creare un registro per le modifiche dello storico. Se le tabelle diventano sufficientemente grandi da causare problemi alle prestazioni, è consigliabile archiviare i vecchi dati in una tabella utilizzata per l&#39;analisi.

## Sovrascrivi dati raramente

La sovrascrittura dei dati dovrebbe essere effettuata con cautela e cautela.

Utilizzando le date di accesso come esempio, molte aziende memorizzeranno la data dell’ultimo accesso anziché una tabella degli accessi storici. Anche se potrebbe essere necessaria solo la data dell’ultimo accesso per scopi funzionali, i dati sovrascritti rappresentano una perdita enorme dal punto di vista di analytics. La mancata conservazione di un registro completo di queste azioni elimina la possibilità di vedere quanti utenti sono rimasti lontani per lunghi periodi di tempo e poi riattivati. Inoltre, rende impossibile creare elementi come le analisi per coorte di coinvolgimento degli utenti basate sugli accessi.

Come regola generale, se aggiorni un record a causa di un tipo di azione dell&#39;utente, non sovrascrivere le informazioni su un&#39;azione utente precedente o separata.

## Includi `Updated_at` Colonne per dati aggiornati nel tempo

Se le righe di una tabella avranno valori variabili nel tempo, ad esempio, **order\_status** modifiche da`processing` a `complete`, include **aggiornato\_at** da registrare quando si verifica l’ultima modifica. Assicurati che **aggiornato\_at** è disponibile quando si inserisce per la prima volta la nuova riga di dati, in cui la **aggiornato\_at** corrisponde alla data **created\_at** data.

Oltre all&#39;ottimizzazione per l&#39;analisi, **aggiornato\_at** le colonne consentono inoltre di utilizzare [Metodi di replica incrementale](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md), che può aiutare a ridurre la lunghezza dei cicli di aggiornamento.

## Archiviare l&#39;origine di acquisizione degli utenti

Uno degli errori più comuni è il [sorgente di acquisizione utente](../data-analyst/analysis/google-track-user-acq.md) (UAS) non archiviato nella banca dati operativa. Nella maggior parte delle situazioni in cui si tratta di un problema, l&#39;UAS viene monitorata solo attraverso [!DNL Google Analytics] o altro strumento di analisi web. Anche se questi strumenti possono essere estremamente preziosi, vi sono alcuni inconvenienti per immagazzinare gli UAS in essi esclusivamente; ad esempio, non è possibile estrarre dati a livello di utente da questi strumenti. Quando è possibile, di solito è un processo difficile. Dovrebbe essere facile ottenere queste informazioni e combinarle con dati provenienti da altre fonti, come le informazioni comportamentali e transazionali anche memorizzate nel database.

L&#39;archiviazione di UAS nel tuo database è spesso il miglioramento più grande che un&#39;azienda online può fare alle sue capacità analitiche. Ciò consente l’analisi di vendite, coinvolgimento dell’utente, periodi di rimborso, valore della durata del cliente, abbandono e altre metriche critiche da parte di UAS. [Questi dati sono fondamentali per decidere dove investire le risorse di marketing](../data-analyst/analysis/most-value-source-channel.md).

Troppe aziende si concentrano esclusivamente sulla ricerca di canali che forniscono nuovi utenti al costo più basso, ma se non tieni traccia della qualità degli utenti acquisiti da ogni canale, corri il rischio di attrarre utenti che non generano valore aziendale.

## Configurazione tabella dati

### Imposta una chiave primaria

A [chiave primaria](http://en.wikipedia.org/wiki/Unique_key) è una colonna (o insieme di colonne) che produce valori univoci all’interno di una tabella. Le chiavi primarie sono incredibilmente importanti in quanto assicurano che le tabelle siano correttamente replicate in [!DNL MBI].

Quando crei le chiavi primarie, utilizza un tipo di dati intero per la colonna che aumenta automaticamente. È inoltre consigliabile evitare di utilizzare, ove possibile, più chiavi primarie delle colonne.

Se la tabella è una vista SQL, aggiungere una colonna che può fungere da chiave primaria. [!DNL MBI] sarà in grado di identificare automaticamente questa colonna come chiave primaria.

### Assegnare un tipo di dati alla colonna dati

Se a una colonna di dati non è assegnato un [tipo di dati](http://en.wikipedia.org/wiki/Data_type), [!DNL MBI] indovinerà quale tipo di dati utilizzare. Se il sistema indovina erroneamente, potresti non essere in grado di eseguire le analisi pertinenti fino a quando il nostro team di supporto non adegua la colonna al tipo di dati appropriato. Ad esempio, se una colonna data è impostata come tipo di dati numerici, è possibile utilizzare nel tempo la dimensione data per tendere.

### Aggiungi i prefissi alle tabelle dati se disponi di più database

Se sono presenti più database connessi a [!DNL MBI], è consigliabile aggiungere dei prefissi alle tabelle per evitare confusione. I prefissi ti aiuteranno a ricordare da dove provengono le metriche o le dimensioni dati.
