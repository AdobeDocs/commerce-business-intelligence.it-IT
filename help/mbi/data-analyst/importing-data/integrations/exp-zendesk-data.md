---
title: Previsti dati Zendesk
description: Scopri le principali tabelle di dati che puoi importare da Zendesk in MBI, inclusi i collegamenti alla documentazione aggiuntiva sui dati di Zendesk.
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# Previsti dati Zendesk

Dopo [hai connesso il tuo [!DNL Zendesk] account](../integrations/zendesk.md), è possibile utilizzare [Gestione Date Warehouse](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) per tracciare facilmente i campi di dati rilevanti per l’analisi.

Questo articolo esplora le tabelle di dati principali da cui è possibile importare [!DNL Zendesk] in [!DNL MBI], inclusi i collegamenti alla documentazione aggiuntiva su [!DNL Zendesk] dati.

| Nome tabella | Descrizione |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | Il `Audits` la tabella registra l’attività associata a un ticket, incluse le modifiche di stato e le risposte sia del cliente che dell’agente. Questa tabella include un ID ticket che consente di tornare al `Tickets` tabella, che consente di analizzare il tempo di prima risposta e il tempo di risoluzione per ogni ticket. |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | Il `audit_~\_events` la tabella è l&#39;elemento figlio del `audits` e registra ulteriori dettagli di un evento ticket. |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | Il `Organizations` la tabella registra le informazioni aziendali sugli utenti finali, ad esempio il nome, l’ID, i nomi di dominio associati, i tag ed eventuali campi personalizzati. |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | Il `Tickets` la tabella registra tutti i dettagli del ticket, incluso `created_at` timestamp e `requester\_id` e `assignee\_id`, che consente di collegare un ticket a un utente finale e a un agente in `Users` tabella. |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | Il `ticket fields` la tabella contiene informazioni sui campi di testo di base e sui campi dei ticket personalizzati nel tuo account. Gli attributi di questa tabella includono il campo `ID`, `URL`, `type`, `title`, `description`, `position`, `requirement setting`, informazioni specifiche sull&#39;agente e sull&#39;utente finale e informazioni sulla creazione e l&#39;aggiornamento. |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | Il `Users` la tabella include tutti i dettagli sugli utenti finali e sugli agenti, inclusi il nome e l’e-mail dell’individuo. Questo consente di analizzare sia il coinvolgimento degli utenti finali che le prestazioni degli agenti. |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | I gruppi sono il modo in cui gli agenti sono organizzati nel tuo account Zendesk. Il `Groups` le informazioni sui record di tabella come `group ID`, `URL`, `name`e informazioni sulla creazione e l&#39;aggiornamento. |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | Le macro sono azioni definite dall&#39;utente che modificano i valori dei campi di un ticket. Questa tabella contiene attributi quali il titolo della macro, l&#39;ID, le azioni, le restrizioni e le informazioni sulla creazione e l&#39;aggiornamento. |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | Il `Tags` La tabella contiene un elenco di tutti i tag presenti nel tuo account. |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | Questa tabella contiene dati sulle metriche dei ticket. I campi includono `ticket ID`, `URL`, e il numero di informazioni su gruppi, assegnatari, riaperture, risposte, tempo di risposta (in minuti), tempo di risoluzione completa e ultimo aggiornamento (ad esempio, stato, assegnatario o richiedente). |

{style="table-layout:auto"}

## Correlato

* [Collegamento di Zendesk](../integrations/zendesk.md)
* [Reautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
