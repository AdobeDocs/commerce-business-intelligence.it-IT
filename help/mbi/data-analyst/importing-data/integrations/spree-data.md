---
title: Previsto Spree data
description: Esplora le tabelle di dati principali che puoi importare da Spree nel tuo account [!DNL Commerce Intelligence] .
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Previsti [!DNL Spree] dati

Dopo aver [connesso il tuo [!DNL Spree] archivio](../../../data-analyst/importing-data/integrations/spree.md), puoi utilizzare [Data Warehouse Manager](../../data-warehouse-mgr/tour-dwm.md) per tenere traccia facilmente dei campi di dati rilevanti dalla piattaforma [!DNL Spree] per l&#39;analisi.

In questo argomento vengono illustrate le principali tabelle dati che è possibile importare da [!DNL Spree] nel proprio account [!DNL Commerce Intelligence], inclusi i collegamenti alla [documentazione aggiuntiva](https://guides.spreecommerce.org/developer/addresses.html#address) relativa ai dati di [!DNL Spree].

| **Nome tabella** | **Descrizione** |
|-----|-----|
| `Users` | La tabella `users` include i dettagli dell&#39;account per i clienti registrati, inclusi l&#39;indirizzo e-mail, il nome e la data di registrazione dell&#39;utente. Questo ti consente di analizzare diversi segmenti di clienti e i loro comportamenti di acquisto. |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | La tabella `orders` funge da base per tutte le metriche a livello di ordine. Qui sono registrati tutti i dettagli dell&#39;ordine degli acquisti effettuati dal tuo store [!DNL Spree], tra cui `completed\_at` (la marca temporale dell&#39;ordine), `user\_id` (ID dell&#39;utente registrato che ha effettuato l&#39;ordine). Se l&#39;ordine è stato effettuato da un utente registrato, `user\_id` esegue il collegamento alla tabella `users` per consentire l&#39;analisi del comportamento di acquisto degli utenti. |
| `Line items` | La tabella `line\_items` è figlio della tabella `orders` o di `subscriptions`. Registra i dettagli della voce di un ordine o di una sottoscrizione. Per gli ordini con più prodotti, ogni prodotto ha la propria riga di dati in questa tabella, incluso un `product\_id` che consente di collegarlo alla tabella `Products`. |
| `Products` | La tabella `products` registra tutti i dettagli di prodotto per un articolo vendibile nel catalogo di vendita. Questo consente di segmentare le metriche a livello di voce per attributi di prodotto. |
| `Subscriptions` | Se si dispone di un&#39;estensione [!DNL Spree] sottoscrizioni, la tabella `subscriptions` contiene le informazioni di ogni singola sottoscrizione, inclusi `created\_at` (la data di inizio), `cancelled\_at` (la data di annullamento di una sottoscrizione) e `interval` della sottoscrizione. |

{style="table-layout:auto"}

## Correlato:

* [Connessione in corso  [!DNL Spree]](../integrations/spree.md)
* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=it)
