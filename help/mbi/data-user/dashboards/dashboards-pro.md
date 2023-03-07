---
title: Dashboard preconfigurati
description: Scopri le dashboard pronte all’uso per fornire informazioni approfondite sulla tua attività.
exl-id: fe61c92e-de87-4317-96d7-01d2a9846bf9
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '2240'
ht-degree: 0%

---

# Dashboard preconfigurati

[!DNL MBI] include dashboard pronte all’uso per fornire informazioni approfondite sulla tua attività. Con le dashboard, puoi verificare lo stato di metriche essenziali come i ricavi dal ciclo di vita dell’utente, il numero di acquisti ripetuti, i prodotti migliori acquistati in un determinato periodo di tempo e altro ancora. Queste dashboard preconfigurate sono state create per aiutarti a prendere decisioni aziendali informate.

>[!NOTE]
>
>L’accesso a queste dashboard dipende dal tipo di account e dal livello di accesso. Se non trovi queste dashboard, contatta [supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

## Disponibilità del rapporto

Per `Customers` e `Executive Summary` dashboard, alcuni rapporti sono disponibili solo a seconda della configurazione di estrazione del tuo archivio. In particolare, se lo store consente il pagamento come ospite o non consente il pagamento come ospite.

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
| `Subsequent Order Probability` | La probabilità che i clienti che hanno effettuato un ordine effettuino un altro ordine, suddiviso per numero dell’ordine. Ossia la percentuale di clienti con un ordine che effettuano un secondo, la percentuale di clienti con due ordini che ne effettuano un terzo e così via). |
| `Time Between Orders` | Il tempo medio e mediano che i clienti prendono tra gli ordini, suddiviso per numero di ordine (ovvero il tempo tra gli ordini uno e due, due e tre e così via). |
| `Number of Customers - Lifetime Orders` | Per un determinato numero di ordini effettuati nel ciclo di vita di un cliente, il numero di clienti che hanno effettuato tali ordini e la percentuale dell&#39;intera base clienti che tale numero rappresenta. |
| `One-Time Customers who Bought 3-6 Months Ago` | Clienti che hanno effettuato il primo e unico acquisto tra tre e sei mesi fa. |
| `Avg LTV by First Order` | Confronta la media cumulativa dei ricavi relativi al ciclo di vita del cliente per coorti. Le coorti sono definite dal mese in cui un cliente ha effettuato per la prima volta un acquisto. Ad esempio, un `Jan 2020` La coorte mostra l’LTV medio cumulativo per i clienti il cui primo acquisto è stato nel gennaio 2020. |
| `Customer's First 30 Day vs Lifetime Revenue` | Confronto dei ricavi medi dei clienti nei 30 giorni successivi al primo acquisto rispetto all’intero ciclo di vita. Ogni bolla corrisponde a un’area di spedizione e la dimensione di ogni bolla rappresenta il numero di clienti acquisiti da tale area. |

## Clienti (non è consentito effettuare il pagamento come ospite)

Il dashboard Clienti (non è consentito effettuare il pagamento come ospite) fornisce informazioni sulla base dei clienti, ad esempio il comportamento di acquisto e le conversioni dalle registrazioni account ai posizionamenti degli ordini. Questa dashboard può aiutarti a migliorare la fidelizzazione dei clienti e a individuare i clienti che generano i ricavi più elevati.

### Rapporti

