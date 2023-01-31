---
title: Tabella entità_Rma_elemento_entità
description: Scopri come analizzare le informazioni su un elemento specifico da una restituzione richiesta.
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# tabella enterprise_rma_item_entity

Ogni riga nel `enterprise_rma_item_entity` tabella (spesso denominata `magento_rma_item_entity` in Commerce 2.x, ma il nome può essere personalizzato) contiene informazioni su un elemento specifico da una restituzione richiesta.

>[!NOTE]
>
>Questa tabella viene fornita con il tuo account Commerce solo se sei un `Enterprise Edition` o `Enterprise Cloud Edition` cliente.

## Colonne native comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `entity\_id` | Identificatore univoco della tabella. Ogni `entity\_id` rappresenta un elemento richiesto per la restituzione. |
| `rma\_entity\_id` | Chiave esterna associata al `enterprise\_rma` tabella. |
| `status` | Stato della restituzione dell&#39;elemento. I valori includono &quot;ricevuto&quot;, &quot;in sospeso&quot;, &quot;autorizzato&quot;, tra gli altri. I valori in questo stato non corrispondono necessariamente al valore dello stato del ritorno complessivo. |
| `qty\_requested` | Quantità richiesta dal cliente per la restituzione. |
| `qty\_approved` | Quantità approvata per la restituzione. |
| `qty\_returned` | La quantità effettivamente restituita. |
| `order\_item\_id` | Chiave esterna associata al `sales\_flat\_order\_item` tabella. |
| `product\_sku` | Lo sku viene restituito. |

{style=&quot;table-layout:auto&quot;}

## Colonne calcolate comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `Return date\_requested` | È la data in cui il cliente ha richiesto la restituzione. |
| `Item price` | Il prezzo dell&#39;oggetto. |
| `Return item's total value (qty\_returned * price)` | Si tratta del valore monetario totale degli elementi restituiti. Verrà utilizzato per calcolare l&#39;importo totale restituito sulla `enterprise\_rma` tabella. |

{style=&quot;table-layout:auto&quot;}

## Metriche comuni

| **Nome della metrica** | **Descrizione** | **Costruzione** |
|---|---|---|
| `Number of items returned` | Il numero di elementi restituiti. | Colonna operazione: qty restituito<br>Operazione: Somma<br>Colonna timestamp: Data di ritorno richiesta |
| `Returned items' total value` | Importo monetario restituito. | Colonna operazione: Valore totale dell&#39;articolo restituito (quantità restituita * prezzo)<br>Operazione: Somma<br>Colonna timestamp: Data di ritorno richiesta |

{style=&quot;table-layout:auto&quot;}

## Connessioni ad altre tabelle

`enterprise_rma`

* Creare colonne collegate, ad esempio `Return date\_requested` sulla `enterprise_rma_item_entity` tabella tramite il seguente join:
* Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id ` (molti) => `enterprise_rma.entity_id` 1)
* Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (molti) => `magento_rma.entity_id` 1)

`sales_flat_order_item`

* Creare colonne collegate  `enterprise_rma_item_entity` tabella tramite il seguente join:

* Commerce 1.x: `enterprise_rma_item_entity.order_item_id ` (molti) => `sales_flat_order_item.item_id` 1)
* Commerce 2.x: `magento_rma_item_entity.order_item_id ` (molti) => `sales_order_item.item_id` 1)
