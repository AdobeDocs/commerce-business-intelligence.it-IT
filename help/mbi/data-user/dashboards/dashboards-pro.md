---
title: Dashboard preconfigurati
description: Scopri le dashboard pronte all’uso per fornire informazioni approfondite sulla tua attività.
exl-id: fe61c92e-de87-4317-96d7-01d2a9846bf9
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1950'
ht-degree: 0%

---

# Dashboard preconfigurati

[!DNL Adobe Commerce Intelligence] include dashboard predefiniti per fornire informazioni approfondite sulla tua attività. Con le dashboard, puoi verificare lo stato di metriche essenziali come i ricavi dal ciclo di vita dell’utente, il numero di acquisti ripetuti, i prodotti migliori acquistati in un determinato periodo di tempo e altro ancora. Queste dashboard preconfigurate sono state create per aiutarti a prendere decisioni aziendali informate.

>[!NOTE]
>
>L’accesso a queste dashboard dipende dal tipo di account e dal livello di accesso. Se queste dashboard non vengono visualizzate, contatta il [supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=it).

## Disponibilità del rapporto

Per i dashboard `Customers` e `Executive Summary`, alcuni report sono disponibili solo a seconda della configurazione di estrazione dell&#39;archivio. In particolare, se lo store consente il pagamento come ospite o non consente il pagamento come ospite.

## Clienti (è consentita l’estrazione come ospite)

La dashboard Clienti (pagamento guest consentito) fornisce informazioni sulla base dei clienti, ad esempio il loro comportamento d’acquisto. Questa dashboard può aiutarti a migliorare la fidelizzazione dei clienti e a individuare i clienti che generano i ricavi più elevati.

### Rapporti

| Nome | Descrizione |
|---|---|
| `Orders by New Customers (Past 30 Days)` | Ordini negli ultimi 30 giorni da clienti che non hanno mai effettuato un ordine in precedenza. |
| `Orders by Existing Customers (Past 30 Days)` | Ordini negli ultimi 30 giorni da clienti che hanno effettuato in precedenza almeno un ordine. |
| `Total Unique Customers (Past 30 Days)` | Numero di clienti univoci che hanno effettuato ordini negli ultimi 30 giorni. |
| `Orders by New vs Existing Customers` | Numero di ordini per clienti senza ordini precedenti rispetto ai clienti con almeno un ordine precedente. |
| `Subsequent Order Probability (All Time)` | La probabilità che i clienti che hanno effettuato un ordine ne effettuino un altro. |
| `% of Customers with Multiple Orders (All Time)` | Percentuale di tutti i clienti che hanno effettuato più ordini. |
| `Median Time Between Orders (All Time)` | Periodo di tempo medio che ogni cliente impiega tra il momento dell&#39;ordine e quello successivo. |
| `Subsequent Order Probability` | La probabilità che i clienti che hanno effettuato un ordine effettuino un altro ordine, suddiviso per numero dell’ordine. Ossia, la percentuale di clienti con un ordine che piazzano un secondo, la percentuale di clienti con due che piazzano un terzo, e così via. |
| `Time Between Orders` | Il tempo medio e mediano che i clienti prendono tra gli ordini, suddiviso per numero di ordine (ovvero il tempo tra gli ordini uno e due, due e tre e così via). |
| `Number of Customers - Lifetime Orders` | Per un determinato numero di ordini effettuati nel ciclo di vita di un cliente, il numero di clienti che hanno effettuato tali ordini e la percentuale dell&#39;intera base clienti che tale numero rappresenta. |
| `One-Time Customers who Bought 3-6 Months Ago` | Clienti che hanno effettuato il primo e unico acquisto tra tre e sei mesi fa. |
| `Avg LTV by First Order` | Confronta la media cumulativa dei ricavi relativi al ciclo di vita del cliente per coorti. Le coorti sono definite dal mese in cui un cliente ha effettuato per la prima volta un acquisto. Ad esempio, una coorte `Jan 2020` mostra il valore LTV medio cumulativo per i clienti il cui primo acquisto è stato nel gennaio 2020. |
| `Customer's First 30 Day vs Lifetime Revenue` | Confronto dei ricavi medi dei clienti nei 30 giorni successivi al primo acquisto rispetto all’intero ciclo di vita. Ogni bolla corrisponde a un’area di spedizione e la dimensione di ogni bolla rappresenta il numero di clienti acquisiti da tale area. |

## Clienti (non è consentito effettuare il pagamento come ospite)

