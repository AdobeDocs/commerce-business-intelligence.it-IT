---
title: Tabella preventivo
description: Scopri come utilizzare la tabella delle offerte.
exl-id: 3a1e9239-33a7-429e-bfc8-628c68701710
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---

# Tabella preventivo

La tabella `quote` (`sales_flat_quote` su M1) contiene record in ogni carrello creato nel negozio, indipendentemente dal fatto che siano stati abbandonati o convertiti in un acquisto. Ogni riga rappresenta un carrello. A causa delle dimensioni potenziali di questa tabella, Adobe consiglia di eliminare periodicamente i record se sono soddisfatti determinati criteri, ad esempio se sono presenti carrelli non convertiti di età superiore a 60 giorni.

>[!NOTE]
>
>L&#39;analisi dei carrelli storici abbandonati è possibile solo se non si eliminano i record dalla tabella `quote`. Se elimini i record, potrai vedere solo i carrelli non ancora rimossi dal database.

## Colonne native comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `base_currency_code` | Valuta per tutti i valori acquisiti nei campi `base_*` (ovvero `base_grand_total`, `base_subtotal` e così via). Questo in genere riflette la valuta predefinita del Commerce Store |
| `base_grand_total` | Prezzo finale offerto al cliente per il carrello, dopo l&#39;applicazione di tutte le imposte, spedizione e sconti. Anche se il calcolo preciso è personalizzabile, in generale `base_grand_total` è calcolato come `base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount` |
| `base_subtotal` | Valore lordo della merce di tutti gli articoli inclusi nel carrello. Non sono inclusi imposte, spedizione, sconti e così via |
| `created_at` | Timestamp di creazione del carrello, memorizzato localmente in UTC. A seconda della configurazione in [!DNL Commerce Intelligence], questa marca temporale può essere convertita in un fuso orario di reporting in [!DNL Commerce Intelligence] diverso dal fuso orario del database |
| `customer_email` | Indirizzo e-mail del cliente che ha creato il carrello |
| `customer_id` | `Foreign key` associato alla tabella `customer_entity`, se il cliente è registrato. Unisciti a `customer_entity.entity_id` per determinare gli attributi del cliente associati all&#39;utente che ha creato il carrello. Se il carrello è stato creato tramite l&#39;estrazione guest, questo campo è `NULL` |
| `entity_id` (PC) | Identificatore univoco della tabella, di solito utilizzato nei join ad altre tabelle nell’istanza di Commerce |
| `is_active` | Campo booleano che restituisce &quot;1&quot; se il carrello è stato creato da un cliente e non è ancora stato convertito in un ordine. Restituisce &quot;0&quot; per i carrelli convertiti o creati tramite l’amministratore |
| `items_qty` | Somma della quantità totale di tutti gli articoli inclusi nel carrello |
| `reserved_order_id` | `Foreign key` associato alla tabella `sales_order`. Unisciti a `sales_order.increment_id` per determinare i dettagli dell&#39;ordine associati a un carrello convertito. Per i carrelli non associati a un ordine convertito, `reserved_order_id` rimane `NULL` |
| `store_id` | `Foreign key` associato alla tabella `store`. Partecipa a `store`.`store_id` per determinare quale visualizzazione archivio Commerce è associata al carrello |

{style="table-layout:auto"}

## Colonne calcolate comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `Order date` | Timestamp che riflette la data di creazione dell’ordine per i carrelli convertiti. Calcolato unendo `quote.reserved_order_id` a `sales_order.increment_id` e restituendo il campo `sales_order.created_at` |
| `Seconds between cart creation and order` | Tempo trascorso tra la creazione del carrello e la creazione dell’ordine. Calcolato sottraendo `created_at` da `Order date`, restituito come numero intero di secondi |
| `Seconds since cart creation` | Tempo trascorso tra la data di creazione del carrello e ora. Calcolato sottraendo `created_at` dalla marca temporale del server al momento dell&#39;esecuzione della query, restituito come numero intero di secondi. Utilizzato più comunemente per identificare l’età di un carrello |
| `Store name` | Nome dell&#39;archivio Commerce associato a questo ordine. Calcolato unendo `quote.store_id` a `store.store_id` e restituendo il campo `name` |

{style="table-layout:auto"}

## Metriche comuni

| **Nome metrica** | **Descrizione** | **Costruzione** |
|---|---|---|
| `Number of abandoned carts` | Il numero di carrelli che soddisfano specifiche condizioni di &quot;abbandono&quot; | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/>Filtri:<br><br>- \[`A`\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x, dove &quot;x&quot; corrisponde al tempo trascorso (in secondi) dalla creazione del carrello oltre il quale un carrello viene considerato abbandonato |
| `Avg time to cart conversion` | Tempo medio tra la creazione del carrello e la creazione dell&#39;ordine per i carrelli convertiti | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | La somma del totale dei ricavi potenziali del carrello abbandonato, dove i ricavi sono definiti come il campo `base_grand_total` | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br>Filtri:<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x, dove &quot;x&quot; corrisponde al tempo trascorso (in secondi) dalla creazione del carrello oltre il quale un carrello viene considerato abbandonato |

{style="table-layout:auto"}

## Percorsi di unione chiave esterna

`customer_entity`

* Partecipa alla tabella `customer_entity` per creare nuove colonne a livello di cliente associate al cliente che ha creato il carrello.
   * Percorso: `quote.customer_id` (molti) => `customer_entity.entity_id` (uno)

`sales_order`

* Partecipa alla tabella `sales_order` per creare colonne che restituiscono i dettagli dell&#39;ordine associati a un carrello convertito.
   * Percorso: `quote.reserved_order_id` (molti) => `sales_order.increment_id` (uno)

`store`

* Partecipa alla tabella `store` per creare colonne che restituiscono dettagli relativi all&#39;archivio Commerce associato al carrello.
   * Percorso: `quote.store_id` (molti) => `store.store_id` (uno)
