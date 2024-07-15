---
title: Dati previsti Salesforce
description: Scopri gli oggetti supportati e non supportati nei dati Salesforce.
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# Previsti [!DNL Salesforce] dati

Al termine dell&#39;[[!DNL Salesforce] installazione](../integrations/salesforce.md), nella Data Warehouse verrà creata una tabella per ogni [oggetto](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_concepts.htm) interrogabile, denominato `sf_/\{sobject-name}`.

>[!NOTE]
>
>La struttura (colonne) di ogni tabella dipende dai campi contenuti nell&#39;oggetto.

Per ottenere un elenco di oggetti disponibili per la tua organizzazione, consulta [!DNL Salesforce] [Documentazione di Get a List of Objects](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). Dopo aver creato un elenco di oggetti, consultare la sezione [ERD (Entity Relationship Diagram)](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) della documentazione di [!DNL Salesforce] per verificare la correlazione tra le entità.

## Oggetti non supportati

Attualmente, [!DNL Salesforce] non espone i seguenti oggetti nella loro API:

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [Cos&#39;è un oggetto esterno?](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_external_objects.htm)
* `CollaborationGroupRecord`
* `ContentDocument`
* `ContentDocumentLink`
* `FeedItem`
* `FieldDefinition`
* `IdeaComment`
* `ListViewChartInstance`
* `Order`
* `PlatformAction`

* `KnowledgeArticleVersion`
* `NewsFeed`
* `RecentlyViewed`
* `TopicAssignment`
* `UserRecordAccess`
* `UserProfileFeed`
* `Vote`

## Correlato:

* [Connessione in corso  [!DNL Salesforce]](../integrations/salesforce.md)
* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
