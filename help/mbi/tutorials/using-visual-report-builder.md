---
title: Utilizzare il Report Builder visivo
description: Scopri come analizzare i dati nel rapporto per un periodo di tempo specifico.
exl-id: da97b63d-63f0-4fd6-87e3-4cac49a42acc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 0%

---

# Utilizza la `Visual Report Builder`

La [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md) consente di esplorare visivamente i dati per acquisire informazioni e guidare le decisioni aziendali. Questa esercitazione descrive come creare un rapporto di base.

>[!NOTE]
>
>Per aggiungere un rapporto a un dashboard, è necessario `Standard` [autorizzazioni utente](../administrator/user-management/user-management.md) e `Edit` accedere al dashboard.

## Passaggio 1: Creazione di un rapporto

Per iniziare a creare un nuovo rapporto, fai clic su **[!UICONTROL Report Builder]** sulla barra laterale o **[!UICONTROL Add Report]** nella parte superiore di qualsiasi dashboard. Quando il `Report Builder` viene visualizzata la pagina di selezione, fai clic sul pulsante **[!UICONTROL Visual Report Builder]** opzione .

Per modificare un rapporto creato in `Visual Report Builder`, fai clic sull’icona a forma di ingranaggio (Opzioni) nell’angolo in alto a destra di qualsiasi grafico, quindi fai clic su **[!UICONTROL Edit]**.

## Passaggio 2: Aggiunta di metriche

Il primo passaggio nella creazione di un’analisi consiste nel selezionare [la metrica](../data-user/reports/ess-manage-data-metrics.md) da analizzare. Anche se le metriche sono elencate in ordine alfabetico per impostazione predefinita, puoi anche raggrupparle in base alla tabella che le abilita.

Puoi aggiungere ulteriori metriche dopo aver selezionato la metrica iniziale e sovrapporre tutte le metriche su un singolo rapporto oppure eseguire calcoli multivalore aggiungendo formule.

## Passaggio 3: Aggiunta `Formulas`

`Formulas` vengono aggiunti ai rapporti facendo clic su **[!UICONTROL Add Formula]**, situata appena sopra l’elenco delle metriche nel rapporto. In [editor di formule](../data-analyst/dev-reports/formulas-in-rpt-bldr.md), qualsiasi metrica inclusa nel rapporto può essere utilizzata come input. Gli operatori matematici di base vengono utilizzati per manipolare le diverse metriche.

Diciamo che vogliamo creare una relazione che ci mostri i ricavi medi per ordine. In questo caso, divideremmo la `Revenue` metrica per `Number of orders` metrica.

![](../assets/ave-rev-per-order.png)

## Passaggio 4: Impostazione della `Time Period` e `Interval of Analysis` {#time}

Per azzerare in un particolare intervallo di tempo, puoi impostare il periodo di tempo per l’analisi. Puoi anche scegliere intervalli di tempo per segmentare i dati (ad esempio, per anno, per trimestre o per mese). Utilizzare i menu nell’angolo in alto a destra del grafico per impostare il periodo di tempo e l’intervallo.

![](../assets/Time_Options_Report_Builder.png)

Quando imposti un intervallo di date specifico per il periodo di tempo, assicurati che la data di inizio sia all’inizio dell’intervallo e che la data di fine sia alla fine dell’intervallo.

Ad esempio, l’impostazione di un periodo di tempo da `January 1st to March 1st` e scegliendo un `monthly` verrà visualizzato l&#39;intervallo `March` come datapoint, ma ignora ogni giorno in `March` eccetto `March 1`. In tal caso, devi effettuare le `Time Period` da `January 1 to March 31`.

## Passaggio 5: `Group by` / `Segmenting the Analysis` {#groupby}

[Segmentazione delle metriche in base a una dimensione dati](../best-practices/segment-filter.md), fai clic su **[!UICONTROL Group by]** in alto a sinistra del grafico. Viene visualizzato un menu a discesa con tutte le dimensioni disponibili della prima metrica inclusa nell’elenco.

Puoi scegliere `None` per evitare che una metrica venga segmentata. Ad esempio, potresti volere una metrica che restituisca i ricavi totali senza essere segmentata, mentre un’altra metrica di ricavi viene segmentata per regione.

Torna al nostro fatturato medio per esempio di ordine e imposta il Gruppo per al codice promozionale. Questo ci mostrerà il ricavo medio per ordine per gli ordini sia con che senza un codice promozionale.

![](../assets/Group_By_Report_Builder.png)

Se le metriche incluse nell’analisi sono create su tabelle di dati diverse, un pop-up ti consentirà di selezionare la dimensione dati corrispondente in ciascuna tabella. L’obiettivo è trovare dimensioni che condividono lo stesso tipo di valori per la segmentazione:

![](../assets/Dimension_Editor.png)

## Passaggio 6: Impostazione `Metric Filters`, `Perspective`e `Time Interval` {#metric-specific}

Per ogni metrica aggiunta all’analisi, puoi aggiungere filtri, selezionare la prospettiva dei dati pertinente e impostare `time interval` opzioni. Per accedere a queste funzioni, fai clic sul funnel (`Filter`), occhio (`Perspective`) e orologio (`Time`) accanto alle metriche incluse nel rapporto.

![](../assets/Filters_Perspective_Interval_Report_builder.png)

### `Filters`

`Filters` limita il set di dati incluso nell’analisi. I filtri sono estremamente utili, ad esempio, quando si valutano i singoli canali di acquisizione e si rimuovono gli outlier.

