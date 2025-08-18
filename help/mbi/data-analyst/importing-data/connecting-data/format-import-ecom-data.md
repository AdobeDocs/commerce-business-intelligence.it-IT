---
title: Formattazione e importazione di dati di eCommerce
description: Scopri i formati di dati ideali da utilizzare per caricare i dati di eCommerce.
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '459'
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
