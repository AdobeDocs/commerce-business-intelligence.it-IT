---
title: Dati Salesforce previsti
description: Scopri gli oggetti supportati e non supportati nei dati Salesforce.
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Previsto [!DNL Salesforce] dati

[Dopo la [!DNL Salesforce] installazione completata](../integrations/salesforce.md), una tabella per ogni query [oggetto](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_concepts.htm) - denominato `sf_/\{sobject-name}` - verrà creato nel data warehouse.

>[!NOTE]
>
>La struttura (colonne) di ciascuna tabella dipende dai campi contenuti nell’oggetto.

Per ottenere un elenco degli oggetti disponibili per la tua organizzazione, consulta [!DNL Salesforce] [Ottenere una documentazione sull’elenco degli oggetti](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). Dopo aver visualizzato un elenco di oggetti, estrarre il [Sezione Diagramma delle relazioni con le entità (ERD)](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) di [!DNL Salesforce] documentazione per vedere in che modo le entità si relazionano tra loro.

## Oggetti non supportati

Al momento, [!DNL Salesforce] al momento non espone i seguenti oggetti nella propria API:

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [Cos’è un oggetto esterno?](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_external_objects.htm)
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

## Correlati:

* [Collegamento [!DNL Salesforce]](../integrations/salesforce.md)
* [Riautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
