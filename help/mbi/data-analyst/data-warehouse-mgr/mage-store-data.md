---
title: Memorizzazione dei dati in Adobe Commerce
description: Scopri come vengono generati i dati, cosa causa l’inserimento di una nuova riga e come vengono registrate le azioni nel database di Adobe Commerce.
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 2%

---

# Memorizzazione dei dati in [!DNL Adobe Commerce]

La piattaforma [!DNL Adobe Commerce] registra e organizza un&#39;ampia gamma di dati di e-commerce importanti in centinaia di tabelle. Questo argomento descrive:

* come vengono generati i dati
* causa dell&#39;inserimento di una nuova riga in una delle [tabelle Commerce principali](../data-warehouse-mgr/common-mage-tables.md)
* registrazione nel database [!DNL Adobe Commerce] di azioni quali l&#39;acquisto o la creazione di un account

Per discutere di questi concetti, consulta l’esempio seguente:

`Clothes4U` è un retailer per l&#39;abbigliamento con presenze sia online che in mattoni. Utilizza [!DNL Magento Open Source] dietro al proprio sito Web per raccogliere e organizzare i dati.

## `catalog\_product\_entity`

È il 22 settembre e `Clothes4U` sta eseguendo il rollout di tre nuovi elementi alla riga Autunno: `Throwback Bellbottoms`, `Straight Leg Jeans` e `V-Neck T-Shirts`. Un dipendente `Clothes4U` apre il proprio amministratore Commerce, fa clic su **[!UICONTROL Add Product]** e immette tutte le informazioni per `Throwback Bellbottoms`.

Soddisfatto di tutte le impostazioni per `Throwback Bellbottoms`, il dipendente fa clic su **[!UICONTROL Save]**, che inserisce la prima riga nella tabella `catalog_product_entity`. Il dipendente ripete il processo, creando un altro prodotto Commerce per `Straight Leg Jeans` e quindi un terzo per `V-Neck T-Shirt`, inserendo la seconda e la terza riga nella tabella `catalog_product_entity`:

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Pantaloni10 | 2016/09/22 09:15:43 |
| 206 | 4 | 8 | Pantaloni11 | 2016/09/22 09:18:17 |
| 207 | 4 | 12 | Camicie6 | 2016/09/22 09:24:02 |

* `entity_id` - Questa è la chiave primaria della tabella `catalog_product_entity`, il che significa che ogni riga della tabella deve avere un `entity_id` diverso. Ogni `entity_id` di questa tabella può essere associato a un solo prodotto e ogni prodotto può essere associato a un solo `entity_id`
   * La riga superiore della tabella precedente, `entity_id` = 205, è la nuova riga creata per &quot;Throwback Bellbottoms&quot;. Ovunque `entity_id` = 205 venga visualizzato nella piattaforma Commerce, si fa riferimento al prodotto &quot;Throwback Bellbottoms&quot;
* `entity_type_id` - Commerce ha più categorie di oggetti (come clienti, indirizzi e prodotti per citarne alcuni) e questa colonna viene utilizzata per indicare la categoria in cui rientra questa riga particolare.
   * Trattandosi della tabella `catalog_product_entity`, ogni riga ha lo stesso tipo di entità: product. In Adobe Commerce, `entity_type_id` per il prodotto è 4, ed è per questo che tutti e tre i nuovi prodotti creati restituiscono 4 per questa colonna.
* `attribute_set_id` - I set di attributi vengono utilizzati per identificare i prodotti che hanno lo stesso di descrittori.
   * Le prime due righe della tabella sono i prodotti `Throwback Bellbottoms` e `Straight Leg Jeans`, entrambi pantaloni. Questi prodotti avrebbero gli stessi descrittori (ad esempio, nome, inseam, girovita) e quindi gli stessi `attribute_set_id`. Il terzo elemento, `V-Neck T-Shirt`, ha un `attribute_set_id` diverso perché non avrebbe gli stessi descrittori dei pantaloni; le camicie non hanno girovita o costine.
* `sku` - Si tratta di valori univoci assegnati a ciascun prodotto dall&#39;utente durante la creazione di un prodotto in Adobe Commerce.
* `created_at` - Questa colonna restituisce il timestamp di quando è stato creato ogni prodotto

## `customer\_entity`

