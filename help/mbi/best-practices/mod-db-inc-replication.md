---
title: Modifica del database per supportare la replica incrementale
description: Scopri come modificare il database per supportare la replica incrementale.
exl-id: c9a38892-6096-4eb5-8a53-35b8b7b083dc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# Supporto per la replica incrementale

Se le tabelle non consentono attualmente la replica incrementale, consulta le seguenti raccomandazioni per le possibili soluzioni.

## Modifiche alla data di modifica

La `Modified At` , che è il metodo di replica più ideale, utilizza un `datetime` per rilevare dati nuovi e/o aggiornati. Ricorda che `datetime` le colonne nelle tabelle che utilizzano questo metodo devono essere indicizzate e non possono contenere valori null in qualsiasi momento.

Se la tabella non dispone di un `datetime` è possibile aggiungere un indice `modified at` colonna. Valori Null non consentiti in un `modified at` colonna. Verifica che la colonna sia compilata per ogni riga.

Per garantire `Modified At` non è possibile eliminare le righe dalla tabella. È invece necessario contrassegnare la riga come non valida aggiungendo un `deleted` alla tabella. Questa colonna restituirà un `1` se la riga non è valida e `0` altrimenti. Puoi quindi utilizzare questa colonna per filtrare le righe non valide durante la creazione di metriche e rapporti.

## Modifiche per l&#39;incremento automatico singolo della chiave primaria

Se la `Modified At` Impossibile abilitare il metodo , quindi l&#39;opzione migliore successiva è la chiave principale di incremento automatico singola. I nuovi dati vengono rilevati nelle tabelle utilizzando questo metodo, ricercando valori di chiave primaria superiori al valore corrente più alto nella Data Warehouse.

Le tabelle che utilizzano questo metodo sono singole colonne con numeri interi che incrementano automaticamente le chiavi primarie. Per utilizzare questo metodo nel database, apporta le seguenti modifiche:

* Se la chiave primaria è una chiave composita o non intera, cambia la chiave primaria in un numero intero che incrementa automaticamente
* Se la chiave primaria è una singola colonna intera ma le chiavi possono essere assegnate in modo non sequenziale, cambiare la chiave primaria in incremento automatico

## Ritorno a capo

Apportare modifiche minori alle tabelle consente di sfruttare i metodi di replica incrementale più rapidi ed efficienti; tuttavia, se ciò non è ancora possibile, puoi comunque adottare altre misure per [ridurre i tempi di aggiornamento](../best-practices/reduce-update-cycle-time.md) e [ottimizzare il database](../best-practices/opt-db-analysis.md).
