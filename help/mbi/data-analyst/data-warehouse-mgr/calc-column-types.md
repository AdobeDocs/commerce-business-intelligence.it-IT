---
title: Tipi di colonne calcolate
description: Scopri come creare colonne per migliorare e ottimizzare i dati per l’analisi.
exl-id: 1af79b9e-77ff-4fc6-917a-4e6743b95035
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 0%

---

# Tipi di colonne calcolate

* [Stessi calcoli delle tabelle](#sametable)
* [Uno o più calcoli](#onetomany)
* [Numeri a uno](#manytoone)
* [Mappa di riferimento di Handy](#map)
* [Colonne calcolate avanzate](#advanced)

All&#39;interno di [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md), puoi creare colonne per migliorare e ottimizzare i dati per l’analisi. [Questa funzionalità](../data-warehouse-mgr/creating-calculated-columns.md) è accessibile selezionando una tabella qualsiasi in Data Warehouse Manager e facendo clic su **[!UICONTROL Create New Column]**.

Questo articolo descrive i tipi di colonne che è possibile creare con Gestione Date Warehouse, insieme a una descrizione, a una descrizione dettagliata visiva di tale colonna e a una [mappa di riferimento](#map) di tutti gli input necessari per creare una colonna. Esistono tre modi per creare le colonne calcolate:

* [Stesse colonne calcolate della tabella](#sametable)
* [Colonne calcolate uno-molti](#onetomany)
* [Colonne calcolate da molti a uno](#manytoone)

## Stesse colonne calcolate della tabella {#sametable}

Queste colonne vengono create utilizzando colonne di input della stessa tabella.

### Età {#age}

Una colonna calcolata per l’età restituisce il numero di secondi tra il tempo corrente e un po’ di tempo di input.

Nell’esempio seguente, abbiamo creato `Seconds since customer's most recent order` in `customers` tabella. Questa funzione può essere utilizzata per creare elenchi di utenti di clienti che non hanno effettuato acquisti (a volte denominati churning) all’interno di `X days`.

![](../../assets/age.gif)

### Convertitore valuta

Una colonna calcolata dal convertitore di valuta converte la valuta nativa di una colonna in una nuova valuta desiderata.

Nell’esempio seguente, abbiamo creato `base\_grand\_total In AED`, conversione `base\_grand\_total` da è valuta nativa ad AED nel `sales\_flat\_order` tabella. Questa colonna funziona bene per gli archivi con più valute che desiderano eseguire il report nella propria valuta locale.

Per i client Commerce, l’ `base\_currency\_code` In genere il campo memorizza le valute native. La `Spot Time` deve corrispondere alla data utilizzata nelle metriche.

![](../../assets/currency_converter.png)

## Colonne calcolate uno-molti {#onetomany}

`One-to-Many` colonne [utilizzare un percorso tra due tabelle](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md). Questo percorso implica sempre una tabella, in cui vive un attributo, e una tabella molti, in cui l’attributo viene &quot;trasferito&quot; verso il basso. Il percorso può essere descritto come `foreign key--primary key` relazione.

### Colonna unita {#joined}

Una colonna unita trasferisce un attributo nell’unica tabella *a* il tavolo. L’esempio classico di uno/molti è quello dei clienti (uno) e degli ordini (molti).

Nell’esempio seguente, la `Customer's group\_id` viene unita alla dimensione `orders` tabella.

![](../../assets/joined_column.gif)

## Colonne calcolate da molti a uno {#manytoone}

Queste colonne utilizzano gli stessi percorsi delle colonne uno-a-molti, ma puntano i dati nella direzione opposta. La colonna viene creata su un lato del percorso, invece che sul lato molti. A causa di questa relazione, il valore nella colonna deve essere un’aggregazione, ovvero un’operazione matematica eseguita sui punti di dati sul lato molti. Ci sono molti casi d’uso per questo e alcuni sono elencati di seguito.

### Conteggio {#count}

Questo tipo di colonna calcolata restituisce il conteggio dei valori della tabella molti *su* l&#39;unico tavolo.

Nell’esempio seguente, la dimensione `Customer's lifetime number of canceled orders` viene creato in `customers` tabella (con filtro per `orders.status`).

![](../../assets/many_to_one.gif){: width=&quot;699&quot; height=&quot;351&quot;}

### Somma {#sum}

Una colonna calcolata a somma è la somma dei valori nel `many` tabella su un tavolo.

Può essere utilizzato per creare dimensioni a livello di cliente come `Customer's lifetime revenue`.

### Min o Max {#minmax}

Una colonna calcolata minima o massima restituisce il record più piccolo o più grande presente sul lato molti.

Può essere utilizzato per creare dimensioni a livello di cliente come `Customer's first order date`.

### Esiste {#exists}

Una colonna calcolata esistente è un test binario che determina la presenza di un record sul lato molti. In altre parole, la nuova colonna restituirà un `1` se il percorso connette almeno una riga in ciascuna tabella, e `0` se non è possibile stabilire una connessione.

Questo tipo di dimensione può determinare, ad esempio, se un cliente ha mai acquistato un particolare prodotto. Utilizzo di un join tra un `customers` tabella e `orders` tabella, un filtro per un prodotto specifico, una dimensione `Customer has purchased Product X?` possono essere costruiti.

## Mappa di riferimento di Handy {#map}

Se hai qualche problema a ricordare cosa sono tutti gli input durante la creazione di una colonna calcolata, prova a mantenere questa mappa di riferimento utile durante la creazione:

![](../../assets/merged_reference_map.png)

## Colonne calcolate avanzate {#advanced}

Nel tuo tentativo di analizzare e rispondere alle domande sul tuo business, potresti incontrare una situazione in cui non sei in grado di costruire la colonna esatta che desideri. In questi casi, ti abbiamo coperto!

Per garantire una rapida inversione di tendenza, si consiglia di controllare la [Tipi di colonne calcolate avanzate](../../data-analyst/data-warehouse-mgr/adv-calc-columns.md) guida per vedere che tipo di colonne può creare il nostro team di supporto. In questo articolo, copriamo anche le informazioni che avremo bisogno da voi per creare la colonna - si prega di includerla con la vostra richiesta.

## Documentazione correlata

* [Creazione di colonne calcolate](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)
* [Creazione/eliminazione di percorsi per le colonne calcolate](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md)
* [Informazioni e valutazione delle relazioni tra tabelle](../../data-analyst/data-warehouse-mgr/table-relationships.md)
