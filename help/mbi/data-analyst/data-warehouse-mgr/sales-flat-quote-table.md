---
title: tabella dei preventivi
description: Scopri come utilizzare la tabella delle virgolette.
exl-id: 3a1e9239-33a7-429e-bfc8-628c68701710
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# tabella dei preventivi

La `quote` tabella (`sales_flat_quote` su M1) contiene record su ogni carrello creato nel tuo negozio, sia che siano stati abbandonati o convertiti in un acquisto. Ogni riga rappresenta un carrello. A causa delle dimensioni potenziali di questa tabella, ti consigliamo di eliminare periodicamente i record se vengono soddisfatti determinati criteri, ad esempio se sono presenti carrelli non convertiti con età superiore a 60 giorni.

>[!NOTE]
>
>L&#39;analisi dei carrelli abbandonati storici è possibile solo se non si eliminano i record dal `quote` tabella. Se elimini i record, potrai solo vedere i carrelli non ancora rimossi dal tuo database.

## Colonne native comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `base_currency_code` | Valuta per tutti i valori acquisiti in `base_*` campi `base_grand_total`, `base_subtotal`e così via). In genere questo riflette la valuta predefinita dell’archivio Commerce |
| `base_grand_total` | Prezzo finale indicato al cliente per il carrello, dopo l&#39;applicazione di tutte le tasse, la spedizione e gli sconti. Sebbene il calcolo preciso sia personalizzabile, in generale il `base_grand_total` è calcolato come segue `base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount` |
| `base_subtotal` | Valore commerciale lordo di tutti gli elementi inclusi nel carrello. Tasse, spedizioni, sconti e così via non sono inclusi |
| `created_at` | Timestamp di creazione del carrello, in genere memorizzato localmente in UTC. A seconda della configurazione in [!DNL MBI], questa marca temporale può essere convertita in un fuso orario per la generazione di rapporti in [!DNL MBI] diverso dal fuso orario del database |
| `customer_email` | Indirizzo e-mail del cliente che ha creato il carrello |
| `customer_id` | `Foreign key` associato a `customer_entity` se il cliente è registrato. Iscriviti a `customer_entity.entity_id` per determinare gli attributi del cliente associati all’utente che ha creato il carrello. Se il carrello è stato creato tramite il pagamento per gli ospiti, questo campo sarà `NULL` |
| `entity_id` (PK) | Identificatore univoco per la tabella e comunemente utilizzato nei join ad altre tabelle all’interno dell’istanza Commerce |
| `is_active` | Campo booleano che restituisce &quot;1&quot; se il carrello è stato creato da un cliente e non è ancora stato convertito in un ordine. Restituisce &quot;0&quot; per i carrelli convertiti, o i carrelli creati tramite l’amministratore |
| `items_qty` | Somma della quantità totale di tutti gli articoli inclusi nel carrello |
| `reserved_order_id` | `Foreign key` associato a `sales_order` tabella. Iscriviti a `sales_order.increment_id` per determinare i dettagli dell’ordine associati a un carrello convertito. Per i carrelli che non sono associati a un ordine convertito, la variabile `reserved_order_id` rimarrà `NULL` |
| `store_id` | `Foreign key` associato a `store` tabella. Iscriviti a `store`.`store_id` per determinare quale visualizzazione dell’archivio Commerce è associata al carrello |

{style=&quot;table-layout:auto&quot;}

## Colonne calcolate comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `Order date` | Timestamp che riflette la data di creazione dell&#39;ordine per i carrelli convertiti. Calcolato mediante unione `quote.reserved_order_id` a `sales_order.increment_id` e restituendo `sales_order.created_at` field |
| `Seconds between cart creation and order` | Tempo trascorso tra la creazione del carrello e la creazione dell’ordine. Calcolato mediante sottrazione `created_at` da `Order date`, restituito come numero intero di secondi |
| `Seconds since cart creation` | Tempo trascorso tra la data di creazione del carrello e ora. Calcolato mediante sottrazione `created_at` dal timestamp del server al momento dell’esecuzione della query, restituito come numero intero di secondi. Utilizzato più comunemente per identificare l&#39;età di un carrello |
| `Store name` | Nome dell&#39;archivio Commerce associato a questo ordine. Calcolato mediante unione `quote.store_id` a `store.store_id` e restituendo `name` field |

{style=&quot;table-layout:auto&quot;}

## Metriche comuni

| **Nome della metrica** | **Descrizione** | **Costruzione** |
|---|---|---|
| `Number of abandoned carts` | Numero di carrelli che soddisfano specifiche condizioni di &quot;abbandono&quot; | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/>Filtri:<br><br>- \[`A`\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x, dove &quot;x&quot; corrisponde al tempo trascorso (in secondi) dalla creazione del carrello oltre il quale un carrello è considerato abbandonato |
| `Avg time to cart conversion` | Tempo medio tra la creazione del carrello e la creazione dell&#39;ordine per i carrelli convertiti | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | La somma del totale dei ricavi potenziali del carrello abbandonati, in cui i ricavi sono definiti come `base_grand_total` field | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br>Filtri:<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x, dove &quot;x&quot; corrisponde al tempo trascorso (in secondi) dalla creazione del carrello oltre il quale un carrello è considerato abbandonato |

{style=&quot;table-layout:auto&quot;}

## Percorsi di unione chiave esterna

`customer_entity`

* Iscriviti a `customer_entity` per creare nuove colonne a livello di cliente associate al cliente che ha creato il carrello.
   * Percorso: `quote.customer_id` (molti) => `customer_entity.entity_id` 1)

`sales_order`

* Iscriviti a `sales_order` per creare nuove colonne i cui dettagli dell’ordine di restituzione sono associati a un carrello convertito.
   * Percorso:`quote.reserved_order_id` (molti) => `sales_order.increment_id` 1)

`store`

* Iscriviti a `store` per creare nuove colonne che restituiscono i dettagli relativi all’archivio Commerce associato al carrello.
   * Percorso: `quote.store_id` (molti) => `store.store_id` 1)
