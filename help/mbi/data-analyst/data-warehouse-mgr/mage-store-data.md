---
title: Memorizzazione di dati in Commerce
description: Scopri come vengono generati i dati, cosa causa esattamente l’inserimento di una nuova riga in una delle tabelle Commerce principali e come vengono registrate le azioni quali l’acquisto o la creazione di un account nel database Commerce.
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 0%

---

# Memorizzazione dei dati in [!DNL Magento]

La piattaforma Commerce registra e organizza un&#39;ampia varietà di preziosi dati di e-commerce in centinaia di tabelle. In questo argomento viene illustrato come vengono generati i dati e cosa causa esattamente l’inserimento di una nuova riga in uno degli [Tabelle Commerce principali](../data-warehouse-mgr/common-mage-tables.md)e come vengono registrate nel database Commerce le azioni quali l’acquisto o la creazione di un account. Per spiegare questi concetti, fai riferimento al seguente esempio:

`Clothes4U` è un rivenditore di abbigliamento con sia una presenza online, sia una presenza di mattoni e mortai. Utilizza il Magento Open Source dietro il suo sito web per raccogliere e organizzare i dati.

## `catalog\_product\_entity`

È il 22 settembre, e `Clothes4U` sta eseguendo il rollout di tre nuovi elementi nella sua linea Autunno: `Throwback Bellbottoms`, `Straight Leg Jeans`e `V-Neck T-Shirts`. A `Clothes4U` il dipendente apre il proprio amministratore Commerce e fa clic su **[!UICONTROL Add Product]** e immette tutte le informazioni per `Throwback Bellbottoms`.

Soddisfatto di tutte le impostazioni per `Throwback Bellbottoms`, il dipendente fa clic su **[!UICONTROL Save]**, che inserisce la prima riga sottostante nel `catalog_product_entity` tabella. Il dipendente ripete il processo, creando un altro nuovo prodotto Commerce per `Straight Leg Jeans`e poi un terzo per `V-Neck T-Shirt`, inserendo la seconda e la terza riga nella `catalog_product_entity` tabella:

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Pantaloni10 | 09/06/22 09:15:43 |
| 206 | 4 | 8 | Pantaloni11 | 09/06/22 09:18:17 |
| 207 | 4 | 12 | Camicie6 | 09/06/22 09:24:02 |

* `entity_id` - Questa è la chiave primaria del `catalog_product_entity` tabella, ovvero ogni riga della tabella deve avere un `entity_id`. Ogni `entity_id` in questa tabella è possibile associare un solo prodotto e ogni prodotto può essere associato a un solo prodotto `entity_id`
   * la riga superiore della tabella precedente, `entity_id` = 205, è la nuova riga creata per &quot;Throwback Bellbottoms&quot;. Ovunque `entity_id` = 205 appare nella piattaforma Commerce, si riferirà al prodotto &quot;Throwback Bellbottoms&quot;
* `entity_type_id` - Commerce dispone di più categorie di oggetti (come clienti, indirizzi e prodotti per denominarne alcuni) e questa colonna viene utilizzata per indicare la categoria in cui rientra questa particolare riga.
   * Questo è il `catalog_product_entity` tabella, ogni riga ha lo stesso tipo di entità: prodotto. Al Magento, il `entity_type_id` per il prodotto è 4, che è il motivo per cui tutti e tre i nuovi prodotti creati restituisce 4 per questa colonna.
* `attribute_set_id` - I set di attributi vengono utilizzati per identificare i prodotti con lo stesso numero di descrittori.
   * Le prime due righe della tabella sono `Throwback Bellbottoms` e `Straight Leg Jeans` prodotti, entrambi pantaloni. Questi prodotti avrebbero gli stessi descrittori (ad esempio, nome, inseam, vita) e quindi hanno lo stesso `attribute_set_id`. il terzo punto, `V-Neck T-Shirt` ha un `attribute_set_id` perché non avrebbe gli stessi descrittori dei pantaloni; le camicie non hanno vita o incudine.
* `sku` - Si tratta di valori univoci assegnati a ciascun prodotto dall’utente durante la creazione di un nuovo prodotto nel Magento.
* `created_at` - Questa colonna restituisce il timestamp di quando è stato creato ogni prodotto

## `customer\_entity`

