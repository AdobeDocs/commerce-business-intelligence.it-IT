---
title: Dati warehouse Google Analytics previsti
description: Scopri come interagire con i dati memorizzati nel data warehouse di Google Analytics.
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# Previsti [!DNL Google Analytics Warehoused] dati

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>Alcune informazioni sono state utilizzate con l&#39;autorizzazione dei tuoi amici all&#39;indirizzo [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

L&#39;integrazione di [!DNL Google Analytics Warehoused] in [!DNL Commerce Intelligence] utilizza l&#39;API [!DNL Google Analytics] [Core di reporting](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>Per evitare risultati inattesi o insensati, verificare che le dimensioni utilizzate siano [compatibili con una o più metriche](https://ga-dev-tools.google/dimensions-metrics-explorer/) utilizzate in `Report Builder`.

Nella Data Warehouse viene creata una singola tabella denominata `report`.

Lo schema di questa tabella è composto dalle metriche e dai Dimension selezionati durante il processo di configurazione e da altre due colonne: `start-date` e `end-date`.

Ad esempio, hai selezionato le metriche e i Dimension seguenti durante la configurazione:

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

La tabella avrà un aspetto simile a quello riportato di seguito.

| **Nome colonna** | **Descrizione** |
|-----|-----|
| `\_id` | Questa colonna è `primary key`. |
| `\_rjm\_record\_hash` | Identificatore univoco [!DNL Commerce Intelligence]. Colonna creata da [!DNL Commerce Intelligence]. |
| `\_updated\_at` | Questa colonna contiene l’ultimo aggiornamento della riga di dati. Colonna creata da [!DNL Commerce Intelligence]. |
| `start-date` | Identificazione del giorno a cui si riferisce la riga. |
| `end-date` | Identificazione del giorno a cui si riferisce la riga. |
| `month` | Dimensione selezionata: mese della sessione, un numero intero di due cifre da 01 a 12. |
| `users` | Metrica selezionata: il numero totale di utenti per il periodo di tempo richiesto. |

{style="table-layout:auto"}

## Qual è la differenza tra [!DNL Google Analytics Warehoused] e [!DNL Live Integration]

Il principale elemento di differenziazione è che un&#39;integrazione è archiviata ([!DNL Google Analytics Warehoused]) e l&#39;altra non è ([!DNL Google Analytics Live]). Nei casi di [!DNL Google Analytics Warehoused], questo consente la manipolazione dei dati di [!DNL Google Analytics] e consente di combinare [!DNL Google Analytics] e altre origini dati per creare report approfonditi.

Osserva le [!DNL Google Analytics] campagne pubblicitarie per un esempio di cosa si può fare dal punto di vista della manipolazione. Supponiamo di avere più campagne pubblicitarie per il quarto trimestre con nomi diversi. Le campagne erano il risultato di un’iniziativa di marketing specifica. Con i dati immagazzinati, puoi creare una colonna che trovi i nomi delle campagne in questione e restituisca il nome dell’iniziativa Q4 di `Operation Dumbo`.

L&#39;aspetto combinato consente di unire i dati di [!DNL Google Analytics] ad altri dati per eseguire analisi. Prendi ad esempio `Total Time On Site By Ad Campaign` dati da [!DNL Google Analytics] e unisciti a `Total Spent Per Campaign` dati da [!DNL Facebook Ads] per ottenere un quadro completo del costo del coinvolgimento.

Con l&#39;integrazione di [!DNL Google Analytics Live], invece, ogni grafico [!DNL Google Analytics] è come un piccolo silo non memorizzato nella Data Warehouse di [!DNL Commerce Intelligence].

## Correlato:

* [Connessione in corso  [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
