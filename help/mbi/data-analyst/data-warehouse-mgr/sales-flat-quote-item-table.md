---
title: tabella quote_item
description: Scopri come utilizzare la tabella quote_item.
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# tabella quote_item

La tabella `quote_item` (`sales_flat_quote_item` su M1) contiene record per ogni elemento aggiunto a un carrello, indipendentemente dal fatto che il carrello sia stato abbandonato o convertito in acquisto. Ogni riga rappresenta un elemento del carrello. A causa delle dimensioni potenziali di questa tabella, Adobe consiglia di eliminare periodicamente i record se sono soddisfatti determinati criteri, ad esempio se sono presenti carrelli non convertiti di età superiore a 60 giorni.

>[!NOTE]
>
>L&#39;analisi dei carrelli storici abbandonati è possibile solo se non si eliminano i record dalla tabella `quote` e `quote_item`. Se elimini i record, potrai vedere solo i carrelli non ancora rimossi dal database.

## Colonne native comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `base_price` | Prezzo di una singola unità di un prodotto al momento dell&#39;aggiunta dell&#39;articolo al carrello, dopo l&#39;applicazione di [regole di prezzo del catalogo, sconti su più livelli e prezzi speciali](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) e prima dell&#39;applicazione di eventuali imposte, spese di spedizione o sconti sul carrello. Viene rappresentata nella valuta di base dell&#39;archivio. |
| `created_at` | Timestamp di creazione dell’elemento del carrello, memorizzato localmente in UTC. A seconda della configurazione in [!DNL Commerce Intelligence], questa marca temporale può essere convertita in un fuso orario di reporting in [!DNL Commerce Intelligence] diverso dal fuso orario del database |
| `item_id` (PC) | Identificatore univoco della tabella |
| `name` | Nome testo dell&#39;ordine |
| `parent_item_id` | `Foreign key` che mette in relazione un prodotto semplice con il relativo pacchetto principale o prodotto configurabile. Partecipa a `quote_item.item_id` per determinare gli attributi del prodotto padre associati al prodotto semplice. Per gli elementi del carrello principale (ovvero bundle o tipi di prodotto configurabili), `parent_item_id` è `NULL` |
| `product_id` | `Foreign key` associato alla tabella `catalog_product_entity`. Partecipa a `catalog_product_entity.entity_id` per determinare gli attributi del prodotto associati all&#39;elemento dell&#39;ordine |
| `product_type` | Tipo di prodotto aggiunto al carrello. I potenziali [tipi di prodotto](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) includono: semplice, configurabile, raggruppato, virtuale, bundle e scaricabile |
| `qty` | Quantità di unità incluse nel carrello per l’articolo del carrello specifico |
| `quote_id` | `Foreign key` associato alla tabella `quote`. Unisciti a `quote.entity_id` per determinare gli attributi del carrello associati all&#39;elemento del carrello |
| `sku` | Identificatore univoco dell’elemento del carrello |
| `store_id` | Chiave esterna associata alla tabella `store`. Unisciti a `store.store_id` per determinare quale visualizzazione dello store di Commerce è associata all&#39;elemento del carrello |

{style="table-layout:auto"}

## Colonne calcolate comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `Cart creation date` | Marca temporale associata alla data di creazione del carrello. Calcolato unendo `quote_item.quote_id` a `quote.entity_id` e restituendo il timestamp `created_at` |
| `Cart is active? (1/0)` | Campo booleano che restituisce &quot;1&quot; se il carrello è stato creato da un cliente e non è ancora stato convertito in un ordine. Restituisce &quot;0&quot; per i carrelli convertiti o creati tramite l’amministratore. Calcolato unendo `quote_item.quote_id` a `quote.entity_id` e restituendo il campo `is_active` |
| `Cart item total value (qty * base_price)` | Valore totale di un articolo al momento dell&#39;aggiunta dell&#39;articolo al carrello, dopo l&#39;applicazione di [regole di prezzo catalogo, sconti su più livelli e prezzi speciali](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) e prima dell&#39;applicazione di eventuali imposte, spese di spedizione o sconti sul carrello. Calcolato moltiplicando `qty` per `base_price` |
| `Seconds since cart creation` | Tempo trascorso tra la data di creazione del carrello e ora. Calcolato unendo `quote_item.quote_id` a `quote.entity_id` e restituendo il campo `Seconds since cart creation` |
| `Store name` | Nome dell&#39;archivio Commerce associato all&#39;articolo dell&#39;ordine. Calcolato unendo `sales_order_item.store_id` a `store.store_id` e restituendo il campo `name` |

{style="table-layout:auto"}

## Metriche comuni

| **Nome metrica** | **Descrizione** | **Costruzione** |
|---|---|---|
| `Number of abandoned cart items` | Quantità totale di articoli aggiunti ai carrelli che soddisfano specifiche condizioni di &quot;abbandono&quot; | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>Filtri:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, dove &quot;x&quot; corrisponde al tempo trascorso (in secondi) dalla creazione del carrello oltre il quale un carrello viene considerato abbandonato |
| `Abandoned cart item value` | Somma dei ricavi totali associati ai carrelli che soddisfano specifiche condizioni di &quot;abbandono&quot; | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>Filtri:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, dove &quot;x&quot; corrisponde al tempo trascorso (in secondi) dalla creazione del carrello oltre il quale il carrello viene considerato abbandonato |

{style="table-layout:auto"}

## Percorsi di unione chiave esterna

`catalog_product_entity`

* Unisciti alla tabella `catalog_product_entity` per creare colonne che restituiscono gli attributi del prodotto associati all&#39;elemento del carrello.
   * Percorso: `quote_item.product_id` (molti) => `catalog_product_entity.entity_id` (uno)

`quote`

* Unisciti alla tabella `quote` per creare nuove colonne a livello di carrello associate all&#39;elemento del carrello.
   * Percorso: `quote_item.quote_id` (molti) => `quote.entity_id` (uno)

`quote_item`

* Unisciti a `quote_item` per creare colonne che associano i dettagli dello SKU configurabile o del bundle padre al prodotto semplice. [Contatta il supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) per assistenza nella configurazione di questi calcoli, se vengono generati in Gestione Date Warehouse.
   * Percorso: `quote_item.parent_item_id` (molti) => `quote_item.item_id` (uno)

`store`

* Partecipa alla tabella `store` per creare colonne che restituiscono dettagli relativi all&#39;archivio Commerce associato all&#39;elemento del carrello.
   * Percorso: `quote_item.store_id` (molti) => `store.store_id` (uno)
