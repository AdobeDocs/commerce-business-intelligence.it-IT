---
title: Tabella enterprise_rma
description: Scopri come analizzare le informazioni su una richiesta di ritorno specifica.
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/ofPlk5xNr8aspjFlpzEtDtjcOPm9DrQFYX9-vPDfK6w
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 267
ht-degree: 0%

---

# Tabella enterprise_rma

Ogni riga della tabella `enterprise_rma` (spesso denominata `magento_rma` in Adobe Commerce 2.x, ma il nome può essere personalizzato) contiene informazioni su una richiesta di ritorno specifica.

>[!NOTE]
>
>Questa tabella è standard solo per il tuo account Adobe Commerce se sei un cliente `Enterprise Edition` o `Enterprise Cloud Edition`.

## Colonne native comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `entity\_id` | Identificatore univoco della tabella. Ogni `entity\_id` rappresenta una richiesta restituita. |
| `date\_requested` | Data in cui è stata richiesta la restituzione. |
| `status` | Stato del reso. I valori includono, tra gli altri, &quot;received&quot;, &quot;pending&quot;, &quot;authorized&quot;. |
| `order\_id` | Chiave esterna associata alla tabella `sales\_flat\_order`. |
| `customer\_id` | Chiave esterna associata alla tabella `customer\_entity`. |

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

| **Nome metrica** | **Descrizione** | **Costruzione** |
|---|---|---|
| `Number of returns` | Il numero di restituzioni richieste. | `Operation` colonna: `entity id`<br>`Operation`: `Count`<br>`Timestamp` colonna: `date requested` |
| `Total returned amount` | Importo monetario totale restituito. | `Operation `Colonna: `Return's total value`<br>`Operation`: Somma<br>`Timestamp` Colonna: data richiesta |
| `Average returned amount` | Importo monetario medio restituito. | `Operation`` Column: Return's total value`<br>`Operation`: `Average`<br>`Timestamp` Colonna: `date requested` |
| `Average time to return` | Tempo medio dall&#39;ordine alla restituzione. | `Operation` Colonna: secondi tra la data di creazione dell&#39;ordine e la data di restituzione richiesta<br>`Operation`: `Average`<br>`Timestamp` Colonna: `date requested` |

{style="table-layout:auto"}

## Connessioni ad altre tabelle

`sale_flat_order`

* Creare colonne unite per segmentare e filtrare in base agli attributi a livello di ordine nella tabella `enterprise_rma` tramite il join seguente:
   * Commerce 1.x: `enterprise_rma.order_id` (molti) => `sales_flat_order.entity_id` (uno)
   * Commerce 2.x: `magento_rma.order_id` (molti) => `sales_order.entity_id` (uno)

`enterprise_rma_item_entity`

* Creare colonne molti-a-uno come `Return's total value` nella tabella `enterprise_rma` tramite il join seguente:
   * Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id` (molti) => `enterprise_rma.entity_id` (uno)
   * Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (molti) => `magento_rma.entity_id` (uno)
