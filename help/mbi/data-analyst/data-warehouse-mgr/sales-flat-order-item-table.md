---
title: tabella sales_order_item
description: Scopri come utilizzare la tabella sales_order_item.
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 0%

---

# `sales_order_item` Tabella

Il `sales_order_item` tabella (`sales_flat_order_item` in M1 1) contiene i record di tutti i prodotti acquistati in un ordine. Ogni riga rappresenta un valore univoco `sku` incluso in un ordine. Quantità di unità acquistate per uno specifico `sku` è spesso rappresentato dal simbolo `qty_ordered` campo.

## Tipi di prodotto

Il `sales_order_item` acquisisce dettagli su tutti [tipi di prodotto](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) che sono stati acquistati. Una pratica comune in Commerce consiste nell’offrire prodotti configurabili, o in altre parole, un prodotto che può essere personalizzato in base alle dimensioni, al colore e ad altri attributi del prodotto. Anche se un prodotto configurabile ha il proprio `sku`, può riferirsi a più prodotti semplici, dove ogni prodotto semplice rappresenta una configurazione di prodotto univoca. Fai riferimento a [configurazione dei prodotti](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/) per ulteriori informazioni.

Ad esempio, considera un prodotto configurabile come una t-shirt. Quando un cliente effettua il check-out, seleziona le opzioni per modificare il colore e le dimensioni. Se il cliente seleziona un colore di `blue`, e una dimensione di `small`, finiscono per acquistare un prodotto semplice come `t-shirt-blue-small` che si riferisce al prodotto principale di `t-shirt`.

Quando un prodotto configurabile viene incluso in un ordine, vengono generate due righe nel `sales_order_item` tabella: uno per [semplice](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) `sku`, e uno per [configurabile](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html) principale. Questi due record in `sales_order_item` La tabella può essere correlata tra loro tramite il seguente join:

* (semplice) `sales_order_item.parent_item_id` => (configurabile) `sales_order_item.item_id`

È quindi possibile riferire sulle vendite dei prodotti sia a livello semplice che a livello configurabile. Per impostazione predefinita, tutti gli standard `order-item-level` metriche in [!DNL MBI] sono configurate per escludere i prodotti semplici, e *solo* generare rapporti sulle versioni configurabili. Questa operazione viene eseguita tramite `Ordered products we count` set di filtri, che filtra in base alla condizione in cui `parent_item_id` è `NULL`.

## Colonne comuni

| **Nome colonna** | **Descrizione** |
|----|----|
| `base_price` | Prezzo di una singola unità di un prodotto al momento della vendita dopo [regole di prezzo di catalogo, sconti su più livelli e prezzi speciali](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) vengono applicati e prima di applicare eventuali imposte, spese di spedizione o sconti sul carrello. Viene rappresentata nella valuta di base dell&#39;archivio |
| `created_at` | Timestamp di creazione dell’elemento dell’ordine, memorizzato localmente in UTC. A seconda della configurazione in [!DNL MBI], questa marca temporale può essere convertita in un fuso orario di reporting in [!DNL MBI] diverso dal fuso orario del database |
| `item_id` PK | Identificatore univoco della tabella |
| `name` | Nome testo dell&#39;ordine |
| `order_id` | `Foreign key` associato al `sales_order` tabella. Partecipa a `sales_order.entity_id` per determinare gli attributi dell&#39;ordine associati all&#39;articolo ordine |
| `parent_item_id` | `Foreign key` che mette in relazione un prodotto semplice con il pacchetto principale o il prodotto configurabile. Partecipa a `sales_order_item.item_id` per determinare gli attributi del prodotto padre associati al prodotto semplice. Per gli articoli dell&#39;ordine padre, ovvero i tipi di prodotto configurabili o raggruppati, il `parent_item_id` è `NULL` |
| `product_id` | `Foreign key` associato al `catalog_product_entity` tabella. Partecipa a `catalog_product_entity.entity_id` per determinare gli attributi del prodotto associati all&#39;articolo dell&#39;ordine |
| `product_type` | Tipo di prodotto venduto. Potenziale [tipi di prodotto](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) include: semplice, configurabile, raggruppata, virtuale, bundle e scaricabile |
| `qty_ordered` | Quantità di unità incluse nel carrello per l&#39;articolo dell&#39;ordine specifico al momento della vendita |
| `sku` | Identificatore univoco dell&#39;articolo dell&#39;ordine acquistato |
| `store_id` | `Foreign key` associato al `store` tabella. Partecipa a `store.store_id` per determinare quale visualizzazione di archivio Commerce associata all’articolo dell’ordine |

