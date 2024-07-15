---
title: tabella customer_entity
description: Scopri come accedere ai record di tutti gli account registrati.
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '610'
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
