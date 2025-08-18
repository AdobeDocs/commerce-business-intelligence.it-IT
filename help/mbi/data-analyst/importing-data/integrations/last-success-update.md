---
title: Comprendere i risultati tra il database e l'editor SQL
description: Scopri come comprendere i risultati tra database ed editor SQL.
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# Risultati database vs. [!DNL SQL Editor] risultati

Potresti essere curioso di sapere cosa contiene il campo `Last successful update began` nella tua pagina `Integrations`:

![Ultimo_aggiornamento_riuscito.png](../../../assets/Last_successful_update.png)

## Comprendere il campo `timestamp`

Mostra l&#39;inizio `timestamp` (nel fuso orario impostato sul tuo account) dell&#39;_ultimo ciclo di aggiornamento riuscito_ sul tuo account.

- Se una delle tabelle sincronizzate ha rilevato un problema durante l&#39;ultimo ciclo di aggiornamento, il timestamp è *non aggiornato*.
- Di conseguenza, possono verificarsi casi in cui i report sono stati aggiornati con nuovi dati, ma l&#39;*Ultimo aggiornamento riuscito è iniziato* è ancora in ritardo.

## Identificare l’ultimo punto dati &quot;reale&quot;

Il punto dati più recente per una particolare integrazione è determinato dalla marca temporale `Last Data Point Received` situata a destra di ciascuna integrazione. Tale timestamp si riferisce all’ultimo punto in cui il Data Warehouse ha ricevuto correttamente i punti dati da tale origine, che si tratti di un database, di un’API o di un’integrazione di terze parti.

Per verificare l&#39;aggiornamento dei dati da *tabelle specifiche*, Adobe consiglia di creare un [[!DNL SQL] report](../../dev-reports/sql-rpt-bldr.md) rapido che esegua `MAX(timestamp)` sulla tabella più importante del tuo account. Il confronto di questa marca temporale con `Last Data Point` indica se il problema ha interessato l&#39;intero account o un sottoinsieme delle tabelle. Adobe consiglia di eseguire questa operazione per tre o quattro tabelle importanti e di uso comune.

- Se i valori `MAX(timestamp)` sono più recenti di `Last Data Point Received`, significa che un sottoinsieme delle tabelle è stato interessato, ma il ciclo di aggiornamento complessivo del conto è stabile.
- Se i valori `MAX(timestamp)` sono uguali o precedenti a `Last Data Point Received`, significa che il ciclo di aggiornamento dell&#39;account è stato interessato. In questa situazione, [invia un ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