Il dashboard Clienti (non è consentito effettuare il pagamento come ospite) fornisce informazioni sulla base dei clienti, ad esempio il comportamento di acquisto e le conversioni dalle registrazioni account ai posizionamenti degli ordini. Questa dashboard può aiutarti a migliorare la fidelizzazione dei clienti e a individuare i clienti che generano i ricavi più elevati.

### Rapporti

| Nome | Descrizione |
|---|---|
| `Account Registration (Past 30 Days)` | Il numero di persone che si sono registrate per un account con il tuo negozio negli ultimi 30 giorni. |
| `Accounts Registered (Past 30 Days) with 1 or More Orders` | Il numero di persone che si sono registrate per un account con il tuo Negozio negli ultimi 30 giorni e che hanno effettuato almeno un ordine. |
| `% Conversion from Registration to First Order (Past 30 Days)` | Percentuale di account registrati negli ultimi 30 giorni che hanno effettuato un ordine. |
| `% Conversion from Registration to First Order` | Percentuale di account registrati che hanno effettuato un ordine, per mese di registrazione. |
| `Orders by New vs Existing Customers` | Numero di ordini per clienti senza ordini precedenti rispetto ai clienti con almeno un ordine precedente. |
| `Subsequent Order Probability (All Time)` | La probabilità che i clienti che hanno effettuato un ordine ne effettuino un altro. |
| `% of Customers with Multiple Orders (All Time)` | Percentuale di tutti i clienti che hanno effettuato più ordini. |
| `Median Time Between Orders (All Time)` | Periodo di tempo medio che ogni cliente impiega tra il momento dell&#39;ordine e quello successivo. |
| `Subsequent Order Probability` | La probabilità che i clienti che hanno effettuato un ordine ne effettuino un altro, suddiviso per numero di ordine. Ossia, la percentuale di clienti con un ordine che piazzano un secondo, la percentuale di clienti con due che piazzano un terzo, e così via. |
| `Time Between Orders` | Il tempo medio e mediano che i clienti prendono tra gli ordini, suddiviso per numero di ordine (ovvero il tempo tra gli ordini uno e due, due e tre e così via). |
| `Number of Customers - Lifetime Orders` | Per un determinato numero di ordini effettuati nel ciclo di vita di un cliente, il numero di clienti che hanno effettuato tali ordini e la percentuale dell&#39;intera base clienti che tale numero rappresenta. |
| `One-Time Customers who Bought 3-6 Months Ago` | Clienti che hanno effettuato il primo e unico acquisto tra tre e sei mesi fa. |
| `Avg LTV by First Order` | Confronta la media cumulativa dei ricavi relativi al ciclo di vita del cliente per coorti. Le coorti sono definite dal mese in cui un cliente ha effettuato per la prima volta un acquisto. Ad esempio, una coorte di gennaio 2020 mostra l’LTV medio cumulativo per i clienti il cui primo acquisto è stato nel gennaio 2020. |
| `Customer's First 30 Day vs Lifetime Revenue` | Confronto dei ricavi medi dei clienti nei 30 giorni successivi al primo acquisto rispetto all’intero ciclo di vita. Ogni bolla corrisponde a un’area di spedizione e la dimensione di ogni bolla rappresenta il numero di clienti acquisiti da tale area. |

## Riepilogo esecutivo (pagamento ospite consentito)

La dashboard Riepilogo esecutivo (pagamento ospite consentito) offre un quadro sintetico delle attività aziendali in termini di ordini e ricavi. Questa dashboard è progettata per consentire ai dirigenti di ottenere una comprensione complessiva delle prestazioni aziendali, ma può essere utile anche per gli altri utenti.

### Rapporti

