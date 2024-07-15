---
title: Dati Commerce previsti
description: Esplora le tabelle di dati principali importate dagli utenti di Commerce in Commerce Intelligence
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# Previsti [!DNL Adobe Commerce] dati

Dopo aver [connesso il tuo [!DNL Adobe Commerce] archivio](../../../data-analyst/importing-data/integrations/magento.md), puoi utilizzare Gestione Date Warehouse per tenere traccia facilmente dei campi di dati rilevanti dal database Commerce per l&#39;analisi.

In questo argomento vengono illustrate le principali tabelle dati importate dagli utenti di Commerce in [!DNL Commerce Intelligence].

| **Nome tabella** | **Descrizione** |
|-----|-----|
| `Customers` | Le tabelle `customer\_entity` e correlate descrivono le informazioni associate a ogni *cliente registrato* nel database, come l&#39;indirizzo e-mail e la data di registrazione. Con queste informazioni, puoi iniziare a segmentare per attributi e coorti a livello di cliente. |
| `Orders` | La tabella `sales\_flat\_order` registra tutti gli ordini, inclusi il timestamp `created\_at` utilizzato per l&#39;ordine e il campo `base\_grand\_total` che somma i ricavi. Questi campi costituiscono la base per le metriche a livello di ordine. Se l&#39;ordine è stato effettuato da un *cliente registrato*, il campo `customer\_id` si collega alla tabella `customer\_entity` per consentire l&#39;analisi del comportamento di acquisto del cliente. |
| `Order items` | La tabella `sales\_flat\_order\_item` registra ogni elemento appartenente a un ordine. Sono inclusi i campi `price` e `qty\_ordered` e il campo `order\_id` che si connette alla tabella `sales\_flat\_order`. Questa tabella è la base per le metriche come `Item sold` e consente di segmentare per `product` e `product type`. |
| `Products` | Nella tabella `catalog\_product\_entity` sono memorizzate informazioni sugli attributi a livello di prodotto, ad esempio categoria, dimensione e colore. |
| `Categories` | I prodotti appartengono a uno o più `product categories` diversi, a seconda di come è configurata la build Commerce. La tabella `catalog\_category\_entity` memorizza la gerarchia di queste categorie (ad esempio, Abbigliamento > Punte superiori > T-shirt) e la tabella `catalog\_category\_product` registra le connessioni tra i prodotti e le categorie. |

{style="table-layout:auto"}

## Correlato

* [Connessione in corso  [!DNL Adobe Commerce]](../integrations/magento.md)
* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
