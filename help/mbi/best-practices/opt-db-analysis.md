---
title: Ottimizzazione del database per l'analisi
description: Scopri come ottimizzare il database per l’analisi.
exl-id: e73e1a1e-c933-476d-97bc-bd8f52bb2fa1
role: Admin, Data Architect, Data Engineer, User
feature: Business Performance, Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---

# Ottimizzazione del database

Il vantaggio principale dell&#39;utilizzo di un database operativo per [!DNL Adobe Commerce Intelligence] è che non è necessario creare o modificare nulla per raccogliere i dati. Le informazioni importanti sono già disponibili, è sufficiente sbloccarle.

Questo argomento contiene alcuni consigli utili per ottimizzare il database per l’analisi e trarre informazioni fruibili dai dati non elaborati.

## Non eliminare dati

>[!TIP]
>
>Le leggi locali e internazionali che riguardano la tua attività (e i tuoi termini di servizio) possono influenzare i tipi di dati che puoi conservare e per quanto tempo puoi conservarli. Il rispetto di queste leggi dovrebbe essere la tua priorità principale.

Quando un ordine viene annullato, un utente disattiva il proprio account o un prodotto viene interrotto, si tenta di eliminare le informazioni associate nel database. Le tabelle crescono ed eliminare il disordine sembra un&#39;idea prudente. Tuttavia, l&#39;eliminazione delle righe comporta la perdita permanente di queste informazioni o la necessità di eseguire ricerche nei backup precedenti per individuarle.

È invece possibile aggiungere alla tabella una colonna di stato che indichi quando la riga non è più attiva o rilevante. Si consiglia inoltre di aggiungere una colonna in cui sia memorizzata la data in cui è stata apportata la modifica o di creare un registro per le modifiche storiche. Se le dimensioni delle tabelle aumentano al punto da compromettere le prestazioni, è consigliabile archiviare i dati obsoleti in una tabella utilizzata per l&#39;analisi.

## Sovrascrivi raramente i dati

La sovrascrittura dei dati deve essere eseguita con cautela e con moderazione.

Utilizzando le date di accesso come esempio, molte aziende memorizzano la data dell’ultimo accesso anziché una tabella di accessi cronologici. Anche se potresti aver bisogno solo dell’ultima data di accesso a scopo funzionale, i dati sovrascritti rappresentano una perdita enorme dal punto di vista dell’analisi. Il mancato mantenimento di un registro completo di queste azioni elimina la possibilità di vedere quanti utenti sono rimasti lontani per lunghi periodi di tempo e poi sono stati riattivati. Rende inoltre impossibile creare elementi come le analisi di coorte di coinvolgimento degli utenti basate sugli accessi.

In genere, se si aggiorna un record a causa di un&#39;azione dell&#39;utente, non sovrascrivere le informazioni relative a un&#39;azione precedente o separata dell&#39;utente.

## Includi `Updated_at` colonne per dati aggiornati nel tempo

Se le righe di una tabella avranno valori che cambiano nel tempo, ad esempio **order\_status** cambia da`processing` a `complete`, includi una colonna **updated\_at** da registrare quando si verifica l&#39;ultima modifica. Assicurati che un valore **updated\_at** sia disponibile al primo inserimento della nuova riga di dati, quando la data **updated\_at** corrisponde alla data **created\_at**.

Oltre all&#39;ottimizzazione per l&#39;analisi, le colonne **updated\_at** consentono anche di utilizzare i [metodi di replica incrementale](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md), che possono aiutare a ridurre la durata dei cicli di aggiornamento.

## Archivia Source di acquisizione utenti

Uno degli errori più comuni è che l&#39;origine di acquisizione [utente](../data-analyst/analysis/google-track-user-acq.md) (UAS) non è memorizzata nel database operativo. Nella maggior parte delle situazioni in cui si verifica questo problema, il tracciamento di UAS viene eseguito solo tramite [!DNL Google Analytics] o un altro strumento di analisi Web. Anche se questi strumenti possono essere utili, esistono alcuni svantaggi nell’archiviazione esclusiva di UAS; ad esempio, non è possibile estrarre dati a livello di utente da questi strumenti. Quando è possibile, di solito è un processo difficile. Dovrebbe essere facile ottenere queste informazioni e combinarle con dati provenienti da altre origini, ad esempio le informazioni comportamentali e transazionali memorizzate anche nel database.

L&#39;archiviazione di UAS nel proprio database è spesso il più grande miglioramento che un&#39;azienda online può apportare alle proprie capacità analitiche. Questo consente di analizzare vendite, coinvolgimento degli utenti, periodi di recupero, valore del ciclo di vita del cliente, abbandono e altre metriche critiche da parte di UAS. [Questi dati sono fondamentali per decidere dove investire le risorse di marketing](../data-analyst/analysis/most-value-source-channel.md).

Troppe aziende si concentrano esclusivamente sulla ricerca di canali che offrano nuovi utenti al costo più basso. Se non tieni traccia della qualità degli utenti acquisiti da ciascun canale, corri il rischio di attrarre utenti che non generano valore aziendale.

## Impostazione tabella dati

### Impostare una chiave primaria

Una [chiave primaria](https://en.wikipedia.org/wiki/Unique_key) è una colonna (o un set di colonne) immutabile che produce valori univoci all&#39;interno di una tabella. Le chiavi primarie sono estremamente importanti in quanto garantiscono la corretta replica delle tabelle in [!DNL Commerce Intelligence].

Quando crei le chiavi primarie, utilizza un tipo di dati integer per la colonna che aumenta automaticamente. L’Adobe consiglia di evitare di utilizzare più chiavi primarie di colonna, ove possibile.

Se la tabella è una vista SQL, aggiungere una colonna che possa fungere da chiave primaria. [!DNL Commerce Intelligence] è in grado di identificare automaticamente questa colonna come chiave primaria.

### Assegnare un tipo di dati alla colonna di dati

Se a una colonna di dati non è assegnato un tipo di dati [](https://en.wikipedia.org/wiki/Data_type), [!DNL Commerce Intelligence] indovina quale tipo di dati utilizzare. Se il sistema non indovina correttamente, potresti non essere in grado di eseguire le analisi pertinenti fino a quando il team di supporto Adobe non regolerà la colonna in base al tipo di dati corretto. Ad esempio, se una colonna data è considerata un tipo di dati numerico, puoi generare tendenze nel tempo utilizzando tale dimensione data.

### Aggiungere prefissi alle tabelle dati se si dispone di più database

Se a [!DNL Commerce Intelligence] è connesso più di un database, l&#39;Adobe consiglia di aggiungere prefissi alle tabelle per evitare confusione. I prefissi consentono di ricordare da dove provengono le metriche o le dimensioni dati.