Poco dopo l&#39;aggiunta dei tre nuovi prodotti, un nuovo cliente, `Sammy Customer`, visite `Clothes4U`Per la prima volta il sito web di Sony. Da `Clothes4U` non [consenti ordini agli ospiti](https://support.magento.com/hc/en-us/articles/360016729951-Common-Magento-Misconceptions), `Sammy Customer` deve prima creare un account sul sito web. immette le sue credenziali e fa clic su invia, con conseguente nuova voce sulla [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md):

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id` - Proprio come la tabella precedente, `entity_id` è la chiave primaria del `customer_entity` tabella.
   * Quando `Sammy Customer` ha creato il suo account e la riga precedente è stata scritta nel `customer_entity` tabella, è stata assegnata `entity_id` = 214. In tutte le tabelle, il cliente identificato come `entity_id` = 214 farà sempre riferimento all&#39;utente Sammy Customer
* `entity_type_id` - Questa colonna identifica il tipo di entità elencato in questa tabella e funziona nello stesso modo in cui lo fa in `catalog_product_entity` tabella
   * Ogni riga `customer_entity` La tabella sarà un cliente e Commerce definisce i clienti come `entity_type_id` 1 per impostazione predefinita
* `email` - questo campo viene compilato tramite l’e-mail inviata da un nuovo cliente al momento della creazione del proprio account
* `created_at` - Questa colonna restituisce il timestamp per l&#39;unione di ogni utente

## `sales\_flat\_order (or Sales\_order` se disponi di Commerce 2.0 o versione successiva)

Al termine della creazione del suo account, `Sammy Customer` è pronta a iniziare a fare il suo acquisto. Mentre naviga sul sito web, aggiunge due coppie di `Throwback Bellbottoms` e uno `V-Neck T-Shirt` al carrello. Soddisfatta delle sue selezioni, si sposta al pagamento e invia il suo ordine, creando la seguente voce sul [tabella degli ordini piatti delle vendite](../data-warehouse-mgr/sales-flat-order-table.md):

| **`entity id`** | **`customer id**`**`subtotal`****`created at`** |
|---|---|---|---|
| 227 | 214 | 94,85 | 09/09/2016/23 15:41:39 |

* `entity_id` - questa è la chiave primaria del `sales_flat_order` tabella.
   * Quando Sammy Customer ha effettuato questo ordine e la riga precedente è stata scritta nel `sales_flat_order` tabella, l&#39;ordine è stato assegnato `entity_id` = 227.
* `customer_id` - Questa colonna è l’identificatore univoco del cliente che ha effettuato questo particolare ordine
   * La `customer_id` associato a questo ordine è 214, che è del cliente Sammy `entity_id` sulla `customer_entity` tabella.
* `subtotal` - Questa colonna rappresenta l&#39;importo totale addebitato a un cliente per l&#39;ordine
   * Le 2 coppie di &quot;Bellbottoms di Throwback&quot; e la &quot;T-shirt di V-Neck&quot; costano $94,85 dollari in totale
* `created_at` - Questa colonna restituisce il timestamp per la creazione di ogni ordine

## `sales\_flat\_order\_item ( or Sales\_order\_item` se disponi di Commerce 2.0 o versione successiva)

Oltre alla riga singola sul `Sales\_flat\_order` tabella, quando `Sammy Customer` invia il suo ordine, viene inserita una riga per ogni elemento univoco in tale ordine nel [`sales\_flat\_order\_item` tabella](../data-warehouse-mgr/sales-flat-order-item-table.md):

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39,95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14,95 |

* `item_id` - Questa colonna è la chiave primaria del `sales_flat_order_item` tabella
   * `Sammy Customer`L&#39;ordine di questa tabella ha creato due linee perché il suo ordine conteneva due prodotti distinti
* `name` - Questa colonna è il nome del prodotto
* `product_id` - Questa colonna è l’identificatore univoco del prodotto a cui fa riferimento questa riga
   * La prima riga sopra ha `product_id` = 205 perché `Throwback Bellbottoms` hanno `entity_id` del 2005 sulla `catalog_product_entity` tabella
* `order_id` - Questa colonna è `entity_id` dell&#39;ordine che contiene questi particolari articoli d&#39;ordine
   * Entrambe le righe sopra hanno `order_id` = 227 perché entrambi fanno parte dell&#39;ordine disposto da `Sammy Customer`, che `entity_id` = 227 sul `sales_flat_order` tabella
* `qty_ordered` - Questa colonna è il numero di unità del prodotto incluse in questo ordine specifico
   * `Sammy Customer`L&#39;ordine conteneva 2 paia di `Throwback Bellbottoms`
* `price` - Questa colonna è il prezzo di una singola unità dell&#39;articolo dell&#39;ordine
   * La `subtotal` da `Sammy Customer`dell&#39;ordine `sales_flat_order` la tabella era 94.85, che è la somma di 2 paia di `Throwback Bellbottoms` a $ 39,95 ciascuno e 1 `V-Neck T-Shirt` a $ 14,95.
