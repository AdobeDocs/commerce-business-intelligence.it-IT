---
title: Dati Mixpanel previsti
description: Esplora le tabelle di dati principali che puoi importare da Mixpanel nel tuo account  [!DNL Commerce Intelligence] .
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Previsti [!DNL Mixpanel] dati

Dopo che [hai connesso il tuo [!DNL Mixpanel] account](../integrations/mixpanel.md), puoi utilizzare [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) per tenere traccia facilmente dei campi di dati rilevanti per l&#39;analisi.

In questo argomento vengono illustrate le principali tabelle dati che è possibile importare da [!DNL Mixpanel] nel proprio account [!DNL Commerce Intelligence]. Dopo la connessione a [!DNL Mixpanel] verranno create le tabelle seguenti nel Data Warehouse. Per visualizzare tutti i campi disponibili per il tracciamento, fai clic sui collegamenti nella colonna nome tabella.

>[!NOTE]
>
>A causa delle limitazioni dell&#39;API [!DNL Mixpanel], i dati storici, ovvero i dati più vecchi di sette (7) giorni dalla data di connessione a [!DNL Commerce Intelligence], non vengono replicati.

| **Nome tabella** | **Descrizione** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | Questa tabella contiene dati evento non elaborati, tra cui l’evento, le date dell’evento e il bucket della piattaforma. |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | Questa tabella contiene dati sui funnel, tra cui l’ID funnel, la lunghezza del funnel (numero di giorni necessari all’utente per completare l’funnel) e le date di inizio e fine del funnel. |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | Contiene dati provenienti da People Analytics, inclusi ID sessione, informazioni sulla pagina e sull’utente e la data/ora dell’ultima visualizzazione dell’utente. |

{style="table-layout:auto"}

## Documentazione correlata

* [Connessione in corso  [!DNL Mixpanel]](../integrations/mixpanel.md)
* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=it)
