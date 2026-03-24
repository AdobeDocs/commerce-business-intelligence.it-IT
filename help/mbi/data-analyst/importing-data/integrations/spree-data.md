---
title: Previsto Spree data
description: Esplora le tabelle di dati principali che puoi importare da Spree nel tuo account [!DNL Commerce Intelligence] .
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/DhJhNDqTEki-evyidC-9d08qq-XSDPRu1jJqG1lOijI
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 263
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
* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
