---
title: Configurazione dei metodi di replica
description: Scopri come sono organizzate le tabelle e come si comportano i dati delle tabelle per consentirti di scegliere il metodo di replica migliore per le tabelle.
exl-id: 83895c48-a6ec-4b01-9890-164e0b21dcbc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1455'
ht-degree: 0%

---

# Configurazione dei metodi di replica

`Replication` metodi e [ricontrollo](../data-warehouse-mgr/cfg-data-rechecks.md) vengono utilizzati per identificare i dati nuovi o aggiornati nelle tabelle del database. La loro corretta impostazione è fondamentale per garantire sia l’accuratezza dei dati che i tempi di aggiornamento ottimizzati. In questo articolo, ci concentreremo solo sui metodi di replica.

Quando le nuove tabelle vengono sincronizzate in Data Warehouse Manager, viene automaticamente scelto un metodo di replica per la tabella. Comprendere i vari metodi di replica, le modalità di organizzazione delle tabelle e il funzionamento dei dati delle tabelle ti consentirà di scegliere il metodo di replica migliore per le tabelle.

## Quali sono i metodi di replica?

`Replication` i metodi rientrano in tre gruppi - `Incremental`, `Full Table`e `Paused`.

[**[!UICONTROL Incremental Replication]**](#incremental) significa che [!DNL MBI] replicherà solo dati nuovi o aggiornati a ogni tentativo di replica. Poiché questi metodi ridurranno notevolmente la latenza, si consiglia vivamente di utilizzarli laddove possibile.

[**[!UICONTROL Full Table Replication]**](#fulltable) significa che [!DNL MBI] replicherà l’intero contenuto di una tabella a ogni tentativo di replica. A causa della quantità potenzialmente elevata di dati da replicare, questi metodi possono aumentare la latenza e i tempi di aggiornamento. Se una tabella contiene colonne con marca temporale o datetime, è consigliabile utilizzare un metodo Incremental.

**[!UICONTROL Paused]** indica che la replica per la tabella viene interrotta o sospesa. [!DNL MBI] non controlla dati nuovi o aggiornati durante un ciclo di aggiornamento; ciò significa che non verranno replicati dati da una tabella con questo metodo di replica.

## Metodi di replica incrementale {#incremental}

### Modificato a (più ideale)

La `Modified At` il metodo di replica utilizza una colonna datetime , popolata quando viene creata una riga e quindi aggiornata quando i dati cambiano, per trovare i dati da replicare. Questo metodo è progettato per lavorare con tabelle che soddisfano i seguenti criteri:

* contiene `datetime` colonna che viene compilata inizialmente quando viene creata una riga e viene aggiornata ogni volta che la riga viene modificata;
* la `datetime` la colonna non è mai nulla;
* le righe non vengono eliminate dalla tabella

Oltre a questi criteri, raccomandiamo vivamente **indicizzazione** la `datetime` colonna utilizzata per `Modified At` la replica, in quanto ciò aiuterà a ottimizzare la velocità di replica.

Quando viene eseguito l’aggiornamento, i dati nuovi o modificati vengono identificati ricercando le righe che hanno un valore nel `datetime` che si è verificato dopo l’aggiornamento più recente. Quando vengono scoperte nuove righe, queste vengono replicate nella tua Data Warehouse. Se nella Data Warehouse sono già presenti righe, queste verranno sovrascritte con i valori del database correnti.

Ad esempio, una tabella può avere una colonna denominata `modified\_at` indica che i dati dell’ultima volta sono stati modificati. Se l&#39;aggiornamento più recente è stato eseguito martedì a mezzogiorno, l&#39;aggiornamento cercherà tutte le righe che hanno un `modified\_at` valore maggiore di martedì a mezzogiorno. Tutte le righe scoperte create o modificate da martedì a mezzogiorno verranno replicate nella Data Warehouse.

**Lo sapevi?**
Anche se il database non supporta attualmente un `Incremental` Metodo di replica, potresti essere in grado di [apportare alcune modifiche al database](../../best-practices/mod-db-inc-replication.md) che consenta l&#39;uso `Modified At` o `Single Auto Incrementing PK`.

`Modified At` non è solo il metodo di replica più ideale, è anche il più veloce. Questo metodo non solo produce aumenti di velocità notevoli con grandi set di dati, ma non richiede anche la configurazione di un&#39;opzione di ricontrollo. Altri metodi dovranno eseguire iterazioni su un’intera tabella per identificare le modifiche, anche se è stato modificato un piccolo sottoinsieme di dati. `Modified At` attraversa solo quel piccolo sottoinsieme.

### Chiave principale incrementale automatico singolo

`Auto Incrementing` è un comportamento che assegna in sequenza le chiavi primarie alle righe. Se una tabella è `Auto Incrementing` e la chiave primaria più alta nella tabella è attualmente 1000, quindi il valore principale successivo sarà 1001 o superiore. Tabella che non utilizza `Auto Incrementing` può assegnare un valore di chiave primaria inferiore a 1000 o passare a un numero molto più grande, ma non viene comunemente utilizzato.

Questo metodo è progettato per replicare nuovi dati da tabelle che soddisfano i seguenti criteri:

* `single-column primary key`; e
* `primary key` tipo di dati `integer`; e
* `auto incrementing` valori di chiave primaria.

Quando una tabella utilizza `Single Auto Incrementing Primary Key` replica, nuovi dati vengono rilevati ricercando valori chiave principali superiori al valore corrente più alto nella Data Warehouse. Ad esempio, se il valore della chiave primaria più alto nella tua Data Warehouse è 500, quando viene eseguito l’aggiornamento successivo cerca le righe con valori di chiave primaria pari o superiori a 501.

### Aggiungi data

La `Add Date` funzioni del metodo simili a `Single Auto Incrementing Primary Key` metodo . Invece di utilizzare un numero intero per la chiave primaria della tabella, questo metodo utilizzerà un valore `timestamped` per verificare la presenza di nuove righe.

Quando una tabella utilizza `Add Date` replica, nuovi dati vengono rilevati ricercando valori con marca temporale maggiori della data più recente sincronizzata con la Data Warehouse. Ad esempio, se un aggiornamento è stato eseguito l’ultima volta il 20/12/2015 09:00:00, tutte le righe con una marca temporale maggiore di questa verranno contrassegnate come nuovi dati e replicate.

>[!NOTE]
>
>A differenza di `Modified At` metodo, `Add Date` non controllerà le righe esistenti per le informazioni aggiornate, ma solo le nuove righe.

## Metodi di replica completi delle tabelle {#fulltable}

### Tabella completa

`Full table` la replica aggiorna l’intera tabella ogni volta che vengono rilevate nuove righe. Questo è di gran lunga il metodo di replica meno efficiente, dal momento che tutti i dati devono essere rielaborati durante ogni aggiornamento, supponendo che ci siano nuove righe.

Vengono rilevate nuove righe eseguendo una query sul database all&#39;inizio del processo di sincronizzazione e contando il numero di righe. Se il database locale contiene più righe di [!DNL MBI], la tabella viene aggiornata. Se i conteggi delle righe sono identici o se [!DNL MBI] contiene *more* rispetto al database locale, la tabella viene ignorata.

Ciò solleva l&#39;importante punto che **`Full Table`la replica è incompatibile quando:**

* tra i cicli di aggiornamento successivi vengono eliminate più righe di quelle create nella tabella di database locale, oppure
* i valori delle colonne vengono modificati, ma non vengono create righe aggiuntive

In uno dei due scenari di cui sopra, `Full Table` la replica non rileverà alcuna modifica e i tuoi dati diventeranno obsoleti. A causa dell&#39;inefficienza di questo metodo di replica e dei requisiti di cui sopra, `Full Table` la replica è consigliata solo come ultima risorsa.

### Batch chiavi principale

Quando una tabella utilizza `Primary Key Batch` (Batch PK), i nuovi dati vengono rilevati contando le righe all’interno di intervalli o batch di valori chiave principali. Anche se tipicamente pensiamo che questo venga utilizzato con i numeri interi, anche i valori di testo possono essere ordinati in modo da consentire al sistema di definire intervalli costanti.

Ad esempio, supponiamo che un aggiornamento venga eseguito ed esegua un conteggio di righe per l’intervallo di chiavi da 1 a 100. In questo aggiornamento, il sistema trova e registra 37 righe. Nell’aggiornamento successivo, viene eseguito di nuovo un conteggio di righe sull’intervallo 1-100 e individua 41 righe. Poiché c&#39;è una differenza nel numero di righe rispetto all&#39;ultimo aggiornamento, il sistema controllerà tale intervallo (o batch) in modo più dettagliato.

Questo metodo ha lo scopo di replicare i dati provenienti da tabelle che soddisfano i seguenti criteri:

* non intero a colonna singola; o
* chiavi composite (più colonne comprendenti la chiave primaria): le colonne utilizzate in una chiave primaria composita non possono mai avere valori nulli; o
* i valori della chiave primaria a una colonna, un numero intero e senza incremento automatico.

Questo metodo non è ideale, in quanto è incredibilmente lento a causa della quantità di elaborazione che deve verificarsi per esaminare batch e trovare modifiche. È consigliabile utilizzare questo metodo solo se non è possibile apportare le modifiche necessarie per supportare gli altri metodi di replica. Se è necessario utilizzare questo metodo, è previsto un aumento dei tempi di aggiornamento.

## Impostazione dei metodi di replica

I metodi di replica sono impostati per tabella. Per impostare un metodo di replica per una tabella, è necessario [`Admin`](../../administrator/user-management/user-management.md) autorizzazioni per accedere a Data Warehouse Manager.

1. Una volta in Gestione Date Warehouse, seleziona la tabella dal `Synced Tables` elenco per visualizzare lo schema della tabella.
1. Il metodo di replica corrente è elencato sotto il nome della tabella. Per modificarlo, fai clic sul collegamento.
1. Nella finestra a comparsa visualizzata, fai clic sul pulsante di scelta accanto a `Incremental` o `Full Table` replica per selezionare un tipo di replica.
1. Fai clic su **[!UICONTROL Replication Method]** menu a discesa per selezionare un metodo, ad esempio `Paused` o `Modified At`.

   >[!NOTE]
   >
   >**Alcuni metodi Incremental richiedono di impostare un`Replication Key`**. [!DNL MBI] utilizzerà questa chiave per determinare dove deve iniziare il prossimo ciclo di aggiornamento.
   >
   >Ad esempio, se desideri utilizzare il `modified at` metodo per `orders` tabella, dobbiamo impostare un `date column` come chiave di replica. Possono esistere diverse opzioni per le chiavi di replica, ma selezioneremo `created at`o l’ora in cui è stato creato l’ordine. Se l&#39;ultimo ciclo di aggiornamento si è arrestato al 12/1/2015 00:10:00, il ciclo successivo inizierebbe a replicare i dati con un `created at` data maggiore di questa.

1. Al termine, fai clic su **[!UICONTROL Save]**.

Date un&#39;occhiata all&#39;intero processo:

![](../../assets/replication_method.gif)<!--{: width="801" height="341"}-->

## Ritorno a capo

Per concludere, abbiamo messo insieme questa tabella che confronta i vari metodi di replica. Lo troviamo incredibilmente utile quando scegliamo un metodo per le tabelle nel nostro data warehouse.

| **`Method`** | **`Syncing New Data`** | **`Processing Rechecks on Large Data Sets`** | **`Handle Composite Keys?`** | **`Handle Non-Integer PKs?`** | **`Handle Non-Sequential PK Population?`** | **`Handle Row Deletion?`** |
|-----|-----|-----|-----|-----|-----|-----|
| `Auto-Incrementing Primary Key` | Più veloce | Lento | No | No | No | Sì |
| `Primary Key Batch Monitoring` | Lento | Lento | Sì | Sì | Sì | Sì |
| `Modified At` | Più veloce | Più veloce | Sì | Sì | Sì | No |

{style=&quot;table-layout:auto&quot;}

## Documentazione correlata

* [Informazioni sui controlli dei dati](../data-warehouse-mgr/cfg-data-rechecks.md)
* [Modifica del database per supportare ](../../best-practices/mod-db-inc-replication.md)
* [Ottimizzazione del database per l’analisi](../../best-practices/opt-db-analysis.md)
* [Riduzione dei tempi di aggiornamento](../../best-practices/reduce-update-cycle-time.md)
