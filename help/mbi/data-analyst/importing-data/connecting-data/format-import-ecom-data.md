---
title: Formattazione e importazione di dati eCommerce
description: Scopri i formati di dati ideali per il caricamento di dati eCommerce.
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Formattazione e importazione dei dati

Se utilizzi un’integrazione non attualmente supportata da [!DNL MBI], puoi ancora utilizzare [Funzione di caricamento file](using-file-uploader.md) per inserire i dati nel data warehouse. In questo articolo, esaminiamo i formati di dati ideali per il caricamento dei dati eCommerce.

## `Orders` tabella

La `orders` La tabella deve contenere una riga per ogni transazione effettuata dall&#39;attività. Le colonne potenziali includono:

| Nome colonna | Descrizione |
|----|----|
| `Order ID` | L’ID ordine deve essere univoco per ogni riga della tabella. Inoltre, si tratta in genere della chiave primaria per la tabella. |
| `Customer` | Il cliente che ha effettuato l’ordine. |
| `Order total` | Totale dell&#39;ordine. Può trattarsi di una colonna basata su calcoli, in cui i valori di altre colonne, come il subtotale e la spedizione, costituiscono il totale per questa colonna. |
| `Currency` | La valuta in cui è stato pagato l&#39;ordine. Includi se pertinente. |
| ` Order status` | Lo stato dell&#39;ordine, ad esempio `In Progress`, `Refunded`oppure `Complete`. Il valore di questa colonna probabilmente cambierà (se non è completo). I dati nuovi e aggiornati possono essere importati utilizzando [Funzione Aggiungi dati](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md) sulla `File Uploads` pagina. |
| `Acquisition/marketing channel` | Il canale di acquisizione o marketing da cui è stato fatto riferimento al cliente che ha effettuato l&#39;ordine. |
| `Order datetime` | Data e ora di creazione dell’ordine. |
| `Order updated at` | Data e ora dell’ultima modifica apportata al record dell’ordine. |

{style=&quot;table-layout:auto&quot;}

## `Order detail/items` tabella {#itemstable}

La `order_detail / items` La tabella deve contenere una riga per ogni elemento distinto in ogni ordine. Le colonne potenziali includono:

| Nome colonna | Descrizione |
|----|----|
| `Order item ID` | L’ID dell’elemento dell’ordine deve essere univoco per ogni riga della tabella. Inoltre, questa è tipicamente la `primary key` per la tabella. |
| `Order ID` | ID dell&#39;ordine. |
| `Product ID` | ID del prodotto. |
| `Product name` | Nome del prodotto. |
| `Product's unit price` | Prezzo per una singola unità del prodotto. |
| `Quantity` | Quantità del prodotto nell&#39;ordine. |

## `Customers` tabella {#customerstable}

La `customers` La tabella deve contenere una riga per ciascun account cliente. Le colonne potenziali includono:

| Nome colonna | Descrizione |
|----|----|
| `Customer ID` | L’ID cliente deve essere univoco per ogni riga della tabella. Inoltre, si tratta in genere della chiave primaria per la tabella. |
| `Customer created at` | Data e ora di creazione dell&#39;account del cliente. |
| `Customer modified at` | Data e ora dell&#39;ultima modifica dell&#39;account del cliente. |
| `Acquisition/marketing channel source` | Canale di acquisizione o di marketing da cui è stato fatto riferimento al cliente. |
| `Demographic info` | Per segmentare i rapporti è possibile utilizzare informazioni demografiche come l’intervallo di età e il genere. |
| `Acquisition/marketing channel` | Il canale di acquisizione o marketing da cui è stato fatto riferimento al cliente che ha effettuato l&#39;ordine. |

## `Subscription payments` tabella

La `subscriptions` La tabella deve contenere una riga per ogni pagamento di abbonamento. Le colonne potenziali includono:

| Nome colonna | Descrizione |
|----|----|
| `Subscription ID` | L’ID della sottoscrizione deve essere univoco per ogni riga della tabella. Inoltre, si tratta in genere della chiave primaria per la tabella. |
| `Customer ID` | ID del cliente che ha effettuato il pagamento. |
| `Payment amount` | Importo del pagamento dell&#39;abbonamento. |
| `Start date` | Data e ora di inizio del periodo coperto dal pagamento. |
| `End date` | Data e ora di fine del periodo coperto dal pagamento. |
