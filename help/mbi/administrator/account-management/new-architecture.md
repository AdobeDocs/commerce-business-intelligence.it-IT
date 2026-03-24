---
title: Nuova architettura
description: Scopri i vantaggi del passaggio a una nuova architettura.
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Import/Export
TQID: https://experienceleague.adobe.com/EtbKFT7OKaTZQ55XNz0NwpxQNSXyazk47dGwKhETNjM
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 390
ht-degree: 0%

---

# Nuova architettura

[!DNL Adobe Commerce Intelligence] I team tecnici e di prodotto si sono concentrati su come rendere possibili i miglioramenti più radicali e altamente richiesti per l&#39;ultimo anno. Adobe è entusiasta di annunciare la disponibilità di una nuova architettura di prodotto [!DNL Commerce Intelligence] che rende questi miglioramenti una realtà.

## Vantaggi della nuova architettura

* Consente di creare tipi di colonne in Data Warehouse, incluse le colonne calcolate con SQL.
* Le nuove colonne sono immediatamente disponibili.
* La latenza dei dati è notevolmente migliorata.

## Vantaggi tecnici

Le principali differenze sono elencate qui sopra, ma il cambiamento principale riguarda il modo in cui i calcoli vengono eseguiti durante il ciclo di aggiornamento. I calcoli non vengono più eseguiti su ogni colonna durante ogni aggiornamento, ma su richiesta da Visual Report Builder.

### Passaggio a una nuova architettura

Poiché gli account sono fondamentalmente creati in modo diverso, non esiste un processo automatico per migrare il Data Warehouse o i rapporti a un nuovo account con architettura. Il passaggio alla nuova architettura richiede la reimplementazione dell’account esistente.

### Costo del passaggio alla nuova architettura

Nessun costo aggiuntivo. Adobe creerà questo nuovo account per iniziare la reimplementazione, gratuita per almeno un mese. Questo ti consente di avere il tempo necessario per aprire entrambi gli account in modo da poter eseguire più facilmente la reimplementazione e garantire che il tuo team non presenti interruzioni nel servizio.

### Tempo necessario per reimplementare l’account nella nuova architettura

I tempi di reimplementazione variano a seconda di cosa desideri ricostruire. Adobe consiglia di eseguire i seguenti passaggi nell’account esistente per avere un’idea di cosa sarebbe coinvolto nella reimplementazione:

* Identifica un set principale di rapporti/dashboard.
* Identifica le metriche e le dimensioni necessarie per creare tali rapporti.
* Identifica le colonne necessarie per ricreare tali metriche e dimensioni.

Una volta completato, sai quali dati devi sincronizzare con la nuova architettura Data Warehouse per ricreare questi rapporti di base.

### Ottenimento della Guida

Il [!DNL Adobe Commerce Intelligence] [team dei servizi](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=it) può eseguire la reimplementazione per un costo aggiuntivo. Contatta il [Adobe Account Team](../../guide-overview.md#Submitting-a-Support-Ticket) e preparati a fornire un elenco di dashboard/report a cui assegnare la priorità per la creazione nel nuovo account

### Mantenere l&#39;architettura esistente

Se queste funzioni non sono importanti per te, puoi mantenere l’account esistente. Non ci sono costi aggiuntivi per mantenere il tuo account esistente. Adobe continua a supportare questi account senza apportare modifiche.