Oltre ai menu a discesa e alle caselle di testo, puoi utilizzare anche operatori di filtro speciali come `LIKE` o `IN` per creare filtri.

L&#39;uso dei caratteri jolly (`%` o `_`) in combinazione con `LIKE` le istruzioni sono supportate. La `%` il carattere jolly corrisponderà a più caratteri, mentre `_` corrisponde a qualsiasi singolo carattere. Ad esempio:

- `affiliate's name Like B%` consentirà solo i dati provenienti da clienti il cui nome inizia con `B`.

- `affiliate's name Like _ake` consentirà solo i dati dei clienti i cui nomi sono simili `Jake`, `Rake`oppure `Bake` ma non `Drake` o `Blake`.

L&#39;aggiunta di più filtri consente un controllo rigoroso dei dati del grafico. Per impostazione predefinita, tutte le condizioni del filtro devono essere soddisfatte per includere un dato, ma è possibile creare relazioni OR modificando la casella di testo Regole filtro.

![](../assets/edit-filter-rules.png)

### `Perspectives`

`Perspectives` consente di passare facilmente da una visualizzazione all’altra dei dati. Diamo un&#39;occhiata a ciò che è disponibile:

- `Standard perspective`: La prospettiva standard mostra il risultato per la data di corrispondenza sull’asse x (ad esempio i ricavi di gennaio). Questa è la prospettiva che usiamo nel nostro esempio di ricavi medi per ordine.

![](../assets/Standard.png)

- `Amount` O `Percent Change` contro `Previous Period` prospettiva: Questa prospettiva mostra la quantità o la percentuale di variazione da un intervallo all&#39;altro ed è utile per misurare il tasso di variazione nelle metriche che cambiano rapidamente.C&#39;è anche una prospettiva per confrontare l&#39;intervallo con lo stesso periodo di tempo dello scorso anno per mostrare la crescita anno su anno.

![](../assets/Amt_or_Percent_Change.png)

- `Cumulative perspective`: La `cumulative perspective` mostra l’importo della metrica corrente o cumulativa nel periodo di tempo. Questo viene spesso utilizzato per analizzare i clienti totali e pianificare la capacità futura.

![](../assets/Cumulative_Perspective.png)

- `Percent of First Value perspective`: Questa prospettiva mostra i dati come percentuale del primo intervallo di tempo incluso nell’analisi. È utile per misurare l’efficacia delle azioni specifiche rispetto alle prestazioni del primo periodo.

![](../assets/Percent_of_First_Value.png)

- `Rolling averages window perspective`: La prospettiva della finestra delle medie mobili mostra il valore medio continuo di una metrica nell’intervallo di tempo specificato. L&#39;intervallo deve essere lo stesso impostato a livello di report. Ad esempio, se il rapporto mostra l’ultimo trimestre completo di Ricavo per settimana, puoi impostare l’intervallo di tempo medio continuo della finestra su 4 settimane, i primi tre valori saranno nulli e il quarto valore rappresenta la media delle prime 4 settimane di Ricavo. Per chiarezza, disattiva la `Multiple Y-Axes` se visualizzi la stessa metrica con una media continua, come nell’esempio seguente.

![](../assets/rolling_avg_window.png)

### Opzioni ora specifiche per la metrica

Esistono due opzioni per le metriche utilizzate nei rapporti: possono tendere nel tempo in base alle opzioni di tempo globali, o meno, che le visualizzeranno come numero scalare.

Modifica di un intervallo di tempo della metrica in `None` restituisce `scalar` , utile quando si creano formule che comportano la divisione di una metrica con tendenze temporali in base a un `scalar` numero. Inoltre, puoi anche modificare l’intervallo di tempo del `scalar` a un intervallo di tempo indipendente da quello del rapporto.

Ad esempio, volevamo che le entrate mensili del 2019 fossero espresse in percentuale delle entrate totali del 2019. Possiamo aggiungerne due `Revenue` metriche per un report con un intervallo di tempo globale dal 1° gennaio 2019 al 31 dicembre 2019, segmentate per intervallo mensile.

>[!NOTE]
>
>Se aggiungi `group by` , scegli una nuova visualizzazione o regola l’intervallo di tempo e salva solo il numero (`scalar`), tali regolazioni non verranno mantenute alla successiva apertura del rapporto da un dashboard: verrà mantenuto solo l’intervallo di tempo.

Per ulteriori informazioni sull’utilizzo delle opzioni di tempo nei rapporti, consulta [tutorial](../tutorials/time-options-visual-rpt-bldr.md).

## Passaggio 7: Salvataggio del rapporto

Quando si crea un nuovo grafico, è possibile salvarlo facendo clic su **[!UICONTROL Save]** nell&#39;angolo in alto a destra del `Visual Report Builder`.

È possibile scegliere di salvare un grafico, una tabella o un numero (`scalar`) utilizzando `Type` a discesa e il dashboard in cui il rapporto deve essere salvato utilizzando `Location` a discesa.

Per salvare il rapporto, fai clic su **[!UICONTROL Save to Dashboard]**.

![](../assets/save-to-dashboard.png)

## Uscite dei rapporti

Per aiutarti a decidere quale output di report scegliere, vedi:

### Grafico

![](../assets/RB_Chart.png)

### Tabella

![](../assets/RB_Table.png)

### Numero (`scalar`)

![](../assets/RB_Scalar.png)

Congratulazioni! Ha finito.