| Nome | Descrizione |
|---|---|
| `Revenue (Current Month)` | Il ricavo generato dal tuo Negozio per il mese corrente. In questo caso, i ricavi sono definiti come il prezzo finale pagato da un cliente su un ordine. |
| `Revenue (Past 6 Months by Day)` | Ricavi giornalieri totali, sovrapposti ai ricavi giornalieri medi dei sette giorni precedenti. In questo caso, i ricavi sono definiti come il prezzo finale pagato da un cliente su un ordine. |
| `% Change in Revenue (MoM MTD)` | Confronto delle entrate nel mese corrente (finora) rispetto alla stessa porzione del mese precedente. |
| `Revenue from New vs Existing Customers (Current Month)` | Ricavi per il mese corrente (finora) attribuiti ai nuovi clienti (prima volta) rispetto ai clienti esistenti (secondo o successivo ordine). |
| `Average Order Value (Current Month)` | Valore medio giornaliero degli ordini effettuati nel mese corrente (finora). Il valore dell&#39;ordine è definito come il prezzo finale pagato da un cliente su un ordine. |
| `Orders (Current Month)` | Il numero di ordini effettuati nel tuo negozio per il mese corrente (finora). |
| `% Change in Orders (MoM MTD)` | Confronto tra il numero di ordini del mese corrente (finora) e la stessa porzione del mese precedente. |
| `Orders by New Customers (Current Month)` | Ordini per il mese corrente da clienti che non hanno mai effettuato un ordine in precedenza. |
| `Orders by Existing Customers (Current Month)` | Ordini per il mese corrente da clienti che hanno precedentemente effettuato almeno un ordine. |
| `Orders by New vs Existing Customers (Current Year by Week)` | Numero di ordini per clienti senza ordini precedenti rispetto a clienti con almeno un ordine precedente, per ogni settimana dell&#39;anno corrente (finora). |

## Riepilogo esecutivo (non è consentito il pagamento come ospite)

La dashboard Riepilogo esecutivo (non è consentito il pagamento degli ospiti) offre un quadro sintetico delle attività aziendali in termini di ordini, entrate e registrazioni di account. Questa dashboard è progettata per consentire ai dirigenti di ottenere una comprensione complessiva delle prestazioni aziendali, ma può essere utile anche per gli altri utenti.

### Rapporti

| Nome | Descrizione |
|---|---|
| `Revenue (Current Month)` | I ricavi generati dal tuo store questo mese. In questo caso, i ricavi sono definiti come il prezzo finale pagato da un cliente su un ordine. |
| `Revenue (Past 6 Months by Day)` | Ricavi giornalieri totali, sovrapposti ai ricavi giornalieri medi dei sette giorni precedenti. In questo caso, i ricavi sono definiti come il prezzo finale pagato da un cliente su un ordine. |
| `% Change in Revenue (MoM MTD)` | Confronto delle entrate registrate finora nel mese corrente rispetto alla stessa porzione del mese precedente. |
| `Revenue from New vs Existing Customers (Current Month)` | Ricavi per il mese corrente (finora) attribuiti ai nuovi clienti (prima volta) rispetto ai clienti esistenti (secondo o successivo ordine). |
| `Average Order Value (Current Month)` | Valore medio giornaliero degli ordini effettuati nel mese corrente (finora). Il valore dell&#39;ordine è definito come il prezzo finale pagato da un cliente su un ordine. |
| `Orders (Current Month)` | Il numero di ordini effettuati nel tuo negozio per il mese corrente (finora). |
| `% Change in Orders (MoM MTD)` | Confronto tra il numero di ordini del mese corrente (finora) e la stessa porzione del mese precedente. |
| `Account Registrations (Current Month)` | Il numero di nuovi account registrati finora questo mese. |
| `% Conversion from Registration to First Order (Current Month)` | Percentuale di account registrati fino a questo mese che hanno effettuato un ordine. |
| `% Conversion from Registration to First Order (Current Year by Week)` | Percentuale di account registrati ogni settimana che hanno effettuato un ordine. |

## Ordini

Il pannello di controllo Ordini fornisce informazioni sul volume transazionale degli ordini, il loro stato, i codici coupon utilizzati, i ricavi generati e i metodi di pagamento utilizzati. Ad esempio, puoi tenere traccia del processo di evasione e verificare che non vi siano problemi o colli di bottiglia.

>[!NOTE]
>
>I rapporti in questo dashboard sono disponibili per gli account connessi a store con entrambi i tipi di configurazione (pagamento guest, nessun pagamento guest).

### Rapporti

