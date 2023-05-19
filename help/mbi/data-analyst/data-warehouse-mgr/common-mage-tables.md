---
title: Tabelle Commerce comuni
description: Scopri alcune delle tabelle più comuni che [!DNL Commerce Intelligence] i clienti utilizzano.
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# Tabelle Commerce comuni

La prima volta che si collega una [!DNL Adobe Commerce] istanza a [[!DNL Adobe Commerce Intelligence]](../importing-data/integrations/magento.md), [!DNL Commerce Intelligence] replica automaticamente i dati da alcune tabelle commerce (in genere 4-6 tabelle) per configurare il set iniziale di dashboard e rapporti. Anche se questo offre un ottimo punto di partenza, la maggior parte delle istanze dello store genera decine se non centinaia di tabelle aggiuntive che possono fornire informazioni critiche sulle prestazioni della tua azienda.

Di seguito è riportato un elenco di alcune delle tabelle più comuni [!DNL Commerce Intelligence] i clienti utilizzano. Dopo di te [collegare la tua istanza Commerce a Commerce Intelligence](../../data-analyst/importing-data/integrations/magento.md), è possibile utilizzare [Gestione Date Warehouse](../../data-analyst/data-warehouse-mgr/tour-dwm.md) per tenere traccia dei campi di dati rilevanti.

| Nome tabella | Descrizione |
|---|---|
| `catalog_category_entity` | Ogni riga nella `catalog_category_entity` tabella descrive una categoria specifica. Con il associato `catalog_category_entity_varchar` tabella e `catalog_category_product` tabella di mappatura, è possibile ottenere informazioni sulle categorie per ciascun prodotto. |
| `catalog_category_product` | Ogni riga nella `catalog_category_product` nella tabella viene elencata una combinazione di un prodotto e una categoria. Pertanto, un determinato prodotto può esistere in questa tabella più volte con categorie diverse e una determinata categoria può esistere in questa tabella più volte associata a prodotti diversi. Questa tabella indicizza `catalog_category_entity` tabella (contenente i dettagli a livello di categoria) e `catalog_product_entity` tabella (contenente i dettagli a livello di prodotto). |
| `catalog_product_entity` | Ogni riga nella `catalog_product_entity` la tabella rappresenta un prodotto specifico. Ciò include quando il prodotto è stato creato nell’account Commerce e nel relativo SKU. |
| `customer_entity` | Ogni riga nella [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) la tabella rappresenta un utente registrato sul sito web. Dettagli di base a livello di cliente come la data di registrazione e l’indirizzo e-mail sono in diretta su questa tabella. |
| `quote` | Ogni riga nella [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) la tabella rappresenta un carrello creato durante il processo di pagamento, indipendentemente dal fatto che sia stato convertito in un ordine. A causa delle dimensioni potenziali di questa tabella, Adobe consiglia di eliminare periodicamente i record se sono soddisfatti determinati criteri, ad esempio se sono presenti carrelli non convertiti di età superiore a 60 giorni. |
| `quote_item` | Ogni riga nella [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) la tabella rappresenta un elemento aggiunto a un carrello, indipendentemente dal fatto che il carrello sia stato convertito in un ordine. A causa delle dimensioni potenziali di questa tabella, Adobe consiglia di eliminare periodicamente i record se sono soddisfatti determinati criteri, ad esempio se sono presenti carrelli non convertiti di età superiore a 60 giorni. |
| `sales_order` | Ogni riga nella [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) la tabella rappresenta un ordine effettuato sul sito. Questa tabella contiene informazioni a livello di ordine quali la data dell&#39;ordine, il cliente che ha effettuato l&#39;ordine, il totale dell&#39;ordine e l&#39;utilizzo del codice sconto e coupon. |
| `sales_order_address` | Ogni riga del `sales_order_address` la tabella contiene le informazioni di spedizione e fatturazione per un ordine specifico. Il giorno `sales_order` tabella, `billing_address_id` e `shipping_address_id` per un determinato ordine si riferisce a una riga specifica (identificata da `entity_id`) sul `sales_order_address` tabella. |
| `sales_order_item` | Ogni riga nella [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) la tabella identifica un articolo specifico di un ordine specifico. Ogni riga contiene dettagli quali il prodotto, la quantità acquistata e l&#39;ordine a cui è associato l&#39;articolo specificato. |

{style="table-layout:auto"}

## Documentazione correlata

[Diagrammi di relazione entità](../data-warehouse-mgr/entity-rel-diag.md)
