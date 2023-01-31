---
title: Utilizzo del Report Builder SQL
description: Scopri i dettagli e le uscite dell'utilizzo del Report Builder SQL.
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
source-git-commit: 09b6983c3e06a1f18035542dfa3b9de9ac3ceb38
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 0%

---

# Utilizzo `SQL Report Builder`

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../administrator/user-management/user-management.md) per creare e modificare i grafici SQL. `Standard` gli utenti possono ridisporre questi grafici su dashboard e `Read-only` gli utenti avranno la stessa esperienza con i grafici tradizionali. Inoltre, `Read-only` gli utenti non hanno accesso al testo della query.

Consulta le nostre [video di formazione](https://support.magento.com/hc/en-us/articles/360016730131) per saperne di più.

`SQL`, o Lingua query strutturata, è un linguaggio di programmazione utilizzato per comunicare con i database. In [!DNL MBI], SQL viene utilizzato per eseguire query o recuperare dati dal data warehouse. Dai un&#39;occhiata ai report sul tuo dashboard - dietro le quinte, ciascuno è alimentato da una query SQL.

È possibile utilizzare [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) per eseguire direttamente una query nel data warehouse, visualizzare i risultati e trasformarli in un grafico. Puoi iniziare a creare un rapporto con `SQL Report Builder` passando a **[!UICONTROL Report Builder** > **SQL Report Builder]**.

Consulta le nostre [video di formazione](https://support.magento.com/hc/en-us/articles/360016730131-Training-Video-SQL-Report-Builder) per saperne di più.

La `SQL Report Builder` consente di eseguire query dirette nel data warehouse, visualizzare i risultati e trasformarli rapidamente in un grafico. La parte migliore sull&#39;utilizzo di SQL per generare rapporti è che [non è necessario attendere i cicli di aggiornamento per eseguire iterazioni sulle colonne](https://support.magento.com/hc/en-us/articles/360016506212) create voi. Se i risultati non sono corretti, puoi modificare ed eseguire rapidamente la query fino a quando le cose non corrispondono alle tue aspettative.

In questo articolo ti guidiamo attraverso l&#39;utilizzo del `SQL Report Builder`. Dopo aver saputo come muoversi, controlla il nostro tutorial SQL per le visualizzazioni o prova ad ottimizzare alcune delle query che hai scritto.

Ecco una panoramica di ciò che descriviamo in questo articolo:

1. [Scrittura di una query](#writing)

1. [Esecuzione della query e visualizzazione dei risultati](#runquery)

1. [Creazione di una visualizzazione](#createviz)

1. [Salvataggio del report](#save)

## Integrazioni di Report Builder SQL

Allo stato attuale del mondo, [[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md) è l’unica integrazione non disponibile per l’utilizzo con [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md). Stiamo lavorando all’inclusione di questa funzionalità in una versione successiva.

Per iniziare a creare un nuovo report SQL, fare clic su **[!UICONTROL Report Builder]** o **[!UICONTROL Add Report]** nella parte superiore di qualsiasi dashboard. In `Report Picker` schermata, fai clic su **[!UICONTROL SQL Report Builder]** per aprire l&#39;editor SQL.

## Introduzione

Per modificare un rapporto, fai clic sull’icona a forma di ingranaggio (![](../../assets/gear-icon.png)) nell&#39;angolo in alto a destra di un grafico basato su SQL e fai clic su **[!UICONTROL Edit]**.

## Scrittura di una query {#writing}

>[!NOTE]
>
>`SQL Report Builder` le query sono sensibili a maiuscole e minuscole. Assicurati di utilizzare il caso corretto durante la scrittura di query o potresti ritrovarti con risultati o errori imprevisti.

Seguendo [linee guida per l’ottimizzazione delle query](../../best-practices/optimizing-your-sql-queries.md), scrivere una query nell&#39;editor SQL.

>[!IMPORTANT]
>
>**Metriche nei rapporti SQL** - Quando si inserisce una metrica in un report SQL, il `current definition` della metrica verrà utilizzata.

Se la metrica viene aggiornata in futuro, il rapporto SQL *non* riflettono le modifiche. Sarà necessario modificare manualmente il rapporto per rendere effettive le modifiche.

Utilizzando i pulsanti nella parte superiore della barra laterale, puoi alternare tra gli elenchi di tabelle e metriche disponibili per l’utilizzo in `SQL Report Builder`. Se l’elenco non contiene gli elementi da cercare, provare a cercarlo utilizzando la barra di ricerca nella parte superiore della barra laterale.

È inoltre possibile utilizzare la barra laterale nell&#39;editor SQL per inserire metriche, tabelle e colonne direttamente nelle query passando il puntatore del mouse sopra di esse e facendo clic su **[!UICONTROL Insert]**:

![Inserimento di una tabella nell&#39;editor SQL.](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>Qualsiasi [Funzione SELECT](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST), o qualsiasi funzione che non muta dati supportata da PostgreSQL è supportata nel Report Builder SQL. Ciò include, ma non è limitato a, AVG, COUNT, COUNT DISTINCT, MIN/MAX e SUM.

Inoltre, è supportato qualsiasi tipo JOIN, ma si consiglia di utilizzare solo INNER JOIN in quanto è il meno costoso dei tipi JOIN.

## Esecuzione della query e visualizzazione dei risultati {#runquery}

Al termine della scrittura della query, fai clic su **[!UICONTROL Run Query]**. I risultati verranno visualizzati in una tabella sotto l&#39;editor SQL:

![Esecuzione della query e visualizzazione dei risultati.](../../assets/SQL_Run_Query.gif)

Se nei risultati si verifica un errore, è possibile modificare la query ed eseguirla nuovamente fino a quando non si è soddisfatti.

A volte potresti vedere [messaggi sotto l&#39;editor con EXPLAIN](../../best-practices/optimizing-your-sql-queries.md). Se ne visualizzi uno, significa che la query non è stata eseguita e che richiede un po&#39; di ottimizzazione.

Dopo aver modificato la query, puoi passare alla creazione di una visualizzazione o al salvataggio del lavoro su un dashboard.

## Creazione di una visualizzazione {#createviz}

Per creare una visualizzazione con i risultati della query, fai clic sul pulsante **[!UICONTROL Chart]** nella scheda `Results` riquadro. In questa scheda, seleziona:

* La `Series`oppure la colonna da misurare, ad esempio **Articoli venduti**.
* La `Category`oppure la colonna che desideri utilizzare per segmentare i dati, ad esempio **sorgente di acquisizione**.
* La `Labels`o i valori dell&#39;asse X.

Ecco un rapido sguardo su come si presenta il processo di visualizzazione:

![](../../assets/SQL_RB_viz_overview.gif)

Per informazioni dettagliate su come creare una visualizzazione, consulta la sezione [Esercitazione sulla creazione di visualizzazioni da query SQL](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;}.

## Salvataggio del report {#save}

Prima di salvare il lavoro, è necessario assegnare un nome al rapporto. Ricorda di seguire le [linee guida sulle best practice per la denominazione](../../best-practices/naming-elements.md){: target=&quot;_blank&quot;} e scegli qualcosa che indichi chiaramente cosa è il report!

Fai clic su **[!UICONTROL Save]** nell&#39;angolo in alto a destra dell&#39;editor SQL e seleziona il report `Type` (`Chart` o `Table`). Per completare il tutto, seleziona il dashboard in cui salvare il rapporto e fai clic su **[!UICONTROL Save to Dashboard]**.

![](../../assets/SQL_Save_Report.gif)

### Analisi dei dati

#### `SQL Report Builder`

[`The SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) consente di eseguire query dirette nel data warehouse, visualizzare i risultati e trasformarli rapidamente in un report. L&#39;utilizzo di SQL consente inoltre di [per utilizzare funzioni SQL non disponibili](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html) in `Visual` o `Cohort` Report Builder, per un maggiore controllo sui dati.

Desideriamo ricordare che le colonne calcolate create con SQL non dipendono dai cicli di aggiornamento, il che significa che è possibile ripeterle come si desidera e vedere immediatamente i risultati.

>[!NOTE]
>
>Questo vale solo per la struttura della colonna, non per la freschezza dei dati. I nuovi dati dipendono ancora dai cicli di aggiornamento completati correttamente.

| **Questo è perfetto per...** | **Questo non è così grande per...** |
|---|---|
| Analisti intermedi/avanzati | Principianti - è necessario conoscere SQL. |
| Salvataggio SQL | Analisi semplici: la scrittura di una query può essere più efficace rispetto all&#39;utilizzo del Report Builder visivo. |
| Creazione di colonne calcolate una tantum | Condivisione con altri : considera il tuo pubblico: capiscono SQL? In caso contrario, potrebbero essere confusi dalla modalità di creazione del rapporto. |
| Dati con `one-to-many` relazioni |  |
| Verifica di una nuova colonna o analisi |  |

#### Risultati database e editor SQL

Nella maggior parte dei casi, le differenze nei risultati possono essere attribuite a cicli di aggiornamento. Se [!DNL MBI] si trova nel processo di replica dei dati dal database alla Data Warehouse, è possibile che vengano visualizzati risultati diversi anche quando si utilizza la stessa query.

Anche i problemi di connessione possono causare discrepanze. Passa a `Connections` facendo clic su **[!DNL Manage Data** > **Connections]**) per eseguire il check-out - c&#39;è un errore per l&#39;integrazione del database in questione? In caso affermativo, può essere necessario [riautenticare l&#39;integrazione](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations) per far funzionare di nuovo le cose.

Se tutte le integrazioni sono collegate correttamente e non sei nel mezzo di un ciclo di aggiornamento, potrebbe mancare un altro elemento. Prova a utilizzare [guide alla risoluzione dei problemi di discrepanza dei dati](https://support.magento.com/hc/en-us/sections/360003074492) sul nostro sito di assistenza per individuare il problema.

#### L&#39;eliminazione di un report SQL comporta anche l&#39;eliminazione delle colonne sottostanti dalla mia Data Warehouse?

No, non perderai nessuna colonna dalla Data Warehouse, indipendentemente da come le hai create.

Colonne create utilizzando `Data Warehouse Manager` non viene influenzato se elimini un report o una query che li utilizza.

Colonne create utilizzando `SQL Report Builder` non vengono salvate nella Data Warehouse.


#### `Report Builder` contro `SQL Report Builder`

La `SQL Report Builder` offre maggiore flessibilità durante la creazione e la strutturazione dei grafici. È possibile, ad esempio, selezionare i valori da visualizzare `X` e `Y` asce. Per ulteriori informazioni sulla creazione di grafici nel `SQL Report Builder`, consulta il nostro [Creazione di visualizzazioni da query SQL](../../tutorials/create-visuals-from-sql.md) esercitazione.

#### `Cohort Report Builder` {#cohortrb}

A differenza di `Visual Report Builder`, [`Cohort Report Builder`](../dev-reports/cohort-rpt-bldr.md) è destinato a un unico scopo: analizzare e identificare le tendenze comportamentali di gruppi di utenti simili nel tempo. L&#39;utilizzo del Report Builder di coorte non richiede alcuna esperienza SQL, pertanto puoi immergerti direttamente senza esitazione se stai solo iniziando.

| **Questo è perfetto per...** | **Questo non è così grande per...** |
|---|---|
| Analisti intermedi/avanzati | Principianti - è necessario esercitarsi nella definizione delle coorti. |
| Identificazione delle tendenze comportamentali nel tempo | Analisi qualitativa - può essere [completato](../dev-reports/create-qual-cohort-analysis.md)Ma richiede il nostro aiuto. |

## Ricostruzione delle query dopo il ciclo di aggiornamento

Non è necessario ricostruire le query. Rapporti creati utilizzando [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) vengono salvati come quelli creati nel tradizionale `Report Builder`. Il processo di aggiornamento dei grafici SQL è esattamente lo stesso: dopo l&#39;aggiornamento dei dati, i valori dei grafici verranno ricalcolati e rivisualizzati.

>[!NOTE]
>
>Durante l&#39;eliminazione di un report/query SQL non elimina le colonne sottostanti dalla Data Warehouse. Non perderai nessuna colonna, indipendentemente da come le hai create.

* Le colonne create utilizzando Gestione Date Warehouse non vengono influenzate se si elimina un report o una query che le utilizza.

* Le colonne create utilizzando il Report Builder SQL non vengono salvate nella Data Warehouse.

## Ritorno a capo {#wrapup}

Se desideri provare qualcosa di un po&#39; più impegnativo, perché non provare a scrivere una query ottimizzata per la visualizzazione? Consulta il nostro [Esercitazione sulla creazione di visualizzazioni da query SQL](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;} per iniziare.
