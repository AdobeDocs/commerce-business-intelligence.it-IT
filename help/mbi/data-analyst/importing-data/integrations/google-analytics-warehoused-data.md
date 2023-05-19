---
title: Dati warehouse Google Analytics previsti
description: Scopri come interagire con i dati memorizzati nel data warehouse di Google Analytics.
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# Previsto [!DNL Google Analytics Warehoused] Dati

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>Alcune informazioni sono state utilizzate con il permesso dei tuoi amici all’indirizzo [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

[!DNL Google Analytics Warehoused] integrazione in [!DNL Commerce Intelligence] utilizza [!DNL Google Analytics] [API di reporting di base](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>Per evitare risultati imprevisti o insensati, verifica che tutte le dimensioni utilizzate siano [compatibile con una o più metriche](https://ga-dev-tools.google/dimensions-metrics-explorer/) utilizzi in `Report Builder`.

Una singola tabella, denominata `report` - viene creato nella Data Warehouse.

Lo schema di questa tabella è composto dalle metriche e dai Dimension selezionati durante il processo di configurazione e da altre due colonne: `start-date` e `end-date`.

Ad esempio, hai selezionato le metriche e i Dimension seguenti durante la configurazione:

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

La tabella avrà un aspetto simile a quello riportato di seguito.

| **Nome colonna** | **Descrizione** |
|-----|-----|
| `\_id` | Questa colonna è la `primary key`. |
| `\_rjm\_record\_hash` | [!DNL Commerce Intelligence] identificatore univoco. Questa colonna viene creata da [!DNL Commerce Intelligence]. |
| `\_updated\_at` | Questa colonna contiene l’ultimo aggiornamento della riga di dati. Questa colonna viene creata da [!DNL Commerce Intelligence]. |
| `start-date` | Identificazione del giorno a cui si riferisce la riga. |
| `end-date` | Identificazione del giorno a cui si riferisce la riga. |
| `month` | Dimensione selezionata: mese della sessione, un numero intero di due cifre da 01 a 12. |
| `users` | Metrica selezionata: il numero totale di utenti per il periodo di tempo richiesto. |

{style="table-layout:auto"}

## Qual è la differenza tra [!DNL Google Analytics Warehoused] e [!DNL Live Integration]

La principale differenza consiste nel fatto che viene memorizzata un’integrazione ([!DNL Google Analytics Warehoused]) e l’altro non è ([!DNL Google Analytics Live]). In caso di [!DNL Google Analytics Warehoused], consente la manipolazione del [!DNL Google Analytics] e consente di combinare [!DNL Google Analytics] e altre origini dati per creare rapporti dettagliati.

Osserva [!DNL Google Analytics] campagne pubblicitarie per un esempio di ciò che può essere fatto dal punto di vista della manipolazione. Supponiamo di avere più campagne pubblicitarie per il quarto trimestre con nomi diversi. Le campagne erano il risultato di un’iniziativa di marketing specifica. Con i dati immagazzinati, puoi creare una colonna che trova i nomi delle campagne in questione e restituisce il nome dell’iniziativa Q4 di `Operation Dumbo`.

L&#39;aspetto combinato consente [!DNL Google Analytics] dati da unire ad altri dati per effettuare analisi. Ad esempio, prendi `Total Time On Site By Ad Campaign` dati da [!DNL Google Analytics] e unisciti a loro contro `Total Spent Per Campaign` dati da [!DNL Facebook Ads] per avere un quadro completo dei costi del coinvolgimento.

Con il [!DNL Google Analytics Live] integrazione, dall&#39;altro, ogni [!DNL Google Analytics] il grafico è simile a un piccolo silo non memorizzato nel [!DNL Commerce Intelligence] Data Warehouse.

## Correlato:

* [Connessione [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
