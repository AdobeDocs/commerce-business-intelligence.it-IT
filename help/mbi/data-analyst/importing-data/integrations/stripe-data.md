---
title: Dati di striping previsti
description: Esplorare le tabelle di dati principali che è possibile importare da Stripe in [!DNL MBI].
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# Previsto [!DNL Stripe] dati

Dopo [hai connesso il tuo [!DNL Stripe] account](../integrations/stripe.md), puoi utilizzare la [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) per tenere traccia facilmente dei campi dati rilevanti ai fini dell’analisi.

In questo articolo, esploriamo le tabelle di dati principali da cui è possibile importare [!DNL Stripe] in [!DNL MBI]. Una volta completata l&#39;installazione, le tabelle seguenti verranno create nel data warehouse. Fai clic sui collegamenti nella colonna Nome tabella per ulteriori informazioni sugli attributi di ciascuna tabella.

| **Nome tabella** | **Descrizione** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/sources/customers) | Gli oggetti cliente consentono di eseguire spese ricorrenti e tenere traccia di più addebiti associati allo stesso cliente. |
| [`Charges`](https://stripe.com/docs/payments/payment-intents/migration/charges) | Questa tabella contiene informazioni sulle spese per le carte di credito e di debito, tra cui l&#39;importo, la valuta, lo stato, l&#39;ID cliente e altro ancora. |
| [`Coupons`](https://stripe.com/docs/api/coupons/object) | Questa tabella contiene informazioni su uno sconto percentuale o importo da applicare a un cliente. Si noti che i coupon si applicano solo alle fatture; non si applicano alle spese una tantum. |
| [`Invoices`](https://stripe.com/docs/billing/migration/invoice-states) | Questa tabella contiene informazioni sulle fatture, tra cui l&#39;importo dovuto, gli abbonamenti, gli articoli fattura, eventuali adeguamenti automatici della ripartizione e altro ancora. |
| [`Plans`](https://stripe.com/docs/api/plans/object) | Questa tabella contiene le informazioni sui prezzi per diversi prodotti e livelli di funzionalità sul sito. Ad esempio, puoi avere un piano di $ 10/mese per le funzioni di base e un piano di $ 20/mese per le funzioni premium. |
| [`Subscriptions`](https://stripe.com/docs/api/subscriptions/object) | Questa tabella contiene i dettagli dei piani di abbonamento a cui appartengono i clienti. Gli attributi includono ID cliente, stato, annullati/terminati alle date, percentuale di imposta, informazioni sulla versione di prova e altro ancora. |
| [`Events`](https://stripe.com/docs/development/dashboard/events) | Gli eventi ti permettono di sapere qualcosa di interessante che è appena successo in un account. [Quando si verifica un evento interessante](https://stripe.com/docs/api/events/types), viene creato un nuovo oggetto evento. Ad esempio, quando un addebito ha esito positivo `charge.succeeded` l&#39;evento viene creato; o, qualora non sia possibile pagare una fattura, `invoice.payment\_failed` viene creato l&#39;evento . |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Molte richieste API possono causare la creazione di più eventi. Ad esempio, se crei un nuovo abbonamento per un cliente, riceverai entrambi un `customer.subscription.created` evento e  `charge.succeeded` evento.

## Correlati:

* [Collegamento [!DNL Stripe]](../integrations/stripe.md)
* [Riautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
