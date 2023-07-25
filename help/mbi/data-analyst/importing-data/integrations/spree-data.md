---
title: Previsto Spree data
description: Esplora le tabelle di dati principali che puoi importare da Sprea in [!DNL Commerce Intelligence] account.
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Previsto [!DNL Spree] dati

Dopo aver [ha connesso [!DNL Spree] archiviare](../../../data-analyst/importing-data/integrations/spree.md), è possibile utilizzare [Gestione Date Warehouse](../../data-warehouse-mgr/tour-dwm.md) per tracciare facilmente i campi di dati rilevanti dal [!DNL Spree] piattaforma di analisi.

Questo argomento descrive le tabelle dati principali da cui è possibile importare [!DNL Spree] nel tuo [!DNL Commerce Intelligence] account, inclusi i collegamenti a [documentazione aggiuntiva](https://guides.spreecommerce.org/developer/addresses.html#address) informazioni su [!DNL Spree] dati.

| **Nome tabella** | **Descrizione** |
|-----|-----|
| `Users` | Il `users` la tabella include i dettagli dell’account per i clienti registrati, inclusi e-mail, nome e data di registrazione dell’individuo. Questo ti consente di analizzare diversi segmenti di clienti e i loro comportamenti di acquisto. |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | Il `orders` funge da base per tutte le metriche a livello di ordine. Registrati qui sono tutti i dettagli dell&#39;ordine di acquisti dal tuo [!DNL Spree] archiviare, inclusi `completed\_at` (la marca temporale dell’ordine), `user\_id` (ID dell’utente registrato che ha effettuato l’ordine). Se l’ordine è stato effettuato da un utente registrato, il `user\_id` collegamenti verso `users` tabella per consentire l’analisi del comportamento di acquisto degli utenti. |
| `Line items` | Il `line\_items` è un elemento figlio di `orders` tabella o `subscriptions`. Registra i dettagli della voce di un ordine o di una sottoscrizione. Per gli ordini con più prodotti, ogni prodotto ha la propria riga di dati in questa tabella, inclusa una `product\_id` che ti consente di collegarlo al `Products` tabella. |
| `Products` | Il `products` nella tabella vengono registrati tutti i dettagli dei prodotti per un articolo vendibile nel catalogo di vendita. Questo consente di segmentare le metriche a livello di voce per attributi di prodotto. |
| `Subscriptions` | Se si dispone di [!DNL Spree] l’estensione subscriptions, il `subscriptions` la tabella contiene le informazioni di ogni singolo abbonamento, tra cui `created\_at` (data di inizio), `cancelled\_at` (la data di annullamento di un abbonamento) e `interval` dell’abbonamento. |

{style="table-layout:auto"}

## Correlato:

* [Connessione [!DNL Spree]](../integrations/spree.md)
* [Reautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
