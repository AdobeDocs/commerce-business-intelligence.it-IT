---
title: tabella quote_item
description: Scopri come utilizzare la tabella quote_item.
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# tabella quote_item

Il `quote_item` tabella (`sales_flat_quote_item` su M1) contiene i record di ogni articolo aggiunto al carrello, indipendentemente dal fatto che il carrello sia stato abbandonato o convertito in acquisto. Ogni riga rappresenta un elemento del carrello. A causa delle dimensioni potenziali di questa tabella, Adobe consiglia di eliminare periodicamente i record se sono soddisfatti determinati criteri, ad esempio se sono presenti carrelli non convertiti di età superiore a 60 giorni.

>[!NOTE]
>
>L’analisi dei carrelli storici abbandonati è possibile solo se non elimini i record dal `quote` e `quote_item` tabella. Se elimini i record, potrai vedere solo i carrelli non ancora rimossi dal database.

## Colonne native comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `base_price` | Prezzo di una singola unità di un prodotto al momento dell’aggiunta dell’articolo al carrello, dopo [regole di prezzo di catalogo, sconti su più livelli e prezzi speciali](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) vengono applicati e prima di applicare eventuali imposte, spese di spedizione o sconti sul carrello. Viene rappresentata nella valuta di base dell&#39;archivio. |
| `created_at` | Timestamp di creazione dell’elemento del carrello, memorizzato localmente in UTC. A seconda della configurazione in [!DNL Commerce Intelligence], questa marca temporale può essere convertita in un fuso orario di reporting in [!DNL Commerce Intelligence] diverso dal fuso orario del database |
| `item_id` PK | Identificatore univoco della tabella |
| `name` | Nome testo dell&#39;ordine |
| `parent_item_id` | `Foreign key` che mette in relazione un prodotto semplice con il pacchetto principale o il prodotto configurabile. Partecipa a `quote_item.item_id` per determinare gli attributi del prodotto padre associati al prodotto semplice. Per gli articoli del carrello principale (ovvero, bundle o tipi di prodotto configurabili), il `parent_item_id` è `NULL` |
| `product_id` | `Foreign key` associato al `catalog_product_entity` tabella. Partecipa a `catalog_product_entity.entity_id` per determinare gli attributi del prodotto associati all&#39;articolo dell&#39;ordine |
| `product_type` | Tipo di prodotto aggiunto al carrello. Potenziale [tipi di prodotto](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) include: semplice, configurabile, raggruppata, virtuale, bundle e scaricabile |
| `qty` | Quantità di unità incluse nel carrello per l’articolo del carrello specifico |
| `quote_id` | `Foreign key` associato al `quote` tabella. Partecipa a `quote.entity_id` per determinare gli attributi del carrello associati all&#39;articolo del carrello |
| `sku` | Identificatore univoco dell’elemento del carrello |
| `store_id` | Chiave esterna associata al `store` tabella. Partecipa a `store.store_id` per determinare quale visualizzazione del punto vendita di Commerce è associata all’articolo del carrello |

{style="table-layout:auto"}

## Colonne calcolate comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `Cart creation date` | Marca temporale associata alla data di creazione del carrello. Calcolato tramite unione `quote_item.quote_id` a `quote.entity_id` e la restituzione del `created_at` timestamp |
| `Cart is active? (1/0)` | Campo booleano che restituisce &quot;1&quot; se il carrello è stato creato da un cliente e non è ancora stato convertito in un ordine. Restituisce &quot;0&quot; per i carrelli convertiti o creati tramite l’amministratore. Calcolato tramite unione `quote_item.quote_id` a `quote.entity_id` e la restituzione del `is_active` campo |
| `Cart item total value (qty * base_price)` | Valore totale di un elemento al momento dell’aggiunta dell’elemento al carrello, dopo [regole di prezzo di catalogo, sconti su più livelli e prezzi speciali](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) vengono applicati e prima di applicare eventuali imposte, spese di spedizione o sconti sul carrello. Calcolato moltiplicando il `qty` da `base_price` |
| `Seconds since cart creation` | Tempo trascorso tra la data di creazione del carrello e ora. Calcolato tramite unione `quote_item.quote_id` a `quote.entity_id` e la restituzione del `Seconds since cart creation` campo |
| `Store name` | Nome dell’archivio Commerce associato all’articolo ordine. Calcolato tramite unione `sales_order_item.store_id` a `store.store_id` e la restituzione del `name` campo |

{style="table-layout:auto"}

## Metriche comuni

| **Nome della metrica** | **Descrizione** | **Costruzione** |
|---|---|---|
| `Number of abandoned cart items` | Quantità totale di articoli aggiunti ai carrelli che soddisfano specifiche condizioni di &quot;abbandono&quot; | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>Filtri:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, dove &quot;x&quot; corrisponde al tempo trascorso (in secondi) dalla creazione del carrello oltre il quale un carrello viene considerato abbandonato |
| `Abandoned cart item value` | Somma dei ricavi totali associati ai carrelli che soddisfano specifiche condizioni di &quot;abbandono&quot; | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>Filtri:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, dove &quot;x&quot; corrisponde al tempo trascorso (in secondi) dalla creazione del carrello oltre il quale un carrello viene considerato abbandonato |

{style="table-layout:auto"}

## Percorsi di unione chiave esterna

`catalog_product_entity`

* Partecipa a `catalog_product_entity` tabella per creare colonne che restituiscono attributi di prodotto associati all&#39;articolo del carrello.
   * Percorso: `quote_item.product_id` (molti) => `catalog_product_entity.entity_id` (uno)

`quote`

* Partecipa a `quote` tabella per creare nuove colonne a livello di carrello associate all’articolo del carrello.
   * Percorso: `quote_item.quote_id` (molti) => `quote.entity_id` (uno)

`quote_item`

* Partecipa a `quote_item` per creare colonne che associano i dettagli dello SKU configurabile principale o del bundle al prodotto semplice. [Contatta l’assistenza](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) per assistenza nella configurazione di questi calcoli, se si crea in Data Warehouse manager.
   * Percorso: `quote_item.parent_item_id` (molti) => `quote_item.item_id` (uno)

`store`

* Partecipa a `store` tabella per creare colonne che restituiscono i dettagli relativi all’archivio Commerce associato all’articolo del carrello.
   * Percorso: `quote_item.store_id` (molti) => `store.store_id` (uno)
