---
title: Dati QuickBooks previsti
description: Scopri come tracciare facilmente i campi di dati rilevanti per l’analisi.
exl-id: a60996bd-e3d1-497d-abce-f02ef1444f1a
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# Previsti [!DNL QuickBooks] dati

Dopo che [hai connesso il tuo [!DNL QuickBooks] account](../../../data-analyst/importing-data/integrations/quickbooks.md), puoi utilizzare [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) per tenere traccia facilmente dei campi di dati rilevanti per l&#39;analisi. Le tabelle seguenti vengono create nel Data Warehouse:

Per visualizzare tutti i campi disponibili per il tracciamento, fai clic sui collegamenti nella colonna nome tabella.

## Entità transazione {#transactionentities}

| **Nome tabella** | **Descrizione** |
|-----|-----|
| [`bill`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Bill) | La tabella `bills` contiene informazioni sulle transazioni di Personalizzazione automatizzata o una richiesta di pagamento da parte di terzi. Gli attributi includono tipo di valuta, tasso di cambio, importo totale, data di scadenza, saldo e altro ancora. |
| [`billpayments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/BillPayment) | Le entità `BillPayment` sono la transazione finale di pagamento delle fatture ricevute da un fornitore. Questa tabella include le informazioni sul fornitore, il tipo di pagamento, l&#39;importo totale, la data della transazione e altro ancora. |
| [`creditmemos`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/CreditMemo) | La tabella `creditmemos` registra le transazioni che sono rimborsi o crediti di pagamenti completi e parziali. Alcuni attributi includono il nome del cliente, le informazioni di fatturazione e spedizione del cliente, l&#39;importo e la data. |
| [`deposits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Deposit) | `Deposits` includono i depositi diretti e i pagamenti dei clienti spostati nel conto attività dopo essere stati detenuti nel conto `Undeposited Funds`. Gli attributi includono l’importo, l’ID deposito e la data. |
| [`estimates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Estimate) | `Estimates` sono transazioni fornite ai clienti che includono i prezzi proposti per un bene o un servizio. Questa tabella registra l&#39;importo, le informazioni sugli sconti, le informazioni sui clienti e la data. |
| [`invoices`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Invoice) | `Invoices` sono moduli di vendita pagati successivamente da un cliente. Nella tabella delle fatture vengono registrate tutte le informazioni relative al versamento, alla data, alle voci, alle imposte e al cliente. |
| [`journalentries`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/JournalEntry) | La tabella `journalentries` registra le informazioni sui conti AR e AP, inclusi l&#39;ID della voce del giornale di registrazione, la data della transazione e le informazioni sulle voci. |
| [`payments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Payment) | Un record `payment` include attributi quali l&#39;ID pagamento, gli importi applicati e non applicati, la data della transazione, il tipo di transazione e lo stato di elaborazione. |
| [`purchases`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Purchase) | La tabella `purchases` rappresenta le spese e include l&#39;ID acquisto, il tipo di pagamento, l&#39;importo ed eventuali informazioni sulle voci. |
| [`purchaseorders`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PurchaseOrder) | La tabella `purchaseorders` contiene le richieste di merci inviate ai fornitori. Questa tabella include le informazioni relative al fornitore, l&#39;ID dell&#39;ordine fornitore, la data della transazione, le informazioni sulla voce, l&#39;importo totale e le informazioni sul conto AP. |
| [`refundreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/RefundReceipt) | La tabella `refundreceipts` registra i rimborsi concessi ai clienti. Gli attributi includono l&#39;ID della ricevuta di rimborso, le informazioni sulla voce, l&#39;importo totale, le informazioni sul cliente e il saldo. |
| [`salesreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/SalesReceipt) | La tabella `salesreceipts` registra le informazioni nelle entrate di vendita fornite ai clienti, inclusi l&#39;ID ricevuta di vendita, le informazioni sulla voce, l&#39;importo totale, le informazioni sul cliente, la data della transazione ed eventuali depositi. |
| [`timeactivities`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TimeActivity) | La tabella `timeactivities` contiene i record di tempo per fornitori e/o dipendenti e include l&#39;ID attività tempo, le informazioni su dipendenti/fornitori, il tempo registrato, la descrizione attività e la data di registrazione. |
| [`transfers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Transfer) | La tabella `transfers` registra le informazioni sui fondi spostati tra conti. Gli attributi includono l’ID trasferimento, l’importo, le informazioni sul conto e la data. |
| [`vendorcredits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/VendorCredit) | I crediti fornitore sono transazioni AP che rappresentano rimborsi o crediti concessi a fornitori. La tabella `vendorcredits` include l&#39;ID credito fornitore, le informazioni sulla voce, le informazioni sul fornitore, il conto AP, l&#39;importo totale e la data. |

