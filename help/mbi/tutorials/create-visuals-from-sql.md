---
title: Creare visualizzazioni da query SQL
description: Scopri come acquisire familiarità con la terminologia utilizzata in SQL Report Builder e come fornire una solida base per la creazione di visualizzazioni SQL.
exl-id: 9b9bc205-5b64-4e64-8d23-057072e5dd72
role: Admin, Data Architect, Data Engineer, Leader, User
feature: SQL Report Builder, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---

# Creare visualizzazioni da query SQL

L&#39;obiettivo di questo tutorial è acquisire familiarità con la terminologia utilizzata in [!DNL SQL Report Builder] e fornire una solida base per la creazione di `SQL visualizations`.

[[!DNL SQL Report Builder]](../data-analyst/dev-reports/sql-rpt-bldr.md) è un generatore di report con opzioni: è possibile eseguire una query al solo scopo di recuperare una tabella di dati oppure è possibile trasformare tali risultati in un report. Questo tutorial spiega come creare una visualizzazione da una query SQL.

## Terminologia

Prima di iniziare questa esercitazione, fare riferimento alla seguente terminologia utilizzata in `SQL Report Builder`.

- `Series`: la colonna che si desidera misurare viene indicata come Serie in SQL Report Builder. Esempi comuni sono `revenue`, `items sold` e `marketing spend`. Almeno una colonna deve essere impostata come `Series` per creare una visualizzazione.

- `Category`: la colonna che si desidera utilizzare per segmentare i dati è denominata `Category`. È simile alla funzionalità `Group By` in [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md). Ad esempio, se desideri segmentare i ricavi relativi al ciclo di vita dei clienti in base all&#39;origine di acquisizione, la colonna che contiene l&#39;origine di acquisizione verrà specificata come `Category`. È possibile impostare più colonne come `Category`.

>[!NOTE]
>
>È inoltre possibile utilizzare date e marche temporali come `Categories`. Si tratta solo di un’altra colonna di dati nella query e deve essere formattata e ordinata come desiderato nella query stessa.

- `Labels`: vengono applicate come etichette dell&#39;asse x. Quando si analizzano i dati con tendenze nel tempo, le colonne anno e mese vengono specificate come etichette. È possibile impostare più colonne come Etichetta.

## Passaggio 1: scrivere la query

Considera quanto segue:

- [!DNL SQL Report Builder] utilizza [`Redshift SQL`](https://docs.aws.amazon.com/redshift/latest/dg/c_redshift-and-postgres-sql.html).

- Se stai creando un report con una serie temporale, assicurati di `ORDER BY` le colonne timestamp. In questo modo le marche temporali vengono tracciate nell’ordine corretto sul rapporto.

- La funzione `EXTRACT` è utile per analizzare il giorno, la settimana, il mese o l&#39;anno della marca temporale. Questa opzione è utile quando `time interval` che si desidera utilizzare nel report è `daily`, `weekly`, `monthly` o `yearly`.

Per iniziare, aprire [!DNL SQL Report Builder] facendo clic su **[!UICONTROL Report Builder** > **SQL Report Builder]**.

Ad esempio, considera questa query che restituisce il numero totale mensile di articoli venduti per ciascun prodotto:

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

![Tabella che mostra i risultati delle query SQL con gli elementi venduti per prodotto, anno e mese](../assets/SQL_results_table.png)

## Passaggio 2: creare la visualizzazione

Con questi risultati, *come si crea la visualizzazione?* Per iniziare, fare clic sulla scheda **[!UICONTROL Chart]** nel riquadro `Results`. Verrà visualizzata la scheda `Chart settings`.

Quando si esegue una query per la prima volta, il report potrebbe risultare imperscrutabile perché tutte le colonne della query vengono tracciate come una serie:

![Report SQL iniziale con tutte le colonne tracciate come serie](../assets/SQL_initial_report_results.png)

In questo esempio, vuoi che sia un grafico a linee con tendenze nel tempo. Per crearlo, usa le seguenti impostazioni:

- `Series`: selezionare la colonna `Items sold` come `Series` poiché si desidera misurarla. Dopo aver definito una colonna `Series`, nel rapporto verrà tracciata una singola riga.

- `Category`: in questo esempio, si desidera visualizzare ogni prodotto come una riga diversa nel report. Per eseguire questa operazione, impostare `Product name` come `Category`.

- `Labels`: utilizzare le colonne `year` e `month` come etichette sull&#39;asse x per visualizzare `Items Sold` come tendenza nel tempo.

>[!NOTE]
>
>La query deve contenere una clausola `ORDER BY` nelle etichette se sono `date`/`time` colonne.

Di seguito è riportato un rapido riepilogo su come hai creato questa visualizzazione, dall’esecuzione della query alla configurazione del rapporto:

![Dimostrazione animata della configurazione delle impostazioni di visualizzazione del report SQL](../assets/SQL_report_settings.gif)

## Passaggio 3: selezionare un `Chart Type`

Questo esempio utilizza il tipo di grafico `Line`. Per utilizzare un `chart type` diverso, fare clic sulle icone sopra la sezione delle opzioni del grafico per modificarlo:

![Icone del tipo di grafico disponibili, incluse opzioni di visualizzazione a linee, a barre, ad area e di altro tipo](../assets/Chart_types.png)

## Passaggio 4: salvare la visualizzazione

Se desideri utilizzare di nuovo questo report, assegna un nome al report e fai clic su **[!UICONTROL Save]** nell&#39;angolo in alto a destra.

Nel menu a discesa, selezionare `Chart` come `Type` e quindi una dashboard in cui salvare il report.

## Ritorno a capo

Vuoi fare un passo avanti? Consulta le [best practice per l&#39;ottimizzazione delle query](../best-practices/optimizing-your-sql-queries.md).
