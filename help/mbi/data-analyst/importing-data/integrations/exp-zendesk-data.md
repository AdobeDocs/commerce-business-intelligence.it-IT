---
title: Dati Zendesk previsti
description: Scopri le principali tabelle di dati che puoi importare da Zendesk in MBI, compresi i collegamenti alla documentazione aggiuntiva sui dati di Zendesk.
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# Dati Zendesk previsti

Dopo [hai connesso il tuo [!DNL Zendesk] account](../integrations/zendesk.md), puoi utilizzare la [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) per tenere traccia facilmente dei campi dati rilevanti ai fini dell’analisi.

In questo articolo, esploriamo le tabelle di dati principali da cui è possibile importare [!DNL Zendesk] in [!DNL MBI], compresi i collegamenti alla documentazione aggiuntiva su [!DNL Zendesk] dati.

| Nome tabella | Descrizione |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | La `Audits` le attività relative ai record di tabella associate a un ticket, comprese le modifiche dello stato e le risposte dei clienti e degli agenti. Questa tabella include un ticket id che effettua il collegamento al `Tickets` tabella, che consente di analizzare il tempo di risposta iniziale e il tempo di risoluzione per ogni ticket. |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | La `audit_~\_events` la tabella è l&#39;elemento secondario di `audits` e registra i dettagli aggiuntivi di un evento ticket. |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | La `Organizations` in tabella vengono registrate informazioni aziendali sugli utenti finali, ad esempio nome, ID, nomi di dominio associati, tag ed eventuali campi personalizzati. |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | La `Tickets` la tabella registra tutti i dettagli del biglietto, compresi `created_at` la marca temporale e `requester\_id` e `assignee\_id`, che consente di collegare un ticket a un utente finale e a un agente nel `Users` rispettivamente. |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | La `ticket fields` la tabella contiene informazioni sui campi di testo di base e sui campi di ticket personalizzati nel tuo account. Gli attributi di questa tabella includono il campo `ID`, `URL`, `type`, `title`, `description`, `position`, `requirement setting`, informazioni specifiche per l&#39;agente e l&#39;utente finale, nonché informazioni sulla creazione e l&#39;aggiornamento. |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | La `Users` la tabella include tutti i dettagli sugli utenti finali e gli agenti, compreso il nome e-mail dell’utente. Questo consente di analizzare sia il coinvolgimento degli utenti finali che le prestazioni degli agenti. |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | I gruppi sono il modo in cui gli agenti sono organizzati nel tuo account Zendesk. La `Groups` le informazioni relative ai record di tabella, ad esempio `group ID`, `URL`, `name`, nonché informazioni su creazione e aggiornamento. |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | Le macro sono azioni definite dall&#39;utente che modificano i valori dei campi di un ticket. Questa tabella contiene attributi quali il titolo, l&#39;ID, le azioni, le restrizioni e le informazioni di creazione e aggiornamento della macro. |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | La `Tags` La tabella contiene un elenco di tutti i tag presenti nel tuo account. |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | Questa tabella contiene dati sulle metriche dei ticket. I campi includono `ticket ID`, `URL`, e il numero di gruppi, assegnatari, riaperti, risposte, tempi di risposta (in minuti), tempo di risoluzione completa e informazioni sull&#39;ultimo aggiornamento (ad esempio, stato, assegnatario o richiedente). |

{style=&quot;table-layout:auto&quot;}

## Correlati

* [Collegamento di Zendesk](../integrations/zendesk.md)
* [Riautenticazione delle integrazioni](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations)
