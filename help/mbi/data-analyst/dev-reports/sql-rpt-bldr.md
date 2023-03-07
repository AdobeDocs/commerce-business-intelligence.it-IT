---
title: Utilizzo del Report Builder SQL
description: Scopri i pro e i contro dell’utilizzo del Report Builder SQL.
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '1461'
ht-degree: 0%

---

# Utilizzo di `SQL Report Builder`

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../administrator/user-management/user-management.md) per creare e modificare grafici SQL. `Standard` gli utenti possono ridisporre questi grafici sulle dashboard e `Read-only` Gli utenti hanno la stessa esperienza dei grafici tradizionali. Inoltre, `Read-only` gli utenti non hanno accesso al testo della query.

Consulta la [video di formazione](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html?lang=en) per ulteriori informazioni.

`SQL`, o Structured Query Language, è un linguaggio di programmazione utilizzato per comunicare con i database. In entrata [!DNL MBI], SQL viene utilizzato per eseguire query o recuperare dati dalla Data Warehouse. Osserva i rapporti sul tuo dashboard: dietro le quinte, ciascuno è alimentato da una query SQL.

È possibile utilizzare [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) per eseguire direttamente una query sulla Data Warehouse, visualizzare i risultati e trasformarli in un grafico. Puoi iniziare a creare un rapporto con `SQL Report Builder` passando a **[!UICONTROL Report Builder** > **SQL Report Builder]**.

Consulta la [video di formazione](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html?lang=en) per ulteriori informazioni.

Il `SQL Report Builder` consente di eseguire direttamente query sulla Data Warehouse, visualizzare i risultati e trasformarli rapidamente in un grafico. La parte migliore sull&#39;utilizzo di SQL per la generazione dei rapporti è che non è necessario attendere i cicli di aggiornamento per eseguire iterazioni sulle colonne create. Se i risultati non sono corretti, puoi modificare ed eseguire nuovamente la query in modo rapido fino a quando le cose non corrispondono alle tue aspettative.

Questo articolo illustra come utilizzare `SQL Report Builder`. Dopo aver individuato il percorso da seguire, consulta l’esercitazione SQL for visualizations (SQL per visualizzazioni) o prova a ottimizzare alcune delle query scritte.

Coperto in questo articolo:

