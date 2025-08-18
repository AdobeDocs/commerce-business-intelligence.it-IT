---
title: Creare e utilizzare le visualizzazioni di Data Warehouse
description: Scopri come creare nuove tabelle warehouse modificando una tabella esistente o unendo o consolidando più tabelle utilizzando SQL.
exl-id: 5aa571c9-7f38-462c-8f1b-76a826c9dc55
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 6%

---

# Utilizzo delle visualizzazioni di Data Warehouse

Questo documento descrive lo scopo e gli utilizzi di `Data Warehouse Views` accessibili passando a **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**. Di seguito viene fornita una spiegazione delle operazioni eseguite e della modalità di creazione delle visualizzazioni, nonché un esempio di come utilizzare `Data Warehouse Views` per consolidare i dati di spesa di [!DNL Facebook] e [!DNL AdWords].

## Scopo generale

La funzionalità `Data Warehouse Views` consente di creare nuove tabelle con data warehouse modificando una tabella esistente oppure unendo o consolidando più tabelle mediante SQL. Una volta creato ed elaborato da un ciclo di aggiornamento, un `Data Warehouse View` viene inserito nel Data Warehouse come nuova tabella sotto il menu a discesa `Data Warehouse Views`, come illustrato di seguito:

![](../../assets/Data_Warehouse.png)

Da qui, la nuova vista funziona come qualsiasi altra tabella, consentendoti di creare nuove colonne calcolate o di creare metriche e rapporti al suo interno.

`Data Warehouse Views` vengono utilizzati principalmente per consolidare più tabelle simili ma disparate, in modo che tutti i rapporti possano essere generati su un&#39;unica nuova tabella. Alcuni esempi comuni includono il consolidamento delle tabelle da un database legacy e da un database live per combinare dati storici e correnti oppure la combinazione di più origini di annunci come Facebook e AdWords in una singola tabella `Consolidated ad spend`.

Se si ha familiarità con SQL, entrambi gli esempi di consolidamento utilizzano la funzione `UNION`, ma è possibile utilizzare qualsiasi sintassi e funzione PostgreSQL durante la creazione di una nuova visualizzazione.

## Creazione e gestione delle visualizzazioni di Data Warehouse

È possibile creare un nuovo `Data Warehouse Views` ed eliminare le visualizzazioni esistenti passando a **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**, come illustrato di seguito:

![](../../assets/Data_Warehouse_Views.png)

Da qui è possibile creare una visualizzazione seguendo le istruzioni di esempio riportate di seguito:

1. Se si osserva una visualizzazione esistente, fare clic su **[!UICONTROL New Data Warehouse View]** per aprire una finestra di query vuota. Se è già aperta una finestra di query vuota, procedere al passaggio successivo.
1. Assegnare un nome alla visualizzazione digitando nel campo `View Name`. Il nome qui fornito determina il nome visualizzato per la visualizzazione nel Data Warehouse. `View names` sono limitati a lettere minuscole, numeri e trattini bassi (_). Tutti gli altri caratteri sono vietati.
1. Immettere la query nella finestra `Select Query` utilizzando la sintassi PostgreSQL standard.

   >[!NOTE]
   >
   >La query deve fare riferimento a nomi di colonna specifici. L&#39;utilizzo del carattere `*` per selezionare tutte le colonne non è consentito.

1. Al termine, fare clic su **[!UICONTROL Save]** per salvare la visualizzazione. Lo stato della visualizzazione è `Pending` finché non viene elaborato dal successivo ciclo di aggiornamento completo, che cambia in `Active`. Dopo essere stata elaborata da un aggiornamento, la vista è pronta per essere utilizzata nei rapporti.

È importante ricordare che dopo il salvataggio, la query sottostante utilizzata per generare un `Data Warehouse View` non può essere modificata. Se è necessario modificare la struttura di un `Data Warehouse View`, è necessario creare una visualizzazione e migrare manualmente le colonne, le metriche o i report calcolati dalla visualizzazione originale a quella nuova. Una volta completata la migrazione, puoi eliminare in tutta sicurezza la visualizzazione originale. Poiché `Data Warehouse Views` non sono modificabili, Adobe consiglia di verificare l&#39;output della query utilizzando `SQL Report Builder` prima di salvare la query come visualizzazione Data Warehouse.

## Esempio: [!DNL Facebook] e [!DNL Google AdWords] dati

Osserva con attenzione uno degli esempi menzionati in precedenza in questo articolo: consolidamento dei dati di spesa di [!DNL Facebook] e [!DNL AdWords] in una nuova tabella di annunci consolidata. Nella maggior parte dei casi ciò comporta il consolidamento di due tabelle, con i set di dati di esempio riportati di seguito:

`Ad source: Google AdWords`

`Table name: campaigns67890`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | eee | 60 | 00:00:00 05/05/2017 | 2000 | 10,2 |
| 2 | ggg | 40 | 2017-05-23 00:00:00 | 900 | 4,6 |
| 3 | aaa | 22 | 12/06/2017 :00: 00 | 400 | 2,5 |
| 4 | eee | 350 | 00:00:00 06-06-2017 | 14500 | 35 |
| 5 | fff | 280 | 00:00:00 17-07-10 | 10200 | 28,5 |

`Ad source: Facebook`