| Nome | Descrizione |
|---|---|
| Registrazione account (ultimi 30 giorni) | Il numero di persone che si sono registrate per un account con il tuo negozio negli ultimi 30 giorni. |
| Account registrati (ultimi 30 giorni) con 1 o più ordini | Il numero di persone che si sono registrate per un account con il tuo Negozio negli ultimi 30 giorni e che hanno effettuato almeno un ordine. |
| % di conversione dalla registrazione al primo ordine (ultimi 30 giorni) | Percentuale di account registrati negli ultimi 30 giorni che hanno effettuato un ordine. |
| % di conversione dalla registrazione al primo ordine | Percentuale di account registrati che hanno effettuato un ordine, per mese di registrazione. |
| Ordini per clienti nuovi e clienti esistenti | Numero di ordini per clienti senza ordini precedenti rispetto ai clienti con almeno un ordine precedente. |
| Probabilità ordine successivo (tutti i tempi) | La probabilità che i clienti che hanno effettuato un ordine ne effettuino un altro. |
| % di clienti con più ordini (tutti i tempi) | Percentuale di tutti i clienti che hanno effettuato più ordini. |
| Tempo mediano tra ordini (tutti i tempi) | Periodo di tempo medio che ogni cliente impiega tra il momento dell&#39;ordine e quello successivo. |
| Probabilità ordine successivo | La probabilità che i clienti che hanno effettuato un ordine ne effettuino un altro, suddiviso per numero di ordine. Ossia, la percentuale di clienti con un ordine che piazzano un secondo, la percentuale di clienti con due che piazzano un terzo, e così via. |
| Tempo tra gli ordini | Il tempo medio e mediano che i clienti prendono tra gli ordini, suddiviso per numero di ordine (ovvero il tempo tra gli ordini uno e due, due e tre e così via). |
| Numero di clienti - Ordini a vita | Per un determinato numero di ordini effettuati nel ciclo di vita di un cliente, il numero di clienti che hanno effettuato tali ordini e la percentuale dell&#39;intera base clienti che tale numero rappresenta. |
| Clienti occasionali che hanno acquistato 3-6 mesi fa | Clienti che hanno effettuato il primo e unico acquisto tra tre e sei mesi fa. |
| Media LTV per primo ordine | Confronta la media cumulativa dei ricavi relativi al ciclo di vita del cliente per coorti. Le coorti sono definite dal mese in cui un cliente ha effettuato per la prima volta un acquisto. Ad esempio, una coorte di gennaio 2020 mostra l’LTV medio cumulativo per i clienti il cui primo acquisto è stato nel gennaio 2020. |
| Primi 30 giorni del cliente rispetto al fatturato del ciclo di vita | Confronto dei ricavi medi dei clienti nei 30 giorni successivi al primo acquisto rispetto all’intero ciclo di vita. Ogni bolla corrisponde a un’area di spedizione e la dimensione di ogni bolla rappresenta il numero di clienti acquisiti da tale area. |

## Riepilogo esecutivo (pagamento ospite consentito)

La dashboard Riepilogo esecutivo (pagamento ospite consentito) offre un quadro sintetico delle attività aziendali in termini di ordini e ricavi. Questa dashboard è progettata per consentire ai dirigenti di ottenere una comprensione complessiva delle prestazioni aziendali, ma può essere utile anche per gli altri utenti.

### Rapporti

| Nome | Descrizione |
|---|---|
| Ricavi (mese corrente) | Il ricavo generato dal tuo Negozio per il mese corrente. In questo caso, i ricavi sono definiti come il prezzo finale pagato da un cliente su un ordine. |
| Ricavi (ultimi 6 mesi per giorno) | Ricavi giornalieri totali, sovrapposti ai ricavi giornalieri medi dei sette giorni precedenti. In questo caso, i ricavi sono definiti come il prezzo finale pagato da un cliente su un ordine. |
| % variazione ricavi (MoM MTD) | Confronto delle entrate nel mese corrente (finora) rispetto alla stessa porzione del mese precedente. |
| Ricavi da clienti nuovi rispetto a clienti esistenti (mese corrente) | Ricavi per il mese corrente (finora) attribuiti ai nuovi clienti (prima volta) rispetto ai clienti esistenti (secondo o successivo ordine). |
| Valore medio ordine (mese corrente) | Valore medio giornaliero degli ordini effettuati nel mese corrente (finora). Il valore dell&#39;ordine è definito come il prezzo finale pagato da un cliente su un ordine. |
| Ordini (mese corrente) | Il numero di ordini effettuati nel tuo negozio per il mese corrente (finora). |
| % modifica ordini (MoM MTD) | Confronto tra il numero di ordini del mese corrente (finora) e la stessa porzione del mese precedente. |
| Ordini per nuovi clienti (mese corrente) | Ordini per il mese corrente da clienti che non hanno mai effettuato un ordine in precedenza. |
| Ordini per clienti esistenti (mese corrente) | Ordini per il mese corrente da clienti che hanno precedentemente effettuato almeno un ordine. |
| Ordini per clienti nuovi e clienti esistenti (anno corrente per settimana) | Numero di ordini per clienti senza ordini precedenti rispetto a clienti con almeno un ordine precedente, per ogni settimana dell&#39;anno corrente (finora). |

