---
title: Previsti dati Zendesk
description: Scopri le principali tabelle di dati che puoi importare da Zendesk in Commerce Intelligence, inclusi i collegamenti alla documentazione aggiuntiva sui dati di Zendesk.
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/0p4SOrpj7wM-y5j3CMpHTs7HpysB5znJu3jSNiVJ2YY
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 362
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
* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
