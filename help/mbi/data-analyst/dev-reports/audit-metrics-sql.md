---
title: Utilizzo del Report Builder SQL
description: Scopri come controllare dati e metriche utilizzando il Report Builder SQL in modo da poter confrontare i risultati con i dati del database locale.
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# `SQL Report Builder`

Il `SQL Report Builder` viene utilizzato principalmente per creare nuovi rapporti e ripetere le analisi, ma può anche essere utilizzato per controllare in modo efficace dati e metriche. Le informazioni seguenti spiegano come controllare dati e metriche utilizzando `SQL Report Builder` in modo da poter confrontare i risultati con i dati del database locale.

## Query di una metrica

Per iniziare, apri `SQL Report Builder` passando a **[!UICONTROL Report Builder > SQL Report Builder > Create Report]**. Puoi utilizzare la barra laterale nell’editor SQL per inserire una metrica direttamente nella query passando il puntatore del mouse sulla metrica e facendo clic su **[!UICONTROL Insert]**. In questo modo la definizione della query di tale metrica viene aggiunta all’editor. La definizione include i seguenti componenti:

- Il **operazione di metrica** in esecuzione, indicato da SUM() nell’esempio seguente.
- Il **tabella su** generata dalla metrica, indicata dalla clausola FROM.
- Qualsiasi **filtri (e set di filtri)** che sono state aggiunte alla metrica, indicate dalla clausola WHERE nell’esempio seguente.
- Il componente del **timestamp** (anno, mese) in cui i dati devono essere ordinati, indicato dalla clausola ORDER BY nell’esempio seguente.

Se si desidera avere una visualizzazione più chiara della query, è possibile riformattare la modalità di visualizzazione nel campo della query. Quando sei pronto, seleziona `Run Query`. I risultati vengono inseriti sotto forma di tabella nel pannello del rapporto sotto la query.

![](../../assets/run-query-results.gif)

## Limitazione della query

Se si tenta di individuare una discrepanza o un insieme di dati specifico, è necessario limitare la query a un esempio specifico da controllare rispetto al database locale. Per farlo, modifica la query in modo che corrisponda alle restrizioni desiderate. Nell’esempio seguente, la query viene limitata per includere solo i ricavi a partire dal 1° gennaio 2013 o versione successiva. Dopo aver aggiornato la query, seleziona **[!UICONTROL Run Query]** per aggiornare i risultati.

![](../../assets/restricting-query.gif)

## Salvataggio ed esportazione

Quando il rapporto soddisfa le tue esigenze, salvalo in una dashboard assegnandogli un nome distinto, facendo clic su **[!UICONTROL Save]** e selezionando il tipo di rapporto da salvare e la dashboard. Durante il controllo delle metriche, l’Adobe consiglia di salvare il rapporto come `Table` e salvarlo in un dashboard di test.

Dopo aver salvato il report, accedi a tale dashboard selezionando `Go to Dashboard`. Da qui, puoi esportare i dati trovando il rapporto e selezionando **[!UICONTROL Options gear > Full `.csv`Esporta]** o **[!UICONTROL Full Excel Export]**.

![](../../assets/export-dboard-data.gif)

## Query personalizzate

Puoi anche scrivere query personalizzate ed esportare i risultati da confrontare con il database locale. Dopo il [linee guida per l’ottimizzazione delle query](../../best-practices/optimizing-your-sql-queries.md), scrivere una query nell&#39;editor SQL. Puoi utilizzare i pulsanti nella parte superiore della barra laterale per passare da un elenco di tabelle a un altro e le metriche disponibili per l’utilizzo in `SQL Report Builder` e aggiungerli alla query. Quando la query personalizzata soddisfa le tue esigenze, puoi salvare il rapporto ed esportare tali dati dal dashboard.

### Sei ancora inciampato?

Se si riscontra una discrepanza dopo aver controllato i dati, vedere [Contattare il supporto: discrepanze nei dati](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-data-discrepancies.html?lang=en) articolo di supporto per ulteriori informazioni su cosa fare dopo.
