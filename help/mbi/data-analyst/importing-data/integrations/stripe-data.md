---
title: Dati Stripe previsti
description: Esplora le tabelle di dati principali che puoi importare da Stripe in Commerce Intelligence.
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/dCiDusso9q9gvZOXKeHcDcuVK-jCXkqR3pQg6eTKzdo
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
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
source-wordcount: 323
ht-degree: 0%

---

# Previsti [!DNL Stripe] dati

Dopo che [hai connesso il tuo [!DNL Stripe] account](../integrations/stripe.md), puoi utilizzare [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) per tenere traccia facilmente dei campi di dati rilevanti per l&#39;analisi.

In questo argomento vengono illustrate le principali tabelle dati che è possibile importare da [!DNL Stripe] in [!DNL Commerce Intelligence]. Al termine dell’installazione, nel Data Warehouse verranno create le seguenti tabelle. Fare clic sui collegamenti nella colonna Nome tabella per ulteriori informazioni sugli attributi di ogni tabella.

| **Nome tabella** | **Descrizione** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/sources/customers) | Gli oggetti cliente consentono di eseguire addebiti ricorrenti e di tenere traccia di più addebiti associati allo stesso cliente. |
| [`Charges`](https://stripe.com/docs/payments/payment-intents/migration/charges) | Questa tabella contiene informazioni sulle spese per le carte di credito e di debito, tra cui l&#39;importo, la valuta, lo stato, l&#39;ID cliente e altro. |
| [`Coupons`](https://stripe.com/docs/api/coupons/object) | Questa tabella contiene informazioni su uno sconto percentuale o importo sconto che è possibile applicare a un cliente. Le cedole si applicano solo alle fatture; non si applicano alle spese una tantum. |
| [`Invoices`](https://stripe.com/docs/billing/migration/invoice-states) | Questa tabella contiene informazioni sulle fatture, tra cui l&#39;importo dovuto, le sottoscrizioni, le voci delle fatture, gli adeguamenti automatici delle quote e altro ancora. |
| [`Plans`](https://stripe.com/docs/api/plans/object) | Questa tabella contiene le informazioni sui prezzi per i diversi prodotti e livelli di funzionalità del sito. Ad esempio, puoi avere un piano mensile di 10 $ per le funzioni di base e un piano mensile di 20 $ per le funzioni premium. |
| [`Subscriptions`](https://stripe.com/docs/api/subscriptions/object) | Questa tabella contiene i dettagli dei piani di abbonamento a cui appartengono i tuoi clienti. Gli attributi includono ID cliente, stato, annullato/terminato alle date, percentuale di imposta, informazioni sulla versione di valutazione e altro ancora. |
| [`Events`](https://stripe.com/docs/development/dashboard/events) | Eventi ti fanno sapere qualcosa di interessante che è successo in un account. [Quando si verifica un evento interessante](https://stripe.com/docs/api/events/types), viene creato un nuovo oggetto evento. Ad esempio, quando viene creato un evento di addebito successivo a `charge.succeeded` oppure, quando non è possibile pagare una fattura, viene creato un evento di `invoice.payment\_failed`. |

{style="table-layout:auto"}

>[!NOTE]
>
>Molte richieste API possono causare la creazione di più eventi. Ad esempio, se crei una sottoscrizione per un cliente, riceverai sia un evento `customer.subscription.created` che un evento `charge.succeeded`.

## Correlato:

* [Connessione in corso  [!DNL Stripe]](../integrations/stripe.md)
* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
