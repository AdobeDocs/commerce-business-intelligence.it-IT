---
title: Previsti dati Zendesk
description: Scopri le principali tabelle di dati che puoi importare da Zendesk in Commerce Intelligence, inclusi i collegamenti alla documentazione aggiuntiva sui dati di Zendesk.
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Previsti [!DNL Zendesk] dati

Dopo che [hai connesso il tuo [!DNL Zendesk] account](../integrations/zendesk.md), puoi utilizzare [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) per tenere traccia facilmente dei campi di dati rilevanti per l&#39;analisi.

In questo argomento vengono illustrate le principali tabelle dati che è possibile importare da [!DNL Zendesk] in [!DNL Adobe Commerce Intelligence], inclusi i collegamenti alla documentazione aggiuntiva sui dati di [!DNL Zendesk].

| Nome tabella | Descrizione |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | La tabella `Audits` registra l&#39;attività associata a un ticket, incluse le modifiche di stato e le risposte sia del cliente che dell&#39;agente. Questa tabella include un ID ticket che viene collegato alla tabella `Tickets`, che consente di analizzare il tempo alla prima risposta e il tempo alla risoluzione per ogni ticket. |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | La tabella `audit_~\_events` è l&#39;elemento figlio della tabella `audits` e registra ulteriori dettagli di un evento ticket. |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | La tabella `Organizations` registra le informazioni sulla società relative agli utenti finali, ad esempio il nome, l&#39;ID, i nomi di dominio associati, i tag ed eventuali campi personalizzati. |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | La tabella `Tickets` registra tutti i dettagli del ticket, inclusi il timestamp `created_at` e `requester\_id` e `assignee\_id`, che consentono di collegare un ticket a un utente finale e a un agente rispettivamente nella tabella `Users`. |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | La tabella `ticket fields` contiene informazioni sui campi di testo di base e sui campi dei ticket personalizzati nel tuo account. Gli attributi di questa tabella includono il campo `ID`, `URL`, `type`, `title`, `description`, `position`, `requirement setting`, le informazioni specifiche dell&#39;agente e dell&#39;utente finale e le informazioni sulla creazione e l&#39;aggiornamento. |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | La tabella `Users` include tutti i dettagli sugli utenti finali e sugli agenti, inclusi il nome e l&#39;indirizzo e-mail dell&#39;utente. Questo consente di analizzare sia il coinvolgimento degli utenti finali che le prestazioni degli agenti. |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | I gruppi sono il modo in cui gli agenti sono organizzati nel tuo account Zendesk. La tabella `Groups` registra informazioni quali `group ID`, `URL`, `name` e le informazioni di creazione e aggiornamento. |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | Le macro sono azioni definite dall&#39;utente che modificano i valori dei campi di un ticket. Questa tabella contiene attributi quali il titolo della macro, l&#39;ID, le azioni, le restrizioni e le informazioni sulla creazione e l&#39;aggiornamento. |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | La tabella `Tags` contiene un elenco di tutti i tag del tuo account. |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | Questa tabella contiene dati sulle metriche dei ticket. I campi includono `ticket ID`, `URL` e il numero di gruppi, assegnatari, riaperture, risposte, tempo di risposta (in minuti), tempo di risoluzione completa e informazioni sull&#39;ultimo aggiornamento (ad esempio stato, assegnatario o richiedente). |

{style="table-layout:auto"}

## Correlato

* [Collegamento di Zendesk](../integrations/zendesk.md)
* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=it)
