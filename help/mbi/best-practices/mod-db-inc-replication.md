---
title: Modifica del database per il supporto della replica incrementale
description: Scopri come modificare il database per supportare la replica incrementale.
exl-id: c9a38892-6096-4eb5-8a53-35b8b7b083dc
role: Admin, Developer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
TQID: https://experienceleague.adobe.com/VH5mhfRJteAxiQAmh14TzhnAqym65X6SFRMGuSuEvwM
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 334
ht-degree: 0%

---

# Supporto per la replica incrementale

Se le tabelle non consentono attualmente la replica incrementale, consulta le seguenti raccomandazioni per le possibili soluzioni.

## Modifiche per Data modifica

Il metodo `Modified At`, che è il metodo di replica più ideale, utilizza una colonna `datetime` per rilevare dati nuovi e/o aggiornati. Tenere presente che la colonna `datetime` nelle tabelle che utilizzano questo metodo deve essere indicizzata e non può contenere valori Null in alcun momento.

Se la tabella non ha una colonna `datetime`, è possibile aggiungere una colonna `modified at` dell&#39;indice. Valori Null non consentiti in una colonna `modified at`. Verifica che la colonna sia compilata per ogni riga.

Per garantire che il metodo `Modified At` funzioni come previsto, non è possibile eliminare righe dalla tabella. Contrassegnare la riga come non valida aggiungendo una colonna `deleted` alla tabella. Questa colonna restituisce `1` se la riga non è valida e `0` in caso contrario. Puoi quindi utilizzare questa colonna per filtrare le righe non valide durante la creazione di metriche e rapporti.

## Modifiche per la chiave primaria con incremento automatico singolo

Se il metodo `Modified At` non può essere abilitato, l&#39;opzione migliore successiva è Incrementa automaticamente chiave primaria singola. I nuovi dati vengono rilevati nelle tabelle utilizzando questo metodo ricercando valori di chiave primaria superiori al valore massimo corrente in Data Warehouse.

Le tabelle che utilizzano questo metodo sono a colonna singola con chiavi primarie a incremento automatico di numeri interi. Per utilizzare questo metodo nel database, effettuare le seguenti modifiche:

* Se la chiave primaria è una chiave composita o non è un numero intero, impostare la chiave primaria su un numero intero incrementale automatico
* Se la chiave primaria è una singola colonna di numeri interi ma le chiavi possono essere assegnate in modo non sequenziale, impostare la chiave primaria su incremento automatico

## Ritorno a capo

Apportando modifiche minori alle tabelle, è possibile sfruttare i metodi di replica incrementale più rapidi ed efficienti. Tuttavia, se ciò non fosse possibile, puoi comunque eseguire altri passaggi per [ridurre il tempo di aggiornamento](../best-practices/reduce-update-cycle-time.md) e [ottimizzare il database](../best-practices/opt-db-analysis.md).