`Table name: facebook_ads_insights_12345`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | aaa | 25 | 00:00:00 01 05/05/2017 | 1200 | 5 |
| 2 | ddd | 12 | 00:00:00 00 05-05-2017 | 800 | 2,5 |
| 3 | aaa | 40 | 2017-05-22 00:00:00 | 2000 | 7 |
| 4 | aaa | 110 | 00:00:00 00 06/08/2017 | 6000 | 10 |
| 5 | ccc | 5 | 00:00:00 06 07/07/2017 | 300 | 1,2 |

Per creare una singola tabella di spesa degli annunci contenente entrambe le campagne [!DNL Facebook] e [!DNL Google AdWords], è necessario scrivere una query SQL e utilizzare la funzione `UNION ALL`. Un&#39;istruzione `UNION ALL` viene spesso utilizzata per combinare più query SQL distinte aggiungendo i risultati di ogni query a un singolo output.

Ci sono alcuni requisiti di un&#39;istruzione `UNION` che vale la pena menzionare, come descritto nella [documentazione](https://www.postgresql.org/docs/8.3/queries-union.html) di PostgreSQL:

* Tutte le query devono restituire lo stesso numero di colonne
* Le colonne corrispondenti devono avere tipi di dati identici

Durante l&#39;esecuzione di un&#39;istruzione `UNION` o `UNION ALL`, i nomi delle colonne nell&#39;output finale riflettono la denominazione delle colonne nella prima query.

In genere, il consolidamento dei dati di spesa di [!DNL Facebook] e [!DNL Google AdWords] in un `Data Warehouse View` richiede la creazione di una tabella con sette colonne, con una query simile alla seguente:

```sql
    SELECT
        "_id" as id,
        'AdWords' as ad_source,
        "date",
        "campaign",
        "adCost" as spend,
        "impressions",
        "adClicks" as clicks
    FROM campaigns67890
    UNION
    SELECT
        "_id" as id,
        'Facebook' as ad_source,
        "date_start" as date,
        "campaign_name" as campaign,
        "spend",
        "impressions",
        "clicks"
    FROM facebook_ads_insights_12345
```

Un paio di punti importanti su quanto sopra:

* Per motivi di chiarezza, sopra tutte le colonne viene visualizzato un alias in modo che i nomi corrispondano in tutte le query. Tuttavia, questo non è un requisito. L&#39;ordine in cui le colonne vengono chiamate nelle query SELECT determina il modo in cui sono allineate.
* È stata creata una nuova colonna denominata `ad_source` per semplificare il filtraggio dei dati [!DNL AdWords] o [!DNL Facebook]. Questa query combina tutti i dati di entrambe le tabelle. Se non si crea una colonna come `ad_source`, non è possibile identificare facilmente la spesa da una determinata origine.

Il salvataggio della query precedente come `Data Warehouse View` crea una tabella con una spesa di [!DNL Facebook] e [!DNL AdWords], simile alla seguente:

| **`id`** | **`ad_source`** | **`date`** | **`campaign`** | **`spend`** | **`impressions`** | **`clicks`** |
|--- |--- |--- |--- |--- |--- |--- |
| **1** | [!DNL Facebook] | 00:00:00 01 05/05/2017 | aaa | 5 | 1200 | 25 |
| **1** | [!DNL Google AdWords] | 00:00:00 05/05/2017 | eee | 10,2 | 2000 | 60 |
| **2** | [!DNL Facebook] | 00:00:00 00 05-05-2017 | ddd | 2,5 | 800 | 12 |
| **2** | [!DNL Google AdWords] | 2017-05-23 00:00:00 | ggg | 4,6 | 900 | 40 |
| **3** | [!DNL Facebook] | 2017-05-22 00:00:00 | aaa | 7 | 2000 | 40 |
| **3** | [!DNL Google AdWords] | 12/06/2017 :00: 00 | aaa | 2,5 | 400 | 22 |
| **4** | [!DNL Facebook] | 00:00:00 00 06/08/2017 | aaa | 10 | 6000 | 110 |
| **4** | [!DNL Google AdWords] | 00:00:00 06-06-2017 | eee | 35 | 14500 | 350 |
| **5** | [!DNL Facebook] | 00:00:00 06 07/07/2017 | ccc | 1,2 | 300 | 5 |
| **5** | [!DNL Google AdWords] | 00:00:00 17-07-10 | fff | 28,5 | 10200 | 280 |

Invece di creare un set separato di metriche di marketing per ogni origine di annuncio, puoi creare un singolo set di metriche utilizzando la tabella precedente per acquisire tutti gli annunci.

**Ricerca di ulteriori informazioni?**

Il supporto tecnico non include la scrittura di SQL e la creazione di `Data Warehouse Views`. Tuttavia, il [team dei servizi](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=it) offre assistenza nella creazione delle visualizzazioni. Il team di supporto può fornire assistenza in tutte le fasi, dalla migrazione di un database legacy con un nuovo database alla creazione di una singola visualizzazione Data Warehouse ai fini di un’analisi specifica.

In genere, la creazione di un nuovo `Data Warehouse View` per il consolidamento di 2-3 tabelle strutturate in modo simile richiede cinque ore di tempo di servizio, il che si traduce in circa $ 1.250 di lavoro. Tuttavia, di seguito sono riportati alcuni fattori comuni che possono aumentare gli investimenti previsti necessari:

* Consolidamento di più di tre tabelle in un&#39;unica visualizzazione
* Creazione di più di una visualizzazione Data Warehouse
* Logica di unione complessa o condizioni di filtro
* Consolidamento di due o più tabelle con strutture di dati dissimili
