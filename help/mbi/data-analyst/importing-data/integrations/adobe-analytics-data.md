---
title: Previsto [!DNL Adobe Analytics] Dati
description: Scopri i passaggi per la connessione dell’istanza RDS.
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Previsto [!DNL Adobe Analytics] Dati

Il [!DNL Adobe Analytics] integrazione per [!DNL Adobe Commerce Intelligence] utilizza [API di reporting di Analytics 2.0](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md).

>[!INFO]
>
>Per garantire di ottenere i dati previsti, puoi prima creare un rapporto in [!DNL Adobe Analytics] Workspace con le metriche e le dimensioni desiderate. Questo consente di verificare la compatibilità e la disponibilità dei dati.

Una tabella per ogni suite di rapporti connessa denominata `report-suite-<ID>` (dove `<ID>` è un ID univoco generato da [!DNL Commerce Intelligence]) è stato creato nella tua Data Warehouse.

Lo schema di questa tabella è composto dalle metriche e dalle dimensioni selezionate nel processo di configurazione dell’integrazione. Sono generate anche diverse colonne aggiuntive da [!DNL Commerce Intelligence], ai fini dell&#39;identificazione.

Ad esempio, se hai selezionato la metrica e la dimensione seguenti durante l’impostazione:
- `Metric`: `Page views`
- `Dimension`: `Page`

La tabella conterrà le seguenti colonne:

| Nome colonna | Descrizione |
| --- | --- |
| `_id` | Questa colonna è la chiave primaria. |
| `_item_hash` | [!DNL Commerce Intelligence] identificatore univoco. Questa colonna viene creata da [!DNL Commerce Intelligence]. |
| `_updated_at` | Questa colonna contiene l’ultimo aggiornamento della riga di dati. Viene creato da [!DNL Commerce Intelligence]. |
| `start_date` | Data di inizio dei dati inclusi per la riga. `start_date` sono sempre le 00:00 dello stesso giorno all’interno di una riga. |
| `end_date` | Data di fine dei dati inclusi per la riga. `end_date` sono sempre le 23:59 dello stesso giorno all’interno di una riga. |
| `page_views` | Metrica selezionata: il numero totale di visualizzazioni di pagina per il periodo di tempo identificato. |
| `page` | Dimensione selezionata: singoli nomi di pagina con viste tracciate. |

Controlla quali delle metriche e dimensioni selezionate hanno dati disponibili nel tuo [!DNL Commerce Intelligence] tabella utilizzando *sincronizzazione* o *desincronizza* opzioni in `Data Warehouse` pagina. Le colonne non sincronizzate vengono visualizzate in grigio. Se interrompi la sincronizzazione di una colonna, puoi iniziare a sincronizzarla nuovamente in un secondo momento.

## Limitazioni attuali

Questa sezione illustra i limiti del [!DNL Adobe Analytics] integrazione per [!DNL Commerce Intelligence].

| Limitazione | Descrizione |
| --- | --- |
| `Historical data period` | Come con altre integrazioni di terze parti, il [!DNL Adobe Analytics] L’integrazione richiama una quantità limitata di dati storici e continua a mantenere aggiornati i dati. Il periodo storico è configurato su 2 settimane. |
| `Empty component combinations` | Alcune combinazioni di metriche e dimensioni non contengono dati. Se tale combinazione è selezionata per la replica, [!DNL Commerce Intelligence] esclude la colonna dalla tabella replicata. Per evitare di selezionare tale combinazione, puoi prima creare un rapporto in [[!DNL Adobe Analytics] Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html) per verificare di aver ottenuto i dati previsti. |
| `Re-authorization cadence` | Riautorizzazione del [!DNL Adobe Analytics] L&#39;integrazione è richiesta ogni due settimane. Per autorizzare nuovamente, vai alla pagina Modifica dell’integrazione e fai clic su **[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**. |
| `One dimension per row` | [!DNL Adobe Analytics] fornisce dati metrici per una dimensione alla volta. Se selezionate più quote durante l&#39;impostazione, ciascuna riga nella [!DNL Commerce Intelligence] La tabella contiene un singolo valore di dimensione e valori Null per ogni altra dimensione. |
