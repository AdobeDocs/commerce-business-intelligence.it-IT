---
title: Creare e utilizzare visualizzazioni Data Warehouse
description: Informazioni su un metodo per la creazione di nuove tabelle in memoria modificando una tabella esistente oppure unendo o consolidando più tabelle tramite l'utilizzo di SQL.
exl-id: 5aa571c9-7f38-462c-8f1b-76a826c9dc55
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 9%

---

# Utilizzo delle visualizzazioni Data Warehouse

Il presente documento delinea lo scopo e gli usi di `Data Warehouse Views` accessibile passando a **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**. Di seguito è riportata una spiegazione di ciò che fa e di come crea nuove viste, nonché un esempio di come utilizzare `Data Warehouse Views` consolidare [!DNL Facebook] e [!DNL AdWords] spendere dati.

## Finalità generale

La `Data Warehouse Views` è un metodo per creare nuove tabelle in memoria modificando una tabella esistente oppure unendo o consolidando più tabelle mediante l&#39;utilizzo di SQL. Una volta `Data Warehouse View` è stato creato ed elaborato da un ciclo di aggiornamento, verrà popolato nella tua Data Warehouse come una nuova tabella sotto `Data Warehouse Views` a discesa, come mostrato di seguito:

![](../../assets/Data_Warehouse.png)

Da qui, la nuova visualizzazione funziona come qualsiasi altra tabella, consentendoti di creare nuove colonne calcolate o generare metriche e rapporti sopra di essa.

`Data Warehouse Views` vengono utilizzati principalmente per consolidare più tabelle simili ma diverse tra loro, in modo che tutti i rapporti possano essere generati su un’unica nuova tabella. Alcuni esempi comuni includono il consolidamento delle tabelle da un database legacy e da un database live per combinare dati storici e correnti o la combinazione di più origini pubblicitarie come Facebook e AdWords in un unico database `Consolidated ad spend` tabella.

Se si ha familiarità con SQL, entrambi questi esempi di consolidamento utilizzano il `UNION` ma è possibile utilizzare qualsiasi sintassi e funzioni PostgreSQL durante la creazione di una nuova visualizzazione.

## Creazione e gestione delle visualizzazioni di Data Warehouse

Nuovo `Data Warehouse Views` può essere creato e le visualizzazioni esistenti possono essere eliminate passando a **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**, come illustrato di seguito:

![](../../assets/Data_Warehouse_Views.png)

Da qui puoi creare una nuova visualizzazione seguendo le istruzioni di esempio riportate di seguito:

1. Se si osserva una visualizzazione esistente, fare clic su **[!UICONTROL New Data Warehouse View]** per aprire una finestra di query vuota. Se è già aperta una finestra di query vuota, procedere al passaggio successivo.
1. Assegna un nome alla visualizzazione digitando nel `View Name` campo . Il nome qui specificato determinerà il nome visualizzato per la visualizzazione nella Data Warehouse. `View names` sono limitati alle lettere minuscole, ai numeri e ai caratteri di sottolineatura (_). Tutti gli altri caratteri sono proibiti.
1. Inserisci la query nella finestra con titolo `Select Query`, utilizzando la sintassi PostgreSQL standard.
   >[!NOTE]
   >
   >La query deve fare riferimento a nomi di colonna specifici. L&#39;uso del `*`non è consentito selezionare tutte le colonne.

1. Al termine, fai clic su **[!UICONTROL Save]** per salvare la visualizzazione. Tieni presente che la visualizzazione avrà temporaneamente un `Pending` stato finché non viene elaborato dal successivo ciclo di aggiornamento completo, in cui lo stato cambia in `Active`. Dopo essere stata elaborata da un aggiornamento, la visualizzazione è pronta per essere utilizzata nei rapporti.

È importante ricordare che dopo il salvataggio, la query sottostante utilizzata per generare un `Data Warehouse View` non può essere modificato. Se per qualche motivo è necessario regolare la struttura di un `Data Warehouse View`, sarà necessario creare una nuova visualizzazione ed eseguire manualmente la migrazione di tutte le colonne, metriche o rapporti calcolati dalla visualizzazione originale a quella nuova. Al termine della migrazione, puoi eliminare in tutta sicurezza la visualizzazione originale. Perché `Data Warehouse Views` non sono modificabili, si consiglia vivamente di testare l’output della query utilizzando `SQL Report Builder` prima di salvare la query come visualizzazione Data Warehouse.

## Esempio: [!DNL Facebook] e [!DNL Google AdWords] dati

Diamo un&#39;occhiata più da vicino ad uno degli esempi citati in precedenza in questo articolo: consolidamento [!DNL Facebook] e [!DNL AdWords] spendere i dati in una nuova tabella annunci consolidata. Ciò comporta in genere il consolidamento di due tabelle, con i set di dati di esempio riportati di seguito:

`Ad source: Google AdWords`

`Table name: campaigns67890`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | orecchio | 60 | 2017-05-05 00:00:00 | 2000 | 10.2 |
| 2 | ggg | 40 | 2017-05-23 00:00:00 | 900 | 4.6 |
| 3 | aaa | 22 | 2017-06-12 00:00:00 | 400 | 2.5 |
| 4 | orecchio | 350 | 2017-06-30 00:00:00 | 14500 | 35 |
| 5 | fff | 280 | 2017-07-10 00:00:00 | 10200 | 28.5 |

