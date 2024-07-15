---
title: Utilizzo del Report Builder SQL
description: Scopri come controllare dati e metriche utilizzando il Report Builder SQL in modo da poter confrontare i risultati con i dati del database locale.
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
role: Admin, Data Architect, Data Engineer, User
feature: Reports, Data Warehouse Manager, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# [!DNL SQL Report Builder]

[!DNL SQL Report Builder] viene utilizzato principalmente per creare nuovi report e ripetere le analisi, ma può anche essere utilizzato per controllare in modo efficace dati e metriche. Le informazioni seguenti spiegano come controllare i dati e le metriche utilizzando [!DNL SQL Report Builder] in modo da poter confrontare i risultati con i dati del database locale.

## Query di una metrica

Per iniziare, aprire [!DNL SQL Report Builder] passando a **[!UICONTROL Report Builder > SQL Report Builder > Create Report]**. È possibile utilizzare la barra laterale nell&#39;editor [!DNL SQL] per inserire una metrica direttamente nella query passando il puntatore del mouse sulla metrica e facendo clic su **[!UICONTROL Insert]**. In questo modo la definizione della query di tale metrica viene aggiunta all’editor. La definizione include i seguenti componenti:

- **operazione di metrica** in esecuzione, indicata da `SUM()` nell&#39;esempio seguente.
- Tabella **su** in cui viene generata la metrica, indicata dalla clausola `FROM`.
- Qualsiasi **filtro (e set di filtri)** aggiunto alla metrica, indicato dalla clausola `WHERE` nell&#39;esempio seguente.
- Componente della **marca temporale** (anno, mese) in cui devono essere ordinati i dati, indicato dalla clausola `ORDER BY` nell&#39;esempio seguente.

Per ottenere una visualizzazione più chiara della query, è possibile riformattarne la visualizzazione nel campo della query. Al termine, selezionare `Run Query`. I risultati vengono inseriti sotto forma di tabella nel pannello del rapporto sotto la query.

![](../../assets/run-query-results.gif)

## Limitazione della query

Se si tenta di individuare una discrepanza o un insieme di dati specifico, è necessario limitare la query a un esempio specifico da controllare rispetto al database locale. Per farlo, modifica la query in modo che corrisponda alle restrizioni desiderate. Nell’esempio seguente, la query viene limitata per includere solo i ricavi a partire dal 1° gennaio 2013 o versione successiva. Dopo aver aggiornato la query, selezionare nuovamente **[!UICONTROL Run Query]** per aggiornare i risultati.

![](../../assets/restricting-query.gif)

## Salvataggio ed esportazione

Quando il report soddisfa le tue esigenze, assegna al report un nome distinto, fai clic su **[!UICONTROL Save]** e seleziona il tipo di report che desideri salvare e la dashboard. Durante il controllo delle metriche, Adobe consiglia di salvare il report come `Table` e salvarlo in un dashboard di test.

Dopo aver salvato il report, passare a tale dashboard selezionando `Go to Dashboard`. Da qui è possibile esportare i dati individuando il report e selezionando **[!UICONTROL Options gear > Full `.csv`Esporta]** o **[!UICONTROL Full Excel Export]**.

![](../../assets/export-dboard-data.gif)

## Query personalizzate

Puoi anche scrivere query personalizzate ed esportare i risultati da confrontare con il database locale. Seguendo le [linee guida per l&#39;ottimizzazione delle query](../../best-practices/optimizing-your-sql-queries.md), scrivere una query nell&#39;editor SQL. È possibile utilizzare i pulsanti nella parte superiore della barra laterale per alternare tra elenchi di tabelle e metriche disponibili per l&#39;utilizzo in [!DNL SQL Report Builder] e aggiungerli alla query. Quando la query personalizzata soddisfa le tue esigenze, puoi salvare il rapporto ed esportare tali dati dal dashboard.

>[!NOTE]
>
>Se riscontri una discrepanza dopo aver controllato i dati, consulta l&#39;argomento di supporto [Contattare il supporto: discrepanze di dati](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-data-discrepancies.html) per ulteriori informazioni su come procedere.
