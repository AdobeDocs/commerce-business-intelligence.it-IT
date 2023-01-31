---
title: Previsto [!DNL Adobe Analytics] Dati
description: Scopri i passaggi per la connessione dell’istanza RDS.
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---

# Previsto [!DNL Adobe Analytics] Dati

La [!DNL Adobe Analytics] integrazione per [!DNL MBI] utilizza [API di reporting di Analytics 2.0](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md).

>[!INFO]
>
>Per ottenere i dati attesi, puoi innanzitutto creare un rapporto nel [!DNL Adobe Analytics] Area di lavoro con le metriche e le dimensioni desiderate. Ciò ti consente di verificare la compatibilità e la disponibilità dei dati.

Una tabella per suite di rapporti connessa - chiamata `report-suite-<ID>`, dove `<ID>` è un ID univoco generato da [!DNL MBI] - sarà creato nella tua Data Warehouse.

Lo schema di questa tabella è composto dalle metriche e dalle dimensioni selezionate nel processo di configurazione dell&#39;integrazione. Sono inoltre generate diverse colonne aggiuntive da [!DNL MBI], a fini di identificazione.

Ad esempio, se hai selezionato la metrica e la dimensione seguenti durante la configurazione:
- `Metric`: `Page views`
- `Dimension`: `Page`

La tabella contiene le colonne seguenti:

| Nome colonna | Descrizione |
| --- | --- |
| `_id` | Questa colonna è la chiave primaria. |
| `_item_hash` | [!DNL MBI] identificatore univoco. Questa colonna viene creata da [!DNL MBI]. |
| `_updated_at` | Questa colonna contiene l’ultima volta che la riga di dati è stata aggiornata. Viene creato da [!DNL MBI]. |
| `start_date` | Data di inizio dei dati inclusi per la riga. `start_date` sarà sempre 00:00 dello stesso giorno all&#39;interno di una riga. |
| `end_date` | Data di fine dei dati inclusi per la riga. `end_date` sarà sempre 23:59 dello stesso giorno all&#39;interno di una riga. |
| `page_views` | Metrica selezionata: Il numero totale di visualizzazioni di pagina per il periodo di tempo identificato. |
| `page` | Dimensione selezionata: Singoli nomi di pagina con viste tracciate. |

Controlla quali delle metriche e delle dimensioni selezionate hanno dati disponibili nel tuo [!DNL MBI] utilizzando la tabella *Sincronizzazione* o *non sincronizzato* nelle opzioni `Data Warehouse` pagina. Le colonne non sincronizzate vengono visualizzate in grigio. Se si interrompe la sincronizzazione di una colonna, è possibile ricominciare a sincronizzarla in un secondo momento.

## Limitazioni attuali

Questa sezione delinea le limitazioni [!DNL Adobe Analytics] integrazione per [!DNL MBI].

| Limitazione | Descrizione |
| --- | --- |
| `Historical data period` | Come per altre integrazioni di terze parti, il [!DNL Adobe Analytics] L’integrazione richiama una quantità limitata di dati storici e quindi continua a mantenere i dati aggiornati. Il periodo storico è configurato a 2 settimane. |
| `Empty component combinations` | Alcune combinazioni di metriche e dimensioni non contengono dati. Se tale combinazione è selezionata per la replica, [!DNL MBI] esclude la colonna dalla tabella replicata. Per evitare di selezionare tale combinazione, puoi innanzitutto creare un rapporto nella [[!DNL Adobe Analytics] Area di lavoro](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html?lang=en) per verificare di ottenere i dati previsti. |
| `Re-authorization cadence` | Riautorizzazione del [!DNL Adobe Analytics] L&#39;integrazione è attualmente necessaria ogni due settimane. Per riautorizzare, vai alla pagina Modifica per l’integrazione e fai clic su **[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**. |
| `One dimension per row` | [!DNL Adobe Analytics] fornisce dati di metrica per una dimensione alla volta. Se durante la configurazione selezioni più dimensioni, ogni riga nel [!DNL MBI] La tabella conterrà un singolo valore di dimensione e valori nulli l’uno per l’altro. |
