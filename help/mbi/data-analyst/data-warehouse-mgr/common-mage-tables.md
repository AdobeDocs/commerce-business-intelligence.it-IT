---
title: Tabelle Commerce comuni
description: Scopri alcune delle tabelle più comuni che [!DNL MBI] i clienti utilizzano.
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# Tabelle Commerce comuni

Quando si collega per la prima volta un’istanza Commerce a [[!DNL MBI]](../importing-data/integrations/magento.md), [!DNL MBI] replica automaticamente i dati da alcune tabelle di e-commerce (in genere 4-6 tabelle) per configurare il set iniziale di dashboard e report. Anche se questo offre un ottimo punto di partenza, la maggior parte delle istanze del negozio genera decine se non centinaia di tabelle aggiuntive che possono fornire informazioni critiche sulle prestazioni della tua azienda.

Di seguito è riportato un elenco di alcune delle tabelle più comuni che [!DNL MBI] i clienti utilizzano. Dopo [collegare l’istanza Commerce a MBI](../../data-analyst/importing-data/integrations/magento.md), puoi utilizzare la [Data Warehouse Manager](../../data-analyst/data-warehouse-mgr/tour-dwm.md) per tenere traccia dei campi dati rilevanti.

| Nome tabella | Descrizione |
|---|---|
| `catalog_category_entity` | Ogni riga nel `catalog_category_entity` La tabella descrive una categoria specifica. Con l&#39;associato `catalog_category_entity_varchar` la tabella e `catalog_category_product` tabella di mappatura, puoi ottenere informazioni sulla categoria per ogni prodotto. |
| `catalog_category_product` | Ogni riga nel `catalog_category_product` nella tabella è riportata una combinazione di un prodotto e una categoria. Pertanto, un dato prodotto può esistere più volte in questa tabella con categorie diverse e una determinata categoria può esistere in questa tabella più volte associata a prodotti diversi. Questa tabella indicizza il `catalog_category_entity` tabella (che contiene i dettagli a livello di categoria) e `catalog_product_entity` tabella (che contiene i dettagli a livello di prodotto). |
| `catalog_product_entity` | Ogni riga nel `catalog_product_entity` La tabella rappresenta un prodotto specifico. Ciò include quando quel prodotto è stato creato nel tuo account Commerce e nel relativo SKU. |
| `customer_entity` | Ogni riga nel [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) rappresenta un utente registrato sul sito web. Informazioni di base a livello di cliente, come la data di registrazione e l&#39;indirizzo e-mail, sono disponibili in questa tabella. |
| `quote` | Ogni riga nel [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) La tabella rappresenta un carrello creato nel processo di pagamento, che il carrello sia stato convertito o meno in un ordine. A causa delle dimensioni potenziali di questa tabella, ti consigliamo di eliminare periodicamente i record se vengono soddisfatti determinati criteri, ad esempio se sono presenti carrelli non convertiti con età superiore a 60 giorni. |
| `quote_item` | Ogni riga nel [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) La tabella rappresenta un elemento aggiunto al carrello, che il carrello sia stato convertito o meno in un ordine. A causa delle dimensioni potenziali di questa tabella, ti consigliamo di eliminare periodicamente i record se vengono soddisfatti determinati criteri, ad esempio se sono presenti carrelli non convertiti con età superiore a 60 giorni. |
| `sales_order` | Ogni riga nel [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) rappresenta un ordine posizionato sul sito. Questa tabella contiene informazioni a livello di ordine, quali la data dell’ordine, il cliente che ha effettuato l’ordine, il totale dell’ordine e l’utilizzo del codice sconto e coupon. |
| `sales_order_address` | Ogni riga del `sales_order_address` La tabella contiene informazioni di spedizione e fatturazione per un ordine specifico. Sulla `sales_order` la tabella `billing_address_id` e `shipping_address_id` per un dato ordine fare riferimento a una riga specifica (identificata da `entity_id`) sul `sales_order_address` tabella. |
| `sales_order_item` | Ogni riga nel [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) una tabella identifica un elemento specifico da un ordine specifico. Ogni riga contiene dettagli quali il prodotto, la quantità acquistata e l&#39;ordine a cui è associato l&#39;articolo specificato. |

{style=&quot;table-layout:auto&quot;}

## Documentazione correlata

[[!DNL Magento] Diagrammi di relazione entità](../data-warehouse-mgr/entity-rel-diag.md)
