---
title: Assegnare un nome ai rapporti e agli elementi in Commerce Intelligence
description: Scopri le best practice per la denominazione di report ed elementi in [!DNL Commerce Intelligence].
exl-id: c662cedd-c779-4254-b04b-f3092a538c85
role: Admin, User
feature: Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---

# Assegnare un nome ai rapporti e agli elementi

Prima di iniziare a generare in [!DNL Adobe Commerce Intelligence], Adobe desidera condividere alcuni segreti per il successo. Sapere come creare metriche, filtri e così via è importante, ma tutto il tuo lavoro potrebbe essere inutile se non riesci a trovare ciò di cui hai bisogno o se c&#39;è ambiguità.

## Perché la nomenclatura è importante? {#why}

Il modo in cui si denominano le colonne calcolate, le metriche e i report determina la facilità con cui utenti diversi possono spostarsi attraverso l&#39;account [!DNL Commerce Intelligence]. Quando denominate queste funzioni, tenete presente le tre C:

* **CHIAREZZA** - In questo modo è possibile verificare immediatamente cosa viene visualizzato in un report, cosa fa una metrica e così via.
* **COERENZA** - In modo che tu (e il team di supporto Adobe) possiate trovare e comprendere facilmente gli elementi e i report nel vostro account.
* **CREDIBILITÀ** - Per ispirare e responsabilizzare altri utenti [!DNL Commerce Intelligence] basati sui dati, è necessario infondere fiducia nel modo in cui comprendono e utilizzano i dati.

Continua a leggere per suggerimenti sulla nomenclatura comprovati e veri!

## Best practice generali {#general}

### Sii significativo {#meaningful}

Siate specifici quando possibile! Ad esempio, se si tratta del paese, sai se si tratta del paese di spedizione o di fatturazione? È la città dell&#39;utente o è la città dell&#39;affare?

**Esempio non valido:**
Ricavi

Questo è vago e non ci dice molto.

**Esempi validi:**
Ricavi (totale generale base + commissione)
Paese di spedizione dell&#39;utente

Questi esempi sono specifici e riducono il rischio di confusione.

### Essere coerente con l&#39;utilizzo delle maiuscole {#capitalize}

[!DNL Adobe] consiglia di utilizzare la prima lettera in maiuscolo con il resto dei caratteri in minuscolo, a meno che non venga utilizzato lo stile di maiuscolo corretto per il nome. Ad esempio, **Numero ordine dell&#39;utente** anziché **Numero ordine dell&#39;utente.**

Si tratta di una vera e propria questione di preferenza, ma è importante ricordare che bisogna essere coerenti con qualsiasi scelta.

### Coerenza entità {#entity}

Probabilmente hai già una nomenclatura in vigore nella tua azienda. Mantieni le metriche e le dimensioni implementate coerenti con quelle utilizzate in altri database e strumenti. Ad esempio:

* Utente vs. Cliente vs. Membro vs. Account
* Confronto tra società e account e organizzazione
* Registrazione e creazione

### Controllo ortografia e grammatica {#spelling}

Assicurati di controllare nuovamente l&#39;ortografia e non dimenticare quei possessivi fastidiosi!

## Grafici {#charts}

Quando si denominano [grafici](../tutorials/using-visual-report-builder.md), è più utile seguire questa formula: **(Prospettiva dati) + (Metrica) + (Periodo di tempo) + (Intervallo di tempo)**

**Esempio non valido:**
Ricavi

Questo non ci dice nulla sul rapporto, che è negativo.

**Esempio corretto:**
Ricavi cumulati oltre 30 giorni per mese

Questo ci dice **esattamente** cosa c&#39;è nel rapporto, che è fantastico.

## Dashboard {#dashboards}

Le dashboard devono essere denominate in modo da rappresentare tematicamente i rapporti al loro interno. Ad esempio, se il dashboard contiene solo informazioni relative a ricavi e ordini, è consigliabile denominarlo ad esempio **Nome store - Ricavi e ordini.**

Al contrario, se il dashboard è un luogo in cui si stanno sperimentando diversi rapporti, è consigliabile denominarlo **Sandbox del tuo nome** in modo da sapere che i rapporti contenuti in sono bozze.

## Dimension (colonne calcolate) {#dimensions}

Quando si denominano le nuove [dimensioni](../data-analyst/data-warehouse-mgr/creating-calculated-columns.md), è più utile seguire questa formula: **(Entità) + (Nth) + (intervallo di tempo) + (calcolo) + (commenti)**. Ad esempio:

Primi ricavi di 30 giorni dell&#39;utente
* Numero ordine utente
* Numero ordine utente (in attesa di controllo)

## Set di filtri {#filterset}

[I set di filtri](../data-user/reports/ess-manage-data-filters.md) sono in genere denominati in modo da spiegare le informazioni che includono o escludono. Ad esempio, la denominazione di un set di filtri **Gli elementi dell&#39;ordine conteggiati** consentono a qualsiasi utente di accedere, visualizzare la logica del set di filtri e capire quali informazioni sull&#39;ordine determinano ciò che viene conteggiato in tutta l&#39;azienda. I set di filtri possono essere applicati sia alle colonne calcolate che alle metriche e devono essere di facile comprensione.

## Metriche {#metrics}

[Le metriche](../data-user/reports/ess-manage-data-metrics.md) sono essenzialmente domande a cui desideri rispondere regolarmente. Qual è stato il numero di ordini nell&#39;ultimo mese? Qual è il valore medio del ciclo di vita dei clienti? È consigliabile denominare le metriche in modo che riflettano la risposta che forniscono agli utenti. Inoltre, se la stessa metrica è filtrata per un negozio o reparto specifico, deve essere etichettata come tale. Ad esempio:

LTV cliente medio (primi 30 giorni)
Nome store - Ricavi

Infine, a volte la stessa metrica può essere organizzata in base a marche temporali diverse, a seconda di come i singoli utenti la calcolano. In tal caso, assicurati di includere la marca temporale nel nome:

Ricavi (spediti\_at)
Ricavi (creato\_at)

## Ritorno a capo {#wrapup}

Stabilire anticipatamente le convenzioni di stile e denominazione ti aiuta a prepararti per il successo nel tuo account [!DNL Commerce Intelligence]. Ricorda le tre C: chiarezza, coerenza e credibilità.
