---
title: Dati di spreco previsti
description: Esplorare le tabelle di dati principali che è possibile importare da Spree nel [!DNL MBI] conto.
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Previsto [!DNL Spree] dati

Dopo aver [ha collegato [!DNL Spree] archiviare](../../../data-analyst/importing-data/integrations/spree.md), puoi utilizzare la [Data Warehouse Manager](../../data-warehouse-mgr/tour-dwm.md) tracciare facilmente i campi dati rilevanti dal [!DNL Spree] piattaforma di analisi.

In questo articolo, esploriamo le tabelle di dati principali da cui è possibile importare [!DNL Spree] nella [!DNL MBI] account, compresi i collegamenti a [documentazione aggiuntiva](https://guides.spreecommerce.org/developer/addresses.html#address) informazioni [!DNL Spree] dati.

| **Nome tabella** | **Descrizione** |
|-----|-----|
| `Users` | La `users` la tabella include i dettagli dell’account per i clienti registrati, compresi l’e-mail, il nome e la data di registrazione dell’utente. Questo ti consente di analizzare diversi segmenti di clienti e i loro comportamenti di acquisto. |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | La `orders` funge da base per tutte le metriche a livello di ordine. Registrati qui sono tutti i dettagli dell&#39;ordine degli acquisti dal tuo [!DNL Spree] immagazzinare, tra cui `completed\_at` (la marca temporale dell’ordine), `user\_id` (ID dell’utente registrato che ha effettuato l’ordine). Se l&#39;ordine è stato effettuato da un utente registrato, il `user\_id` tornerà a `users` per consentire l’analisi del comportamento di acquisto degli utenti. |
| `Line items` | La `line\_items` è un elemento secondario di `orders` tabella o `subscriptions`. Registra i dettagli dell&#39;articolo riga di un ordine o di un abbonamento. Per gli ordini con più prodotti, ogni prodotto avrà la propria riga di dati in questa tabella, inclusa una `product\_id` che consente di collegarlo al `Products` tabella. |
| `Products` | La `products` la tabella registra tutti i dettagli dei prodotti per un articolo vendibile nel catalogo Spree. Ciò ti consente di segmentare le metriche a livello di elemento della riga in base agli attributi del prodotto. |
| `Subscriptions` | Se hai [!DNL Spree] estensione degli abbonamenti, `subscriptions` la tabella contiene le informazioni di ogni singolo abbonamento, tra cui `created\_at` (data di inizio), `cancelled\_at` (la data di annullamento di un abbonamento) e `interval` della sottoscrizione. |

{style=&quot;table-layout:auto&quot;}

## Correlati:

* [Collegamento [!DNL Spree]](../integrations/spree.md)
* [Riautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
