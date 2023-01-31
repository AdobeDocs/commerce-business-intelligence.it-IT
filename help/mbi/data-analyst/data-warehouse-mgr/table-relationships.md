---
title: Comprendere e valutare le relazioni tra tabelle
description: Scopri come comprendere quante occorrenze possibili in una tabella possono appartenere a un’entità in un’altra tabella e viceversa.
exl-id: e7256f46-879a-41da-9919-b700f2691013
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# Comprendere e valutare le relazioni tra tabelle

Quando si valuta la relazione tra due tabelle, è necessario comprendere quante occorrenze possibili in una tabella possono appartenere a un’entità in un’altra tabella e viceversa. Ad esempio, utilizziamo un `users` tabella e `orders` tabella. In questo caso, vuoi sapere quanti **ordini** una data **user** ha posizionato e quante più possibilità **utenti** un **ordine** potrebbe appartenere a.

La comprensione delle relazioni è fondamentale per mantenere l’integrità dei dati, in quanto influisce sulla precisione delle [colonne calcolate](../data-warehouse-mgr/creating-calculated-columns.md) e [dimensioni](../data-warehouse-mgr/manage-data-dimensions-metrics.md). Per ulteriori informazioni, consulta [tipi di relazione](#types) e [come valutare le tabelle nella Data Warehouse.](#eval)

## Tipi di relazione {#types}

Esistono tre tipi di relazioni tra due tabelle:

* [&quot;one-to-one&quot;](#onetoone)
* [`one-to-many`](#onetomany)
* [`molti-a-molti`](#manytomany)

### `One-to-One` {#onetoone}

In una `one-to-one` relazione, un record nella tabella `B` appartiene a un solo record della tabella `A`. E un record nella tabella `A` appartiene a un solo record della tabella `B`.

Ad esempio, nel rapporto tra le persone e i numeri di patente di guida, una persona può avere un solo numero di patente di guida e un numero di patente di guida appartiene a una sola persona.

![](../../assets/one-to-one.png)

### `One-to-Many` {#onetomany}

In una `one-to-many` relazione, un record nella tabella `A` può appartenere a più record nella tabella `B`. Pensate alla relazione tra `orders` e `items` - un ordine può contenere molti articoli, ma un articolo appartiene a un singolo ordine. In questo caso, il `orders` la tabella è un lato e la `items` il tavolo è il lato molti.

![](../../assets/one-to-many_001.png)

### `Many-to-Many` {#manytomany}

In una `many-to-many` relazione, un record nella tabella `B` può appartenere a più record nella tabella `A`. E viceversa, un record in tabella `A` può appartenere a più record nella tabella `B`.

Pensate alla relazione tra **products** e **categorie**: un prodotto può appartenere a molte categorie e una categoria può contenere molti prodotti.

![](../../assets/many-to-many.png)

## Valutazione delle tabelle {#eval}

Dati i tipi di relazioni esistenti tra le tabelle, è possibile imparare a valutare le tabelle nel data warehouse. Poiché queste relazioni determinano il modo in cui vengono definite le colonne calcolate di più tabelle, è importante comprendere come identificare le relazioni tra tabelle e il lato - `one` o `many` - la tabella appartiene a.

Esistono due metodi per valutare le relazioni di una determinata coppia di tabelle all’interno della Data Warehouse. Il primo metodo utilizza un [quadro concettuale](#concept) che considera il modo in cui le entità della tabella interagiscono tra loro. Il secondo metodo utilizza [schema della tabella](#schema).

### Utilizzo del quadro concettuale {#concept}

Questo metodo utilizza un quadro concettuale per descrivere come le entità nelle due tabelle sono in grado di interagire tra loro. È importante comprendere che tale quadro valuta le possibilità, tenuto conto delle relazioni.

Ad esempio, quando pensi a utenti e ordini, considera tutto ciò che è possibile nella relazione. Un utente registrato non può effettuare ordini, un solo ordine o più ordini nel corso della sua vita. Se hai appena avviato la tua attività e non sono ancora stati ordinati, è ancora possibile che un dato utente possa effettuare molti ordini nella loro vita e le tabelle sono costruite per adattarsi a questo.

Per utilizzare questo metodo:

1. Identifica l’entità descritta in ogni tabella. **Suggerimento: di solito è un sostantivo**. Ad esempio, il `user` e `orders` le tabelle descrivono in modo esplicito utenti e ordini.
1. Identifica il verbo o i verbi che descrivono come interagiscono queste entità. Ad esempio, quando si confrontano gli utenti con gli ordini, gli utenti inseriscono gli ordini. Andando nella direzione opposta, gli ordini &quot;appartengono&quot; agli utenti.

Questo tipo di framework può essere applicato a qualsiasi accoppiamento di tabelle nella Data Warehouse, consentendo di identificare facilmente il tipo di relazione e quale tabella è un lato unico e quale tabella è un lato molti.

Dopo aver identificato la terminologia che descrive l’interazione delle due tabelle, inquadra l’interazione in entrambe le direzioni considerando come una determinata istanza della prima entità si relaziona alla seconda. Di seguito sono riportati alcuni esempi di ciascuna relazione:

### `One-to-One`

Una persona può avere un solo numero di patente di guida. Un dato numero di patente di guida appartiene a una sola persona.

Questa è una `one-to-one` relazione in cui ogni tabella è un lato unico.

![](../../assets/one-to-one3.png)

### `One-to-Many`

Un dato ordine può eventualmente contenere molti elementi. Un dato articolo appartiene a un solo ordine.

Questa è una `one-to-many` relazione in cui la tabella degli ordini è un lato e la tabella degli articoli è il lato molti.

![](../../assets/one-to-many3.png)

### `Many-to-Many`

Un dato prodotto può appartenere a molte categorie. Una determinata categoria può eventualmente contenere molti prodotti.

Questa è una `many-to-many` relazione in cui ogni tabella è un lato molti.

![](../../assets/many-to-many3.png)

### Utilizzo dello schema della tabella {#schema}

Il secondo metodo sfrutta lo schema della tabella. Lo schema definisce quali colonne sono [`Primary`](http://en.wikipedia.org/wiki/Unique_key) e [`Foreign`](https://en.wikipedia.org/wiki/Foreign_key) chiavi. Puoi utilizzare queste chiavi per collegare le tabelle e determinare i tipi di relazione.

Una volta identificate le colonne che collegano due tabelle, utilizza i tipi di colonna per valutare la relazione tra le tabelle. Di seguito sono riportati alcuni esempi:

### `One-to-one`

Se le tabelle sono collegate utilizzando la variabile `primary key` di entrambe le tabelle, la stessa entità univoca viene descritta in ogni tabella e la relazione è `one-to-one`.

Ad esempio, un `users` la tabella può acquisire la maggior parte degli attributi utente (ad esempio il nome) mentre un `user_source` acquisisce le origini di registrazione utente. In ogni tabella, una riga rappresenta un utente.

![](../../assets/one-to-one1.png)

### `One-to-many`

>[!NOTE]
>
>Accetta gli ordini degli ospiti? [Ordini degli ospiti](../data-warehouse-mgr/guest-orders.md) per scoprire in che modo gli ordini degli ospiti possono influenzare le relazioni tra le tabelle.

Quando le tabelle sono collegate mediante un `Foreign key` indica un `primary key`, questa configurazione descrive un `one-to-many` relazione. L’unico lato sarà la tabella contenente il `primary key` e il lato molti sarà la tabella contenente il `foreign key`.

![](../../assets/one-to-many1.png)

### `Many-to-many`

Se una delle seguenti affermazioni è vera, la relazione è `many-to-many`:

* `Non-primary key` colonne utilizzate per collegare due tabelle
   ![](../../assets/many-to-many1.png)
* Parte di un composito `primary key` viene utilizzato per collegare due tabelle

![](../../assets/many-to-mnay2.png)

## Passaggi successivi

La corretta valutazione delle relazioni tra tabelle è fondamentale per modellare accuratamente i dati. Ora che si capisce in che modo le tabelle sono correlate l’una all’altra, vedere [operazioni possibili con Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md).
