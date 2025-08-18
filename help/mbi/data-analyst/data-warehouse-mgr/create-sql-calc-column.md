---
title: Creazione e utilizzo di una colonna calcolata SQL
description: Scopri come creare colonne avanzate sotto forma di colonne di calcolo SQL nella nuova architettura di Adobe Commerce Intelligence.
exl-id: f16e4ee4-ed73-4ddb-b701-1fe3db14346a
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, SQL Report Builder, Commerce Tables
source-git-commit: 8090c2e0f17f0e8d3bdec668ce546206bf024691
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---

# Creare una colonna calcolata SQL

Questo argomento descrive lo scopo e gli utilizzi del tipo di colonna `Calculation` che è possibile aggiungere alle tabelle utilizzando [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md). Di seguito vengono illustrate le operazioni dei calcoli SQL, il motivo per cui vengono utilizzati e il processo per la creazione di un calcolo SQL. Sono inclusi due esempi.

**Spiegazione**

In passato, le colonne considerate `advanced` potevano essere eseguite solo da un analista del team Customer Success qui in [!DNL Adobe Commerce Intelligence]. Ora tutto il potere è nelle mani dell&#39;utente finale e le colonne avanzate possono essere create sotto forma di `SQL Calculation` colonne sulla nuova architettura di [!DNL Commerce Intelligence].

Il tipo di colonna `Calculation`, ora disponibile come opzione in Data Warehouse Manager, è la stessa operazione di tabella che consente di trasformare le colonne in una tabella utilizzando la logica PostgreSQL. La documentazione relativa alle funzioni e agli operatori utilizzabili nel tipo di colonna `Calculation` è disponibile nel sito Web PostgreSQL [qui](https://www.postgresql.org/docs/9.6/functions.html).

Le diverse colonne che possono essere create con la colonna `Calculation` sono quasi illimitate, ma la maggior parte delle colonne può essere creata utilizzando le istruzioni IF-THEN e l&#39;aritmetica di base, utilizzata negli esempi seguenti.

**Esempio 1: ultimo ordine del cliente?**

La maggior parte degli account dispone di una colonna denominata `Is customer's last order?` nella tabella `orders` per eseguire analisi sui tassi di acquisto ripetuti e sui clienti abbandonati. Se il tuo account si trova nella nuova architettura, questa colonna viene creata utilizzando una colonna `Calculation` ed è visibile nella schermata seguente:

![](../../assets/Is_customer_s_last_order.png)

La colonna `Is customer's last order?` utilizza gli input `Customer's lifetime number of orders` e `Customer's order number` con alias rispettivamente `A` e `B`.

Riga per riga, il significato di PostgreSQL è:

* caso: inizia una serie di istruzioni If - Then
* se `A` è null o `B` è null, allora null: se uno dei due input è vuoto, anche l&#39;output deve essere vuoto. In questo modo si evitano errori SQL
* quando `A=B` e poi `Yes`: se `Customer's lifetime number of orders` è uguale a `Customer's order number` per questa riga, restituisce `Yes`. Pertanto, se un cliente ha effettuato quattro ordini, la riga per il quarto ordine restituirà `Yes` per `Is customer's last order?`
* else `No`: se non viene soddisfatta nessuna delle altre istruzioni, restituire `No`
* end: termina le istruzioni If - Then

I valori che possono essere restituiti da questa colonna (`NULL`, `Yes`, `No`) contengono caratteri non numerici, pertanto il tipo di dati è String.

**Esempio 2: valore totale articolo ordine (quantità * prezzo)**

A molti clienti piace analizzare i ricavi a livello di elemento, suddividendoli per campi come `product name` o `category`. La maggior parte dei database non fornisce effettivamente i ricavi di un prodotto in un ordine, ma fornisce la quantità venduta nell&#39;ordine e il prezzo dell&#39;articolo.

Per abilitare le analisi dei ricavi dei prodotti, la maggior parte degli account dispone di una colonna denominata `Order item total value (quantity * price)` nella tabella `Orders Items`. Se il tuo account utilizza la nuova architettura, questa colonna viene creata anche utilizzando una colonna `Calculation` ed è visibile nella schermata seguente:

![](../../assets/Order_item_total_value.png)

Nello schema Commerce, la colonna `Order item total value (quantity * price)` utilizza gli input `qty ordered` e `base price` con alias rispettivamente `A` e `B`.

I valori restituiti da questa nuova colonna sono espressi in dollari e centesimi, pertanto il tipo di dati corretto è `Decimal(10,2)`.

**Meccanica**

È possibile aggiungere una nuova colonna `Calculation` a una tabella passando a **[!DNL Manage Data > Data Warehouse]** come illustrato di seguito:

![](../../assets/blobid2.png)

Da qui puoi creare una colonna `Calculation` seguendo la procedura seguente:

1. Selezionare la tabella in cui aggiungere la colonna `Calculation`.
1. Nella tabella corretta, fare clic su **[!UICONTROL Create New Column]** in alto a destra dello schermo.
1. Dal menu a discesa `Select a definition`, seleziona `Same Table`.
1. Seleziona `Calculation` come `column definition equation`.
1. Immettere il nome della colonna.
1. Scegliere le colonne `input` dalla tabella utilizzate nella logica per la nuova colonna. Ogni colonna aggiunta ottiene un alias di lettera, pertanto la prima colonna è `A`, la seconda è `B` e così via.
1. Nella finestra, digita la logica PostgreSQL per la nuova colonna utilizzando gli alias delle lettere degli input. Il calcolo SQL deve essere limitato a una singola definizione di colonna, inclusa tutta la logica tra le istruzioni SELECT e FROM di una query SQL. Le parole chiave SQL che utilizzano una qualsiasi delle lettere di input devono essere in minuscolo. Ad esempio, quando si utilizza l&#39;istruzione `CASE`, questa deve essere scritta in minuscolo - `case`. Il sistema presuppone che un `A` in maiuscolo faccia riferimento a uno degli input.
1. Scegli il tipo di dati appropriato.
   * `Integer` - Numero intero
   * `Decimal(10,2)` - numero decimale con 10 cifre totali, di cui 2 a destra del separatore decimale
   * `String` - Qualsiasi tipo di testo o serie di caratteri che non utilizzano numeri
   * `Datetime` - Formato `yyyy-MM-dd hh:mm:ss`

1. Fare clic su **[!UICONTROL test column]**. In questo modo viene generato un elenco di cinque valori di test per ogni input e viene visualizzato il risultato della logica del passaggio 6 per ogni set di valori di test. Se una parte qualsiasi dell&#39;istruzione SQL genera un errore, viene restituito il messaggio di errore appropriato. I risultati di esempio possono essere generati solo se tutte le colonne di input sono campi nativi. Se una delle colonne di input è una colonna calcolata, è necessario convalidare i risultati aggiungendo la colonna a una metrica e visualizzandola in Visual Report Builder

1. Quando si è soddisfatti dei risultati, fare clic su **[!UICONTROL Save]**. La colonna è abilitata per l’uso.
