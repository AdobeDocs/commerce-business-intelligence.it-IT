---
title: Configurazione dei metodi di replica
description: Scopri come sono organizzate le tabelle e come si comportano i dati delle tabelle, per scegliere il metodo di replica migliore per le tabelle.
exl-id: 83895c48-a6ec-4b01-9890-164e0b21dcbc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Data Import/Export
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 0%

---

# Configurazione dei metodi di replica

I metodi `Replication` e le [verifiche](../data-warehouse-mgr/cfg-data-rechecks.md) vengono utilizzati per identificare dati nuovi o aggiornati nelle tabelle del database. Impostarle correttamente è fondamentale per garantire sia la precisione dei dati che tempi di aggiornamento ottimizzati. Questo argomento si concentra sui metodi di replica.

Quando vengono sincronizzate nuove tabelle in [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md), viene scelto automaticamente un metodo di replica per la tabella. I vari metodi di replica, l&#39;organizzazione delle tabelle e il comportamento dei dati delle tabelle consentono di scegliere il metodo di replica più adatto alle tabelle.

## Quali sono i metodi di replica?

I metodi `Replication` rientrano in tre gruppi: `Incremental`, `Full Table` e `Paused`.

[**[!UICONTROL Incremental Replication]**](#incremental) significa che [!DNL Commerce Intelligence] replica solo dati nuovi o aggiornati a ogni tentativo di replica. Poiché questi metodi riducono notevolmente la latenza, Adobe consiglia di utilizzarla ove possibile.

[**[!UICONTROL Full Table Replication]**](#fulltable) significa che [!DNL Commerce Intelligence] replica l&#39;intero contenuto di una tabella a ogni tentativo di replica. A causa della quantità potenzialmente elevata di dati da replicare, questi metodi possono aumentare la latenza e i tempi di aggiornamento. Se una tabella contiene colonne con marca temporale o datetime, Adobe consiglia di utilizzare un metodo Incremental.

**[!UICONTROL Paused]** indica che la replica per la tabella è stata interrotta o sospesa. [!DNL Commerce Intelligence] non verifica la presenza di dati nuovi o aggiornati durante un ciclo di aggiornamento. Ciò significa che non viene replicato alcun dato da una tabella con questo metodo di replica.

## Metodi di replica incrementali {#incremental}

### Modificato a (più ideale)

Il metodo di replica `Modified At` utilizza una colonna datetime, che viene compilata quando si crea e quindi si aggiorna una riga in seguito alla modifica dei dati, per trovare i dati da replicare. Questo metodo è progettato per l&#39;utilizzo con tabelle che soddisfano i seguenti criteri:

* contiene una colonna `datetime` che viene inizialmente compilata al momento della creazione di una riga e viene aggiornata ogni volta che la riga viene modificata;
* la colonna `datetime` non è mai null;
* righe non eliminate dalla tabella

Oltre a questi criteri, Adobe consiglia di **indicizzare** la colonna `datetime` utilizzata per la replica `Modified At`, in quanto consente di ottimizzare la velocità di replica.

Durante l&#39;esecuzione dell&#39;aggiornamento, i dati nuovi o modificati vengono identificati ricercando le righe con un valore nella colonna `datetime` che si è verificato dopo l&#39;aggiornamento più recente. Quando vengono rilevate nuove righe, queste vengono replicate nel Data Warehouse. Le eventuali righe presenti in [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md) vengono sovrascritte con i valori di database correnti.

Ad esempio, una tabella può avere una colonna denominata `modified\_at` che indica l&#39;ultima modifica dei dati. Se l&#39;aggiornamento più recente è stato eseguito martedì a mezzogiorno, verranno cercate tutte le righe con un valore `modified\_at` maggiore di martedì a mezzogiorno. Tutte le righe individuate create o modificate a partire da mezzogiorno di martedì vengono replicate in Data Warehouse.

**Lo sapevi?**
Anche se il database non supporta attualmente un metodo di replica di `Incremental`, è possibile [apportare modifiche al database](../../best-practices/mod-db-inc-replication.md) che consentirebbero l&#39;utilizzo di `Modified At` o `Single Auto Incrementing PK`.

`Modified At` non è solo il metodo di replica più ideale, ma anche il più veloce. Questo metodo non solo produce un notevole aumento di velocità con set di dati di grandi dimensioni, ma non richiede anche la configurazione di un&#39;opzione di ricontrollo. Altri metodi devono scorrere un&#39;intera tabella per identificare le modifiche, anche se è stato modificato un piccolo sottoinsieme di dati. `Modified At` esegue l&#39;iterazione solo di quel piccolo sottoinsieme.

### Singola chiave primaria con incremento automatico

`Auto Incrementing` è un comportamento che assegna in sequenza le chiavi primarie alle righe. Se una tabella è `Auto Incrementing` e la chiave primaria più alta della tabella è 1.000, il valore primario successivo è 1.001 o superiore. Una tabella che non utilizza il comportamento `Auto Incrementing` può assegnare un valore di chiave primaria inferiore a 1.000 o passare a un numero molto più grande, ma questo valore non viene comunemente utilizzato.

Questo metodo è progettato per replicare nuovi dati da tabelle che soddisfano i seguenti criteri:

* `single-column primary key`; e
* Il tipo di dati `primary key` è `integer`; e
* `auto incrementing` valori chiave primaria.

Quando una tabella utilizza la replica di `Single Auto Incrementing Primary Key`, i nuovi dati vengono rilevati ricercando valori di chiave primaria superiori al valore massimo corrente nel Data Warehouse. Ad esempio, se il valore di chiave primaria più alto nel Data Warehouse è 500, quando viene eseguito l’aggiornamento successivo verranno cercate le righe con valori di chiave primaria pari o superiori a 501.

### Aggiungi data

Il metodo `Add Date` funziona in modo simile al metodo `Single Auto Incrementing Primary Key`. Invece di utilizzare un numero intero per la chiave primaria della tabella, questo metodo utilizza una colonna `timestamped` per verificare la presenza di nuove righe.

Quando una tabella utilizza la replica `Add Date`, i nuovi dati vengono rilevati ricercando valori con marca temporale maggiori dell&#39;ultima data sincronizzata nel Data Warehouse. Ad esempio, se l’ultimo aggiornamento è stato eseguito il 20/12/2015 09:00:00, tutte le righe con una marca temporale maggiore di questa verranno contrassegnate come nuovi dati e replicate.

>[!NOTE]
>
>A differenza del metodo `Modified At`, `Add Date` non controlla le righe esistenti per ottenere informazioni aggiornate, ma cerca solo le nuove righe.

## Metodi di replica a tabella completa {#fulltable}

### Tabella completa

La replica di `Full table` aggiorna l&#39;intera tabella ogni volta che vengono rilevate nuove righe. Questo è di gran lunga il metodo di replica meno efficiente, perché tutti i dati devono essere rielaborati durante ogni aggiornamento, supponendo che vi siano nuove righe.

Le nuove righe vengono rilevate eseguendo una query nel database all&#39;inizio del processo di sincronizzazione e contando il numero di righe. Se il database locale contiene più righe di [!DNL Commerce Intelligence], la tabella verrà aggiornata. Se i conteggi delle righe sono identici o se [!DNL Commerce Intelligence] contiene *più* righe rispetto al database locale, la tabella verrà ignorata.

Ciò solleva il punto importante che la replica di **`Full Table`non è compatibile quando:**

* vengono eliminate più righe di quelle create nella tabella del database locale tra i cicli di aggiornamento successivi, oppure
* i valori di colonna vengono modificati, ma non vengono create righe aggiuntive

In uno degli scenari sopra indicati, la replica di `Full Table` non rileva alcuna modifica e i dati diventano obsoleti. A causa dell&#39;inefficienza di questo metodo di replica e dei requisiti indicati in precedenza, la replica di `Full Table` è consigliata solo come ultima risorsa.

### Batch chiave primaria

Quando una tabella utilizza `Primary Key Batch` (batch PK), i nuovi dati vengono rilevati contando le righe all&#39;interno di intervalli, o batch, di valori di chiave primaria. Anche se in genere questo viene utilizzato con numeri interi, anche i valori di testo possono essere ordinati in modo da consentire al sistema di definire intervalli costanti.

Ad esempio, supponiamo che un aggiornamento esegua ed esegua un conteggio di righe per l’intervallo di chiavi da 1 a 100. In questo aggiornamento, il sistema trova e registra 37 righe. Nel prossimo aggiornamento, viene eseguito di nuovo un conteggio di righe sull’intervallo 1-100 e trova 41 righe. Poiché esiste una differenza nel numero di righe rispetto all’ultimo aggiornamento, il sistema controlla tale intervallo (o batch) in modo più dettagliato.

Questo metodo ha lo scopo di replicare i dati da tabelle che soddisfano i seguenti criteri:

* non intero a colonna singola; o
* chiavi composite (più colonne che includono la chiave primaria): le colonne utilizzate in una chiave primaria composita non possono mai avere valori null; oppure
* valori di chiave primaria a colonna singola, numero intero, senza incremento automatico.

Questo metodo non è ideale, in quanto è incredibilmente lento a causa della quantità di elaborazione che deve verificarsi per esaminare i batch e trovare le modifiche. Adobe consiglia di non utilizzare questo metodo, a meno che non sia impossibile apportare le modifiche necessarie per supportare gli altri metodi di replica. Se è necessario utilizzare questo metodo, i tempi di aggiornamento dovrebbero aumentare.

## Impostazione dei metodi di replica

I metodi di replica sono impostati tabella per tabella. Per impostare un metodo di replica per una tabella, sono necessarie le autorizzazioni [`Admin`](../../administrator/user-management/user-management.md) per accedere a Data Warehouse Manager.

1. Una volta in Data Warehouse Manager, selezionare la tabella dall&#39;elenco `Synced Tables` per visualizzare lo schema della tabella.
1. Il metodo di replica corrente è elencato sotto il nome della tabella. Per modificarlo, fai clic sul collegamento.
1. Nel popup visualizzato, fare clic sul pulsante di opzione accanto alla replica `Incremental` o `Full Table` per selezionare un tipo di replica.
1. Fare quindi clic sul menu a discesa **[!UICONTROL Replication Method]** per selezionare un metodo. Ad esempio, `Paused` o `Modified At`.

   >[!NOTE]
   >
   >**Alcuni metodi incrementali richiedono l&#39;impostazione di`Replication Key`**. [!DNL Commerce Intelligence] utilizzerà questa chiave per determinare dove deve iniziare il prossimo ciclo di aggiornamento.
   >
   >Se ad esempio si desidera utilizzare il metodo `modified at` per la tabella `orders`, è necessario impostare `date column` come chiave di replica. Possono esistere diverse opzioni per le chiavi di replica, ma si seleziona `created at` o l&#39;ora di creazione dell&#39;ordine. Se l&#39;ultimo ciclo di aggiornamento si interrompe alle 12/1/2015 00:10:00, il ciclo successivo inizierà a replicare i dati con una data `created at` successiva a questa.

1. Al termine, fare clic su **[!UICONTROL Save]**.

Osservare l&#39;intero processo:

![](../../assets/replication_method.gif)<!--{: width="801" height="341"}-->

## Ritorno a capo

Per terminare, avete creato questa tabella che confronta i vari metodi di replica. È estremamente utile quando si seleziona un metodo per le tabelle nel Data Warehouse.

| **`Method`** | **`Syncing New Data`** | **`Processing Rechecks on Large Data Sets`** | **`Handle Composite Keys?`** | **`Handle Non-Integer PKs?`** | **`Handle Non-Sequential PK Population?`** | **`Handle Row Deletion?`** |
|-----|-----|-----|-----|-----|-----|-----|
| `Auto-Incrementing Primary Key` | Più veloce | Lento | No | No | No | Sì |
| `Primary Key Batch Monitoring` | Lento | Lento | Sì | Sì | Sì | Sì |
| `Modified At` | Più veloce | Più veloce | Sì | Sì | Sì | No |

{style="table-layout:auto"}

## Documentazione correlata

* [Ricontrolli dei dati](../data-warehouse-mgr/cfg-data-rechecks.md)
* [Modifica del database per supportare ](../../best-practices/mod-db-inc-replication.md)
* [Ottimizzazione del database per l&#39;analisi](../../best-practices/opt-db-analysis.md)
* [Riduzione dei tempi di aggiornamento](../../best-practices/reduce-update-cycle-time.md)
