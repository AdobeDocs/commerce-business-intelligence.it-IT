---
title: Dati Stripe previsti
description: Esplora le tabelle di dati principali che puoi importare da Stripe in Commerce Intelligence.
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# Previsto [!DNL Stripe] dati

Dopo [hai connesso il tuo [!DNL Stripe] account](../integrations/stripe.md), è possibile utilizzare [Gestione Date Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) per tracciare facilmente i campi di dati rilevanti per l’analisi.

Questo argomento descrive le tabelle dati principali da cui è possibile importare [!DNL Stripe] in [!DNL Commerce Intelligence]. Al termine dell’installazione, nella Data Warehouse verranno create le seguenti tabelle. Fare clic sui collegamenti nella colonna Nome tabella per ulteriori informazioni sugli attributi di ogni tabella.

| **Nome tabella** | **Descrizione** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/sources/customers) | Gli oggetti cliente consentono di eseguire addebiti ricorrenti e di tenere traccia di più addebiti associati allo stesso cliente. |
| [`Charges`](https://stripe.com/docs/payments/payment-intents/migration/charges) | Questa tabella contiene informazioni sulle spese per le carte di credito e di debito, tra cui l&#39;importo, la valuta, lo stato, l&#39;ID cliente e altro. |
| [`Coupons`](https://stripe.com/docs/api/coupons/object) | Questa tabella contiene informazioni su uno sconto percentuale o importo sconto che è possibile applicare a un cliente. Le cedole si applicano solo alle fatture; non si applicano alle spese una tantum. |
| [`Invoices`](https://stripe.com/docs/billing/migration/invoice-states) | Questa tabella contiene informazioni sulle fatture, tra cui l&#39;importo dovuto, le sottoscrizioni, le voci delle fatture, gli adeguamenti automatici delle quote e altro ancora. |
| [`Plans`](https://stripe.com/docs/api/plans/object) | Questa tabella contiene le informazioni sui prezzi per i diversi prodotti e livelli di funzionalità del sito. Ad esempio, puoi avere un piano mensile di 10 $ per le funzioni di base e un piano mensile di 20 $ per le funzioni premium. |
| [`Subscriptions`](https://stripe.com/docs/api/subscriptions/object) | Questa tabella contiene i dettagli dei piani di abbonamento a cui appartengono i tuoi clienti. Gli attributi includono ID cliente, stato, annullato/terminato alle date, percentuale di imposta, informazioni sulla versione di valutazione e altro ancora. |
| [`Events`](https://stripe.com/docs/development/dashboard/events) | Eventi ti fanno sapere qualcosa di interessante che è successo in un account. [Quando si verifica un evento interessante](https://stripe.com/docs/api/events/types), viene creato un nuovo oggetto evento. Ad esempio, quando un addebito ha esito positivo `charge.succeeded` o, quando una fattura non può essere pagata, un `invoice.payment\_failed` viene creato. |

{style="table-layout:auto"}

>[!NOTE]
>
>Molte richieste API possono causare la creazione di più eventi. Ad esempio, se crei un abbonamento per un cliente, riceverai sia un `customer.subscription.created` evento e un  `charge.succeeded` evento.

## Correlato:

* [Connessione [!DNL Stripe]](../integrations/stripe.md)
* [Reautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
