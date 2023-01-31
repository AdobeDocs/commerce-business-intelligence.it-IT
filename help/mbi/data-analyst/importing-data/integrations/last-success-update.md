---
title: Comprendere i risultati tra il database e l'editor SQL
description: Scopri i risultati tra il database e l'editor SQL.
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# Risultati del database e `SQL Editor` Risultati

Puoi essere curioso di sapere cosa `Last successful update began` all&#39;interno del campo `Integrations` pagina:

![Last_success_update.png](../../../assets/Last_successful_update.png)

## Comprendere il `timestamp` field

Mostra l&#39;inizio `timestamp` (nel fuso orario impostato sul tuo account) del _ultimo ciclo di aggiornamento riuscito_ sul tuo account.

- Se una delle tabelle sincronizzate ha riscontrato un problema durante l&#39;ultimo ciclo di aggiornamento, la marca temporale è *non aggiornato*.
- Di conseguenza, possono verificarsi casi in cui i rapporti sono stati aggiornati con nuovi dati, ma *Ultimo aggiornamento completato* è ancora in ritardo.

## Identificare l&#39;ultimo punto dati &quot;reale&quot;

L&#39;ultimo punto dati per una particolare integrazione è determinato dal `Last Data Point Received` `timestamp` a destra di ogni integrazione. Tale marca temporale si riferisce all&#39;ultimo punto in cui il data warehouse ha ricevuto correttamente i punti dati da tale origine, che si tratti di un database, API o integrazione di terze parti.

Per verificare la freschezza dei dati da *tabelle specifiche*, si consiglia di creare una [Report SQL](../../dev-reports/sql-rpt-bldr.md) che esegue `MAX(timestamp)` sulla tabella più importante del tuo account. Confronto di questa marca temporale con `Last Data Point` indicherà se il problema ha interessato l&#39;intero conto o un sottoinsieme delle tabelle. Si consiglia di eseguire questa operazione per tre o quattro tabelle importanti di uso comune.

- Se la `MAX(timestamp)` valori più recenti di `Last Data Point Received`Ciò significa che un sottoinsieme delle tabelle è stato interessato, ma il ciclo di aggiornamento complessivo del conto è stabile.
- Se la `MAX(timestamp)` sono uguali o precedenti a `Last Data Point Received`, significa che il ciclo di aggiornamento dell’account è stato interessato. In tale situazione, [inviare un ticket di supporto](../../../guide-overview.md).
