---
title: Tabelle Commerce comuni
description: Scopri alcune delle tabelle più comuni utilizzate dai clienti  [!DNL Commerce Intelligence] .
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# Tabelle Commerce comuni

Quando si connette per la prima volta un&#39;istanza di [!DNL Adobe Commerce] a [[!DNL Adobe Commerce Intelligence]](../importing-data/integrations/magento.md), [!DNL Commerce Intelligence] replica automaticamente i dati da alcune tabelle commerce (in genere 4-6 tabelle) per configurare il set iniziale di dashboard e report. Anche se questo offre un ottimo punto di partenza, la maggior parte delle istanze dello store genera decine se non centinaia di tabelle aggiuntive che possono fornire informazioni critiche sulle prestazioni della tua azienda.

Di seguito è riportato un elenco di alcune delle tabelle più comuni utilizzate dai clienti [!DNL Commerce Intelligence]. Dopo aver [connesso l&#39;istanza di Commerce a Commerce Intelligence](../../data-analyst/importing-data/integrations/magento.md), puoi utilizzare [Data Warehouse Manager](../../data-analyst/data-warehouse-mgr/tour-dwm.md) per tenere traccia dei campi di dati rilevanti.

| Nome tabella | Descrizione |
|---|---|
| `catalog_category_entity` | Ogni riga della tabella `catalog_category_entity` descrive una categoria specifica. Con la tabella `catalog_category_entity_varchar` associata e la tabella di mappatura `catalog_category_product`, è possibile ottenere informazioni sulle categorie per ciascun prodotto. |
| `catalog_category_product` | Ogni riga della tabella `catalog_category_product` contiene una combinazione di un prodotto e una categoria. Pertanto, un determinato prodotto può esistere in questa tabella più volte con categorie diverse e una determinata categoria può esistere in questa tabella più volte associata a prodotti diversi. Questa tabella indicizza la tabella `catalog_category_entity` (contenente i dettagli a livello di categoria) e la tabella `catalog_product_entity` (contenente i dettagli a livello di prodotto). |
| `catalog_product_entity` | Ogni riga della tabella `catalog_product_entity` rappresenta un prodotto specifico. Ciò include quando il prodotto è stato creato nell’account Commerce e nel relativo SKU. |
| `customer_entity` | Ogni riga della tabella [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) rappresenta un utente registrato nel sito Web. Dettagli di base a livello di cliente come la data di registrazione e l’indirizzo e-mail sono in diretta su questa tabella. |
| `quote` | Ogni riga della tabella [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) rappresenta un carrello creato durante il processo di pagamento, indipendentemente dal fatto che il carrello sia stato convertito in un ordine. A causa delle dimensioni potenziali di questa tabella, Adobe consiglia di eliminare periodicamente i record se sono soddisfatti determinati criteri, ad esempio se sono presenti carrelli non convertiti di età superiore a 60 giorni. |
| `quote_item` | Ogni riga della tabella [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) rappresenta un elemento aggiunto a un carrello, indipendentemente dal fatto che il carrello sia stato convertito in un ordine. A causa delle dimensioni potenziali di questa tabella, Adobe consiglia di eliminare periodicamente i record se sono soddisfatti determinati criteri, ad esempio se sono presenti carrelli non convertiti di età superiore a 60 giorni. |
| `sales_order` | Ogni riga della tabella [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) rappresenta un ordine effettuato sul sito. Questa tabella contiene informazioni a livello di ordine quali la data dell&#39;ordine, il cliente che ha effettuato l&#39;ordine, il totale dell&#39;ordine e l&#39;utilizzo del codice sconto e coupon. |
| `sales_order_address` | Ogni riga della tabella `sales_order_address` contiene le informazioni di spedizione e fatturazione per un ordine specifico. Nella tabella `sales_order`, `billing_address_id` e `shipping_address_id` per un determinato ordine fanno riferimento a una riga specifica (identificata da `entity_id`) nella tabella `sales_order_address`. |
| `sales_order_item` | Ogni riga della tabella [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) identifica un elemento specifico di un ordine specifico. Ogni riga contiene dettagli quali il prodotto, la quantità acquistata e l&#39;ordine a cui è associato l&#39;articolo specificato. |

{style="table-layout:auto"}

## Documentazione correlata

[Diagrammi di relazione entità](../data-warehouse-mgr/entity-rel-diag.md)