`Ad source: Facebook`

`Table name: facebook_ads_insights_12345`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | aaa | 25 | 2017-05-01 00:00:00 | 1200 | 5 |
| 2 | ddd | 12 | 2017-05-15 00:00:00 | 800 | 2.5 |
| 3 | aaa | 40 | 2017-05-22 00:00:00 | 2000 | 7 |
| 4 | aaa | 110 | 2017-06-08 00:00:00 | 6000 | 10 |
| 5 | ccc | 5 | 2017-07-06 00:00:00 | 300 | 1.2 |

Per creare una singola tabella di spesa pubblicitaria contenente entrambi [!DNL Facebook] e [!DNL AdWords] campagne, sarà necessario scrivere una query SQL e utilizzare `UNION ALL` funzione . A `UNION ALL` viene utilizzato più spesso per combinare più query SQL distinte aggiungendo i risultati di ogni query a un singolo output.

Ci sono alcuni requisiti di un `UNION` istruzione che vale la pena citare, come descritto in PostgreSQL [documentazione](https://www.postgresql.org/docs/8.3/queries-union.html):

* Tutte le query devono restituire lo stesso numero di colonne
* Le colonne corrispondenti devono avere tipi di dati identici

Durante l’esecuzione di un `UNION` o `UNION ALL` i nomi delle colonne nell&#39;output finale riflettono la denominazione delle colonne nella prima query.

Nella maggior parte dei casi, il consolidamento [!DNL Facebook] e [!DNL Google AdWords] spendere dati in un `Data Warehouse View` richiederà la creazione di una tabella con sette colonne, con una query simile alla seguente:

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

* Per motivi di chiarezza, tutte le colonne sono precedute da un alias tale che i nomi corrispondano tra tutte le query. Tuttavia, questo non è un requisito. L&#39;ordine in cui le colonne vengono chiamate nelle query SELECT determina la loro struttura.
* Una nuova colonna denominata `ad_source` è stato creato per semplificare il filtro di [!DNL AdWords] o [!DNL Facebook] dati. Tenere presente che questa query combina tutti i dati di entrambe le tabelle. Se non crei una colonna come `ad_source`, non vi sarà un modo semplice per identificare la spesa da una particolare fonte.

Salvataggio della query sopra come `Data Warehouse View` creerà una nuova tabella con entrambi [!DNL Facebook] e [!DNL AdWords] spesa, simile alla seguente:

| **`id`** | **`ad_source`** | **`date`** | **`campaign`** | **`spend`** | **`impressions`** | **`clicks`** |
|--- |--- |--- |--- |--- |--- |--- |
| **1** | [!DNL Facebook] | 2017-05-01 00:00:00 | aaa | 5 | 1200 | 25 |
| **1** | [!DNL Google AdWords] | 2017-05-05 00:00:00 | orecchio | 10.2 | 2000 | 60 |
| **2** | [!DNL Facebook] | 2017-05-15 00:00:00 | ddd | 2.5 | 800 | 12 |
| **2** | [!DNL Google AdWords] | 2017-05-23 00:00:00 | ggg | 4.6 | 900 | 40 |
| **3** | [!DNL Facebook] | 2017-05-22 00:00:00 | aaa | 7 | 2000 | 40 |
| **3** | [!DNL Google AdWords] | 2017-06-12 00:00:00 | aaa | 2.5 | 400 | 22 |
| **4** | [!DNL Facebook] | 2017-06-08 00:00:00 | aaa | 10 | 6000 | 110 |
| **4** | [!DNL Google AdWords] | 2017-06-30 00:00:00 | orecchio | 35 | 14500 | 350 |
| **5** | [!DNL Facebook] | 2017-07-06 00:00:00 | ccc | 1.2 | 300 | 5 |
| **5** | [!DNL Google AdWords] | 2017-07-10 00:00:00 | fff | 28.5 | 10200 | 280 |

Invece di creare un set separato di metriche di marketing per ogni origine di annunci, ora puoi creare un solo set di metriche utilizzando la tabella precedente per acquisire tutti gli annunci.

**Stai cercando ulteriore aiuto?**

Scrittura di SQL e creazione `Data Warehouse Views` non è incluso nel supporto tecnico.  Tuttavia, il team Servizi offre assistenza nella creazione di visualizzazioni. Dalla migrazione e dal consolidamento di un database legacy con un nuovo database alla creazione di una visualizzazione a Data Warehouse singola ai fini di un&#39;analisi specifica, sono in grado di curare soluzioni basate su SQL per tutte le sfide della struttura dei dati.

Nella maggior parte dei casi, la creazione di un nuovo `Data Warehouse View` ai fini del consolidamento di 2-3 tabelle strutturate in modo simile richiede 5 ore di tempo di servizio, che si traduce in circa $1250 di lavoro. Tuttavia, di seguito sono riportati alcuni fattori comuni che possono aumentare gli investimenti previsti necessari:

* Consolidamento di più di 3 tabelle in un&#39;unica visualizzazione
* Creazione di più viste data warehouse
* Combinazione di condizioni logiche o di filtro complesse
* Consolidamento di 2 o più tabelle con strutture di dati dissimili
