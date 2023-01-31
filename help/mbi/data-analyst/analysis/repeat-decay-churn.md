---
title: Analisi del decadimento e abbandono della probabilità di ripetizione
description: Scopri e capisci come intercorre il tempo tra gli ordini e quando ci si aspetta che i clienti procedano a un abbandono.
exl-id: ea26052d-ac74-43b7-a4a6-977800d4c719
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 0%

---

# Ripeti decadimento probabilità e abbandono

Se una parte dei ricavi proviene da acquisti ripetuti, probabilmente sei consapevole dell&#39;enorme valore di una base di clienti fedele. A tal fine, è fondamentale comprendere come intercorre il tempo tra gli ordini e quando ci si aspetta che i clienti procedano a un abbandono.

Questo argomento esplora le analisi che possono essere utili per rispondere alle seguenti domande:

* Qual è la probabilità che un cliente effettui un altro acquisto?
* In che modo la probabilità dell&#39;ordine di ripetizione varia in base al tempo dall&#39;acquisto più recente del cliente?
* Quando si deve considerare che un cliente deve essere eseguito? E quindi, quando dovrebbe iniziare una campagna di riattivazione?

## Metriche consigliate

Quando analizzi la probabilità di decadimento e abbandono ripetuti, considera l’utilizzo di ([o edificio](../../data-user/reports/ess-manage-data-metrics.md)) queste metriche:

### Probabilità dell&#39;ordine di ripetizione iniziale

Questa misura è definita come il numero totale di ordini ripetuti, in percentuale degli ordini totali. In un altro modo, questa è la probabilità che un ordine sia seguito da un altro ordine. Quando questa probabilità è superiore al 50%, implica che più della metà di tutti gli ordini sono seguiti da un ordine successivo.

### Probabilità dell&#39;ordine di ripetizione in base a mesi dall&#39;ordine

Questa misura dimostra la probabilità che un utente riordini, in base al numero di mesi trascorsi dall’ultimo ordine. La formula utilizzata per generare questa metrica semplifica:

![Formula di probabilità di ripetizione](../../assets/Repeat_probability_formula.png)

A seconda del modello di business, la probabilità di ripetizione dell’ordine può scendere immediatamente dopo che un cliente ha effettuato un ordine e continuare a diminuire nei mesi successivi oppure può dimostrare variazioni stagionali e picchi.

In entrambi i casi, è importante comprendere la percentuale di acquisti ripetuti che i clienti devono effettuare e come queste tendenze nel tempo consentono di eseguire il targeting dei clienti a intervalli critici per massimizzare la probabilità di un acquisto ripetuto. Pertanto, quando la probabilità di acquisto ripetuto diminuisce, puoi scegliere un momento per identificare un cliente come eseguito e cambiare i tuoi sforzi da fidelizzazione a riattivazione.

## Esempio di oggi

Date un&#39;occhiata al decadimento delle probabilità di ripetizione per un tipico business di eCommerce.

