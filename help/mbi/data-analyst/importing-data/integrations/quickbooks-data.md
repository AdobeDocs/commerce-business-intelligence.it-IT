---
title: Dati QuickBooks previsti
description: Scopri come tracciare facilmente i campi dati rilevanti per l’analisi.
exl-id: a60996bd-e3d1-497d-abce-f02ef1444f1a
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 0%

---

# Previsto [!DNL QuickBooks] dati

![](../../../assets/Quickbooks.png)

Dopo [hai connesso il tuo [!DNL QuickBooks] account](../../../data-analyst/importing-data/integrations/quickbooks.md), puoi utilizzare la [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) per tenere traccia facilmente dei campi dati rilevanti ai fini dell’analisi. Le tabelle seguenti verranno create nel Data Warehouse:

Per visualizzare tutti i campi disponibili per il tracciamento, fai clic sui collegamenti nella colonna del nome della tabella.

## Entità transazione {#transactionentities}

| **Nome tabella** | **Descrizione** |
|-----|-----|
| [`bill`](https://developer.intuit.com/docs/api/accounting/Bill) | La tabella delle fatture contiene informazioni sulle transazioni AP o su una richiesta di pagamento di terze parti. Gli attributi includono tipo di valuta, tasso di cambio, importo totale, data di scadenza, saldo e altro ancora. |
| [`billpayments`](https://developer.intuit.com/docs/api/accounting/BillPayment) | Le entità BillPayment sono la transazione finale di pagamento delle fatture ricevute da un fornitore. Questa tabella include le informazioni sul fornitore, il tipo di pagamento, l&#39;importo totale, la data della transazione e altro ancora. |
| [`creditmemos`](https://developer.intuit.com/docs/api/accounting/CreditMemo) | La tabella dei crediti registra le transazioni che sono rimborsi o crediti sia per i pagamenti completi che per quelli parziali. Alcuni attributi includono il nome del cliente, le informazioni di fatturazione e spedizione del cliente, l&#39;importo e la data. |
| [`deposits`](https://developer.intuit.com/docs/api/accounting/Deposit) | I depositi includono i depositi diretti e i pagamenti della clientela trasferiti nel Conto Attività dopo essere stati detenuti nel `Undeposited Funds` conto. Gli attributi includono l&#39;importo, l&#39;ID del deposito e la data. |
| [`estimates`](https://developer.intuit.com/docs/api/accounting/Estimate) | Le stime sono transazioni date ai clienti che includono prezzi proposti per un bene o un servizio. Questa tabella registra l&#39;importo, le informazioni sugli sconti, le informazioni sui clienti e la data. |
| [`invoices`](https://developer.intuit.com/docs/api/accounting/Invoice) | Le fatture sono moduli di vendita che un cliente paga successivamente. Nella tabella delle fatture vengono registrate le informazioni sui depositi, la data, le voci, le informazioni fiscali e le informazioni sui clienti. |
| [`journalentries`](https://developer.intuit.com/docs/api/accounting/JournalEntry) | Nella tabella delle scritture contabili vengono registrate le informazioni sui conti AR e AP, tra cui l&#39;ID della scrittura contabile, la data della transazione e le informazioni sull&#39;articolo della riga. |
| [`payments`](https://developer.intuit.com/docs/api/accounting/Payment) | Un record di pagamento include attributi quali ID pagamento, importi applicati e non applicati, data transazione, tipo di transazione e stato di elaborazione. |
| [`purchases`](https://developer.intuit.com/docs/api/accounting/Purchase) | La tabella degli acquisti rappresenta le tue spese e include l&#39;ID acquisto, il tipo di pagamento, l&#39;importo ed eventuali informazioni sull&#39;articolo della riga. |
| [`purchaseorders`](https://developer.intuit.com/docs/api/accounting/PurchaseOrder) | Gli ordini di acquisto sono richieste di beni inviati a fornitori. Questa tabella include le informazioni sul fornitore, l&#39;ID dell&#39;ordine di acquisto, la data della transazione, le informazioni sull&#39;articolo della riga, l&#39;importo totale e le informazioni sul conto AP. |
| [`refundreceipts`](https://developer.intuit.com/docs/api/accounting/RefundReceipt) | Questa tabella registra i rimborsi concessi ai clienti. Gli attributi includono l&#39;ID ricevuta di ritorno, le informazioni sull&#39;articolo della riga, l&#39;importo totale, le informazioni sui clienti e il saldo. |
| [`salesreceipts`](https://developer.intuit.com/docs/api/accounting/SalesReceipt) | Nella tabella ricezioni vendite vengono registrate le informazioni negli incassi delle vendite forniti ai clienti, tra cui l&#39;ID ricevuta di vendita, le informazioni sugli articoli della riga, l&#39;importo totale, le informazioni sui clienti, la data della transazione e gli eventuali depositi. |
| [`timeactivities`](https://developer.intuit.com/docs/api/accounting/TimeActivity) | Le attività temporali sono registrazioni temporali per fornitori e/o dipendenti. La tabella delle attività temporali include l&#39;ID attività ora, le informazioni relative a dipendente/fornitore, l&#39;ora registrata, la descrizione dell&#39;attività e la data registrata. |
| [`transfers`](https://developer.intuit.com/docs/api/accounting/Transfer) | La tabella dei trasferimenti registra le informazioni sui fondi spostati tra i conti. Gli attributi includono ID trasferimento, importo, informazioni sul conto e data. |
| [`vendorcredits`](https://developer.intuit.com/docs/api/accounting/VendorCredit) | I crediti fornitore sono transazioni AP che sono rimborsi o crediti concessi ai fornitori. La `vendorcredits` La tabella include l&#39;ID credito fornitore, le informazioni sull&#39;articolo riga, le informazioni sul fornitore, il conto AP, l&#39;importo totale e la data. |

{style=&quot;table-layout:auto&quot;}

## Entità elenco nomi {#namelistentities}

| **Nome tabella** | **Descrizione** |
|-----|-----|
| [`accounts`](https://developer.intuit.com/docs/api/accounting/Account) | Questa tabella include l&#39;ID del conto, il nome, lo stato, il tipo, il saldo, la valuta e il tempo di creazione. |
| [`budgets`](https://developer.intuit.com/docs/api/accounting/Budget) | Questa tabella registra tutte le informazioni relative ai budget aziendali, inclusi ID budget, nome, date di inizio e fine, tipo, stato e dettagli. |
| [`classes`](https://developer.intuit.com/docs/api/accounting/Class) | Le classi, applicate alle linee dettagliate delle transazioni, consentono di tenere traccia dei segmenti che non sono legati a un cliente o a un progetto. Questa tabella registra l’ID classe, il nome, la sottoclasse e lo stato. |
| [`customers`](https://developer.intuit.com/docs/api/accounting/Customer) | La tabella dei clienti contiene tutte le informazioni relative ai clienti, inclusi l’ID del cliente, il nome, gli indirizzi di fatturazione e spedizione, il numero di telefono e l’indirizzo e-mail. |
| [`departments`](https://developer.intuit.com/docs/api/accounting/Department) | La tabella dei reparti include l&#39;ID del reparto, il nome e il tipo (sottoreparto rispetto al reparto di livello superiore). |
| [`employees`](https://developer.intuit.com/docs/api/accounting/Employee) | La tabella dei dipendenti registra informazioni sulle persone che lavorano per la tua azienda. Gli attributi includono l&#39;ID dipendente, il nome, l&#39;indirizzo, il numero di telefono e le informazioni fatturabili, se l&#39;azienda è abilitata per il ciclo paghe. |
| [`items`](https://developer.intuit.com/docs/api/accounting/Item) | La tabella degli articoli contiene dettagli sui prodotti o servizi venduti dalla tua azienda. Questa tabella include l&#39;ID articolo, il nome, la descrizione, il prezzo unitario, il tipo, le informazioni di acquisto, la quantità esistente e le informazioni sul conto profitti e attività. |
| [`paymentmethods`](https://developer.intuit.com/docs/api/accounting/PaymentMethod) | La tabella dei metodi di pagamento registra il metodo di pagamento ricevuto per beni e servizi. Contiene l’ID, il tipo e il nome del pagamento. |
| [`taxagencies`](https://developer.intuit.com/docs/api/accounting/TaxAgency) | Questa tabella registra informazioni sulle agenzie fiscali, incluso l&#39;ID dell&#39;agenzia fiscale, e tiene traccia delle informazioni sulle imposte per acquisti e vendite. |
| [`taxcodes`](https://developer.intuit.com/docs/api/accounting/TaxCode) | I codici imposta vengono utilizzati per tenere traccia dello stato fiscale (imponibile e non imponibile) di prodotti, servizi e clienti. La tabella dei codici fiscali include l&#39;ID del codice fiscale, il nome, la descrizione, lo stato, lo stato imponibile, l&#39;aliquota fiscale e il gruppo di imposte. |
| [`taxrates`](https://developer.intuit.com/docs/api/accounting/TaxRate) | Le aliquote fiscali sono utilizzate per calcolare le passività fiscali. Questa tabella include l&#39;ID dell&#39;aliquota fiscale, il nome, la descrizione, l&#39;aliquota, l&#39;agenzia fiscale e altro ancora. |
| [`terms`](https://developer.intuit.com/docs/api/accounting/Term) | Questa entità rappresenta i termini in base ai quali vengono effettuate le vendite. La tabella dei termini include il termine ID, nome, tipo, percentuale di sconto e giorni di scadenza. |
| [`vendors`](https://developer.intuit.com/docs/api/accounting/Vendor) | La tabella dei fornitori contiene informazioni sui fornitori da cui acquisti. Gli attributi della tabella includono l’ID fornitore, il nome società, il numero di conto, il saldo del conto, lo stato 1099, l’indirizzo di fatturazione, il numero di telefono, l’indirizzo e-mail e l’indirizzo Web. |

{style=&quot;table-layout:auto&quot;}

## Correlati:

* [Collegamento [!DNL QuickBooks]](../integrations/quickbooks.md)
* [Riautenticazione delle integrazioni](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations)
