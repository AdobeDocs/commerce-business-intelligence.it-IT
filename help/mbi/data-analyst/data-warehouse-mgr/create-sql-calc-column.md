---
title: Creazione e utilizzo di una colonna calcolata SQL
description: Scopri come creare colonne avanzate sotto forma di colonne di calcolo SQL nella nuova architettura MBI.
exl-id: f16e4ee4-ed73-4ddb-b701-1fe3db14346a
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# Creare una colonna calcolata SQL

In questo argomento vengono illustrati lo scopo e gli usi `Calculation` tipo di colonna: che può essere aggiunto alle tabelle utilizzando [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md). Di seguito è riportata una spiegazione delle operazioni eseguite dai calcoli SQL, del motivo per cui vengono utilizzati, del processo per la creazione di un calcolo SQL e due esempi.

**Spiegazione**

In passato, colonne considerate `advanced` può essere eseguito solo da un analista del team Customer Success qui a [!DNL MBI]. Ora tutta la potenza è nelle mani dell&#39;utente finale, e le colonne avanzate possono essere create sotto forma di `SQL Calculation` colonne nel nuovo [!DNL MBI] architettura.

La `Calculation` il tipo di colonna, ora disponibile come opzione in Data Warehouse Manager, è una stessa operazione di tabella che consente di trasformare le colonne di una tabella utilizzando la logica PostgreSQL. Documentazione sulle funzioni e gli operatori che possono essere utilizzati nel `Calculatio`Nel sito Web PostgreSQL è possibile trovare un tipo di colonna [qui](https://www.postgresql.org/docs/9.6/static/functions.html).

Le diverse colonne che possono essere create con il `Calculation` le colonne sono quasi illimitate, ma la maggior parte delle colonne può essere creata utilizzando istruzioni IF-THEN e l’aritmetica di base, che verranno utilizzate negli esempi seguenti.

**Esempio 1: L&#39;ultimo ordine del cliente?**

La maggior parte degli account ha una colonna denominata `Is customer's last order?` sulle `orders` tabella per eseguire analisi sui tassi di acquisto ripetuti e sui clienti fidelizzati. Se l’account si trova nella nuova architettura, questa colonna viene creata utilizzando un `Calculation` e può essere visto nella schermata sottostante:

![](../../assets/Is_customer_s_last_order.png)

La `Is customer's last order?` utilizza gli input `Customer's lifetime number of orders` e `Customer's order number` aliasing come `A` e `B` rispettivamente.

Linea per riga, il significato di PostgreSQL è:

* caso: Viene avviata una serie di istruzioni If - Then
* quando `A` è nullo o `B` è nullo e quindi nullo: Se uno degli input è vuoto, anche l&#39;output deve essere vuoto. Questo per evitare errori SQL
* quando `A=B` then `Yes`: Se `Customer's lifetime number of orders` è `Customer's order number` per questa riga, quindi restituisce `Yes`. Quindi, se un cliente ha effettuato 4 ordini, la riga per il suo quarto ordine restituirà `Yes` per `Is customer's last order?`
* else `No`: Se nessuna delle altre situazioni in cui le istruzioni sono soddisfatte, restituisce `No`
* fine: Termina le istruzioni If - Then

I possibili valori che possono essere restituiti da questa colonna (`NULL`, `Yes`, `No`) contiene caratteri non numerici, quindi il tipo di dati qui è String.

**Esempio 2: Valore totale articolo ordine (quantità * prezzo)**

A molti dei nostri clienti piace analizzare i ricavi a livello di articolo, suddividendoli per campi come `product name` o `category`. La maggior parte dei database non ti dà effettivamente i ricavi di un prodotto in un ordine; forniscono invece la quantità venduta nell&#39;ordine e il prezzo dell&#39;articolo.

Per abilitare l’analisi dei ricavi di prodotto, la maggior parte degli account dispone di una colonna denominata `Order item total value (quantity * price)` sulle `Orders Items` tabella. Se l’account si trova nella nuova architettura, questa colonna viene creata anche utilizzando un `Calculation` e può essere visto nella schermata sottostante:

![](../../assets/Order_item_total_value.png)

Nello schema Commerce, l’ `Order item total value (quantity * price)` utilizza gli input `qty ordered` e `base price` aliasing come `A` e `B` rispettivamente.

I valori che verranno restituiti da questa nuova colonna saranno in dollari e centesimi, quindi il tipo di dati corretto è `Decimal(10,2)`.

**Meccanica**

Nuovo `Calculation` è possibile aggiungere una colonna a una tabella passando a **[!DNL Manage Data > Data Warehouse]** come mostrato di seguito:

![](../../assets/blobid2.png)

Da qui puoi creare una nuova `Calculation` seguendo i passaggi seguenti:

1. Seleziona la tabella in cui desideri aggiungere la `Calculation` colonna.
1. Nella tabella corretta, fai clic su **[!UICONTROL Create New Column]** in alto a destra dello schermo.
1. Da `Select a definition` a discesa, seleziona `Same Table`.
1. Seleziona `Calculation` come `column definition equation`.
1. Immetti il nome della colonna.
1. Scegli la `input` dalla tabella che verrà utilizzata nella logica per la nuova colonna. Ogni colonna aggiunta riceverà un alias di lettera, quindi la prima colonna sarà `A`, la seconda `B` e così via.
1. Nella finestra, digitare la logica PostgreSQL per la nuova colonna utilizzando gli alias lettera degli input. Il calcolo SQL deve essere limitato a una singola definizione di colonna, inclusa tutta la logica tra le istruzioni SELECT e FROM di una query SQL. Le parole chiave SQL che utilizzano una qualsiasi delle lettere di input devono essere in minuscolo. Ad esempio, quando si utilizza il `CASE` dichiarazione, dovrebbe essere scritto in minuscolo - `case`. Il sistema presuppone che una maiuscola `A` si riferisce a uno degli input.
1. Scegli il tipo di dati appropriato.
   * `Integer` - Numero intero
   * `Decimal(10,2)` - un numero decimale con 10 cifre totali, di cui 2 a destra del punto decimale
   * `String` - Qualsiasi tipo di testo o serie di caratteri che utilizza non numeri
   * `Datetime` - aaaa-MM-gg hh:mm:formato ss

1. Fai clic su **[!UICONTROL test column]**. Verrà generato un elenco di 5 valori di test per ciascuno degli input e verrà mostrato il risultato della logica del passaggio 6 per ciascun set di valori di test. Se una parte qualsiasi dell&#39;SQL genera un errore, viene restituito il messaggio di errore appropriato. I risultati di esempio possono essere generati solo se tutte le colonne di input sono campi nativi. Se una delle colonne di input è calcolata, è necessario convalidare i risultati aggiungendo la colonna a una metrica e visualizzandola nel Report Builder visivo
1. Quando si è soddisfatti dei risultati, fare clic su **[!UICONTROL Save]** e la colonna sarà disponibile per l’uso.
