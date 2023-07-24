---
title: Configurazione dei metodi di replica
description: Scopri come sono organizzate le tabelle e come si comportano i dati delle tabelle, per scegliere il metodo di replica migliore per le tabelle.
exl-id: 83895c48-a6ec-4b01-9890-164e0b21dcbc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Data Import/Export
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1414'
ht-degree: 0%

---

# Configurazione dei metodi di replica

`Replication` metodi e [ricontrolli](../data-warehouse-mgr/cfg-data-rechecks.md) vengono utilizzati per identificare dati nuovi o aggiornati nelle tabelle del database. Impostarle correttamente è fondamentale per garantire sia la precisione dei dati che tempi di aggiornamento ottimizzati. Questo argomento si concentra sui metodi di replica.

Quando vengono sincronizzate nuove tabelle in [Gestione Date Warehouse](../data-warehouse-mgr/tour-dwm.md), viene scelto automaticamente un metodo di replica per la tabella. I vari metodi di replica, l&#39;organizzazione delle tabelle e il comportamento dei dati delle tabelle consentono di scegliere il metodo di replica più adatto alle tabelle.

## Quali sono i metodi di replica?

`Replication` i metodi sono suddivisi in tre gruppi: `Incremental`, `Full Table`, e `Paused`.

[**[!UICONTROL Incremental Replication]**](#incremental) significa che [!DNL Commerce Intelligence] replica solo i dati nuovi o aggiornati a ogni tentativo di replica. Poiché questi metodi riducono notevolmente la latenza, Adobe consiglia di utilizzarla ove possibile.

[**[!UICONTROL Full Table Replication]**](#fulltable) significa che [!DNL Commerce Intelligence] replica l’intero contenuto di una tabella a ogni tentativo di replica. A causa della quantità potenzialmente elevata di dati da replicare, questi metodi possono aumentare la latenza e i tempi di aggiornamento. Se una tabella contiene colonne con marca temporale o datetime, l&#39;Adobe consiglia di utilizzare un metodo Incremental.

**[!UICONTROL Paused]** indica che la replica per la tabella viene interrotta o sospesa. [!DNL Commerce Intelligence] non verifica la presenza di dati nuovi o aggiornati durante un ciclo di aggiornamento; ciò significa che non viene replicato alcun dato da una tabella che ha questo come metodo di replica.

## Metodi di replica incrementali {#incremental}

### Modificato a (più ideale)

Il `Modified At` per trovare i dati da replicare, il metodo di replica utilizza una colonna datetime, che viene compilata quando si crea e quindi si aggiorna una riga in seguito alla modifica dei dati. Questo metodo è progettato per l&#39;utilizzo con tabelle che soddisfano i seguenti criteri:

* contiene un `datetime` colonna che viene inizialmente compilata al momento della creazione di una riga e che viene aggiornata ogni volta che la riga viene modificata;
* il `datetime` la colonna non è mai null;
* righe non eliminate dalla tabella

Oltre a tali criteri, l&#39;Adobe raccomanda **indicizzazione** il `datetime` colonna utilizzata per `Modified At` la replica, in quanto consente di ottimizzare la velocità di replica.

Durante l’esecuzione dell’aggiornamento, i dati nuovi o modificati vengono identificati ricercando le righe con un valore in `datetime` che si è verificata dopo l’aggiornamento più recente. Quando vengono rilevate nuove righe, queste vengono replicate nella Data Warehouse. Se sono presenti righe in [Gestione Date Warehouse](../data-warehouse-mgr/tour-dwm.md), vengono sovrascritti con i valori correnti del database.

Ad esempio, una tabella può avere una colonna denominata `modified\_at` indica l’ultima modifica apportata ai dati. Se l’aggiornamento più recente è stato eseguito martedì a mezzogiorno, vengono cercate tutte le righe con `modified\_at` maggiore di martedì a mezzogiorno. Tutte le righe individuate che sono state create o modificate a partire da mezzogiorno di martedì vengono replicate nella Data Warehouse.

**Lo sapevate?**
Anche se il database non supporta attualmente un `Incremental` metodo di replica, è possibile: [apportare modifiche al database](../../best-practices/mod-db-inc-replication.md) che consentirebbe l&#39;uso di `Modified At` o `Single Auto Incrementing PK`.

`Modified At` non è solo il metodo di replica più ideale, ma anche il più veloce. Questo metodo non solo produce un notevole aumento di velocità con set di dati di grandi dimensioni, ma non richiede anche la configurazione di un&#39;opzione di ricontrollo. Altri metodi devono scorrere un&#39;intera tabella per identificare le modifiche, anche se è stato modificato un piccolo sottoinsieme di dati. `Modified At` scorre solo quel piccolo sottoinsieme.

### Singola chiave primaria con incremento automatico

`Auto Incrementing` è un comportamento che assegna in sequenza le chiavi primarie alle righe. Se una tabella è `Auto Incrementing` e la chiave primaria più alta nella tabella è 1.000, quindi il valore primario successivo è 1.001 o superiore. Una tabella che non utilizza `Auto Incrementing` Questo comportamento può assegnare un valore di chiave primaria inferiore a 1.000 o passare a un numero molto più grande, ma non è comunemente utilizzato.

Questo metodo è progettato per replicare nuovi dati da tabelle che soddisfano i seguenti criteri:

* `single-column primary key`; e
* `primary key` tipo di dati è `integer`; e
* `auto incrementing` valori della chiave primaria.

Quando una tabella utilizza `Single Auto Incrementing Primary Key` replica, i nuovi dati vengono rilevati ricercando valori di chiave primaria superiori al valore massimo corrente nella Data Warehouse. Se ad esempio il valore di chiave primaria più alto nella Data Warehouse è 500, quando viene eseguito l&#39;aggiornamento successivo verranno cercate le righe con valori di chiave primaria pari o superiori a 501.

### Aggiungi data

Il `Add Date` funziona in modo simile al `Single Auto Incrementing Primary Key` metodo. Invece di utilizzare un numero intero per la chiave primaria della tabella, questo metodo utilizza un valore `timestamped` per verificare la presenza di nuove righe.

Quando una tabella utilizza `Add Date` replica, i nuovi dati vengono rilevati ricercando valori con marca temporale superiori all’ultima data sincronizzata nella Data Warehouse. Ad esempio, se l’ultimo aggiornamento è stato eseguito il 20/12/2015 09:00:00, tutte le righe con una marca temporale maggiore di questa verranno contrassegnate come nuovi dati e replicate.

>[!NOTE]
>
>A differenza della `Modified At` metodo, `Add Date` non controlla le righe esistenti per informazioni aggiornate, ma cerca solo nuove righe.

## Metodi di replica a tabella completa {#fulltable}

### Tabella completa

`Full table` la replica aggiorna l&#39;intera tabella ogni volta che vengono rilevate nuove righe. Questo è di gran lunga il metodo di replica meno efficiente, perché tutti i dati devono essere rielaborati durante ogni aggiornamento, supponendo che vi siano nuove righe.

Le nuove righe vengono rilevate eseguendo una query nel database all&#39;inizio del processo di sincronizzazione e contando il numero di righe. Se il database locale contiene più righe di [!DNL Commerce Intelligence], la tabella viene aggiornata. Se i conteggi delle righe sono identici o se [!DNL Commerce Intelligence] contiene *altro* rispetto al database locale, la tabella viene ignorata.

Ciò solleva l&#39;importante questione che **`Full Table`la replica non è compatibile quando:**

* vengono eliminate più righe di quelle create nella tabella del database locale tra i cicli di aggiornamento successivi, oppure
* i valori di colonna vengono modificati, ma non vengono create righe aggiuntive

In uno degli scenari sopra indicati, `Full Table` la replica non rileva alcuna modifica e i dati diventano obsoleti. A causa dell&#39;inefficienza di questo metodo di replica e dei requisiti di cui sopra, `Full Table` la replica è consigliata solo come ultima risorsa.

### Batch chiave primaria

Quando una tabella utilizza `Primary Key Batch` (Batch PK), i nuovi dati vengono rilevati contando le righe all’interno di intervalli, o batch, di valori di chiave primaria. Anche se in genere questo viene utilizzato con numeri interi, anche i valori di testo possono essere ordinati in modo da consentire al sistema di definire intervalli costanti.

Ad esempio, supponiamo che un aggiornamento esegua ed esegua un conteggio di righe per l’intervallo di chiavi da 1 a 100. In questo aggiornamento, il sistema trova e registra 37 righe. Nel prossimo aggiornamento, viene eseguito di nuovo un conteggio di righe sull’intervallo 1-100 e trova 41 righe. Poiché esiste una differenza nel numero di righe rispetto all’ultimo aggiornamento, il sistema controlla tale intervallo (o batch) in modo più dettagliato.

Questo metodo ha lo scopo di replicare i dati da tabelle che soddisfano i seguenti criteri:

* non intero a colonna singola; o
* chiavi composite (più colonne che includono la chiave primaria): le colonne utilizzate in una chiave primaria composita non possono mai avere valori null; oppure
* valori di chiave primaria a colonna singola, numero intero, senza incremento automatico.

Questo metodo non è ideale, in quanto è incredibilmente lento a causa della quantità di elaborazione che deve verificarsi per esaminare i batch e trovare le modifiche. L’Adobe consiglia di non utilizzare questo metodo, a meno che non sia impossibile apportare le modifiche necessarie per supportare gli altri metodi di replica. Se è necessario utilizzare questo metodo, i tempi di aggiornamento dovrebbero aumentare.

## Impostazione dei metodi di replica

I metodi di replica sono impostati tabella per tabella. Per impostare un metodo di replica per una tabella, è necessario [`Admin`](../../administrator/user-management/user-management.md) in modo da poter accedere a Data Warehouse Manager.

1. Una volta in Gestione Date Warehouse, selezionare la tabella dal menu `Synced Tables` per visualizzare lo schema della tabella.
1. Il metodo di replica corrente è elencato sotto il nome della tabella. Per modificarlo, fai clic sul collegamento.
1. Nel pop-up visualizzato, fai clic sul pulsante di opzione accanto a `Incremental` o `Full Table` per selezionare un tipo di replica.
1. Quindi, fai clic su **[!UICONTROL Replication Method]** per selezionare un metodo. Ad esempio: `Paused` o `Modified At`.

   >[!NOTE]
   >
   >**Alcuni metodi incrementali richiedono l&#39;impostazione di un`Replication Key`**. [!DNL Commerce Intelligence] utilizzerà questa chiave per determinare dove deve iniziare il ciclo di aggiornamento successivo.
   >
   >Ad esempio, se desideri utilizzare il `modified at` metodo per il `orders` tabella, è necessario impostare un `date column` come chiave di replica. Possono esistere diverse opzioni per le chiavi di replica, ma puoi selezionare `created at`o l’ora di creazione dell’ordine. Se l’ultimo ciclo di aggiornamento si è interrotto al 12/1/2015 00:10:00, il ciclo successivo inizierebbe a replicare i dati con un `created at` data successiva a questa.

1. Al termine, fai clic su **[!UICONTROL Save]**.

Osservare l&#39;intero processo:

![](../../assets/replication_method.gif)<!--{: width="801" height="341"}-->

## Ritorno a capo

Per finire, avete creato questa tabella che confronta i vari metodi di replica. È molto utile quando si seleziona un metodo per le tabelle della Data Warehouse.

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
