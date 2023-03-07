---
title: Creare o eliminare percorsi per colonne calcolate
description: Scopri come definire un percorso che descriva il modo in cui la tabella su cui stai creando una colonna è correlata alla tabella da cui stai estraendo le informazioni.
exl-id: 734a8046-8058-4f03-93a2-8d59b9be6d2d
source-git-commit: 8de036e2717aedef95a8bb908898fd9b9bc9c3fa
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 0%

---

# Creare o eliminare percorsi per colonne calcolate

## Aggiornamento colonne calcolate

Quando [creazione di colonne calcolate](../data-warehouse-mgr/creating-calculated-columns.md) nella Data Warehouse viene chiesto di definire un percorso che descriva il modo in cui la tabella su cui si sta creando una colonna è correlata alla tabella da cui si stanno estraendo le informazioni. Per creare correttamente un percorso, è necessario conoscere due cose:

1. Correlazione tra le tabelle dei database
1. Chiavi primarie ed esterne che definiscono questa relazione

Se conosci queste informazioni, puoi creare facilmente un percorso seguendo le istruzioni riportate in questo articolo. Una panoramica di questi concetti se ti senti in dubbio, ma potresti voler chiedere a un esperto tecnico della tua organizzazione o contattare il team di supporto Adobe.

## Aggiornamenti relativi alle relazioni tra tabelle e ai tipi di chiave {#refresher}

### Relazioni tra tabelle {#relationships}

Questo concetto è trattato nel [Articolo Informazioni e valutazione delle relazioni tra tabelle](../../data-analyst/data-warehouse-mgr/table-relationships.md)Ma un rapido riassunto non ha mai fatto male a nessuno, giusto?

Le tabelle possono essere correlate tra loro in uno dei tre modi seguenti:

| **`Relationship Type`** | **`Example`** |
|-----|-----|
| **`one-to-one`** | Relazione tra persone e numeri di patente. Una persona può avere un solo numero di patente di guida e il numero di patente di guida appartiene a una sola persona. |
| **`one-to-many`** | Relazione tra ordini e articoli: un ordine può contenere più articoli, ma un articolo appartiene a un singolo ordine. In questo caso, la tabella ordini è il lato uno e la tabella articoli è il lato molti. |
| **`many-to-many`** | La relazione tra prodotti e categorie: un prodotto può appartenere a più categorie e una categoria può contenere più prodotti. |

{style="table-layout:auto"}

Una volta compresa una relazione tra due tabelle, è possibile utilizzarla per determinare quale percorso deve essere creato per portare le informazioni da una tabella all’altra. Per questo passaggio successivo è necessario conoscere le chiavi primarie ed esterne che facilitano una relazione tra tabelle.

### Chiavi primarie ed esterne {#keys}

A `Primary Key` è una colonna o un insieme di colonne invariabili che produce valori univoci all’interno di una tabella. Ad esempio, quando un cliente effettua un ordine su un sito web, viene aggiunta una nuova riga al `orders` tavolo nel carrello, con un nuovo `order_id`. Questo `order_id` consente sia al cliente che all’azienda di tenere traccia dell’avanzamento di quell’ordine specifico. Poiché l’ID ordine è univoco, in genere corrisponde al `Primary Key` di un `orders` tabella.

A `Foreign Key` è una colonna creata all’interno di una tabella che si collega al `Primary Key` di un&#39;altra tabella. Le chiavi esterne creano riferimenti tra tabelle, consentendo agli analisti di cercare e collegare facilmente i record. Dire che si desidera sapere quali ordini appartengono a ciascuno dei vostri clienti. Il `customer id` column (`Primary Key` del `customers` tabella) e `order_id` column (`Foreign Key` nel `customers` tabella, con riferimento alla `Primary Key` del `orders` tabella) ci consente di collegare e analizzare queste informazioni. Durante la creazione di un percorso, viene richiesto di definire entrambi i `Primary Key` e `Foreign Key`.

## Creazione di un percorso {#createpath}

Durante la creazione di una colonna nella Data Warehouse, è necessario definire il percorso che porta le informazioni da una tabella a un&#39;altra. A volte i percorsi vengono precompilati perché esiste un percorso tra le tabelle, ma se ciò non accade, è necessario crearne uno.

Utilizzare la relazione tra **clienti** e **ordini** per mostrarti come si fa. Suddiviso:

* La relazione è `one-to-many` - un cliente può avere molti ordini, ma un ordine può avere un solo cliente. Questo indica la direzione della relazione o il punto in cui creare la colonna calcolata. In questo caso, significa informazioni provenienti dal `orders` la tabella può essere inserita nel `customers` tabella.
* Il `primary key` desideri utilizzare è `customers.customerid`o `customer ID` colonna nella `customers` tabella.
* Il `foreign key` desideri utilizzare è `orders.customerid`o `customer ID` colonna nella `orders` tabella.

Ora puoi creare il percorso.

1. Clic **[!UICONTROL Data > Data Warehouse]**.
1. Nell&#39;elenco della tabella fare clic sulla tabella in cui si desidera creare la colonna. In questo esempio, è `customers` tabella.
1. Viene visualizzato lo schema della tabella. Clic **[!UICONTROL Create New Column]**.
1. Assegna un nome alla colonna, ad esempio: `Customer's orders`.
1. Selezionare la definizione della colonna. Consulta la sezione [Guida delle colonne calcolate](../data-warehouse-mgr/creating-calculated-columns.md) per una pratica scheda di riferimento.
1. In [!UICONTROL Select table and column] a discesa, fai clic su **[!UICONTROL Create new path]** opzione.

   ![Creazione di percorsi per colonne calcolate modali](../../assets/Creating_Paths_modal.png)

1. Utilizzando i menu a discesa, seleziona le chiavi primarie ed esterne per ciascuna tabella.

   Il giorno `Many` lato, seleziona `orders.customerid` - ricorda che i clienti possono avere molti ordini.

   Il giorno `One` lato, seleziona `customers.customerid` - un ordine può avere un solo cliente.

1. Clic **[!UICONTROL Save]** per salvare il percorso e completare la creazione della colonna.

### Limitazioni della creazione di percorsi {#limits}

* **[!DNL MBI]impossibile indovinare le relazioni chiave primaria/esterna**. Non desideri introdurre dati errati nell’account, pertanto la creazione dei percorsi deve essere eseguita manualmente.
* **Attualmente è possibile specificare percorsi solo tra due tabelle diverse**. La logica che si sta tentando di ricreare coinvolge più di due tabelle? Potrebbe quindi essere utile (1) unire le colonne a una tabella intermedia, quindi alla tabella di &quot;destinazione finale&quot;, oppure (2) consultare il team di Adobi per trovare l’approccio migliore ai tuoi obiettivi.
* **Una colonna può essere solo il riferimento di chiave esterna per UN percorso alla volta**. Ad esempio, se `order_items.order_id` punta a `orders.id`, quindi `order_items.order_id` non può indicare altro.
* **`Many-to-many`tecnicamente è possibile creare percorsi, ma spesso producono dati non validi perché nessuno dei due lati è un vero `one-to-many` chiave esterna**. Il modo migliore per approcciare questi percorsi dipende sempre dall’analisi specifica desiderata. Consulta il team di analisti di RJ per scoprire la soluzione migliore.

Se non riesci a creare una colonna calcolata a causa di una o più delle limitazioni di cui sopra, contatta il supporto tecnico fornendo una descrizione della colonna che stai utilizzando

## Eliminare un percorso di colonna calcolato {#delete}

Hai creato un percorso errato nella tua Data Warehouse? O forse stai facendo una piccola pulizia di primavera e vuoi riordinare? Se devi eliminare un percorso dal tuo account, puoi [invia una segnalazione agli analisti del supporto Adobe](../../guide-overview.md). **Assicurarsi di includere il nome del percorso.**

## Ritorno a capo {#wrapup}

Ora che hai familiarità con la creazione di percorsi per le colonne calcolate nella Data Warehouse. Se non sei ancora sicuro di un particolare percorso, ricorda che puoi sempre fare clic su **[!UICONTROL Support]** nel tuo [!DNL MBI] per ottenere assistenza.

## Correlato

* [Informazioni e valutazione delle relazioni tra tabelle](../data-warehouse-mgr/table-relationships.md)
* [Creazione di percorsi per colonne calcolate](../data-warehouse-mgr/create-paths-calc-columns.md)
* [Tipi di colonne calcolate](../data-warehouse-mgr/calc-column-types.md) tentativo di creazione.
