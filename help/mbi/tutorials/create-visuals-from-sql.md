---
title: Creare visualizzazioni da query SQL
description: Scopri come acquisire familiarità con la terminologia utilizzata nel Report Builder SQL e come creare le visualizzazioni SQL.
exl-id: 9b9bc205-5b64-4e64-8d23-057072e5dd72
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# Creare visualizzazioni da query SQL

L’obiettivo di questa esercitazione è quello di acquisire familiarità con la terminologia utilizzata nel `SQL Report Builder` e fornisci solide basi per la creazione `SQL visualizations`.

La [`SQL Report Builder`](../data-analyst/dev-reports/sql-rpt-bldr.md) è un generatore di report con opzioni: è possibile eseguire una query al solo scopo di recuperare una tabella di dati oppure trasformare tali risultati in un rapporto. Questa esercitazione spiega come creare una visualizzazione da una query SQL.

## Terminologia

Prima di iniziare questa esercitazione, fai riferimento alla seguente terminologia utilizzata nella `SQL Report Builder`.

- `Series`: La colonna che si desidera misurare è definita Serie nel Report Builder SQL. Esempi comuni `revenue`, `items sold`e `marketing spend`. Almeno una colonna deve essere impostata come `Series` per creare una visualizzazione.

- `Category`: La colonna che desideri utilizzare per segmentare i dati è denominata `Category` Questo è proprio come il `Group By` nella [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md). Ad esempio, se desideri segmentare i ricavi del ciclo di vita dei clienti per l’origine di acquisizione, la colonna contenente l’origine di acquisizione viene specificata come `Category`. È possibile impostare più colonne come `Category`.

>[!NOTE]
>
>Le date e le marche temporali possono essere utilizzate anche come `Categories`. Sono solo un’altra colonna di dati nella query e devono essere formattati e ordinati come desiderato nella query stessa.

- `Labels`: Vengono applicate come etichette dell&#39;asse x. Quando si analizzano le tendenze dei dati nel tempo, le colonne anno e mese sono generalmente specificate come etichette. È possibile impostare più colonne su Etichetta.

## Passaggio 1: Scrivere la query

Tieni presente quanto segue:

- La `SQL Report Builder` utilizza [`Redshift SQL`](https://docs.aws.amazon.com/redshift/latest/dg/c_redshift-and-postgres-sql.html).

- Se crei un rapporto con una serie temporale, assicurati di `ORDER BY` le colonne di marca temporale. In questo modo le marche temporali verranno tracciate nell’ordine corretto del rapporto.

- La `EXTRACT` è utile per analizzare il giorno, la settimana, il mese o l’anno della marca temporale. Questa funzione è utile quando `time interval` desideri utilizzare nel rapporto `daily`, `weekly`, `monthly`oppure `yearly`.

Per iniziare, apri le `SQL Report Builder` facendo clic su **[!UICONTROL Report Builder** > **SQL Report Builder]**.

Ad esempio, considera questa query che restituisce il numero totale mensile di articoli venduti per ogni prodotto:

```sql
    SELECT SUM("qty") AS "Items Sold", "products's name" AS "product name",
    EXTRACT(year from "Order date") AS "year",
    EXTRACT(month from "Order date") AS "month"
    FROM "items"
    WHERE "products's name" LIKE '%Jeans'
    GROUP BY  "products's name", "year","month"
    ORDER BY "year" ASC,"month" ASC
    LIMIT 3500
```

Questa query restituisce questa tabella di risultati:

![](../assets/SQL_results_table.png)

## Passaggio 2: Creare la visualizzazione

Con questi risultati, *come si crea la visualizzazione?* Per iniziare, fai clic sul pulsante **[!UICONTROL Chart]** nella scheda `Results` riquadro. Verrà visualizzata la `Chart settings` scheda .

Quando una query viene eseguita per la prima volta, il report potrebbe apparire inscrutabile perché tutte le colonne della query sono tracciate come serie:

![](../assets/SQL_initial_report_results.png)

Per questo esempio, vogliamo che sia un grafico a linee con tendenze nel tempo. Per crearlo, utilizza le seguenti impostazioni:

- `Series`: Seleziona la `Items sold` come colonna `Series` dal momento che vogliamo misurarlo. Dopo aver definito un `Series` viene visualizzata una singola riga tracciata nel rapporto.

- `Category`: In questo esempio, vogliamo visualizzare ogni prodotto come riga diversa nel rapporto. Per farlo, ci siamo messi `Product name` come `Category`.

- `Labels`: Utilizzare le colonne `year` e `month` come etichette sull&#39;asse x per visualizzare `Items Sold` come tendenza nel tempo.

>[!NOTE]
>
>La query deve contenere un `ORDER BY` sulle etichette, se sono `date`/`time` colonne.

Di seguito è riportato un rapido sguardo su come abbiamo creato questa visualizzazione, dall’esecuzione della query alla configurazione del rapporto:

![](../assets/SQL_report_settings.gif)

## Passaggio 3: Seleziona una `Chart Type`

In questo esempio viene utilizzato `Line` tipo di grafico. Per utilizzare un `chart type`, fai clic sulle icone sopra la sezione delle opzioni del grafico per modificarla:

![](../assets/Chart_types.png)

## Passaggio 4: Salvare la visualizzazione

Se desideri utilizzare nuovamente il rapporto, assegna un nome al rapporto e fai clic su **[!UICONTROL Save]** nell&#39;angolo in alto a destra.

Nel menu a discesa , seleziona `Chart` come `Type` e quindi un dashboard in cui salvare il rapporto.

## Congratulazioni! Ha finito.

Vuoi fare un passo avanti? Consulta la sezione [best practice per l’ottimizzazione delle query](../best-practices/optimizing-your-sql-queries.md).
