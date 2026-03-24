---
title: Dati Mixpanel previsti
description: Esplora le tabelle di dati principali che puoi importare da Mixpanel nel tuo account  [!DNL Commerce Intelligence] .
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/iM6GzisImrjed7uCZf6lf6HIze9MwWdhq2gEP-IrIXA
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 187
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
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | Questa tabella contiene dati sui funnel, tra cui l’ID funnel, la lunghezza di funnel (numero di giorni necessari per il completamento di funnel) e le date di inizio e fine di funnel. |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | Contiene dati provenienti da People Analytics, inclusi ID sessione, informazioni sulla pagina e sull’utente e la data/ora dell’ultima visualizzazione dell’utente. |

{style="table-layout:auto"}

## Documentazione correlata

* [Connessione in corso  [!DNL Mixpanel]](../integrations/mixpanel.md)
* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
