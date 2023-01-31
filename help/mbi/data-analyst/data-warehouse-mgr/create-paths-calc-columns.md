---
title: Crea o elimina percorsi per le colonne calcolate
description: Scopri come definire un percorso che descrive come la tabella su cui si sta creando una colonna è correlata alla tabella da cui si stanno estraendo le informazioni.
exl-id: 734a8046-8058-4f03-93a2-8d59b9be6d2d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---

# Creare o eliminare percorsi per le colonne calcolate

## Aggiornamento colonne calcolate

Quando [creazione di colonne calcolate](../data-warehouse-mgr/creating-calculated-columns.md) nella Data Warehouse, ti verrà chiesto di definire un percorso che descriva come la tabella su cui stai creando una colonna è correlata alla tabella da cui stai estraendo le informazioni. Per creare correttamente un percorso, devi sapere due cose:

1. Relazioni tra le tabelle dei database
1. Le chiavi primarie ed esterne che definiscono questa relazione

Se conosci queste informazioni, potrai creare facilmente un percorso seguendo le istruzioni contenute in questo articolo. Abbiamo fornito una panoramica di questi concetti se non sei sicuro, ma potresti voler chiedere a un esperto tecnico della tua organizzazione o contattare il nostro team di supporto.

## Aggiornamento delle relazioni tra tabelle e dei tipi di chiave {#refresher}

### Relazioni tabella {#relationships}

Abbiamo approfondito questo concetto nel nostro [Articolo Informazioni e valutazione delle relazioni tra tabelle](../../data-analyst/data-warehouse-mgr/table-relationships.md)ma una breve sintesi non ha mai fatto male a nessuno, giusto?

Le tabelle possono essere correlate tra loro in uno dei tre modi seguenti:

| **`Relationship Type`** | **`Example`** |
|-----|-----|
| **`one-to-one`** | Il rapporto tra le persone e i numeri di patente. Una persona può avere un solo numero di patente e un numero di patente di guida appartiene a una sola persona. |
| **`one-to-many`** | Relazione tra ordini e articoli - un ordine può contenere molti articoli, ma un articolo appartiene a un singolo ordine. In questo caso, la tabella ordini è un lato e la tabella articoli è il lato molti. |
| **`many-to-many`** | Il rapporto tra prodotti e categorie: un prodotto può appartenere a molte categorie e una categoria può contenere molti prodotti. |

{style=&quot;table-layout:auto&quot;}

Una volta compresa una relazione tra due tabelle, è possibile utilizzarla per determinare quale percorso deve essere creato per spostare le informazioni da una tabella all’altra. Questo passaggio successivo richiede la conoscenza delle chiavi primarie ed esterne che facilitino una relazione tra tabelle.

### Chiavi primarie ed esterne {#keys}

A `Primary Key` è una colonna o un insieme di colonne che genera valori univoci all’interno di una tabella. Ad esempio, quando un cliente effettua un ordine su un sito web, viene aggiunta una nuova riga al `orders` tavolo nel carrello, con un nuovo `order_id`. Questo `order_id` consente al cliente e all&#39;azienda di tenere traccia dell&#39;avanzamento di tale ordine specifico. Poiché l’ID ordine è univoco, in genere è il `Primary Key` di `orders` tabella.

