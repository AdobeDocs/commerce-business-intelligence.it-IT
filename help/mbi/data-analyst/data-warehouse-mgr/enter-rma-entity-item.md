---
title: Tabella Enterprise_Rma_Item_Entity
description: Scopri come analizzare le informazioni su un elemento specifico di una richiesta di reso.
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# Tabella enterprise_rma_item_entity

Ogni riga nella `enterprise_rma_item_entity` tabella (spesso chiamata `magento_rma_item_entity` in Commerce 2.x, ma il nome può essere personalizzato) contiene informazioni su un elemento specifico di una richiesta di reso.

>[!NOTE]
>
>Questa tabella viene fornita con il tuo account Commerce solo se sei un `Enterprise Edition` o `Enterprise Cloud Edition` cliente.

## Colonne native comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `entity\_id` | Identificatore univoco della tabella. Ogni `entity\_id` rappresenta un elemento che è stato richiesto per la restituzione. |
| `rma\_entity\_id` | Chiave esterna associata al `enterprise\_rma` tabella. |
| `status` | Stato della restituzione dell&#39;elemento. I valori includono, tra gli altri, &quot;received&quot;, &quot;pending&quot;, &quot;authorized&quot;. I valori in questo stato potrebbero non corrispondere al valore dello stato complessivo della restituzione. |
| `qty\_requested` | Quantità richiesta da parte del cliente per la restituzione. |
| `qty\_approved` | Quantità approvata per la restituzione. |
| `qty\_returned` | Quantità restituita. |
| `order\_item\_id` | Chiave esterna associata al `sales\_flat\_order\_item` tabella. |
| `product\_sku` | Lo SKU restituito. |

{style="table-layout:auto"}

## Colonne calcolate comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `Return date\_requested` | Questa è la data in cui il cliente ha richiesto la restituzione. |
| `Item price` | Prezzo dell’articolo. |
| `Return item's total value (qty\_returned * price)` | Si tratta del valore monetario totale degli elementi restituiti. Viene utilizzato per calcolare l&#39;importo del rendimento totale sul `enterprise\_rma` tabella. |

{style="table-layout:auto"}

## Metriche comuni

| **Nome della metrica** | **Descrizione** | **Costruzione** |
|---|---|---|
| `Number of items returned` | Numero di elementi restituiti. | Colonna operazione: qtà restituita<br>Operazione: Somma<br>Colonna timestamp: data di ritorno richiesta |
| `Returned items' total value` | Importo monetario restituito. | Colonna operazione: valore totale dell&#39;articolo reso (qtà restituita * prezzo)<br>Operazione: Somma<br>Colonna timestamp: data di ritorno richiesta |

{style="table-layout:auto"}

## Connessioni ad altre tabelle

`enterprise_rma`

* Creare colonne unite come `Return date\_requested` il `enterprise_rma_item_entity` tabella tramite il seguente join:
* Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id ` (molti) => `enterprise_rma.entity_id` (uno)
* Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (molti) => `magento_rma.entity_id` (uno)

`sales_flat_order_item`

* Crea colonne unite in join nel  `enterprise_rma_item_entity` tabella tramite il seguente join:

* Commerce 1.x: `enterprise_rma_item_entity.order_item_id ` (molti) => `sales_flat_order_item.item_id` (uno)
* Commerce 2.x: `magento_rma_item_entity.order_item_id ` (molti) => `sales_order_item.item_id` (uno)
