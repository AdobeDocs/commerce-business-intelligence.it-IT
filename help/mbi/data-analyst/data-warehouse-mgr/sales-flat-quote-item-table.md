---
title: tabella quote_item
description: Scopri come utilizzare la tabella quote_item.
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 0%

---

# tabella quote_item

La `quote_item` tabella (`sales_flat_quote_item` su [!DNL Magento] 1) contiene record su ogni articolo aggiunto al carrello, sia che il carrello sia stato abbandonato o convertito in un acquisto. Ogni riga rappresenta un elemento carrello. A causa delle dimensioni potenziali di questa tabella, ti consigliamo di eliminare periodicamente i record se vengono soddisfatti determinati criteri, ad esempio se sono presenti carrelli non convertiti con età superiore a 60 giorni.

>[!NOTE]
>
>L&#39;analisi dei carrelli abbandonati storici è possibile solo se non si eliminano i record dal `quote` e `quote_item` tabella. Se elimini i record, potrai solo vedere i carrelli non ancora rimossi dal tuo database.

## Colonne native comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `base_price` | Prezzo di una singola unità di un prodotto al momento in cui l&#39;articolo è stato aggiunto a un carrello, dopo [regole sui prezzi di catalogo, sconti su più livelli e prezzi speciali](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) sono applicati e prima che vengano applicate imposte, spedizioni o sconti sul carrello, rappresentati nella valuta di base del negozio |
| `created_at` | Timestamp di creazione dell&#39;elemento carrello, in genere memorizzato localmente in UTC. A seconda della configurazione in [!DNL MBI], questa marca temporale può essere convertita in un fuso orario per la generazione di rapporti in [!DNL MBI] diverso dal fuso orario del database |
| `item_id` (PK) | Identificatore univoco della tabella |
| `name` | Nome del testo dell’elemento dell’ordine |
| `parent_item_id` | `Foreign key` che collega un prodotto semplice al suo bundle padre o al prodotto configurabile. Iscriviti a `quote_item.item_id` per determinare gli attributi del prodotto padre associati a un prodotto semplice. Per gli elementi del carrello padre (ovvero, i tipi di prodotto raggruppati o configurabili), la `parent_item_id` sarà `NULL` |
| `product_id` | `Foreign key` associato a `catalog_product_entity` tabella. Iscriviti a `catalog_product_entity.entity_id` per determinare gli attributi di prodotto associati all’articolo dell’ordine |
| `product_type` | Tipo di prodotto aggiunto al carrello. Potenziale [tipi di prodotto](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) include: semplice, configurabile, raggruppato, virtuale, bundle e scaricabile |
| `qty` | Quantità di unità incluse nel carrello per il particolare articolo del carrello |
| `quote_id` | `Foreign key` associato a `quote` tabella. Iscriviti a `quote.entity_id` per determinare gli attributi del carrello associati all’elemento carrello |
| `sku` | Identificatore univoco per l&#39;elemento carrello |
| `store_id` | Chiave esterna associata al `store` tabella. Iscriviti a `store.store_id` per determinare quale visualizzazione dell’archivio Commerce è associata all’elemento carrello |

{style=&quot;table-layout:auto&quot;}

## Colonne calcolate comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `Cart creation date` | Timestamp associato alla data di creazione del carrello. Calcolato mediante unione `quote_item.quote_id` a `quote.entity_id` e restituendo `created_at` timestamp |
| `Cart is active? (1/0)` | Campo booleano che restituisce &quot;1&quot; se il carrello è stato creato da un cliente e non è ancora stato convertito in un ordine. Restituisce &quot;0&quot; per i carrelli convertiti o i carrelli creati tramite l’amministratore. Calcolato mediante unione `quote_item.quote_id` a `quote.entity_id` e restituendo `is_active` field |
| `Cart item total value (qty * base_price)` | Valore totale di un articolo al momento dell’aggiunta dell’articolo a un carrello, dopo [regole sui prezzi di catalogo, sconti su più livelli e prezzi speciali](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) sono applicati e prima che vengano applicate tasse, spedizioni o sconti sul carrello. Calcolato moltiplicando il `qty` dal `base_price` |
| `Seconds since cart creation` | Tempo trascorso tra la data di creazione del carrello e ora. Calcolato mediante unione `quote_item.quote_id` a `quote.entity_id` e restituendo `Seconds since cart creation` field |
| `Store name` | Nome dell&#39;archivio Commerce associato all&#39;articolo dell&#39;ordine. Calcolato mediante unione `sales_order_item.store_id` a `store.store_id` e restituendo `name` field |

{style=&quot;table-layout:auto&quot;}

## Metriche comuni

| **Nome della metrica** | **Descrizione** | **Costruzione** |
|---|---|---|
| `Number of abandoned cart items` | Quantità totale di articoli aggiunti ai carrelli che soddisfano specifiche condizioni di &quot;abbandono&quot; | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>Filtri:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, dove &quot;x&quot; corrisponde al tempo trascorso (in secondi) dalla creazione del carrello oltre il quale un carrello è considerato abbandonato |
| `Abandoned cart item value` | Somma dei ricavi totali associati ai carrelli che soddisfano specifiche condizioni di &quot;abbandono&quot; | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>Filtri:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, dove &quot;x&quot; corrisponde al tempo trascorso (in secondi) dalla creazione del carrello oltre il quale un carrello è considerato abbandonato |

{style=&quot;table-layout:auto&quot;}

## Percorsi di unione chiave esterna

`catalog_product_entity`

* Iscriviti a `catalog_product_entity` per creare nuove colonne che restituiscono gli attributi di prodotto associati all’elemento carrello.
   * Percorso: `quote_item.product_id` (molti) => `catalog_product_entity.entity_id` 1)

`quote`

* Iscriviti a `quote` per creare nuove colonne a livello di carrello associate all’elemento carrello.
   * Percorso: `quote_item.quote_id` (molti) => `quote.entity_id` 1)

`quote_item`

* Iscriviti a `quote_item` per creare nuove colonne che associano i dettagli della SKU configurabile o del bundle principale al prodotto semplice. Tieni presente che dovrai [contattare il supporto](../../guide-overview.md) per assistenza nella configurazione di questi calcoli, se la creazione è nel gestore Data Warehouse.
   * Percorso: `quote_item.parent_item_id` (molti) => `quote_item.item_id` 1)

`store`

* Iscriviti a `store` per creare nuove colonne che restituiscono i dettagli relativi all’archivio Commerce associato all’elemento carrello.
   * Percorso: `quote_item.store_id` (molti) => `store.store_id` 1)
