---
title: Dati previsti di Google Analytics warehouse
description: Scopri come interagire con i dati immagazzinati delle Google Analytics.
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# Previsto [!DNL Google Analytics] Dati memorizzati

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>Alcune informazioni sono state utilizzate con il permesso dei nostri amici su [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

[!DNL Google Analytics Warehoused] integrazione in [!DNL MBI] utilizza [!DNL Google Analytics] [API di reportistica di base](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>Per evitare risultati imprevisti o insensati, verifica che le dimensioni utilizzate siano [compatibile con le metriche](https://developers.google.com/analytics/devguides/reporting/core/dimsmets) utilizzi in `Report Builder`.

Una singola tabella, denominata `report` - sarà creato nella tua Data Warehouse.

Lo schema di questa tabella sarà composto dalle metriche e dai Dimension selezionati durante il processo di configurazione e da altre due colonne: `start-date` e `end-date`.

Se, ad esempio, hai selezionato le metriche e i Dimension seguenti durante la configurazione:

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

La tabella è simile a quella riportata di seguito.

| **Nome colonna** | **Descrizione** |
|-----|-----|
| `\_id` | Questa colonna è `primary key`. |
| `\_rjm\_record\_hash` | [!DNL MBI] identificatore univoco. Questa colonna viene creata da [!DNL MBI]. |
| `\_updated\_at` | Questa colonna contiene l’ultima volta che la riga di dati è stata aggiornata. Questa colonna viene creata da [!DNL MBI]. |
| `start-date` | Identificazione del giorno a cui appartiene la riga. |
| `end-date` | Identificazione del giorno a cui appartiene la riga. |
| `month` | Dimensione selezionata: Mese della sessione, un numero intero di due cifre da 01 a 12. |
| `users` | Metrica selezionata: Numero totale di utenti per il periodo di tempo richiesto. |

{style=&quot;table-layout:auto&quot;}

## Promemoria: Differenza tra integrazione Google Analytics Warehouse e Live

Il principale fattore di differenziazione consiste nell&#39;archiviazione di un&#39;integrazione ([!DNL Google Analytics Warehoused]) e l&#39;altro non è ([!DNL Google Analytics Live]). Nel caso di [!DNL Google Analytics Warehoused], questo consente la manipolazione del [!DNL Google Analytics] e consente di combinare [!DNL Google Analytics] e altre origini dati per creare rapporti approfonditi.

Diamo un&#39;occhiata [!DNL Google Analytics] campagne pubblicitarie per un esempio di ciò che può essere fatto da un punto di vista di manipolazione. Supponiamo di avere più campagne pubblicitarie per Q4 con nomi diversi. Le campagne sono il risultato di una specifica iniziativa di marketing. Con i dati memorizzati, possiamo creare una nuova colonna che trovi i nomi delle campagne in questione e restituisca il nome dell&#39;iniziativa Q4 di `Operation Dumbo`.

L&#39;aspetto combinato consente [!DNL Google Analytics] dati da unire ad altri dati per effettuare analisi. Ad esempio, `Total Time On Site By Ad Campaign` dati da [!DNL Google Analytics] e unisciti `Total Spent Per Campaign` dati da [!DNL Facebook Ads] per avere un quadro completo di quanto impegno vi sta costando.

Con la [!DNL Google Analytics Live] l&#39;integrazione, d&#39;altra parte, [!DNL Google Analytics] grafico è come un piccolo silo che non è memorizzato nel tuo [!DNL MBI] data warehouse.

## Correlati:

* [Collegamento [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