1. [Scrittura di una query](#writing)

1. [Esecuzione della query e visualizzazione dei risultati](#runquery)

1. [Creazione di una visualizzazione](#createviz)

1. [Salvataggio del report](#save)

## Integrazioni di Report Builder SQL

Allo stato attuale del mondo, [[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md) è l’unica integrazione non disponibile per l’utilizzo con [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md). Questa funzionalità è in fase di sviluppo.

Per iniziare a creare un report SQL, fare clic su **[!UICONTROL Report Builder]** o **[!UICONTROL Add Report]** nella parte superiore di qualsiasi dashboard. In `Report Picker` schermata, fai clic su **[!UICONTROL SQL Report Builder]** per aprire l&#39;editor SQL.

## Introduzione

Per modificare un rapporto, fai clic sull’ingranaggio (![](../../assets/gear-icon.png)) nell&#39;angolo superiore destro di un grafico basato su SQL e fare clic su **[!UICONTROL Edit]**.

## Scrittura di una query {#writing}

>[!NOTE]
>
>`SQL Report Builder` nelle query viene fatta distinzione tra maiuscole e minuscole. Quando scrivi le query, assicurati di usare la maiuscola/minuscola corretta, altrimenti potresti riscontrare risultati imprevisti o errori.

Dopo il [linee guida per l’ottimizzazione delle query](../../best-practices/optimizing-your-sql-queries.md), scrivere una query nell&#39;editor SQL.

>[!IMPORTANT]
>
>**Metriche nei report SQL** - Quando si inserisce una metrica in un report SQL, il `current definition` della metrica utilizzata.

Se la metrica viene aggiornata in futuro, il rapporto SQL *non* rispecchia le modifiche. Per rendere effettive le modifiche, è necessario modificare manualmente il rapporto.

Utilizzando i pulsanti nella parte superiore della barra laterale, puoi passare da un elenco di tabelle a un elenco di metriche disponibili per l’utilizzo in `SQL Report Builder`. Se nell’elenco non trovi ciò che stai cercando, prova a cercarlo utilizzando la barra di ricerca nella parte superiore della barra laterale.

È inoltre possibile utilizzare la barra laterale nell’editor SQL per inserire metriche, tabelle e colonne direttamente nelle query passando con il mouse sopra di esse e facendo clic su **[!UICONTROL Insert]**:

![Inserimento di una tabella nell&#39;editor SQL.](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>Qualsiasi [Funzione SELECT](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST), o qualsiasi funzione che non muta dati supportata da PostgreSQL è supportata nel Report Builder SQL. Sono inclusi, ma senza limitazioni, AVG, COUNT, COUNT DISTINCT, MIN/MAX e SUM.

Inoltre, qualsiasi tipo JOIN è supportato, ma l&#39;Adobe consiglia di utilizzare solo INNER JOIN, in quanto è il meno costoso tra i tipi JOIN.

## Esecuzione della query e visualizzazione dei risultati {#runquery}

Una volta completata la scrittura della query, fare clic su **[!UICONTROL Run Query]**. I risultati vengono visualizzati in una tabella sotto l&#39;editor SQL:

![Esecuzione della query e visualizzazione dei risultati.](../../assets/SQL_Run_Query.gif)

Se qualcosa non appare nei risultati, è possibile modificare la query ed eseguirla nuovamente fino a quando non si è soddisfatti.

A volte potresti vedere [messaggi sotto l’editor con la dicitura SPIEGA](../../best-practices/optimizing-your-sql-queries.md). Se visualizzi uno di questi, significa che la query non è stata eseguita e richiede alcune regolazioni.

Dopo aver modificato la query, puoi passare alla creazione di una visualizzazione o al salvataggio del lavoro in una dashboard.

## Creazione di una visualizzazione {#createviz}

Per creare una visualizzazione con i risultati della query, fai clic sul pulsante **[!UICONTROL Chart]** scheda in `Results` riquadro. In questa scheda, seleziona:

* Il `Series`o la colonna che desideri misurare, ad esempio **Oggetti venduti**.
* Il `Category`o la colonna che desideri utilizzare per segmentare i dati, ad esempio **origine di acquisizione**.
* Il `Labels`o i valori dell&#39;asse X.

Ecco un rapido sguardo a come si presenta il processo di visualizzazione:

![](../../assets/SQL_RB_viz_overview.gif)

Per una descrizione dettagliata di come creare una visualizzazione, consulta [Tutorial sulla creazione di visualizzazioni da query SQL](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;}.

## Salvataggio del report {#save}

Prima di salvare i dati, è necessario assegnare un nome al report. Ricordati di seguire le [linee guida sulle best practice per la denominazione](../../best-practices/naming-elements.md){: target=&quot;_blank&quot;} e scegli qualcosa che trasmetta chiaramente cos’è il rapporto.

Clic **[!UICONTROL Save]** nell&#39;angolo superiore destro dell&#39;editor SQL e selezionare il report `Type` (`Chart` o `Table`). Per concludere, seleziona il dashboard in cui salvare il rapporto e fai clic su **[!UICONTROL Save to Dashboard]**.

![](../../assets/SQL_Save_Report.gif)

### Analizzare i dati

#### `SQL Report Builder`

[`The SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) consente di eseguire query dirette sulla Data Warehouse, visualizzare i risultati e trasformarli rapidamente in un rapporto. L&#39;utilizzo di SQL consente inoltre di: [per utilizzare funzioni SQL non disponibili](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html) nel `Visual` o `Cohort` Report Builder, fornendo così un maggiore controllo sui dati.

Le colonne calcolate create utilizzando SQL non dipendono dai cicli di aggiornamento, il che significa che è possibile iterare su di essi come si desidera e visualizzare immediatamente i risultati.

>[!NOTE]
>
>Questo vale solo per la struttura della colonna, non per l’aggiornamento dei dati. I nuovi dati dipendono ancora dai cicli di aggiornamento completati correttamente.

| **Questo è perfetto per...** | **Questo non è grandioso per...** |
|---|---|
| Analisti intermedi/avanzati | Principianti: è necessario conoscere SQL. |
| L&#39;esperienza SQL | Analisi semplici: la scrittura di una query può essere più efficace che utilizzare semplicemente il Report Builder visivo. |
| Creazione di colonne calcolate monouso | Condivisione con altri - considera il tuo pubblico: capiscono il linguaggio SQL? In caso contrario, potrebbero essere confusi dalla modalità di creazione del rapporto. |
| Dati con `one-to-many` relazioni |  |
| Verifica di una nuova colonna o analisi |  |

#### Risultati database e editor SQL

Nella maggior parte dei casi, le differenze nei risultati possono essere attribuite ai cicli di aggiornamento. Se [!DNL MBI] : durante la replica dei dati dal database alla Data Warehouse, è possibile che vengano visualizzati risultati diversi anche quando si utilizza la stessa query.

Anche i problemi di connessione possono causare discrepanze. Accedi a `Connections` pagina facendo clic su **[!DNL Manage Data** > **Connections]**) per estrarlo: si è verificato un errore per l’integrazione del database in questione? In tal caso, potrebbe essere necessario [autenticare nuovamente l’integrazione](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en) per eseguire di nuovo le operazioni.

Se tutte le integrazioni sono connesse correttamente e non sei nel bel mezzo di un ciclo di aggiornamento, qualcos’altro potrebbe non funzionare.

#### L&#39;eliminazione di un report SQL comporta anche l&#39;eliminazione delle colonne sottostanti dalla Data Warehouse?

No, non si perdono colonne dalla Data Warehouse, indipendentemente da come le si è create.

Colonne create utilizzando `Data Warehouse Manager` non vengono influenzate se si elimina un report o una query che li utilizza.

Colonne create utilizzando `SQL Report Builder` non vengono salvati nella tua Data Warehouse.


#### `Report Builder` rispetto a `SQL Report Builder`

Il `SQL Report Builder` offre maggiore flessibilità nella creazione e strutturazione dei grafici: è possibile, ad esempio, selezionare i valori da visualizzare nel `X` e `Y` assi. Per ulteriori informazioni sulla creazione di grafici in `SQL Report Builder`, controlla [Creazione di visualizzazioni da query SQL](../../tutorials/create-visuals-from-sql.md) esercitazione.

#### `Cohort Report Builder` {#cohortrb}

A differenza della `Visual Report Builder`, il [`Cohort Report Builder`](../dev-reports/cohort-rpt-bldr.md) è destinato a un singolo scopo: analizzare e identificare le tendenze comportamentali di gruppi di utenti simili nel tempo. L’utilizzo del Report Builder coorte non richiede alcuna esperienza SQL, quindi puoi iniziare subito senza esitazioni.

| **Questo è perfetto per...** | **Questo non è grandioso per...** |
|---|---|
| Analisti intermedi/avanzati | Principianti: sono necessarie coorti che definiscano la pratica. |
| Identificazione delle tendenze comportamentali nel tempo | Analisi qualitativa: [completato](../dev-reports/create-qual-cohort-analysis.md), ma richiede assistenza Adobe. |

## Ricostruzione delle query dopo il ciclo di aggiornamento

Non è necessario ricreare le query. Rapporti creati utilizzando [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) vengono salvate come quelle create nel `Report Builder`. Il processo di aggiornamento per i grafici SQL è lo stesso: dopo l&#39;aggiornamento dei dati, i valori nei grafici verranno ricalcolati e rivisualizzati.

>[!NOTE]
>
>Quando si elimina un report/query SQL, le colonne sottostanti non vengono eliminate dalla Data Warehouse. Le colonne non vengono perse, indipendentemente dalla modalità di creazione.

* Le colonne create mediante Gestione Date Warehouse non vengono influenzate dall&#39;eliminazione di un report o di una query che le utilizza.

* Le colonne create utilizzando il Report Builder SQL non vengono salvate nella Data Warehouse.

## Ritorno a capo {#wrapup}

Se vuoi provare qualcosa di un po’ più impegnativo, perché non provare a scrivere una query ottimizzata per la visualizzazione? Consulta la sezione [Tutorial sulla creazione di visualizzazioni da query SQL](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;} per iniziare.
