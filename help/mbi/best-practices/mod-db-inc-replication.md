---
title: Modifica del database per il supporto della replica incrementale
description: Scopri come modificare il database per supportare la replica incrementale.
exl-id: c9a38892-6096-4eb5-8a53-35b8b7b083dc
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# Supporto per la replica incrementale

Se le tabelle non consentono attualmente la replica incrementale, consulta le seguenti raccomandazioni per le possibili soluzioni.

## Modifiche per Data modifica

Il `Modified At` , che è il metodo di replica più ideale, utilizza un `datetime` per rilevare dati nuovi e/o aggiornati. Ricorda che il `datetime` le colonne nelle tabelle che utilizzano questo metodo devono essere indicizzate e non possono contenere valori Null in alcun momento.

Se nella tabella non è presente `datetime` , è possibile aggiungere un indice `modified at` colonna. I valori Null non sono consentiti in un `modified at` colonna. Verifica che la colonna sia compilata per ogni riga.

Per garantire `Modified At` il metodo funziona come previsto, non è possibile eliminare righe dalla tabella. È preferibile contrassegnare la riga come non valida aggiungendo un `deleted` nella tabella. Questa colonna restituisce un `1` se la riga non è valida e `0` altrimenti. Puoi quindi utilizzare questa colonna per filtrare le righe non valide durante la creazione di metriche e rapporti.

## Modifiche per la chiave primaria con incremento automatico singolo

Se il `Modified At` non può essere abilitato, l’opzione Migliore successiva è l’opzione Singola chiave primaria con incremento automatico. I nuovi dati vengono rilevati nelle tabelle utilizzando questo metodo ricercando valori di chiave primaria superiori al valore massimo corrente nella Data Warehouse.

Le tabelle che utilizzano questo metodo sono a colonna singola con chiavi primarie a incremento automatico di numeri interi. Per utilizzare questo metodo nel database, effettuare le seguenti modifiche:

* Se la chiave primaria è una chiave composita o non è un numero intero, impostare la chiave primaria su un numero intero incrementale automatico
* Se la chiave primaria è una singola colonna di numeri interi ma le chiavi possono essere assegnate in modo non sequenziale, impostare la chiave primaria su incremento automatico

## Ritorno a capo

Apportando modifiche minori alle tabelle, è possibile sfruttare i metodi di replica incrementale più rapidi ed efficienti. Tuttavia, se ciò non fosse possibile, puoi comunque adottare altre misure per [ridurre i tempi di aggiornamento](../best-practices/reduce-update-cycle-time.md) e [ottimizzare il database](../best-practices/opt-db-analysis.md).