| Nome | Descrizione |
|---|---|
| `Orders (Past 30 Days)` | Il numero di ordini effettuati presso il tuo negozio negli ultimi 30 giorni. |
| `Revenue (Past 30 Days)` | Il ricavo generato dal tuo Negozio negli ultimi 30 giorni. I ricavi sono definiti come il prezzo finale pagato da un cliente su un ordine. |
| `Average Order Value (Past 30 Days)` | Valore medio degli ordini effettuati negli ultimi 30 giorni. Il valore dell&#39;ordine è definito come il prezzo finale pagato da un cliente su un ordine. |
| `Orders` | Il numero di ordini effettuati nel tuo negozio ogni mese. |
| `Revenue by Payment Method` | I ricavi generati dal tuo negozio, suddivisi per metodo di pagamento. I ricavi sono definiti come il prezzo finale pagato da un cliente su un ordine. |
| `AOV by New vs Existing Customers` | Valore medio mensile degli ordini effettuati nel negozio, suddiviso tra gli ordini dei clienti che non hanno effettuato ordini precedenti e quelli che hanno effettuato almeno un ordine precedente. Il valore dell&#39;ordine è definito come il prezzo finale pagato da un cliente su un ordine. |
| `% Orders by Status (Past 30 Days)` | Percentuale di ordini di ogni giorno negli ultimi 30 giorni attualmente in ogni stato dell&#39;ordine. |
| `Incomplete Orders (Created more than 1 Day Ago)` | Un elenco di tutti gli ordini effettuati più di un giorno fa che sono ancora in uno stato incompleto (non annullati o completati). |
| `Orders Per Hour (Past 7 Days)` | Ordina volume per giorno e ora. |
| `Revenue Details (Past 30 Days)` | La scomposizione giornaliera dei ricavi per gli ultimi 30 giorni in tutte le componenti del valore totale dei ricavi. |
| `Order Details by Coupon Code (Past 30 Days)` | Per ogni codice coupon offerto dal tuo negozio, dettagli su come è stato utilizzato quel codice coupon e cosa restituisce portato in durante gli ultimi 30 giorni. |
| `% Orders with Coupon (Past 30 Days)` | Percentuale di ordini effettuati negli ultimi 30 giorni che hanno utilizzato una cedola rispetto a quelli non utilizzati. |

## Prodotti

Il dashboard Prodotti mostra le prestazioni generali del prodotto in termini di prodotti ordinati, valore lordo delle merci (GMV, Gross Merchandise Value) e principali prodotti acquistati e rimborsati. Può aiutarti a bilanciare acquisti e restituzioni e a determinare il successo e la popolarità del prodotto. L&#39;archivio deve essere [configurato per tenere traccia dei rimborsi](https://experienceleague.adobe.com/docs/commerce-admin/customers/customer-accounts/store-credit/credit-configure.html?lang=it) per i grafici da compilare.

>[!NOTE]
>
>I rapporti in questo dashboard sono disponibili per gli account connessi a store con entrambi i tipi di configurazione (pagamento guest, nessun pagamento guest).

### Rapporti

| Nome | Descrizione |
|---|---|
| `GMV (Past 30 Days)` | Il valore lordo delle merci di tutti i prodotti venduti negli ultimi 30 giorni. GMV è definito come la quantità ordinata moltiplicata per il prezzo di base di ciascun prodotto. |
| `% GMV (Past 30 Days) Refunded` | Percentuale di GMV per i prodotti acquistati negli ultimi 30 giorni che hanno comportato un rimborso. |
| `Product Quantity Ordered (Past 30 Days)` | Quantità totale di articoli ordinati negli ultimi 30 giorni. |
| `% Purchased Products (Past 30 Days) Refunded` | Percentuale di articoli acquistati negli ultimi 30 giorni che hanno comportato un rimborso. |
| `Gross Merchandise Value` | Il valore lordo della merce di tutti i prodotti venduti, per mese. GMV è definito come la quantità ordinata moltiplicata per il prezzo di base di ciascun prodotto. |
| `Purchases vs Refund Rate per Product (Past 30 Days)` | Per ciascun prodotto, confronto tra il numero totale di ordinazioni effettuate negli ultimi 30 giorni e il tasso di rimborso del prodotto. La dimensione di ogni bolla rappresenta il tasso di rimborso. |
| `Product Performance Details (Past 30 Days)` | Informazioni dettagliate sulle vendite e sui successivi rimborsi negli ultimi 30 giorni, per SKU prodotto e nome del prodotto. |
| `Top Purchased Products by GMV (Past 30 Days)` | Prodotti venduti negli ultimi 30 giorni che hanno generato il maggior fatturato (primi 10). |
| `Top Refunded Products by GMV (Past 30 Days)` | Prodotti acquistati negli ultimi 30 giorni che hanno determinato la perdita di GMV maggiore a causa di rimborsi (top 10). |
| `Top Purchased Products by Quantity (Past 30 Days)` | I prodotti venduti negli ultimi 30 giorni sono stati i più venduti (primi 10). |
| `Top Refunded Products by Quantity (Past 30 Days)` | Prodotti acquistati negli ultimi 30 giorni che hanno dato luogo alla maggiore quantità rimborsata (primi 10). |
