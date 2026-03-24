---
title: Formattazione e importazione di dati di eCommerce
description: Scopri i formati di dati ideali da utilizzare per caricare i dati di eCommerce.
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/3Aa9DgQL0H9cNeJOJ7-qHkROOkphjzpQkDvJ0KwOIwY
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 459
ht-degree: 0%

---

# Formattazione e importazione di dati

Se utilizzi un&#39;integrazione non attualmente supportata da [!DNL Adobe Commerce Intelligence], puoi comunque utilizzare la [funzione di caricamento file](using-file-uploader.md) per inserire i dati nel Data Warehouse. Questo argomento descrive i formati di dati ideali da utilizzare per caricare i dati di e-commerce.

## Tabella `Orders`

La tabella `orders` deve contenere una riga per ogni transazione eseguita dall&#39;azienda. Le colonne potenziali includono:

| Nome colonna | Descrizione |
|----|----|
| `Order ID` | L’ID dell’ordine deve essere univoco per ogni riga della tabella. Inoltre, in genere si tratta della chiave primaria della tabella. |
| `Customer` | Il cliente che ha effettuato l’ordine. |
| `Order total` | Totale dell&#39;ordine. Può trattarsi di una colonna basata su calcoli, in cui i valori di altre colonne, ad esempio subtotale e spedizione, costituiscono il totale di questa colonna. |
| `Currency` | La valuta in cui è stato pagato l’ordine. Includere se pertinente. |
| ` Order status` | Stato dell&#39;ordine, ad esempio `In Progress`, `Refunded` o `Complete`. Il valore di questa colonna cambia (se non è completo). È possibile importare dati nuovi e aggiornati utilizzando la funzionalità [Aggiungi dati](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md) nella pagina `File Uploads`. |
| `Acquisition/marketing channel` | Il canale di acquisizione o marketing da cui proviene il cliente che ha effettuato l’ordine. |
| `Order datetime` | Data e ora di creazione dell&#39;ordine. |
| `Order updated at` | La data e l’ora dell’ultima modifica apportata al record dell’ordine. |

{style="table-layout:auto"}

## Tabella `Order detail/items` {#itemstable}

La tabella `order_detail / items` deve contenere una riga per ogni elemento distinto in ogni ordine. Le colonne potenziali includono:

| Nome colonna | Descrizione |
|----|----|
| `Order item ID` | L’ID dell’articolo dell’ordine deve essere univoco per ogni riga della tabella. Inoltre, in genere si tratta di `primary key` per la tabella. |
| `Order ID` | ID dell’ordine. |
| `Product ID` | ID del prodotto. |
| `Product name` | Il nome del prodotto. |
| `Product's unit price` | Il prezzo di una singola unità del prodotto. |
| `Quantity` | Quantità del prodotto nell’ordine. |

## Tabella `Customers` {#customerstable}

La tabella `customers` deve contenere una riga per ogni account cliente. Le colonne potenziali includono:

| Nome colonna | Descrizione |
|----|----|
| `Customer ID` | L’ID cliente deve essere univoco per ogni riga della tabella. Inoltre, in genere si tratta della chiave primaria della tabella. |
| `Customer created at` | La data e l’ora di creazione dell’account del cliente. |
| `Customer modified at` | La data e l’ora dell’ultima modifica apportata all’account del cliente. |
| `Acquisition/marketing channel source` | Il canale di acquisizione o marketing da cui il cliente proviene. |
| `Demographic info` | Per segmentare i rapporti è possibile utilizzare informazioni demografiche come la fascia di età e il genere. |
| `Acquisition/marketing channel` | Il canale di acquisizione o marketing da cui proviene il cliente che ha effettuato l’ordine. |

## Tabella `Subscription payments`

La tabella `subscriptions` deve contenere una riga per ogni pagamento dell&#39;abbonamento. Le colonne potenziali includono:

| Nome colonna | Descrizione |
|----|----|
| `Subscription ID` | L’ID dell’abbonamento deve essere univoco per ogni riga della tabella. Inoltre, in genere si tratta della chiave primaria della tabella. |
| `Customer ID` | ID del cliente che ha effettuato il pagamento. |
| `Payment amount` | Importo del pagamento dell’abbonamento. |
| `Start date` | Data e ora di inizio del periodo coperto dal pagamento. |
| `End date` | Data e ora di fine del periodo coperto dal pagamento. |