![Probabilità di ripetizione iniziale dell&#39;ordine di ripetizione dell&#39;ordine a causa di mesi dall&#39;ordine.](../../assets/Order_probability_reports.png)

### Probabilità dell&#39;ordine di ripetizione iniziale

In questo esempio, la probabilità iniziale di un ordine di ripetizione, o la probabilità che un ordine sia seguito da un altro ordine, è del 60%. Ciò significa che al 60% di tutti gli ordini effettuati con questa attività fa seguito un ordine successivo.

### Probabilità dell&#39;ordine di ripetizione in base a mesi dall&#39;ordine

Questo rapporto mostra la probabilità che un cliente ordini di nuovo, dato che sono trascorsi alcuni mesi dall&#39;ultimo ordine. Anche se non esiste una definizione singolare per la soglia di abbandono specificata in questo rapporto, si consiglia di definire l’abbandono come il punto in cui il decadimento di probabilità supera il valore che è la metà del tasso di probabilità di ripetizione iniziale.

Poiché il tasso di probabilità di ripetizione iniziale per questo esempio è del 60%, la data di abbandono corrisponde al momento in cui la probabilità di ripetizione dell’ordine scende al di sotto del 60%/2 = 30%, o a circa 6 mesi. Del 60% degli ordini che saranno seguiti con un altro ordine, la metà è stata effettuata nei primi 6 mesi.

In un altro modo, se un cliente dovesse effettuare un ordine di follow-up, è più probabile che lo abbia fatto entro 6 mesi dal loro ultimo ordine che dopo il limite di 6 mesi. Se un cliente non ha effettuato un nuovo acquisto dopo 6 mesi, è necessario avviare una campagna di riattivazione per richiamare questo cliente.

A seconda del modello di business, è invece possibile scegliere una soglia diversa, ad esempio il punto in cui la probabilità di ripetizione dell’ordine scende al di sotto del 50% o del 10%. Se le tue conoscenze interne suggeriscono un numero diverso, allora in ogni modo dovresti usarlo!

In ultima analisi, l&#39;obiettivo è quello di selezionare la soglia in cui ha senso passare dalle attività di conservazione a quelle di riattivazione. Le attività di conservazione possono includere e-mail per coinvolgere nuovamente i clienti esistenti con acquisti di follow-up consigliati da effettuare, mentre le attività di riattivazione possono includere e-mail ai clienti non più in vendita con buoni e contratti.

## Quali domande dovrei considerare?

Per aiutarti a comprendere la probabilità di ripetizione dell’ordine applicata alla tua azienda, ti consigliamo di considerare queste domande quando esplori i tuoi dati:

* È prevista la probabilità iniziale di ordine di ripetizione? In caso contrario, perché pensa che dovrebbe essere più alto o più basso?
* Ci sono grandi diminuzioni nella probabilità di ordine ripetuto per mesi specifici dall&#39;ultimo ordine? In caso affermativo, sono previste tali modifiche?
* Qual è la soglia di abbandono corrente?
* La soglia di abbandono corrente si allinea a uno dei valori della probabilità di ripetizione dell’ordine, in base ai mesi dall’ultimo rapporto sull’ordine?
* La soglia attuale riflette le tue iniziative pubblicitarie che passano dalla conservazione alla riattivazione?
* Ha senso che la tua azienda cambi la soglia al mese in cui il decadimento della probabilità supera il valore che è la metà del tasso di probabilità di ripetizione iniziale?

## Che altro dovrei analizzare?

Dopo aver creato l’analisi di cui sopra e aver determinato una soglia di abbandono, puoi generare più analisi per identificare le tendenze comuni negli utenti con esecuzione. Ad esempio, i clienti che hanno effettuato acquisti durante lo stesso periodo di tempo, o hanno acquistato prodotti simili nel loro ultimo ordine? Una volta impostata la soglia di abbandono, puoi effettuare ulteriori immersioni in caratteristiche specifiche di questi clienti acquisiti.

Se offri più di un prodotto, probabilmente ti chiedi in che modo i clienti che acquistano un prodotto specifico si comportano in modo diverso nel tempo rispetto ad altri clienti. Vuoi saperne di più? Consulta questa esercitazione per scoprire il comportamento di acquisto delle coorti dei clienti nel corso della vita in base a prodotti specifici acquistati.

Questa best practice è fornita da [!DNL MBI] Data Analysis Services (DAS). Non vediamo l&#39;ora di rispondere a tutte le vostre domande di business specifiche! [Contatta il supporto](../../guide-overview.md) per ulteriori informazioni.

### Correlati

* [Analisi dell&#39;impatto sulle cedole sull&#39;acquisizione e sulla fidelizzazione dei clienti](../analysis/coupon-impact.md)
* [Analisi del comportamento di riacquisto dei clienti](../analysis/repurchase-behavior.md)