Poco dopo l&#39;aggiunta dei tre nuovi prodotti, un nuovo cliente, `Sammy Customer`, visita per la prima volta il sito Web di `Clothes4U`. Poiché `Clothes4U` non consente gli ordini degli ospiti, `Sammy Customer` deve prima creare un account sul sito Web. Il cliente immette le credenziali richieste e fa clic su invia, con conseguente nuova voce in [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md):

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id` - Proprio come la tabella precedente, `entity_id` è la chiave primaria della tabella `customer_entity`.
   * Quando `Sammy Customer` ha creato un account e la riga precedente è stata scritta nella tabella `customer_entity`, al cliente è stato assegnato `entity_id` = 214. In tutte le tabelle, il cliente identificato come `entity_id` = 214 fa sempre riferimento all&#39;utente Sammy Customer
* `entity_type_id` - Questa colonna identifica il tipo di entità elencato in questa tabella e funziona come nella tabella `catalog_product_entity`
   * Ogni riga della tabella `customer_entity` è un cliente e Commerce definisce i clienti come `entity_type_id` 1 per impostazione predefinita
* `email` - questo campo viene compilato dall&#39;e-mail che un nuovo cliente inserisce quando crea il proprio account
* `created_at` - Questa colonna restituisce la marca temporale per l&#39;iscrizione di ogni utente

## `sales\_flat\_order (or Sales\_order` se hai [!DNL Adobe Commerce 2.x]

Al termine della creazione dell&#39;account, `Sammy Customer` è pronto per iniziare a effettuare un acquisto. Nel sito Web, il cliente aggiunge due coppie di `Throwback Bellbottoms` e una `V-Neck T-Shirt` al carrello. Soddisfatto delle selezioni, il cliente passa al pagamento e invia l&#39;ordine, creando la seguente voce nella [tabella ordini vendite a tariffa fissa](../data-warehouse-mgr/sales-flat-order-table.md):

| **`entity id`** | **`customer id**` | **`subtotal`** | **`created at`** |
|---|---|---|---|
| 227 | 214 | 94,85 | 2016/09/23 15:41:39 |

* `entity_id` - chiave primaria della tabella `sales_flat_order`.
   * Quando Sammy Customer ha effettuato l&#39;ordine e la riga precedente è stata scritta nella tabella `sales_flat_order`, all&#39;ordine è stato assegnato `entity_id` = 227.
* `customer_id` - Questa colonna è l&#39;identificatore univoco del cliente che ha effettuato questo particolare ordine
   * Il `customer_id` associato a questo ordine è 214, che è il `entity_id` del cliente Sammy nella tabella `customer_entity`.
* `subtotal` - Questa colonna è l&#39;importo totale addebitato a un cliente per l&#39;ordine
   * Le due coppie di &quot;Throwback Bellbottoms&quot; e &quot;V-Neck T-Shirt&quot; costarono in totale 94,85 dollari
* `created_at` - Questa colonna restituisce la marca temporale per la creazione di ogni ordine

## `sales\_flat\_order\_item ( or Sales\_order\_item`

(se si dispone di Commerce 2.0 o versione successiva)

Oltre alla riga singola nella tabella `Sales\_flat\_order`, quando `Sammy Customer` invia l&#39;ordine, nella tabella [`sales\_flat\_order\_item` viene inserita una riga per ogni elemento univoco in tale ordine](../data-warehouse-mgr/sales-flat-order-item-table.md):

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39,95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14,95 |

* `item_id` - Questa colonna è la chiave primaria della tabella `sales_flat_order_item`
   * L&#39;ordine di `Sammy Customer` ha creato due righe in questa tabella perché l&#39;ordine conteneva due prodotti distinti
* `name` - Questa colonna è il nome del prodotto
* `product_id` - Questa colonna è l&#39;identificatore univoco del prodotto a cui si riferisce la riga
   * La prima riga contiene `product_id` = 205 perché `Throwback Bellbottoms` ha un `entity_id` di 205 nella tabella `catalog_product_entity`
* `order_id` - Questa colonna è `entity_id` dell&#39;ordine che contiene questi particolari elementi dell&#39;ordine
   * Entrambe le righe precedenti hanno `order_id` = 227 perché fanno entrambe parte dell&#39;ordine effettuato da `Sammy Customer`, che ha `entity_id` = 227 nella tabella `sales_flat_order`
* `qty_ordered` - Questa colonna indica il numero di unità del prodotto incluse in questo ordine specifico
   * L&#39;ordine di `Sammy Customer` conteneva due coppie di `Throwback Bellbottoms`
* `price` - Questa colonna è il prezzo di una singola unità dell&#39;ordine
   * L&#39;ordine di `subtotal` da `Sammy Customer` nella tabella `sales_flat_order` è stato di 94,85, ovvero la somma di due coppie di `Throwback Bellbottoms` a $39,95 ciascuna e di 1 `V-Neck T-Shirt` a $14,95.
