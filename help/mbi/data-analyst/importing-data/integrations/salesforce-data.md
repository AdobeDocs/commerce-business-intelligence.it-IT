---
title: Dati previsti Salesforce
description: Scopri gli oggetti supportati e non supportati nei dati Salesforce.
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# Previsto [!DNL Salesforce] dati

Dopo il [[!DNL Salesforce] configurazione](../integrations/salesforce.md) è completo, una tabella per ogni query [oggetto](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_concepts.htm) - denominato `sf_/\{sobject-name}` - viene creato nella Data Warehouse.

>[!NOTE]
>
>La struttura (colonne) di ogni tabella dipende dai campi contenuti nell&#39;oggetto.

Per ottenere un elenco degli oggetti disponibili per la tua organizzazione, consulta [!DNL Salesforce] [Documentazione di Ottenere un elenco di oggetti](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). Dopo aver creato un elenco di oggetti, eseguire il Check-Out del [Sezione ERD (Entity Relationship Diagram)](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) di [!DNL Salesforce] per vedere in che modo le entità si relazionano tra loro.

## Oggetti non supportati

Attualmente, [!DNL Salesforce] al momento non espone i seguenti oggetti nella loro API:

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [Che cos&#39;è un oggetto esterno?](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_external_objects.htm)
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

* [Connessione [!DNL Salesforce]](../integrations/salesforce.md)
* [Reautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
