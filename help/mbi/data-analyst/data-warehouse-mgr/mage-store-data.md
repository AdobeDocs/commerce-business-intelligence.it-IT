---
title: Memorizzazione dei dati in Adobe Commerce
description: Scopri come vengono generati i dati, cosa causa l’inserimento di una nuova riga e come vengono registrate le azioni nel database di Adobe Commerce.
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 3%

---

# Memorizzazione dei dati in [!DNL Adobe Commerce]

Il [!DNL Adobe Commerce] platform registra e organizza un’ampia varietà di preziosi dati di e-commerce su centinaia di tabelle. Questo argomento descrive:

* come vengono generati i dati
* che cosa causa l’inserimento di una nuova riga in una delle [Tabelle Commerce Core](../data-warehouse-mgr/common-mage-tables.md)
* in che modo azioni quali l’acquisto o la creazione di un account vengono registrate in [!DNL Adobe Commerce] database

Per discutere di questi concetti, consulta l’esempio seguente:

`Clothes4U` è un rivenditore di abbigliamento con presenze sia online che in mattoni e malta. Utilizza [!DNL Magento Open Source] per raccogliere e organizzare i dati.

## `catalog\_product\_entity`

È il 22 settembre, e `Clothes4U` : sta implementando tre nuovi elementi nella linea Autunno: `Throwback Bellbottoms`, `Straight Leg Jeans`, e `V-Neck T-Shirts`. A `Clothes4U` il dipendente apre il proprio amministratore Commerce, fa clic su **[!UICONTROL Add Product]** e immette tutte le informazioni per `Throwback Bellbottoms`.

Soddisfatto con tutte le impostazioni per `Throwback Bellbottoms`, il dipendente fa clic **[!UICONTROL Save]**, che inserisce la prima riga sotto nel `catalog_product_entity` tabella. Il dipendente ripete il processo, creando un altro prodotto Commerce per `Straight Leg Jeans`e quindi un terzo per `V-Neck T-Shirt`, inserendo la seconda e la terza riga sotto nella `catalog_product_entity` tabella:

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Pants10 | 2016/09/22 09:15:43 |
| 206 | 4 | 8 | Pants11 | 2016/09/22 09:18:17 |
| 207 | 4 | 12 | Shirts6 | 2016/09/22 09:24:02 |

* `entity_id` - Questa è la chiave primaria del `catalog_product_entity` tabella, il che significa che ogni riga della tabella deve avere un `entity_id`. Ogni `entity_id` in questa tabella può essere associato a un solo prodotto e ogni prodotto può essere associato a un solo `entity_id`
   * La riga superiore della tabella precedente, `entity_id` = 205, è la nuova riga creata per &quot;Throwback Bellbottoms&quot;. Ovunque `entity_id` = 205 appare nella piattaforma Commerce, si riferisce al prodotto &quot;Throwback Bellbottoms&quot;
* `entity_type_id` - Commerce ha più categorie di oggetti (come clienti, indirizzi e prodotti per citarne alcuni) e questa colonna viene utilizzata per indicare la categoria in cui rientra questa riga particolare.
   * Questo è il `catalog_product_entity` tabella, ogni riga ha lo stesso tipo di entità: product. In Adobe Commerce, il `entity_type_id` per il prodotto è 4, ed è per questo che tutti e tre i nuovi prodotti creati restituiscono 4 per questa colonna.
* `attribute_set_id` - I set di attributi vengono utilizzati per identificare i prodotti che hanno lo stesso di descrittori.
   * Le prime due righe della tabella sono `Throwback Bellbottoms` e `Straight Leg Jeans` prodotti, entrambi pantaloni. Questi prodotti avrebbero gli stessi descrittori (ad esempio, nome, inseam, girovita) e quindi gli stessi `attribute_set_id`. La terza voce, `V-Neck T-Shirt` ha un diverso `attribute_set_id` perché non avrebbe gli stessi descrittori dei pantaloni; le camicie non hanno girovita o costumi.
* `sku` : si tratta di valori univoci assegnati a ciascun prodotto dall’utente durante la creazione di un prodotto in Adobe Commerce.
* `created_at` - Questa colonna restituisce la marca temporale di quando è stato creato ciascun prodotto

## `customer\_entity`