## Riepilogo esecutivo (non è consentito il pagamento come ospite)

La dashboard Riepilogo esecutivo (non è consentito il pagamento degli ospiti) offre un quadro sintetico delle attività aziendali in termini di ordini, entrate e registrazioni di account. Questa dashboard è progettata per consentire ai dirigenti di ottenere una comprensione complessiva delle prestazioni aziendali, ma può essere utile anche per gli altri utenti.

### Rapporti

| Nome | Descrizione |
|---|---|
| Ricavi (mese corrente) | I ricavi generati dal tuo store questo mese. In questo caso, i ricavi sono definiti come il prezzo finale pagato da un cliente su un ordine. |
| Ricavi (ultimi 6 mesi per giorno) | Ricavi giornalieri totali, sovrapposti ai ricavi giornalieri medi dei sette giorni precedenti. In questo caso, i ricavi sono definiti come il prezzo finale pagato da un cliente su un ordine. |
| % variazione ricavi (MoM MTD) | Confronto delle entrate registrate finora nel mese corrente rispetto alla stessa porzione del mese precedente. |
| Ricavi da clienti nuovi rispetto a clienti esistenti (mese corrente) | Ricavi per il mese corrente (finora) attribuiti ai nuovi clienti (prima volta) rispetto ai clienti esistenti (secondo o successivo ordine). |
| Valore medio ordine (mese corrente) | Valore medio giornaliero degli ordini effettuati nel mese corrente (finora). Il valore dell&#39;ordine è definito come il prezzo finale pagato da un cliente su un ordine. |
| Ordini (mese corrente) | Il numero di ordini effettuati nel tuo negozio per il mese corrente (finora). |
| % modifica ordini (MoM MTD) | Confronto tra il numero di ordini del mese corrente (finora) e la stessa porzione del mese precedente. |
| Registrazioni conti (mese corrente) | Il numero di nuovi account registrati finora questo mese. |
| % di conversione dalla registrazione al primo ordine (mese corrente) | Percentuale di account registrati fino a questo mese che hanno effettuato un ordine. |
| % di conversione dalla registrazione al primo ordine (anno corrente per settimana) | Percentuale di account registrati ogni settimana che hanno effettuato un ordine. |

## Ordini

Il pannello di controllo Ordini fornisce informazioni sul volume transazionale degli ordini, il loro stato, i codici coupon utilizzati, i ricavi generati e i metodi di pagamento utilizzati. Ad esempio, puoi tenere traccia del processo di evasione e verificare che non vi siano problemi o colli di bottiglia.

>[!NOTE]
>
>I rapporti in questo dashboard sono disponibili per gli account connessi a store con entrambi i tipi di configurazione (pagamento guest, nessun pagamento guest).

### Rapporti

| Nome | Descrizione |
|---|---|
| Ordini (ultimi 30 giorni) | Il numero di ordini effettuati presso il tuo negozio negli ultimi 30 giorni. |
| Ricavi (ultimi 30 giorni) | Il ricavo generato dal tuo Negozio negli ultimi 30 giorni. I ricavi sono definiti come il prezzo finale pagato da un cliente su un ordine. |
| Valore medio ordine (ultimi 30 giorni) | Valore medio degli ordini effettuati negli ultimi 30 giorni. Il valore dell&#39;ordine è definito come il prezzo finale pagato da un cliente su un ordine. |
| Ordini | Il numero di ordini effettuati nel tuo negozio ogni mese. |
| Ricavi per metodo di pagamento | I ricavi generati dal tuo negozio, suddivisi per metodo di pagamento. I ricavi sono definiti come il prezzo finale pagato da un cliente su un ordine. |
| Valutazione positiva per clienti nuovi e clienti esistenti | Valore medio mensile degli ordini effettuati nel negozio, suddiviso tra gli ordini dei clienti che non hanno effettuato ordini precedenti e quelli che hanno effettuato almeno un ordine precedente. Il valore dell&#39;ordine è definito come il prezzo finale pagato da un cliente su un ordine. |
| % ordini per stato (ultimi 30 giorni) | Percentuale di ordini di ogni giorno negli ultimi 30 giorni attualmente in ogni stato dell&#39;ordine. |
| Ordini incompleti (creati più di 1 giorno fa) | Un elenco di tutti gli ordini effettuati più di un giorno fa che sono ancora in uno stato incompleto (non annullati o completati). |
| Ordini all&#39;ora (ultimi 7 giorni) | Ordina volume per giorno e ora. |
| Dettagli ricavi (ultimi 30 giorni) | La scomposizione giornaliera dei ricavi per gli ultimi 30 giorni in tutte le componenti del valore totale dei ricavi. |
| Dettagli ordine per codice coupon (ultimi 30 giorni) | Per ogni codice coupon offerto dal tuo negozio, dettagli su come è stato utilizzato quel codice coupon e cosa restituisce portato in durante gli ultimi 30 giorni. |
| % ordini con coupon (ultimi 30 giorni) | Percentuale di ordini effettuati negli ultimi 30 giorni che hanno utilizzato una cedola rispetto a quelli non utilizzati. |

