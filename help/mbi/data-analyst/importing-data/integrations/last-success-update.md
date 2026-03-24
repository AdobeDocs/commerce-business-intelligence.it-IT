---
title: Comprendere i risultati tra il database e l'editor SQL
description: Scopri come comprendere i risultati tra database ed editor SQL.
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/pScH-yKW8hbSNZzsJ537CN7rxhcuygaLmCu3fdVaYgk
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 257
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
- Se i valori `MAX(timestamp)` sono uguali o precedenti a `Last Data Point Received`, significa che il ciclo di aggiornamento dell&#39;account è stato interessato. In questa situazione, [invia un ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=it).
