---
title: Denomina report ed elementi in MBI
description: Scopri le best practice per la denominazione di report ed elementi in [!DNL MBI].
exl-id: c662cedd-c779-4254-b04b-f3092a538c85
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 0%

---

# Nome dei report e degli elementi

Prima di iniziare a costruire in[!DNL MBI], vogliamo condividere alcuni dei nostri segreti con il successo. È importante sapere come creare metriche, filtri e così via, ma tutto il lavoro sarà inutile se non riesci a trovare ciò che ti serve o se c’è qualche ambiguità.

## Perché la nomenclatura è importante? {#why}

Il modo in cui denominate le colonne, le metriche e i rapporti calcolati determina la facilità con cui i diversi utenti possono navigare all’interno dell’app [!DNL MBI] conto. Per denominare queste funzioni, teniamo a mente le tre Cs:

* **CHIAREZZA** - È quindi possibile vedere immediatamente cosa mostra un rapporto, cosa fa una metrica e così via.
* **COERENZA** - In modo che tu (e il nostro team di supporto) possiate trovare e comprendere facilmente elementi e rapporti nel vostro account.
* **CREDIBILITÀ** - Per ispirare e potenziare altri dati [!DNL MBI] utenti, devi instillare fiducia nel modo in cui comprendono e utilizzano i dati!

Continua a leggere per i nostri consigli di nomenclatura provati e veri!

## Best practice generali {#general}

### Sii significativo {#meaningful}

Sii specifica quando possibile! Ad esempio, se si tratta del paese, sai se si tratta del paese di spedizione o di fatturazione? È la città dell&#39;utente, o è la città dell&#39;affare?

**Esempio non valido:**
Entrate

Questo è vago e non ci dice molto.

**Buoni esempi:**
Entrate (totale complessivo base + costo) Paese di spedizione dell&#39;utente

Si tratta di esempi specifici che riducono il potenziale di confusione.

### Sii coerente con la capitalizzazione {#capitalize}

Siamo grandi fan della prima lettera maiuscola, il resto dei caratteri minuscolo a meno che non lo stile di noun corretto della capitalizzazione. Ad esempio: **Numero dell&#39;ordine dell&#39;utente** piuttosto che **Numero ordine dell&#39;utente.**

È una questione di preferenza, ma la cosa da ricordare è essere coerenti con qualsiasi cosa si scelga.

### Coerenza entità {#entity}

Probabilmente hai già una nomenclatura in atto presso la tua azienda. Mantieni le metriche e le dimensioni inserite coerenti con quelle utilizzate in altri database e strumenti. Ad esempio:

* Utente vs. cliente vs. membro vs. account
* Società vs. conto vs. organizzazione
* Registrazione e creazione

### Controllo ortografia e grammatica {#spelling}

Assicurati di controllare l&#39;ortografia e non dimenticare di quei possessivi fastidiosi!

## Grafici {#charts}

Durante la denominazione [grafici](../tutorials/using-visual-report-builder.md), riteniamo più utile seguire questa formula: **(Prospettiva dati) + (Metrica) + (Periodo di tempo) + (Intervallo di tempo)**

**Esempio non valido:**
Entrate

Questo non ci dice nulla sulla relazione, che è negativa.

**Esempio:**
Entrate cumulative passate 30 giorni per mese

Questo ci dice **esattamente** la relazione, che è fantastica.

## Dashboard {#dashboards}

I dashboard devono essere denominati in modo che rappresentino tematicamente i rapporti al loro interno. Ad esempio, se il dashboard contiene solo informazioni relative a ricavi e ordini, considera la possibilità di assegnargli un nome simile a **Nome store - Ricavi e ordini.**

Viceversa, se il dashboard è un punto in cui si stanno sperimentando con rapporti diversi, è consigliabile assegnargli un nome **Sandbox del tuo nome** quindi sai che i rapporti contenuti sono bozze.

## Dimension (colonne calcolate) {#dimensions}

Per la denominazione di nuove [dimensioni](../data-analyst/data-warehouse-mgr/creating-calculated-columns.md), riteniamo più utile seguire questa formula: **(Entità) + (Nth) + (time frame) + (calcolo) + (commenti)**. Ad esempio:

I primi ricavi di 30 giorni dell&#39;utente
* Numero dell&#39;ordine dell&#39;utente
* Numero dell’ordine dell’utente (in attesa del controllo di audit)

## Set di filtri {#filterset}

[Set di filtri](../data-user/reports/ess-manage-data-filters.md) sono generalmente denominati in modi che spiegano le informazioni che includono o escludono. Ad esempio, la denominazione di un set di filtri **Ordina articoli contati** consentirà a qualsiasi utente di entrare, visualizzare la logica del set di filtri e comprendere quali informazioni dell’ordine determinano ciò che viene conteggiato nell’attività. I set di filtri possono essere applicati sia alle colonne calcolate che alle metriche e devono essere di facile comprensione.

## Metriche {#metrics}

[Metriche](../data-user/reports/ess-manage-data-metrics.md) sono essenzialmente domande a cui desideri rispondere regolarmente. Qual era il numero di ordini nell&#39;ultimo mese? Qual è il valore medio del ciclo di vita dei nostri clienti? In genere è consigliabile denominare le metriche in modo da riflettere la risposta che forniscono agli utenti. Inoltre, se hai la stessa metrica filtrata per uno specifico negozio o reparto, devi etichettarla come tale. Ad esempio:

Media LTV cliente (primi 30 giorni) Nome negozio - Ricavi

Infine, a volte la stessa metrica può essere organizzata con marche temporali diverse, a seconda di come i singoli utenti la calcolano. In questo caso, accertati di includere la marca temporale nel nome:

Entrate (spedite\_at) Entrate (create\_at)

## Ritorno a capo {#wrapup}

L&#39;istituzione anticipata delle convenzioni di stile e di denominazione ti aiuterà a configurarti per il successo nel tuo [!DNL MBI] conto. Ricordate le tre C: chiarezza, coerenza e credibilità.
