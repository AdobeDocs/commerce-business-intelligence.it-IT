---
title: Dati Commerce previsti
description: Esplora le tabelle di dati principali importate dagli utenti Commerce in MBI
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# Dati Commerce previsti

Dopo aver [ha collegato il tuo archivio Commerce](../../../data-analyst/importing-data/integrations/magento.md), è possibile utilizzare Data Warehouse Manager per tracciare facilmente i campi di dati rilevanti dal database Commerce per l’analisi.

Questo articolo esplora le tabelle di dati principali importate dagli utenti Commerce in [!DNL MBI].

| **Nome tabella** | **Descrizione** |
|-----|-----|
| `Customers` | Il `customer\_entity` e tabelle correlate descrivono le informazioni associate a ciascuna *cliente registrato* nel database, ad esempio l’indirizzo e-mail e la data di registrazione. Con queste informazioni, puoi iniziare a segmentare per attributi e coorti a livello di cliente. |
| `Orders` | Il `sales\_flat\_order` nella tabella vengono registrati tutti gli ordini, inclusi `created\_at` la marca temporale in cui è stato effettuato l’ordine e il `base\_grand\_total` campo che somma i ricavi. Questi campi costituiscono la base per le metriche a livello di ordine. Se l’ordine è stato effettuato da un *cliente registrato*, il `customer\_id` collegamenti di campo al  `customer\_entity` tabella per consentire l’analisi del comportamento di acquisto dei clienti. |
| `Order items` | Il `sales\_flat\_order\_item` la tabella registra ogni articolo appartenente a un ordine. Ciò include `price` e `qty\_ordered` e `order\_id` campo che si connette al `sales\_flat\_order` tabella. Questa tabella è la base per le metriche come `Item sold`, e consente di segmentare per `product` e `product type`. |
| `Products` | Il `catalog\_product\_entity` nella tabella sono memorizzate informazioni sugli attributi a livello di prodotto, come categoria, dimensione e colore. |
| `Categories` | I tuoi prodotti appartengono a uno o più diversi `product categories`, a seconda della configurazione della build Commerce. Il `catalog\_category\_entity` La tabella memorizza la gerarchia di queste categorie (ad esempio, Abbigliamento > Punte superiori > T-shirt) e il `catalog\_category\_product` La tabella registra le connessioni tra i prodotti e le categorie. |

{style="table-layout:auto"}

## Correlato

* [Connessione [!DNL Adobe Commerce]](../integrations/magento.md)
* [Reautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
