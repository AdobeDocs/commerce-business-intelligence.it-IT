---
title: Nuova architettura
description: Scopri i vantaggi del passaggio alla nuova architettura.
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# Nuova architettura

I nostri team di prodotti e tecnici si sono concentrati sul miglioramento più ampio e richiesto possibile nell&#39;ultimo anno. Siamo entusiasti di annunciare la disponibilità di un nuovo [!DNL MBI] architettura di prodotto che rende tali miglioramenti una realtà.

## Vantaggi della nuova architettura

* Crea nuovi tipi di colonne nel data warehouse, incluse le colonne calcolate con SQL.
* Le nuove colonne sono immediatamente disponibili.
* La latenza dei dati viene notevolmente migliorata.

## Vantaggi tecnici

Le principali differenze sono elencate sopra, ma ciò che è tecnicamente cambiato è il modo in cui eseguiamo i calcoli durante il ciclo di aggiornamento. I calcoli non vengono più eseguiti su ogni colonna durante ogni aggiornamento; vengono invece eseguiti on-demand dal Report Builder visivo.

### Passaggio alla nuova architettura

Poiché gli account sono costruiti in modo fondamentalmente diverso, non esiste un processo automatico che possiamo utilizzare per migrare il data warehouse o i report in un nuovo account di architettura, pertanto il passaggio alla nuova architettura richiede una nuova implementazione dell&#39;account esistente.

### Costo del passaggio alla nuova architettura

Nessun costo aggiunto! Creeremo un nuovo account per iniziare la reimplementazione, gratuita da almeno un mese. Questo ti consente di avere il tempo necessario per aprire entrambi gli account in modo da poter eseguire più facilmente la reimplementazione e garantire che il tuo team non abbia una mancanza di servizio.

### Tempo necessario per la riimplementazione dell’account nella nuova architettura

I tempi di reimplementazione variano a seconda di cosa desideri ricostruire. Per un’idea di cosa potrebbe essere coinvolto nella reimplementazione, ti consigliamo di eseguire i seguenti passaggi nell’account esistente:

* Identifica un set principale di report/dashboard.
* Identifica le metriche e le dimensioni necessarie per generare tali rapporti.
* Identifica le colonne necessarie per ricreare tali metriche e dimensioni.

Una volta completato, saprai quali dati devi sincronizzare con il nuovo data warehouse di architettura per ricreare questi report di base.

### Aiuto

La [!DNL MBI] Il team dei servizi può eseguire la reimplementazione a un costo aggiuntivo. Contatta il nostro [Team di successo del cliente](../../guide-overview.md) e preparatevi a fornire un elenco di dashboard/report che desiderate dare priorità alla creazione nel nuovo account

### Stare con l&#39;architettura esistente

Se queste funzioni non sono importanti per te, puoi attenerti all’account esistente. Non vi sono costi aggiuntivi per mantenere il tuo account esistente e continueremo a supportare tali account senza modifiche.
