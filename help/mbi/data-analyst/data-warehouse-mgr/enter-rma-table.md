---
title: Tabella enterprise_rma
description: Scopri come analizzare le informazioni su una richiesta di ritorno specifica.
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# Tabella enterprise_rma

Ogni riga nella `enterprise_rma` tabella (spesso chiamata `magento_rma` in Commerce 2.x, ma il nome può essere personalizzato) contiene informazioni su una richiesta di ritorno specifica.

>[!NOTE]
>
>Questa tabella viene fornita con il tuo account Commerce solo se sei un `Enterprise Edition` o `Enterprise Cloud Edition` cliente.

## Colonne native comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `entity\_id` | Identificatore univoco della tabella. Ogni `entity\_id` rappresenta una richiesta di ritorno. |
| `date\_requested` | Data in cui è stata richiesta la restituzione. |
| `status` | Stato del reso. I valori includono, tra gli altri, &quot;received&quot;, &quot;pending&quot;, &quot;authorized&quot;. |
| `order\_id` | Chiave esterna associata al `sales\_flat\_order` tabella. |
| `customer\_id` | Chiave esterna associata al `customer\_entity` tabella. |

{style="table-layout:auto"}

## Colonne calcolate comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `Order's created\_at` | Questa è la data dell&#39;ordine originale. Può essere utilizzato per ottenere il tempo tra l&#39;ordine e la richiesta di restituzione. |
| `Customer's order number` | Si tratta del numero di ordine del cliente associato all&#39;ordine originale. |
| `Seconds between order's created\_at and return's date\_requested` | Il numero di secondi dalla data dell’ordine alla richiesta di ritorno. |
| `Return's total value` | Si tratta dell&#39;importo monetario totale restituito. Si tratta della somma dell&#39;importo del reso individuale di ogni articolo di reso. |

{style="table-layout:auto"}

## Metriche comuni

| **Nome della metrica** | **Descrizione** | **Costruzione** |
|---|---|---|
| `Number of returns` | Il numero di restituzioni richieste. | `Operation` colonna: `entity id`<br>`Operation`: `Count`<br>`Timestamp` Colonna: `date requested` |
| `Total returned amount` | Importo monetario totale restituito. | `Operation `Colonna: `Return's total value`<br>`Operation`: Somma<br>`Timestamp` Colonna: data richiesta |
| `Average returned amount` | Importo monetario medio restituito. | `Operation`` Column: Return's total value`<br>`Operation`: `Average`<br>`Timestamp` Colonna: `date requested` |
| `Average time to return` | Tempo medio dall&#39;ordine alla restituzione. | `Operation` Colonna: secondi tra la data di creazione dell’ordine e la data di restituzione richiesta<br>`Operation`: `Average`<br>`Timestamp` Colonna: `date requested` |

{style="table-layout:auto"}

## Connessioni ad altre tabelle

`sale_flat_order`

* Crea colonne unite per segmentare e filtrare in base agli attributi a livello di ordine nel `enterprise_rma` tabella tramite il seguente join:
   * Commerce 1.x: `enterprise_rma.order_id` (molti) => `sales_flat_order.entity_id` (uno)
   * Commerce 2.x: `magento_rma.order_id` (molti) => `sales_order.entity_id` (uno)

`enterprise_rma_item_entity`

* Creare colonne molti-a-uno come `Return's total value` il `enterprise_rma` tabella tramite il seguente join:
   * Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id` (molti) => `enterprise_rma.entity_id` (uno)
   * Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (molti) => `magento_rma.entity_id` (uno)
