---
title: tabella sales_order_item
description: Scopri come utilizzare la tabella sales_order_item.
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
source-git-commit: c0892aa046c80f90561b4a178525ef9ed05b435a
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 0%

---

# `sales_order_item` Tabella

La `sales_order_item` tabella (`sales_flat_order_item` su [!DNL Magento] 1) contiene le registrazioni di tutti i prodotti acquistati in un ordine. Ogni riga rappresenta un `sku` incluso in un ordine. Quantità di unità acquistate per uno specifico `sku` è rappresentato più spesso da `qty_ordered` campo .

## Tipi di prodotti

La `sales_order_item` acquisisce i dettagli su tutti [tipi di prodotto](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) che sono stati acquistati. In Commerce, una pratica comune consiste nell’offrire prodotti configurabili, o in altre parole, un prodotto che può essere personalizzato in base a dimensioni, colore e altri attributi di prodotto. Anche se un prodotto configurabile ha un proprio `sku`, può riferirsi a più prodotti semplici, in cui ogni prodotto semplice rappresenta una configurazione di prodotto unica. Fai riferimento a [configurazione dei prodotti](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/) per ulteriori informazioni.

Ad esempio, considera un prodotto configurabile come una t-shirt. Quando un cliente effettua il check-out, seleziona le opzioni per modificare il colore e le dimensioni. Se il cliente seleziona un colore di `blue`e le dimensioni di `small`, finiscono per acquistare un prodotto semplice come `t-shirt-blue-small` che si riferisce al prodotto principale di `t-shirt`.

Quando un prodotto configurabile viene incluso in un ordine, vengono generate due righe nel `sales_order_item` tabella: per [semplice](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) `sku`e uno per il [configurabile](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html) genitore. Questi due documenti nel `sales_order_item` la tabella può essere correlata tra loro tramite il join seguente:

* (semplice) `sales_order_item.parent_item_id` => (configurabile) `sales_order_item.item_id`

Pertanto è possibile riferire sulle vendite dei prodotti sia a livello semplice che a livello configurabile. Per impostazione predefinita, tutti gli standard `order-item-level` metriche in [!DNL MBI] sono configurati per escludere i prodotti semplici, e *only* rapporti sulle versioni configurabili. Questa operazione viene eseguita tramite `Ordered products we count` set di filtri, che filtra in base alla condizione in cui `parent_item_id` è `NULL`.

## Colonne comuni

| **Nome colonna** | **Descrizione** |
|----|----|
| `base_price` | Prezzo di una singola unità di un prodotto al momento della vendita dopo [regole sui prezzi di catalogo, sconti su più livelli e prezzi speciali](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) sono applicati e prima che vengano applicate imposte, spedizioni o sconti sul carrello, rappresentati nella valuta di base del negozio |
| `created_at` | Timestamp di creazione dell&#39;elemento dell&#39;ordine, in genere memorizzato localmente in UTC. A seconda della configurazione in [!DNL MBI], questa marca temporale può essere convertita in un fuso orario per la generazione di rapporti in [!DNL MBI] diverso dal fuso orario del database |
| `item_id` (PK) | Identificatore univoco della tabella |
| `name` | Nome del testo dell’elemento dell’ordine |
| `order_id` | `Foreign key` associato a `sales_order` tabella. Iscriviti a `sales_order.entity_id` per determinare gli attributi dell’ordine associati all’articolo dell’ordine |
| `parent_item_id` | `Foreign key` che collega un prodotto semplice al suo bundle padre o al prodotto configurabile. Iscriviti a `sales_order_item.item_id` per determinare gli attributi del prodotto padre associati a un prodotto semplice. Per gli articoli dell&#39;ordine padre (ovvero, i tipi di prodotto raggruppati o configurabili), la `parent_item_id` sarà `NULL` |
| `product_id` | `Foreign key` associato a `catalog_product_entity` tabella. Iscriviti a `catalog_product_entity.entity_id` per determinare gli attributi di prodotto associati all’articolo dell’ordine |
| `product_type` | Tipo di prodotto venduto. Potenziale [tipi di prodotto](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) include: semplice, configurabile, raggruppato, virtuale, bundle e scaricabile |
| `qty_ordered` | Quantità di unità incluse nel carrello per il particolare articolo d&#39;ordine al momento della vendita |
| `sku` | Identificatore univoco per l&#39;articolo dell&#39;ordine acquistato |
| `store_id` | `Foreign key` associato a `store` tabella. Iscriviti a `store.store_id` per determinare quale visualizzazione Negozio commerciale associata all&#39;articolo dell&#39;ordine |

