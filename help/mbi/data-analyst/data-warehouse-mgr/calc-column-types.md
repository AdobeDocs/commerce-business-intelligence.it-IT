---
title: Tipi di colonne calcolate
description: Scopri come creare colonne per migliorare e ottimizzare i dati per l’analisi.
exl-id: 1af79b9e-77ff-4fc6-917a-4e6743b95035
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 0%

---

# Tipi di colonne calcolate

* [Stessi calcoli per la tabella](#sametable)
* [Da uno a molti calcoli](#onetomany)
* [Molti a uno calcoli](#manytoone)
* [Mappa di riferimento utile](#map)
* [Colonne calcolate avanzate](#advanced)

All&#39;interno del [Gestione Date Warehouse](../data-warehouse-mgr/tour-dwm.md), puoi creare colonne per migliorare e ottimizzare i dati per l’analisi. [Questa funzionalità](../data-warehouse-mgr/creating-calculated-columns.md) è accessibile selezionando qualsiasi tabella in Gestione Date Warehouse e facendo clic su **[!UICONTROL Create New Column]**.

In questo argomento vengono descritti i tipi di colonne che è possibile creare con Gestione Date Warehouse. Include inoltre la descrizione, una descrizione visiva della colonna e una descrizione [mappa di riferimento](#map) di tutti gli input necessari per creare una colonna. Sono disponibili tre modi per creare colonne calcolate:

1. [Stesse colonne calcolate della tabella](#sametable)
1. [Colonne calcolate uno-a-molti](#onetomany)
1. [Colonne calcolate &quot;molti a uno&quot;](#manytoone)

## Stesse colonne calcolate della tabella {#sametable}

Queste colonne vengono create utilizzando le colonne di input della stessa tabella.

### Età {#age}

Una colonna calcolata in base all&#39;età restituisce il numero di secondi che intercorrono tra l&#39;ora corrente e un tempo di input.

L’esempio seguente crea `Seconds since customer's most recent order` nel `customers` tabella. Questa può essere utilizzata per creare elenchi di utenti di clienti che non hanno effettuato acquisti (talvolta denominati abbandono) in `X days`.

![](../../assets/age.gif)

### Convertitore valuta

Una colonna calcolata per il convertitore di valuta converte la valuta nativa di una colonna in una nuova valuta desiderata.

L’esempio seguente crea `base\_grand\_total In AED`, conversione `base\_grand\_total` dalla valuta nativa ad AED nel `sales\_flat\_order` tabella. Questa colonna funziona correttamente per i negozi con più valute che desiderano effettuare rapporti nella loro valuta locale.

Per i clienti Commerce, la `base\_currency\_code` in genere memorizza le valute native. Il `Spot Time` deve corrispondere alla data utilizzata nelle metriche.

![](../../assets/currency_converter.png)

## Colonne calcolate uno-a-molti {#onetomany}

`One-to-Many` colonne [utilizzare un percorso tra due tabelle](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md). Questo percorso implica sempre una tabella, in cui risiede un attributo, e una tabella molti, in cui l’attributo viene &quot;spostato&quot; giù in. Il percorso può essere descritto come `foreign key--primary key` relazione.

### Colonna unita in join {#joined}

Una colonna unita in join riposiziona un attributo nella tabella uno *a* il tavolo molti. L’esempio classico di uno/molti sono i clienti (uno) e gli ordini (molti).

Nell’esempio seguente, il `Customer's group\_id` La dimensione viene unita al nodo `orders` tabella.

![](../../assets/joined_column.gif)

## Colonne calcolate &quot;molti a uno&quot; {#manytoone}

Queste colonne utilizzano gli stessi percorsi delle colonne uno-a-molti, ma puntano i dati nella direzione opposta. La colonna viene creata sul lato uno del percorso, anziché sul lato molti. A causa di questa relazione, il valore nella colonna deve essere un&#39;aggregazione, ovvero un&#39;operazione matematica eseguita sui punti dati sul lato molti. Esistono molti casi d’uso per questo e alcuni sono elencati di seguito.

### Conteggio {#count}

Questo tipo di colonna calcolata restituisce il conteggio dei valori nella tabella molti *su* l&#39;unica tabella.

Nell’esempio seguente, la dimensione `Customer's lifetime number of canceled orders` viene creato il `customers` tabella (con un filtro per `orders.status`).

![](../../assets/many_to_one.gif){: width=&quot;699&quot; height=&quot;351&quot;}

### Somma {#sum}

Una colonna Somma calcolata è la somma dei valori sul `many` sul tavolo unico.

Può essere utilizzato per creare dimensioni a livello di cliente come `Customer's lifetime revenue`.

### Min o Max {#minmax}

Una colonna calcolata min o max restituisce il record più piccolo o più grande esistente sul lato molti.

Può essere utilizzato per creare dimensioni a livello di cliente come `Customer's first order date`.

### Esiste {#exists}

Una colonna calcolata è un test binario che determina la presenza di un record sul lato molti. In altre parole, la nuova colonna restituisce un `1` se il tracciato collega almeno una riga in ciascuna tabella, e `0` se non è possibile effettuare alcuna connessione.

Questo tipo di dimensione potrebbe determinare, ad esempio, se un cliente ha mai acquistato un particolare prodotto. Utilizzo di un join tra `customers` tabella e `orders` tabella, filtro per un prodotto specifico, dimensione `Customer has purchased Product X?` possono essere create.

## Mappa di riferimento utile {#map}

Se non riesci a ricordare quali sono tutti gli input durante la creazione di una colonna calcolata, tieni a portata di mano questa mappa di riferimento durante la creazione di:

![](../../assets/merged_reference_map.png)

## Colonne calcolate avanzate {#advanced}

Nella tua ricerca per analizzare e rispondere a domande sulla tua attività, potresti incontrare una situazione in cui non sei in grado di creare la colonna esatta che desideri.

Per garantire una rapida risposta, Adobe consiglia di controllare il [Tipi di colonne calcolate avanzate](../../data-analyst/data-warehouse-mgr/adv-calc-columns.md) per vedere che tipo di colonne può creare il team di supporto Adobe. In questo argomento vengono inoltre trattate le informazioni necessarie per creare la colonna, includendole nella richiesta.

## Documentazione correlata

* [Creazione di colonne calcolate](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)
* [Creazione/eliminazione di percorsi per colonne calcolate](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md)
* [Informazioni e valutazione delle relazioni tra tabelle](../../data-analyst/data-warehouse-mgr/table-relationships.md)
