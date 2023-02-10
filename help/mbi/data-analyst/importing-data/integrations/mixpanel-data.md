---
title: Dati previsti del pannello multiplo
description: Esplorare le tabelle di dati principali che è possibile importare da Mixpanel nel [!DNL MBI] conto.
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# Previsto [!DNL Mixpanel] dati

Dopo [hai connesso il tuo [!DNL Mixpanel] account](../integrations/mixpanel.md), puoi utilizzare la [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) per tenere traccia facilmente dei campi dati rilevanti ai fini dell’analisi.

In questo articolo, esploriamo le tabelle di dati principali da cui è possibile importare [!DNL Mixpanel] nella [!DNL MBI] conto. Le tabelle seguenti verranno create nel data warehouse dopo la connessione di Mixpanel. Per visualizzare tutti i campi disponibili per il tracciamento, fai clic sui collegamenti nella colonna del nome della tabella.

>[!NOTE]
>
>A causa delle limitazioni del [!DNL Mixpanel] API, dati storici - dati più vecchi di sette (7) giorni dalla data di connessione a [!DNL MBI] - non verrà replicato.

| **Nome tabella** | **Descrizione** |
|-----|-----|
| [`mixpanel\_export`](https://mixpanel.com/docs/api-documentation/exporting-raw-data-you-inserted-into-mixpanel#datafeed) | Questa tabella contiene dati evento non elaborati, inclusi evento, date evento e bucket della piattaforma. |
| [`mixpanel\_funnels`](https://mixpanel.com/docs/api-documentation/data-export-api#funnels-default) | Questa tabella contiene i dati sui funnel, tra cui l’ID funnel, la lunghezza dell’imbuto (# giorni per cui l’utente deve completare l’imbuto) e le date di inizio e fine dell’imbuto. |
| [`mixpanel\_engage`](https://mixpanel.com/docs/api-documentation/data-export-api#engage-default) | Contiene i dati di People Analytics, inclusi gli ID sessione, le informazioni sulla pagina e sull’utente, e la data/ora dell’ultima visualizzazione dell’utente. |

{style=&quot;table-layout:auto&quot;}

## Documentazione correlata

* [Collegamento [!DNL Mixpanel]](../integrations/mixpanel.md)
* [Riautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
