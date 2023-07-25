---
title: Dati Mixpanel previsti
description: Esplora le tabelle di dati principali che puoi importare da Mixpanel nel tuo [!DNL Commerce Intelligence] account.
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# Previsto [!DNL Mixpanel] dati

Dopo [hai connesso il tuo [!DNL Mixpanel] account](../integrations/mixpanel.md), è possibile utilizzare [Gestione Date Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) per tracciare facilmente i campi di dati rilevanti per l’analisi.

Questo argomento descrive le tabelle dati principali da cui è possibile importare [!DNL Mixpanel] nel tuo [!DNL Commerce Intelligence] account. Dopo la connessione verranno create le tabelle seguenti nella Data Warehouse [!DNL Mixpanel]. Per visualizzare tutti i campi disponibili per il tracciamento, fai clic sui collegamenti nella colonna nome tabella.

>[!NOTE]
>
>A causa dei limiti del [!DNL Mixpanel] API, dati storici: dati risalenti a più di sette (7) giorni prima della data di connessione a [!DNL Commerce Intelligence] - non viene replicato.

| **Nome tabella** | **Descrizione** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | Questa tabella contiene dati evento non elaborati, tra cui l’evento, le date dell’evento e il bucket della piattaforma. |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | Questa tabella contiene dati sui funnel, tra cui l’ID funnel, la lunghezza del funnel (numero di giorni necessari all’utente per completare l’funnel) e le date di inizio e fine del funnel. |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | Contiene dati provenienti da People Analytics, inclusi ID sessione, informazioni sulla pagina e sull’utente e la data/ora dell’ultima visualizzazione dell’utente. |

{style="table-layout:auto"}

## Documentazione correlata

* [Connessione [!DNL Mixpanel]](../integrations/mixpanel.md)
* [Reautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