Poco dopo l&#39;aggiunta dei tre nuovi prodotti, un nuovo cliente, `Sammy Customer`, visite `Clothes4U`per la prima volta il sito Web di. Da `Clothes4U` non consente ordini degli ospiti, `Sammy Customer` deve innanzitutto creare un account sul sito web. Il cliente immette le credenziali richieste e fa clic su invia, con conseguente nuova voce nella [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md):

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id` - Proprio come la tabella precedente, `entity_id` è la chiave primaria del `customer_entity` tabella.
   * Quando `Sammy Customer` ha creato un account e la riga precedente è stata scritta nel `customer_entity` tabella, il cliente è stato assegnato `entity_id` = 214. In tutte le tabelle, il cliente ha identificato come `entity_id` = 214 si riferisce sempre all&#39;utente Sammy Customer
* `entity_type_id` - Questa colonna identifica il tipo di entità elencato in questa tabella e funziona come nella `catalog_product_entity` tabella
   * Ogni riga del `customer_entity` la tabella è un cliente e Commerce definisce i clienti come `entity_type_id` 1 per impostazione predefinita
* `email` : questo campo viene compilato dall’e-mail che un nuovo cliente inserisce quando crea il proprio account
* `created_at` - Questa colonna restituisce la marca temporale per l’iscrizione di ogni utente

## `sales\_flat\_order (or Sales\_order` se ha [!DNL Adobe Commerce 2.x]

Al termine della creazione dell’account, `Sammy Customer` è pronto per iniziare a effettuare un acquisto. Sul sito web, il cliente aggiunge due coppie di `Throwback Bellbottoms` e uno `V-Neck T-Shirt` al carrello. Soddisfatto delle selezioni, il cliente passa al pagamento e invia l&#39;ordine, creando la seguente voce nella [tabella ordini vendite a tariffa fissa](../data-warehouse-mgr/sales-flat-order-table.md):

| **`entity id`** | **`customer id**` | **`subtotal`** | **`created at`** |
|---|---|---|---|
| 227 | 214 | 94.85 | 2016/09/23 15:41:39 |

* `entity_id` - questa è la chiave primaria del `sales_flat_order` tabella.
   * Quando Sammy Customer ha effettuato questo ordine e la riga precedente è stata scritta nel `sales_flat_order` tabella, l&#39;ordine è stato assegnato `entity_id` = 227.
* `customer_id` - Questa colonna è l&#39;identificatore univoco del cliente che ha effettuato questo particolare ordine
   * Il `customer_id` associato a questo ordine è 214, che è di Sammy `entity_id` il `customer_entity` tabella.
* `subtotal` - Questa colonna rappresenta l&#39;importo totale addebitato a un cliente per l&#39;ordine
   * Le due coppie di &quot;Throwback Bellbottoms&quot; e &quot;V-Neck T-Shirt&quot; costarono in totale 94,85 dollari
* `created_at` - Questa colonna restituisce la marca temporale per la creazione di ciascun ordine

## `sales\_flat\_order\_item ( or Sales\_order\_item`

(se hai Commerce 2.0 o versione successiva)

Oltre alla riga singola sulla `Sales\_flat\_order` tabella, quando `Sammy Customer` invia l&#39;ordine, viene inserita una riga per ogni elemento univoco in tale ordine [`sales\_flat\_order\_item` tabella](../data-warehouse-mgr/sales-flat-order-item-table.md):

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39.95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14.95 |

* `item_id` - Questa colonna è la chiave primaria del `sales_flat_order_item` tabella
   * `Sammy Customer`L&#39;ordine di ha creato due righe in questa tabella perché l&#39;ordine conteneva due prodotti distinti
* `name` - Questa colonna è il nome del prodotto
* `product_id` - Questa colonna è l&#39;identificatore univoco del prodotto a cui si riferisce la riga
   * La prima riga qui sopra contiene `product_id` = 205 perché `Throwback Bellbottoms` hanno un `entity_id` del 205 sulla `catalog_product_entity` tabella
* `order_id` - Questa colonna è la `entity_id` dell&#39;ordine che contiene questi particolari elementi dell&#39;ordine
   * Entrambe le righe precedenti hanno `order_id` = 227 perché entrambi fanno parte dell’ordine effettuato da `Sammy Customer`, che ha `entity_id` = 227 sul `sales_flat_order` tabella
* `qty_ordered` - Questa colonna indica il numero di unità del prodotto incluse nell&#39;ordine specifico
   * `Sammy Customer`l&#39;ordine di conteneva due coppie di `Throwback Bellbottoms`
* `price` - Questa colonna è il prezzo di una singola unità dell&#39;articolo dell&#39;ordine
   * Il `subtotal` da `Sammy Customer`dell&#39;ordine in `sales_flat_order` la tabella era 94,85, che è la somma di due coppie di `Throwback Bellbottoms` a $ 39,95 ciascuno e 1 `V-Neck T-Shirt` 14,95 dollari.
