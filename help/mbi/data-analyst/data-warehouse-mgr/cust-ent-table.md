---
title: tabella customer_entity
description: Scopri come accedere ai record di tutti gli account registrati.
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---

# tabella customer_entity

La `customer_entity` la tabella contiene i record di tutti i conti registrati. Un account viene considerato registrato se si iscrive a un account, indipendentemente dal fatto che completino o meno un acquisto. Ogni riga corrisponde a un account registrato univoco, identificato dal `entity_id`.

Questa tabella non contiene i record dei clienti che effettuano un ordine tramite il pagamento degli ospiti. Se il tuo negozio accetta il pagamento degli ospiti, [scopri come utilizzare l’account](../data-warehouse-mgr/guest-orders.md) per quei clienti.

## Colonne comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `created_at` | Timestamp corrispondente alla data di registrazione dell&#39;account, in genere memorizzato localmente in UTC. A seconda della configurazione in [!DNL MBI], questa marca temporale può essere convertita in un fuso orario per la generazione di rapporti in [!DNL MBI] diverso dal fuso orario del database |
| `email` | Indirizzo e-mail associato all’account |
| `entity_id` (PK) | Identificatore univoco della tabella e comunemente utilizzato nei join della tabella `customer_id` in altre tabelle all’interno dell’istanza |
| `group_id` | Chiave esterna associata al `customer_group` tabella. Iscriviti a `customer_group.customer_group_id` per determinare il gruppo di clienti associato al conto registrato |
| `store_id` | Chiave esterna associata al `store` tabella. Iscriviti a `store`.`store_id` per determinare quale visualizzazione dell&#39;archivio commerciale è associata all&#39;account registrato |

{style=&quot;table-layout:auto&quot;}

## Colonne calcolate comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `Customer's first 30 day revenue` | Somma totale dei ricavi per tutti gli ordini effettuati dal cliente entro 30 giorni dalla data del primo ordine del cliente. Calcolato mediante unione `customer_entity.entity_id` a `sales_order.customer_id` e sommare `base_grand_total` campo per tutti gli ordini in cui `sales_order.Seconds between customer's first order date and this order` ≤ 2592000, corrispondente al numero di secondi in 30 giorni |
| `Customer's first order date` | Timestamp del primo ordine inserito dal cliente. Calcolato mediante unione `customer_entity.entity_id` a `sales_order.customer_id` e restituire il minimo `sales_order`.`created_at` value |
| `Customer's first order's billing region` | Area di fatturazione associata al primo ordine del cliente. Calcolato mediante unione `customer_entity.entity_id` a `sales_order.customer_id` e restituendo `Billing address region` dove `sales_order.Customer's order number` = 1 |
| `Customer's first order's coupon_code` | Codice coupon associato al primo ordine del cliente. Calcolato mediante unione `customer_entity.entity_id` a `sales_order.customer_id` e restituendo `sales_order.coupon_code` dove `sales_order.Customer's order number` = 1 |
| `Customer's group code` | Nome del gruppo del cliente registrato. Calcolato mediante unione `customer_entity.group_id` a `customer_group`.`customer_group_id` e restituendo `customer_group_code` field |
| `Customer's lifetime number of coupons` | Numero totale di coupon applicati a tutti gli ordini immessi dal cliente. Calcolato mediante unione `customer_entity.entity_id` a `sales_order.customer_id` e contando il numero di ordini in cui `sales_order.coupon_code` non `NULL` |
| `Customer's lifetime number of orders` | Totale degli ordini effettuati dal cliente. Calcolato mediante unione `customer_entity.entity_id` a `sales_order.customer_id` e contando il numero di righe nel `sales_order` tabella |
| `Customer's lifetime revenue` | Somma totale dei ricavi per tutti gli ordini effettuati dal cliente. Calcolato mediante unione `customer_entity.entity_id` a `sales_order.customer_id` e sommare `base_grand_total` campo per tutti gli ordini effettuati dal cliente |
| `Seconds since customer's first order date` | Tempo trascorso tra la data del primo ordine del cliente e ora. Calcolato mediante sottrazione `Customer's first order date` dal timestamp del server al momento dell’esecuzione della query, restituito come numero intero di secondi |
| `Store name` | Nome dell&#39;archivio commerciale associato a questo account registrato. Calcolato mediante unione `customer_entity.store_id` a `store.store_id` e restituendo `name` field |

{style=&quot;table-layout:auto&quot;}

## Metriche comuni

| **Nome della metrica** | **Descrizione** | **Costruzione** |
|---|---|---|
| `Avg first 30 day revenue` | Ricavo medio per cliente per gli ordini effettuati entro 30 giorni dal primo ordine del cliente | Operazione: Media<br/>Operatore: `Customer's first 30 day revenue`<br/>Timestamp: `created_at`<br/>Filtri:<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000 (esclusi i clienti che non hanno ancora raggiunto i 30 giorni dal loro primo ordine) |
| `Avg lifetime coupons` | Numero medio di coupon applicati agli ordini per cliente nel corso della loro vita | Operazione: Media<br/>Operatore: `Customer's lifetime number of coupons`<br/>Timestamp: `created_at` |
| `Avg lifetime orders` | Numero medio di ordini effettuati per cliente nel corso della loro vita | Operazione: Media<br/>Operatore: `Customer's lifetime number of orders`<br/>Timestamp: `created_at` |
| `Avg lifetime revenue` | Ricavo totale medio per cliente per tutti gli ordini effettuati nel corso della loro vita | Operazione: Media<br/>Operatore: `Customer's lifetime revenue`<br/>Timestamp: `created_at` |
| `New customers` | Il numero di clienti con almeno un ordine, conteggiato alla data del loro primo ordine. Esclude gli account che si registrano ma non eseguono mai un ordine | Operazione: Conteggio<br/>Operatore: `entity_id`<br/>Timestamp: `Customer's first order date` |
| `Registered accounts` | Numero di account registrati. Include tutti i conti registrati, indipendentemente dal fatto che il conto abbia effettuato o meno un ordine | Operazione: Conteggio<br/>Operatore: `entity_id`<br/>Timestamp: `created_at` |

{style=&quot;table-layout:auto&quot;}

## Percorsi di unione chiave esterna

`customer_group`

* Iscriviti a `customer_group` per creare nuove colonne che restituiscono il nome del gruppo di clienti dell&#39;account registrato.
   * Percorso: `customer_entity.group_id` (molti) => `customer_group.customer_group_id` 1)

`store`

* Iscriviti a `store` per creare nuove colonne che restituiscono i dettagli relativi all&#39;archivio associato all&#39;account registrato.
   * Percorso: `customer_entity.store_id` (molti) => `store.store_id` 1)
