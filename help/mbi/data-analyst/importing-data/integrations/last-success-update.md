---
title: Comprendere i risultati tra il database e l'editor SQL
description: Scopri come comprendere i risultati tra database ed editor SQL.
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# Risultati database e `SQL Editor` Risultati

Potresti essere curioso di sapere cosa... `Last successful update began` il campo è all&#39;interno del `Integrations` pagina:

![Ultimo_aggiornamento_riuscito.png](../../../assets/Last_successful_update.png)

## Comprendere la `timestamp` campo

Mostra l&#39;inizio `timestamp` (nel fuso orario impostato sul tuo account) del _ultimo ciclo di aggiornamento riuscito_ sul tuo account.

- Se una delle tabelle sincronizzate ha riscontrato un problema durante l’ultimo ciclo di aggiornamento, il timestamp è *non aggiornato*.
- Di conseguenza, in alcuni casi i report possono essere stati aggiornati con dati aggiornati, ma il *L’ultimo aggiornamento riuscito è iniziato* è ancora in ritardo.

## Identificare l’ultimo punto dati &quot;reale&quot;

Il punto dati più recente per una particolare integrazione è determinato da `Last Data Point Received` `timestamp` si trova a destra di ogni integrazione. Tale marca temporale si riferisce all’ultimo punto in cui la tua Data Warehouse ha ricevuto correttamente punti dati da tale origine, che si tratti di un database, di un’API o di un’integrazione di terze parti.

Per verificare l&#39;aggiornamento dei dati da *tabelle specifiche*, Adobe consiglia di creare un [Report SQL](../../dev-reports/sql-rpt-bldr.md) che esegue un `MAX(timestamp)` nella tabella più importante del tuo account. Confronto di questa marca temporale con `Last Data Point` indica se il problema ha interessato l’intero account o un sottoinsieme delle tabelle. L’Adobe consiglia di eseguire questa operazione per tre o quattro tabelle importanti e di uso comune.

- Se il `MAX(timestamp)` i valori sono più recenti di `Last Data Point Received`Ciò significa che un sottoinsieme delle tabelle è stato interessato, ma il ciclo di aggiornamento del conto complessivo è stabile.
- Se il `MAX(timestamp)` i valori sono uguali o precedenti a `Last Data Point Received`, significa che il ciclo di aggiornamento dell’account è stato interessato. In questa situazione, [invia un ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