A `Foreign Key` è una colonna creata all’interno di una tabella che effettua un collegamento a `Primary Key` di un’altra tabella. Le chiavi esterne creano riferimenti tra le tabelle, consentendo agli analisti di cercare e collegare facilmente i record. Diciamo che volevamo sapere quali ordini appartenevano a ciascuno dei nostri clienti. La `customer id` colonna (`Primary Key` del `customers` e `order_id` colonna (`Foreign Key` in `customers` tabella, facendo riferimento alla `Primary Key` del `orders` (tabella) ci consente di collegare e analizzare queste informazioni. Quando crei un percorso, ti verrà chiesto di definire sia il `Primary Key` e `Foreign Key`.

## Creazione di un percorso {#createpath}

Quando crei una colonna nel data warehouse, dovrai definire il percorso che porta informazioni da una tabella all&#39;altra. A volte i percorsi vengono precompilati perché esiste già un percorso tra le tabelle, ma in caso contrario sarà necessario crearne uno.

Usiamo la relazione tra **clienti** e **ordini** per mostrarti come si fa. Suddivisione:

* La relazione è `one-to-many` - un cliente può avere molti ordini, ma un ordine può avere un solo cliente. Questo indica la direzione della relazione o dove deve essere creata la colonna calcolata. In questo caso, si intende l&#39;informazione del `orders` è possibile inserire nella tabella `customers` tabella.
* La `primary key` vogliamo usare `customers.customerid`o `customer ID` nella colonna `customers` tabella.
* La `foreign key` vogliamo usare `orders.customerid`o `customer ID` nella colonna `orders` tabella.

Ora, vi camminiamo attraverso la creazione del percorso.

1. Fai clic su **[!UICONTROL Data > Data Warehouse]**.
1. Nell’elenco delle tabelle, fare clic sulla tabella in cui si desidera creare la colonna. Nel nostro esempio, è il `customers` tabella.
1. Verrà visualizzato lo schema della tabella. Fai clic su **[!UICONTROL Create New Column]**.
1. Assegna un nome alla colonna, ad esempio `Customer's orders`.
1. Seleziona la definizione della colonna. Consulta la sezione [Guida alle colonne calcolate](../data-warehouse-mgr/creating-calculated-columns.md) per un comodo foglio di imbroglio.
1. In [!UICONTROL Select table and column] fai clic sul menu a discesa **[!UICONTROL Create new path]** opzione .

   ![Creazione di percorsi per colonne calcolate modali](../../assets/Creating_Paths_modal.png)

1. Utilizzando i menu a discesa, selezionare le chiavi primaria ed esterna per ciascuna tabella.

   Sulla `Many` lato, selezioniamo `orders.customerid` - ricorda, i clienti possono avere molti ordini.

   Sulla `One` lato, selezioniamo `customers.customerid` - un ordine può avere un solo cliente.

1. Fai clic su **[!UICONTROL Save]** per salvare il percorso e completare la creazione della colonna.

### Limitazioni della creazione dei percorsi {#limits}

* **[!DNL MBI]non è in grado di indovinare le relazioni chiave primaria/estera**. Non vogliamo introdurre dati errati nel tuo account, pertanto la creazione dei percorsi deve essere eseguita manualmente.
* **Attualmente, i percorsi possono essere specificati solo tra due tabelle diverse**. La logica che si sta tentando di ricreare coinvolge più di due tabelle? Potrebbe quindi avere senso (1) unire prima le colonne a una tabella intermedia, poi alla tabella &quot;destinazione finale&quot;, o (2) consultare il nostro team per trovare l&#39;approccio migliore ai tuoi obiettivi.
* **Una colonna può essere solo il riferimento di chiave esterna per un percorso ONE alla volta**. Ad esempio, se `order_items.order_id` punti `orders.id`, quindi `order_items.order_id` non può indicare altro.
* **`Many-to-many`i percorsi possono essere tecnicamente creati, ma molto spesso producono dati negativi perché nessuno dei due lati è vero `one-to-many` chiave estera**. Il modo migliore per affrontare questi percorsi dipende sempre dall’analisi specifica desiderata. Consulta il team di analisi RJ per scoprire la soluzione migliore.

Se non riesci a creare una colonna calcolata a causa di una o più limitazioni, contatta il supporto per una descrizione della colonna in uso

## Eliminare un percorso colonna calcolato {#delete}

Hai creato un percorso non corretto nella tua Data Warehouse? O forse state facendo un po&#39; di pulizia primaverile e volete riordinare? Se devi eliminare un percorso dall’account, puoi [invia un ticket ai nostri analisti di supporto](../../guide-overview.md). **Accertati di includere il nome del percorso!**

## Ritorno a capo {#wrapup}

Ora dovresti sentirti a tuo agio nel creare percorsi per le colonne calcolate nella tua Data Warehouse. Se non sei ancora sicuro di un particolare percorso, ricorda che puoi sempre fare clic su **[!UICONTROL Support]** nel tuo [!DNL MBI] conto per ottenere assistenza.

## Correlati

* [Informazioni e valutazione delle relazioni tra tabelle](../data-warehouse-mgr/table-relationships.md)
* [Creazione di percorsi per le colonne calcolate](../data-warehouse-mgr/create-paths-calc-columns.md)
* [Tipi di colonne calcolate](../data-warehouse-mgr/calc-column-types.md) tentativo di creazione.