{style=&quot;table-layout:auto&quot;}

## Colonne calcolate comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `Customer's email` | Indirizzo e-mail del cliente che effettua l’ordine. Calcolato mediante unione `sales_order_item.order_id` a `sales_order.entity_id` e restituendo `customer_email` field |
| `Customer's lifetime number of orders` | Totale degli ordini effettuati dal cliente. Calcolato mediante unione `sales_order_item.order_id` a `sales_order.entity_id` e restituendo `Customer's lifetime number of orders` field |
| `Customer's lifetime revenue` | Somma totale dei ricavi per tutti gli ordini effettuati dal cliente. Calcolato mediante unione `sales_order_item.order_id` a `sales_order.entity_id` e restituendo `Customer's lifetime revenue` field |
| `Customer's order number` | Classificazione ordine sequenziale per l&#39;ordine del cliente. Calcolato mediante unione `sales_order_item.order_id` a `sales_order.entity_id` e restituendo `Customer's order number` field |
| `Order item total value (quantity * price)` | Valore totale di un articolo dell&#39;ordine al momento della vendita dopo [regole sui prezzi di catalogo, sconti su più livelli e prezzi speciali](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) sono applicati e prima che vengano applicate tasse, spedizioni o sconti sul carrello. Calcolato moltiplicando il `qty_ordered` dal `base_price` |
| `Order's coupon_code` | Coupon applicato all&#39;ordine. Calcolato mediante unione `sales_order_item.order_id` a `sales_order.entity_id` e restituendo `coupon_code` field |
| `Order's increment_id` | Identificatore univoco dell&#39;ordine. Calcolato mediante unione `sales_order_item.order_id` a `sales_order.entity_id` e restituendo `increment_id` field |
| `Order's status` | Stato dell&#39;ordine. Calcolato mediante unione `sales_order_item.order_id` a `sales_order.entity_id` e restituendo `status` field |
| `Store name` | Nome dell&#39;archivio Commerce associato all&#39;articolo dell&#39;ordine. Calcolato mediante unione `sales_order_item.store_id` a `store.store_id` e restituendo `name` field |

{style=&quot;table-layout:auto&quot;}

## Metriche comuni

| **Nome della metrica** | **Descrizione** | **Costruzione** |
|---|---|---|
| `Products ordered` | Quantità totale dei prodotti inclusi nei carrelli al momento della vendita | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | Valore totale dei prodotti inclusi nei carrelli al momento della vendita dopo l&#39;applicazione delle regole di prezzo di catalogo, degli sconti su più livelli e dei prezzi speciali e prima dell&#39;applicazione di eventuali tasse, spedizioni o sconti sul carrello | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style=&quot;table-layout:auto&quot;}

## `Foreign Key` Unione dei percorsi

`catalog_product_entity`

* Iscriviti a `catalog_product_entity` per creare nuove colonne che restituiscono gli attributi di prodotto associati all’articolo dell’ordine.
   * Percorso: `sales_order_item.product_id` (molti) => `catalog_product_entity.entity_id` 1)

`sales_order`

* Iscriviti a `sales_order` tabella per creare nuove colonne a livello di ordine associate all’elemento dell’ordine.
   * Percorso: `sales_order_item.order_id` (molti) => `sales_order.entity_id` 1)

`sales_order_item`

* Iscriviti a `sales_order_item` per creare nuove colonne che associano i dettagli della SKU configurabile o del bundle principale al prodotto semplice. Tieni presente che dovrai [contattare il supporto](../../guide-overview.md) per assistenza nella configurazione di questi calcoli, se la creazione è nel gestore Data Warehouse.
   * Percorso: `sales_order_item.parent_item_id` (molti) => `sales_order_item.item_id` 1)

`store`

* Iscriviti a `store` per creare nuove colonne che restituiscono i dettagli relativi all&#39;archivio Commerce associato all&#39;articolo dell&#39;ordine.
   * Percorso: `sales_order_item.store_id` (molti) => `store.store_id` 1)
