---
title: tabella customer_entity
description: Scopri come accedere ai record di tutti gli account registrati.
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/iTzls4nEtW9ep-3s536ZnRCCr2TeMD6AsDecZc3Cdys
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 610
ht-degree: 0%

---

# tabella customer_entity

La tabella `customer_entity` contiene i record di tutti gli account registrati. Un account viene considerato registrato se si iscrive a un account, indipendentemente dal fatto che abbia completato o meno un acquisto. Ogni riga corrisponde a un account registrato univoco, identificato dall&#39;account `entity_id` dell&#39;account.

Questa tabella non contiene i record dei clienti che effettuano un ordine tramite il pagamento come ospite. Se il tuo negozio accetta l&#39;acquisto degli ospiti, consulta [come gestire gli ordini degli ospiti](../data-warehouse-mgr/guest-orders.md) per tali ordini.

## Colonne comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `created_at` | Marca temporale corrispondente alla data di registrazione dell’account, memorizzata localmente in UTC. A seconda della configurazione in [!DNL Commerce Intelligence], questa marca temporale può essere convertita in un fuso orario di reporting in [!DNL Commerce Intelligence] diverso dal fuso orario del database |
| `email` | Indirizzo e-mail associato all’account |
| `entity_id` (PC) | Identificatore univoco della tabella, di solito utilizzato nei join di `customer_id` in altre tabelle dell&#39;istanza |
| `group_id` | Chiave esterna associata alla tabella `customer_group`. Partecipa a `customer_group.customer_group_id` per determinare il gruppo di clienti associato all&#39;account registrato |
| `store_id` | Chiave esterna associata alla tabella `store`. Partecipa a `store`.`store_id` per determinare quale visualizzazione archivio Commerce è associata all&#39;account registrato |

{style="table-layout:auto"}

## Colonne calcolate comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `Customer's first 30 day revenue` | Somma il totale dei ricavi per tutti gli ordini effettuati dal cliente entro 30 giorni dalla data del primo ordine del cliente. Calcolato unendo `customer_entity.entity_id` a `sales_order.customer_id` e sommando il campo `base_grand_total` per tutti gli ordini in cui `sales_order.Seconds between customer's first order date and this order` ≤ 2592000, ovvero il numero di secondi in 30 giorni |
| `Customer's first order date` | Timestamp del primo ordine effettuato da questo cliente. Calcolato unendo `customer_entity.entity_id` a `sales_order.customer_id` e restituendo il minimo `sales_order`.Valore `created_at` |
| `Customer's first order's billing region` | Area di fatturazione associata al primo ordine del cliente. Calcolato unendo `customer_entity.entity_id` a `sales_order.customer_id` e restituendo `Billing address region` dove `sales_order.Customer's order number` = 1 |
| `Customer's first order's coupon_code` | Codice coupon associato al primo ordine del cliente. Calcolato unendo `customer_entity.entity_id` a `sales_order.customer_id` e restituendo `sales_order.coupon_code` dove `sales_order.Customer's order number` = 1 |
| `Customer's group code` | Nome del gruppo del cliente registrato. Calcolato unendo `customer_entity.group_id` a `customer_group`.`customer_group_id` e restituzione del campo `customer_group_code` |
| `Customer's lifetime number of coupons` | Numero totale di coupon applicati a tutti gli ordini effettuati dal cliente. Calcolato unendo `customer_entity.entity_id` a `sales_order.customer_id` e contando il numero di ordini in cui `sales_order.coupon_code` non è `NULL` |
| `Customer's lifetime number of orders` | Numero totale di ordini effettuati dal cliente. Calcolato unendo `customer_entity.entity_id` a `sales_order.customer_id` e contando il numero di righe nella tabella `sales_order` |
| `Customer's lifetime revenue` | Somma il totale dei ricavi per tutti gli ordini effettuati dal cliente. Calcolato unendo `customer_entity.entity_id` a `sales_order.customer_id` e sommando il campo `base_grand_total` per tutti gli ordini effettuati da questo cliente |
| `Seconds since customer's first order date` | Tempo trascorso tra la data del primo ordine del cliente e ora. Calcolato sottraendo `Customer's first order date` dalla marca temporale del server al momento dell&#39;esecuzione della query, restituito come numero intero di secondi |
| `Store name` | Il nome dell&#39;archivio Commerce associato a questo account registrato. Calcolato unendo `customer_entity.store_id` a `store.store_id` e restituendo il campo `name` |

{style="table-layout:auto"}

## Metriche comuni

| **Nome metrica** | **Descrizione** | **Costruzione** |
|---|---|---|
| `Avg first 30 day revenue` | Ricavo medio per cliente per gli ordini effettuati entro 30 giorni dal primo ordine del cliente | Operazione: Media<br/>Operando: `Customer's first 30 day revenue`<br/>Timestamp: `created_at`<br/>Filtri:<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000 (esclusi i clienti che non hanno ancora raggiunto i 30 giorni dal primo ordine) |
| `Avg lifetime coupons` | Numero medio di coupon applicati agli ordini per cliente nel corso della loro durata | Operazione: Average<br/>Operando: `Customer's lifetime number of coupons`<br/>Timestamp: `created_at` |
| `Avg lifetime orders` | Il numero medio di ordini effettuati per cliente nel corso della loro durata | Operazione: Average<br/>Operando: `Customer's lifetime number of orders`<br/>Timestamp: `created_at` |
| `Avg lifetime revenue` | Ricavi totali medi per cliente per tutti gli ordini effettuati nel corso della loro durata | Operazione: Average<br/>Operando: `Customer's lifetime revenue`<br/>Timestamp: `created_at` |
| `New customers` | Il numero di clienti con almeno un ordine, conteggiato alla data del primo ordine. Esclude gli account che si registrano ma che non effettuano mai un ordine | Operazione: Count<br/>Operando: `entity_id`<br/>Timestamp: `Customer's first order date` |
| `Registered accounts` | Numero di account registrati. Include tutti gli account registrati, indipendentemente dal fatto che abbiano effettuato un ordine | Operazione: Count<br/>Operando: `entity_id`<br/>Timestamp: `created_at` |

{style="table-layout:auto"}

## Percorsi di unione chiave esterna

`customer_group`

* Partecipa alla tabella `customer_group` per creare colonne che restituiscono il nome del gruppo di clienti dell&#39;account registrato.
   * Percorso: `customer_entity.group_id` (molti) => `customer_group.customer_group_id` (uno)

`store`

* Partecipa alla tabella `store` per creare colonne che restituiscono dettagli relativi all&#39;archivio associato all&#39;account registrato.
   * Percorso: `customer_entity.store_id` (molti) => `store.store_id` (uno)