{style="table-layout:auto"}

## Colonne calcolate comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `Customer's email` | Indirizzo e-mail del cliente che effettua l’ordine. Calcolato tramite unione `sales_order_item.order_id` a `sales_order.entity_id` e la restituzione del `customer_email` campo |
| `Customer's lifetime number of orders` | Numero totale di ordini effettuati dal cliente. Calcolato tramite unione `sales_order_item.order_id` a `sales_order.entity_id` e la restituzione del `Customer's lifetime number of orders` campo |
| `Customer's lifetime revenue` | Somma il totale dei ricavi per tutti gli ordini effettuati dal cliente. Calcolato tramite unione `sales_order_item.order_id` a `sales_order.entity_id` e la restituzione del `Customer's lifetime revenue` campo |
| `Customer's order number` | Classificazione ordine sequenziale per l&#39;ordine del cliente. Calcolato tramite unione `sales_order_item.order_id` a `sales_order.entity_id` e la restituzione del `Customer's order number` campo |
| `Order item total value (quantity * price)` | Valore totale di un articolo dell&#39;ordine al momento della vendita dopo [regole di prezzo di catalogo, sconti su più livelli e prezzi speciali](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) vengono applicati e prima di applicare eventuali imposte, spese di spedizione o sconti sul carrello. Calcolato moltiplicando il `qty_ordered` da `base_price` |
| `Order's coupon_code` | Coupon applicato all’ordine. Calcolato tramite unione `sales_order_item.order_id` a `sales_order.entity_id` e la restituzione del `coupon_code` campo |
| `Order's increment_id` | Identificatore univoco dell’ordine. Calcolato tramite unione `sales_order_item.order_id` a `sales_order.entity_id` e la restituzione del `increment_id` campo |
| `Order's status` | Stato dell’ordine. Calcolato tramite unione `sales_order_item.order_id` a `sales_order.entity_id` e la restituzione del `status` campo |
| `Store name` | Nome dell’archivio Commerce associato all’articolo ordine. Calcolato tramite unione `sales_order_item.store_id` a `store.store_id` e la restituzione del `name` campo |

{style="table-layout:auto"}

## Metriche comuni

| **Nome della metrica** | **Descrizione** | **Costruzione** |
|---|---|---|
| `Products ordered` | Quantità totale di prodotti inclusi nei carrelli al momento della vendita | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | Valore totale dei prodotti inclusi nei carrelli al momento della vendita dopo l&#39;applicazione delle regole del prezzo di catalogo, degli sconti su più livelli e dei prezzi speciali e prima dell&#39;applicazione di eventuali imposte, spese di spedizione o sconti sul carrello | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style="table-layout:auto"}

## `Foreign Key` Percorsi di unione

`catalog_product_entity`

* Partecipa a `catalog_product_entity` tabella per creare colonne che restituiscono gli attributi del prodotto associati all&#39;articolo dell&#39;ordine.
   * Percorso: `sales_order_item.product_id` (molti) => `catalog_product_entity.entity_id` (uno)

`sales_order`

* Partecipa a `sales_order` tabella per creare nuove colonne a livello di ordine associate all&#39;articolo dell&#39;ordine.
   * Percorso: `sales_order_item.order_id` (molti) => `sales_order.entity_id` (uno)

`sales_order_item`

* Partecipa a `sales_order_item` per creare colonne che associano i dettagli dello SKU configurabile principale o del bundle al prodotto semplice. [Contatta l’assistenza](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) per assistenza nella configurazione di questi calcoli, se si crea in Data Warehouse manager.
   * Percorso: `sales_order_item.parent_item_id` (molti) => `sales_order_item.item_id` (uno)

`store`

* Partecipa a `store` tabella per creare colonne che restituiscono i dettagli relativi all’archivio Commerce associato all’articolo dell’ordine.
   * Percorso: `sales_order_item.store_id` (molti) => `store.store_id` (uno)
