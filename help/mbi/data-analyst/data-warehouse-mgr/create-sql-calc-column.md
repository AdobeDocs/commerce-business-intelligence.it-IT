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

Questo argomento illustra lo scopo e gli utilizzi del `Calculation` tipo di colonna, che può essere aggiunto alle tabelle utilizzando [Gestione Date Warehouse](../data-warehouse-mgr/tour-dwm.md). Di seguito vengono illustrate le operazioni dei calcoli SQL, il motivo per cui vengono utilizzati e il processo per la creazione di un calcolo SQL. Sono inclusi due esempi.

**Spiegazione**

In passato, le colonne considerate `advanced` può essere eseguito solo da un analista del team Customer Success, qui [!DNL Adobe Commerce Intelligence]. Ora tutto il potere è nelle mani dell&#39;utente finale, e colonne avanzate possono essere create sotto forma di `SQL Calculation` colonne sul nuovo [!DNL Commerce Intelligence] architettura.

Il `Calculation` Il tipo di colonna, ora disponibile come opzione in Gestione Date Warehouse, è la stessa operazione di tabella che consente di trasformare le colonne in una tabella utilizzando la logica PostgreSQL. Documentazione sulle funzioni e sugli operatori che possono essere utilizzati nel `Calculation` Il tipo di colonna si trova sul sito Web PostgreSQL [qui](https://www.postgresql.org/docs/9.6/functions.html).

Le diverse colonne che possono essere create con `Calculation` Le colonne sono quasi illimitate, ma la maggior parte delle colonne può essere creata utilizzando le istruzioni IF-THEN e l&#39;aritmetica di base, utilizzata negli esempi seguenti.

**Esempio 1: ultimo ordine del cliente?**

La maggior parte degli account dispone di una colonna denominata `Is customer's last order?` sul loro `orders` tabella per eseguire analisi sui tassi di acquisto ripetuti e sui clienti abbandonati. Se l’account si trova nella nuova architettura, questa colonna viene creata utilizzando una `Calculation` e possono essere visualizzati nella schermata seguente:

![](../../assets/Is_customer_s_last_order.png)

Il `Is customer's last order?` utilizza gli input `Customer's lifetime number of orders` e `Customer's order number` alias come `A` e `B` rispettivamente.

Riga per riga, il significato di PostgreSQL è:

* caso: inizia una serie di istruzioni If - Then
* quando `A` è nullo o `B` is null then null: se uno dei due input è vuoto, anche l’output deve essere vuoto. In questo modo si evitano errori SQL
* quando `A=B` allora `Yes`: Se `Customer's lifetime number of orders` è uguale a `Customer's order number` per questa riga, quindi restituisce `Yes`. Quindi, se un cliente ha effettuato quattro ordini, la riga per il quarto ordine restituirà `Yes` per `Is customer's last order?`
* else `No`: se non viene soddisfatta nessuna delle altre istruzioni, restituisce `No`
* end: termina le istruzioni If - Then

I possibili valori restituibili da questa colonna (`NULL`, `Yes`, `No`) contengono caratteri non numerici, pertanto il tipo di dati qui è String.

**Esempio 2: valore totale articolo ordine (quantità * prezzo)**

A molti clienti piace analizzare i ricavi a livello di elemento, suddividendoli in campi come `product name` o `category`. La maggior parte dei database non fornisce effettivamente i ricavi di un prodotto in un ordine, ma fornisce la quantità venduta nell&#39;ordine e il prezzo dell&#39;articolo.

Per abilitare l’analisi dei ricavi dei prodotti, la maggior parte dei conti ha una colonna denominata `Order item total value (quantity * price)` sul loro `Orders Items` tabella. Se l’account si trova nella nuova architettura, questa colonna viene creata anche utilizzando una `Calculation` e possono essere visualizzati nella schermata seguente:

![](../../assets/Order_item_total_value.png)

Nello schema Commerce, la `Order item total value (quantity * price)` utilizza gli input `qty ordered` e `base price` alias come `A` e `B` rispettivamente.

I valori restituiti da questa nuova colonna sono espressi in dollari e centesimi, pertanto il tipo di dati corretto è `Decimal(10,2)`.

**Meccanica**

Una nuova `Calculation` può essere aggiunta a una tabella passando a **[!DNL Manage Data > Data Warehouse]** come mostrato di seguito:

![](../../assets/blobid2.png)

Da qui puoi creare una `Calculation` seguendo i passaggi seguenti:

1. Seleziona la tabella a cui desideri aggiungere il `Calculation` colonna.
1. Nella tabella corretta, fai clic su **[!UICONTROL Create New Column]** in alto a destra.
1. Dalla sezione `Select a definition` a discesa, seleziona `Same Table`.
1. Seleziona `Calculation` come `column definition equation`.
1. Immettere il nome della colonna.
1. Scegli la `input` colonne della tabella utilizzate nella logica per la nuova colonna. Ogni colonna aggiunta ottiene un alias di lettera, pertanto la prima colonna è `A`, il secondo è `B` e così via.
1. Nella finestra, digita la logica PostgreSQL per la nuova colonna utilizzando gli alias delle lettere degli input. Il calcolo SQL deve essere limitato a una singola definizione di colonna, inclusa tutta la logica tra le istruzioni SELECT e FROM di una query SQL. Le parole chiave SQL che utilizzano una qualsiasi delle lettere di input devono essere in minuscolo. Ad esempio, quando si utilizza `CASE` , deve essere scritto in minuscolo - `case`. Il sistema presuppone che le lettere maiuscole `A` si riferisce a uno degli input.
1. Scegli il tipo di dati appropriato.
   * `Integer` - Numero intero
   * `Decimal(10,2)` - un numero decimale composto da dieci cifre totali, di cui due a destra del separatore decimale
   * `String` - Qualsiasi tipo di testo o serie di caratteri che non utilizzano numeri
   * `Datetime` - `yyyy-MM-dd hh:mm:ss` formato

1. Clic **[!UICONTROL test column]**. In questo modo viene generato un elenco di cinque valori di test per ogni input e viene visualizzato il risultato della logica del passaggio 6 per ogni set di valori di test. Se una parte qualsiasi dell&#39;istruzione SQL genera un errore, viene restituito il messaggio di errore appropriato. I risultati di esempio possono essere generati solo se tutte le colonne di input sono campi nativi. Se una delle colonne di input è una colonna calcolata, devi convalidarne i risultati aggiungendo la colonna a una metrica e visualizzandola nel Report Builder visivo

1. Quando si è soddisfatti dei risultati, fare clic su **[!UICONTROL Save]**. La colonna è abilitata per l’uso.
