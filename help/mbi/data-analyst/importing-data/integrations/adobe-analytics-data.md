---
title: Previsti [!DNL Adobe Analytics] Dati
description: Scopri i passaggi per la connessione dell’istanza RDS.
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Previsti [!DNL Adobe Analytics] dati

L&#39;integrazione [!DNL Adobe Analytics] per [!DNL Adobe Commerce Intelligence] utilizza l&#39;API di reporting [Analytics 2.0](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md).

>[!INFO]
>
>Per ottenere i dati previsti, è innanzitutto possibile creare un report nel Workspace [!DNL Adobe Analytics] con le metriche e le dimensioni desiderate. Questo consente di verificare la compatibilità e la disponibilità dei dati.

Nella tua Data Warehouse viene creata una tabella per ogni suite di rapporti connessa denominata `report-suite-<ID>` (dove `<ID>` è un ID univoco generato da [!DNL Commerce Intelligence]).

Lo schema di questa tabella è composto dalle metriche e dalle dimensioni selezionate nel processo di configurazione dell’integrazione. [!DNL Commerce Intelligence] genera anche diverse colonne aggiuntive a scopo di identificazione.

Ad esempio, se hai selezionato la metrica e la dimensione seguenti durante l’impostazione:
- `Metric`: `Page views`
- `Dimension`: `Page`

La tabella conterrà le seguenti colonne:

| Nome colonna | Descrizione |
| --- | --- |
| `_id` | Questa colonna è la chiave primaria. |
| `_item_hash` | Identificatore univoco [!DNL Commerce Intelligence]. Colonna creata da [!DNL Commerce Intelligence]. |
| `_updated_at` | Questa colonna contiene l’ultimo aggiornamento della riga di dati. È stato creato da [!DNL Commerce Intelligence]. |
| `start_date` | Data di inizio dei dati inclusi per la riga. `start_date` è sempre alle 00:00 dello stesso giorno all&#39;interno di una riga. |
| `end_date` | Data di fine dei dati inclusi per la riga. `end_date` è sempre 23:59 dello stesso giorno all&#39;interno di una riga. |
| `page_views` | Metrica selezionata: il numero totale di visualizzazioni di pagina per il periodo di tempo identificato. |
| `page` | Dimensione selezionata: singoli nomi di pagina con viste tracciate. |

Controlla quali delle metriche e dimensioni selezionate hanno dati disponibili nella tabella [!DNL Commerce Intelligence] utilizzando le opzioni *sincronizza* o *ssincronizza* nella pagina `Data Warehouse`. Le colonne non sincronizzate vengono visualizzate in grigio. Se interrompi la sincronizzazione di una colonna, puoi iniziare a sincronizzarla nuovamente in un secondo momento.

## Limitazioni attuali

Questa sezione descrive i limiti dell&#39;integrazione di [!DNL Adobe Analytics] per [!DNL Commerce Intelligence].

| Limitazione | Descrizione |
| --- | --- |
| `Historical data period` | Come con altre integrazioni di terze parti, l&#39;integrazione di [!DNL Adobe Analytics] estrae una quantità limitata di dati storici e continua a mantenere aggiornati i dati. Il periodo storico è configurato su 2 settimane. |
| `Empty component combinations` | Alcune combinazioni di metriche e dimensioni non contengono dati. Se questa combinazione è selezionata per la replica, [!DNL Commerce Intelligence] esclude la colonna dalla tabella replicata. Per evitare di selezionare tale combinazione, è innanzitutto possibile creare un report in [[!DNL Adobe Analytics] Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html) per verificare di aver ottenuto i dati previsti. |
| `Re-authorization cadence` | È necessaria una nuova autorizzazione dell&#39;integrazione [!DNL Adobe Analytics] ogni due settimane. Per autorizzare nuovamente, passare alla pagina Modifica per l&#39;integrazione e fare clic su **[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**. |
| `One dimension per row` | [!DNL Adobe Analytics] fornisce dati metrici per una dimensione alla volta. Se si selezionano più dimensioni durante l&#39;installazione, ogni riga della tabella [!DNL Commerce Intelligence] contiene un singolo valore di dimensione e valori Null per ogni altra dimensione. |