## Prodotti

Il dashboard Prodotti mostra le prestazioni generali del prodotto in termini di prodotti ordinati, valore lordo delle merci (GMV, Gross Merchandise Value) e principali prodotti acquistati e rimborsati. Può aiutarti a bilanciare acquisti e restituzioni e a determinare il successo e la popolarità del prodotto. Il punto vendita deve essere [configurato per tenere traccia dei rimborsi](https://experienceleague.adobe.com/docs/commerce-admin/customers/customer-accounts/store-credit/credit-configure.html) per compilare tali grafici.

>[!NOTE]
>
>I rapporti in questo dashboard sono disponibili per gli account connessi a store con entrambi i tipi di configurazione (pagamento guest, nessun pagamento guest).

### Rapporti

| Nome | Descrizione |
|---|---|
| GMV (ultimi 30 giorni) | Il valore lordo delle merci di tutti i prodotti venduti negli ultimi 30 giorni. GMV è definito come la quantità ordinata moltiplicata per il prezzo di base di ciascun prodotto. |
| % GMV (ultimi 30 giorni) rimborsato | Percentuale di GMV per i prodotti acquistati negli ultimi 30 giorni che hanno comportato un rimborso. |
| Quantità prodotto ordinata (ultimi 30 giorni) | Quantità totale di articoli ordinati negli ultimi 30 giorni. |
| % prodotti acquistati (ultimi 30 giorni) rimborsati | Percentuale di articoli acquistati negli ultimi 30 giorni che hanno comportato un rimborso. |
| Valore lordo merce | Il valore lordo della merce di tutti i prodotti venduti, per mese. GMV è definito come la quantità ordinata moltiplicata per il prezzo di base di ciascun prodotto. |
| Acquisti e tasso di rimborso per prodotto (ultimi 30 giorni) | Per ciascun prodotto, confronto tra il numero totale di ordinazioni effettuate negli ultimi 30 giorni e il tasso di rimborso del prodotto. La dimensione di ogni bolla rappresenta il tasso di rimborso. |
| Dettagli sulle prestazioni del prodotto (ultimi 30 giorni) | Informazioni dettagliate sulle vendite e sui successivi rimborsi negli ultimi 30 giorni, per SKU prodotto e nome del prodotto. |
| Principali prodotti acquistati da GMV (ultimi 30 giorni) | Prodotti venduti negli ultimi 30 giorni che hanno generato il maggior fatturato (primi 10). |
| Principali prodotti rimborsati da GMV (ultimi 30 giorni) | Prodotti acquistati negli ultimi 30 giorni che hanno determinato la perdita di GMV maggiore a causa di rimborsi (top 10). |
| Primi prodotti acquistati per quantità (ultimi 30 giorni) | I prodotti venduti negli ultimi 30 giorni sono stati i più venduti (primi 10). |
| Primi prodotti rimborsati per quantità (ultimi 30 giorni) | Prodotti acquistati negli ultimi 30 giorni che hanno dato luogo alla maggiore quantità rimborsata (primi 10). |