{style="table-layout:auto"}

## Entità elenco nomi {#namelistentities}

| **Nome tabella** | **Descrizione** |
|-----|-----|
| [`accounts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Account) | Questa tabella include ID conto, nome, stato, tipo, saldo, valuta e ora di creazione. |
| [`budgets`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Budget) | Questa tabella registra tutte le informazioni relative ai budget aziendali, inclusi ID budget, nome, date di inizio e fine, tipo, stato e dettagli. |
| [`classes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Class) | Le classi, applicate alle righe di dettaglio delle transazioni, consentono di tenere traccia dei segmenti non associati a un cliente o a un progetto. Questa tabella registra l&#39;ID, il nome, la sottoclasse e lo stato della classe. |
| [`customers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Customer) | La tabella `customers` contiene tutte le informazioni relative ai clienti, inclusi l&#39;ID, il nome, gli indirizzi di fatturazione e spedizione, il numero di telefono e l&#39;indirizzo di posta elettronica del cliente. |
| [`departments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Department) | La tabella `departments` include l&#39;ID reparto, il nome e il tipo (reparto secondario e reparto principale). |
| [`employees`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Employee) | La tabella `employees` contiene informazioni sulle persone che lavorano per la tua azienda. Gli attributi includono ID dipendente, nome, indirizzo, numero di telefono e informazioni fatturabili, se la società è abilitata per il ciclo paghe. |
| [`items`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Item) | La tabella `items` contiene dettagli sui prodotti o servizi venduti dalla tua azienda. Questa tabella include l&#39;ID articolo, il nome, la descrizione, il prezzo unitario, il tipo, le informazioni sugli acquisti, la quantità esistente e le informazioni sul conto ricavi e cespiti. |
| [`paymentmethods`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PaymentMethod) | La tabella `paymentmethods` registra il metodo di pagamento ricevuto per beni e servizi. Contiene l’ID, il tipo e il nome del pagamento. |
| [`taxagencies`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxAgency) | In questa tabella vengono registrate le informazioni sulle agenzie fiscali, incluso l&#39;ID agenzia fiscale, e le informazioni di registrazione sulle imposte per acquisti e vendite. |
| [`taxcodes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxCode) | I codici imposta vengono utilizzati per tenere traccia dello stato dell&#39;imposta (imponibile e non imponibile) di prodotti, servizi e clienti. La tabella `taxcodes` include l&#39;ID del codice imposta, il nome, la descrizione, lo stato, lo stato imponibile, l&#39;aliquota e il gruppo di imposte. |
| [`taxrates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxRate) | Le aliquote vengono utilizzate per calcolare le passività fiscali. Questa tabella include l&#39;ID aliquota, il nome, la descrizione, l&#39;aliquota, l&#39;agenzia fiscale e altro ancora. |
| [`terms`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Term) | Questa entità rappresenta le condizioni in base alle quali vengono effettuate le vendite. La tabella dei termini include ID termine, nome, tipo, percentuale di sconto e giorni di scadenza. |
| [`vendors`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Vendor) | La tabella fornitori contiene informazioni sui fornitori da cui si effettuano gli acquisti. Gli attributi della tabella includono l’ID fornitore, il nome società, il numero di account, il saldo dell’account, lo stato 1099, l’indirizzo di fatturazione, il numero di telefono, l’indirizzo e-mail e l’indirizzo web. |

{style="table-layout:auto"}

## Correlato:

* [Connessione in corso  [!DNL QuickBooks]](../integrations/quickbooks.md)
* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
