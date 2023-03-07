---
title: Nuova architettura
description: Scopri i vantaggi del passaggio a una nuova architettura.
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Nuova architettura

I team tecnici e di prodotto di MBI si sono concentrati per rendere possibili i miglioramenti più radicali e richiesti per l&#39;ultimo anno. L&#39;Adobe è entusiasta di annunciare la disponibilità di un nuovo [!DNL MBI] che rende questi miglioramenti una realtà.

## Vantaggi della nuova architettura

* Consente di creare tipi di colonne nella Data Warehouse, incluse le colonne calcolate con SQL.
* Le nuove colonne sono immediatamente disponibili.
* La latenza dei dati è notevolmente migliorata.

## Vantaggi tecnici

Le principali differenze sono elencate qui sopra, ma il cambiamento principale riguarda il modo in cui i calcoli vengono eseguiti durante il ciclo di aggiornamento. I calcoli non vengono più eseguiti su ogni colonna durante ogni aggiornamento, ma su richiesta dal Report Builder visivo.

### Passaggio a una nuova architettura

Poiché gli account sono fondamentalmente creati in modo diverso, non esiste alcuna procedura automatica per migrare la Data Warehouse o i report a un nuovo account dell’architettura. Il passaggio alla nuova architettura richiede la reimplementazione dell’account esistente.

### Costo del passaggio alla nuova architettura

Nessun costo aggiuntivo. Adobe creerà questo nuovo account per iniziare la reimplementazione, gratuita per almeno un mese. Questo ti consente di avere il tempo necessario per aprire entrambi gli account in modo da poter eseguire più facilmente la reimplementazione e garantire che il tuo team non presenti interruzioni nel servizio.

### Tempo necessario per reimplementare l’account nella nuova architettura

I tempi di reimplementazione variano a seconda di ciò che si desidera ricostruire. L’Adobe consiglia di eseguire i seguenti passaggi nell’account esistente per avere un’idea di cosa sarebbe coinvolto nella reimplementazione:

* Identifica un set principale di rapporti/dashboard.
* Identifica le metriche e le dimensioni necessarie per creare tali rapporti.
* Identifica le colonne necessarie per ricreare tali metriche e dimensioni.

Una volta completato, sai quali dati devi sincronizzare con la nuova Data Warehouse dell’architettura per ricreare questi rapporti di base.

### Ottenimento della Guida

Il [!DNL MBI] Il team dei servizi può eseguire la reimplementazione a un costo aggiuntivo. Contatta il tuo [Adobe team account](../../guide-overview.md) e preparati a fornire un elenco di dashboard/report da creare con priorità nel nuovo account

### Mantenere l&#39;architettura esistente

Se queste funzioni non sono importanti per te, puoi mantenere l’account esistente. Non ci sono costi aggiuntivi per mantenere il tuo account esistente. Adobe continua a supportare tali account senza modifiche.
