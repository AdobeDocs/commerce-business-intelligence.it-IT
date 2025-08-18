---
title: tabella sales_order_item
description: Scopri come utilizzare la tabella sales_order_item.
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---

# Tabella `sales_order_item`

La tabella `sales_order_item` (`sales_flat_order_item` su M1) contiene i record di tutti i prodotti acquistati in un ordine. Ogni riga rappresenta un `sku` univoco incluso in un ordine. La quantità di unità acquistate per un `sku` specifico è spesso rappresentata dal campo `qty_ordered`.

## Tipi di prodotto

`sales_order_item` acquisisce i dettagli su tutti i [tipi di prodotto](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html?lang=it#product-types) acquistati. Una pratica comune in [!DNL Adobe Commerce] consiste nell&#39;offrire prodotti configurabili o, in altre parole, un prodotto che può essere personalizzato in base alle dimensioni, al colore e ad altri attributi del prodotto. Sebbene un prodotto configurabile abbia un proprio `sku`, può essere correlato a più prodotti semplici, in cui ogni prodotto semplice rappresenta una configurazione di prodotto univoca. Per ulteriori informazioni, consultare [configurazione dei prodotti](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/).

Ad esempio, considera un prodotto configurabile come una t-shirt. Quando un cliente effettua il check-out, seleziona le opzioni per modificare il colore e le dimensioni. Se il cliente seleziona un colore di `blue` e una dimensione di `small`, acquista un prodotto semplice come `t-shirt-blue-small` che si riferisce al prodotto principale di `t-shirt`.

Quando un prodotto configurabile viene incluso in un ordine, nella tabella `sales_order_item` vengono generate due righe: una per [simple](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html?lang=it) `sku` e una per [configurable](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html?lang=it). Questi due record della tabella `sales_order_item` possono essere correlati tra loro tramite il seguente join:

* (semplice) `sales_order_item.parent_item_id` => (configurabile) `sales_order_item.item_id`

È quindi possibile riferire sulle vendite dei prodotti sia a livello semplice che a livello configurabile. Per impostazione predefinita, tutte le metriche `order-item-level` standard in [!DNL Commerce Intelligence] sono configurate per escludere i prodotti semplici e *solo* generano rapporti sulle versioni configurabili. Questa operazione viene eseguita tramite il set di filtri `Ordered products we count`, che filtra la condizione in cui `parent_item_id` è `NULL`.

## Colonne comuni

| **Nome colonna** | **Descrizione** |
|----|----|
| `base_price` | Prezzo di una singola unità di un prodotto al momento della vendita dopo l&#39;applicazione di [regole del prezzo di catalogo, sconti su più livelli e prezzi speciali](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=it) e prima dell&#39;applicazione di eventuali imposte, spese di spedizione o sconti sul carrello. Viene rappresentata nella valuta di base dell&#39;archivio. |
| `created_at` | Timestamp di creazione dell’elemento dell’ordine, memorizzato localmente in UTC. A seconda della configurazione in [!DNL Commerce Intelligence], questa marca temporale può essere convertita in un fuso orario di reporting in [!DNL Commerce Intelligence] diverso dal fuso orario del database. |
| `item_id` (PC) | Identificatore univoco della tabella. |
| `name` | Nome testuale dell&#39;elemento dell&#39;ordine. |
| `order_id` | `Foreign key` associato alla tabella `sales_order`. Partecipa a `sales_order.entity_id` per determinare gli attributi dell&#39;ordine associati all&#39;elemento dell&#39;ordine. |
| `parent_item_id` | `Foreign key` che mette in relazione un prodotto semplice con il relativo pacchetto principale o prodotto configurabile. Partecipa a `sales_order_item.item_id` per determinare gli attributi del prodotto padre associati al prodotto semplice. Per gli elementi dell&#39;ordine padre (ovvero, bundle o tipi di prodotto configurabili), `parent_item_id` è `NULL`. |
| `product_id` | `Foreign key` associato alla tabella `catalog_product_entity`. Partecipa a `catalog_product_entity.entity_id` per determinare gli attributi del prodotto associati all&#39;elemento dell&#39;ordine. |
| `product_type` | Tipo di prodotto venduto. I potenziali [tipi di prodotto](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html?lang=it#product-types) includono: semplice, configurabile, raggruppato, virtuale, bundle e scaricabile. |
| `qty_ordered` | Quantità di unità incluse nel carrello per l&#39;articolo dell&#39;ordine specifico al momento della vendita. |
| `sku` | Identificatore univoco dell&#39;articolo dell&#39;ordine acquistato. |
| `store_id` | `Foreign key` associato alla tabella `store`. Partecipa a `store.store_id` per determinare quale visualizzazione di Commerce Store è associata all&#39;elemento dell&#39;ordine. |

{style="table-layout:auto"}

## Colonne calcolate comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `Customer's email` | Indirizzo e-mail del cliente che effettua l’ordine. Calcolato unendo `sales_order_item.order_id` a `sales_order.entity_id` e restituendo il campo `customer_email`. |
| `Customer's lifetime number of orders` | Numero totale di ordini effettuati dal cliente. Calcolato unendo `sales_order_item.order_id` a `sales_order.entity_id` e restituendo il campo `Customer's lifetime number of orders`. |
| `Customer's lifetime revenue` | Somma il totale dei ricavi per tutti gli ordini effettuati dal cliente. Calcolato unendo `sales_order_item.order_id` a `sales_order.entity_id` e restituendo il campo `Customer's lifetime revenue`. |
| `Customer's order number` | Classificazione ordine sequenziale per l&#39;ordine del cliente. Calcolato unendo `sales_order_item.order_id` a `sales_order.entity_id` e restituendo il campo `Customer's order number`. |
| `Order item total value (quantity * price)` | Valore totale di un articolo dell&#39;ordine al momento della vendita dopo l&#39;applicazione di [regole del prezzo di catalogo, sconti su più livelli e prezzi speciali](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=it) e prima dell&#39;applicazione di eventuali imposte, spese di spedizione o sconti sul carrello. Calcolato moltiplicando `qty_ordered` per `base_price`. |
| `Order's coupon_code` | Coupon applicato all’ordine. Calcolato unendo `sales_order_item.order_id` a `sales_order.entity_id` e restituendo il campo `coupon_code`. |
| `Order's increment_id` | Identificatore univoco dell’ordine. Calcolato unendo `sales_order_item.order_id` a `sales_order.entity_id` e restituendo il campo `increment_id`. |
| `Order's status` | Stato dell’ordine. Calcolato unendo `sales_order_item.order_id` a `sales_order.entity_id` e restituendo il campo `status`. |
| `Store name` | Nome dell&#39;archivio Commerce associato all&#39;articolo dell&#39;ordine. Calcolato unendo `sales_order_item.store_id` a `store.store_id` e restituendo il campo `name`. |

{style="table-layout:auto"}

## Metriche comuni

| **Nome metrica** | **Descrizione** | **Costruzione** |
|---|---|---|
| `Products ordered` | Quantità totale di prodotti inclusi nei carrelli al momento della vendita | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | Valore totale dei prodotti inclusi nei carrelli al momento della vendita dopo l&#39;applicazione delle regole del prezzo di catalogo, degli sconti su più livelli e dei prezzi speciali e prima dell&#39;applicazione di eventuali imposte, spese di spedizione o sconti sul carrello | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style="table-layout:auto"}

## `Foreign Key` percorsi di unione

`catalog_product_entity`

* Partecipa alla tabella `catalog_product_entity` per creare colonne che restituiscono attributi di prodotto associati all&#39;elemento dell&#39;ordine.
   * Percorso: `sales_order_item.product_id` (molti) => `catalog_product_entity.entity_id` (uno)

`sales_order`

* Unire alla tabella `sales_order` per creare nuove colonne a livello di ordine associate all&#39;elemento dell&#39;ordine.
   * Percorso: `sales_order_item.order_id` (molti) => `sales_order.entity_id` (uno)

`sales_order_item`

* Unisciti a `sales_order_item` per creare colonne che associano i dettagli dello SKU configurabile o del bundle padre al prodotto semplice. [Contatta il supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=it) per assistenza nella configurazione di questi calcoli, se vengono generati in Data Warehouse Manager.
   * Percorso: `sales_order_item.parent_item_id` (molti) => `sales_order_item.item_id` (uno)

`store`

* Partecipa alla tabella `store` per creare colonne che restituiscono i dettagli relativi all&#39;archivio Commerce associato all&#39;elemento dell&#39;ordine.
   * Percorso: `sales_order_item.store_id` (molti) => `store.store_id` (uno)
