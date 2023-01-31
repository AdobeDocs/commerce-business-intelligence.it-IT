---
title: Dati Commerce previsti
description: Esplorare le tabelle di dati principali importate dagli utenti Commerce in MBI
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Dati Commerce previsti

Dopo aver [connesso a Commerce store](../../../data-analyst/importing-data/integrations/magento.md), puoi utilizzare Data Warehouse Manager per monitorare facilmente i campi dati rilevanti dal database Commerce per l’analisi.

In questo articolo, esploriamo le tabelle di dati principali in cui gli utenti Commerce importano [!DNL MBI].

| **Nome tabella** | **Descrizione** |
|-----|-----|
| `Customers` | La `customer\_entity` e tabelle correlate descrivono le informazioni associate a ciascuna *cliente registrato* nel tuo database, come il loro indirizzo e-mail e la data di registrazione. Con queste informazioni puoi iniziare a segmentare per attributi e coorti a livello di cliente. |
| `Orders` | La `sales\_flat\_order` la tabella registra tutti gli ordini, compresi `created\_at` marca temporale in cui l’ordine è stato inserito e `base\_grand\_total` campo che somma i ricavi. Questi campi costituiranno la base per le metriche a livello di ordine. Se l&#39;ordine è stato effettuato da un *cliente registrato*, `customer\_id` il campo sarà collegato di nuovo al  `customer\_entity` per consentire l’analisi del comportamento d’acquisto dei clienti. |
| `Order items` | La `sales\_flat\_order\_item` la tabella registra ogni elemento appartenente a un ordine. Ciò include `price` e `qty\_ordered` i campi e `order\_id` campo che si connette al `sales\_flat\_order` tabella. Questa tabella è alla base di metriche come `Item sold`e ti consente di segmentare per `product` e `product type`. |
| `Products` | La `catalog\_product\_entity` in tabella vengono memorizzate informazioni sugli attributi a livello di prodotto, ad esempio categoria, dimensione e colore. |
| `Categories` | I tuoi prodotti appartengono a uno o più `product categories`, a seconda della configurazione della build Commerce. La `catalog\_category\_entity` la tabella memorizza la gerarchia di queste categorie (ad esempio Apprarel > Tops > T-Shirts) e la `catalog\_category\_product` la tabella registra le connessioni tra i prodotti e le categorie. |

{style=&quot;table-layout:auto&quot;}

## Correlati

* [Collegamento [!DNL Magento]](../integrations/magento.md)
* [Riautenticazione delle integrazioni](https://support.magento.com/hc/en-us/articles/360016733151)
