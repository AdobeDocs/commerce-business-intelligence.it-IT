---
title: Rapporti helpdesk per Zendesk
description: Scopri i canali di riferimento più importanti.
exl-id: b6142ef2-2be8-401f-ac35-f86fc68d204e
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/2X87aaT7tJ-Rn6TK7g084p5OB-iML0vPaJlRUYAIesQ
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 392
ht-degree: 0%

---

# Report helpdesk per [!DNL Zendesk]

>[!NOTE]
>
>Questa opzione è disponibile solo per i client inclusi nel piano `Pro` che utilizzano la nuova architettura. La nuova architettura è attiva se è disponibile la sezione `Data Warehouse Views` dopo aver selezionato `Manage Data` dalla barra degli strumenti principale.

Il consolidamento dei dati di [!DNL Zendesk] con il database transazionale è un modo eccellente per comprendere meglio come i clienti interagiscono con i team di vendita o di successo dei clienti. Consente inoltre di conoscere il tipo di clienti che utilizzano la piattaforma di supporto. In questo argomento viene illustrato come impostare un dashboard per ottenere rapporti granulari sulle prestazioni di [!DNL Zendesk] e sul tempo di connessione ai clienti transazionali.

Prima di iniziare, connettere [[!DNL Zendesk]](../integrations/zendesk.md). Questa analisi contiene [colonne calcolate avanzate](../../data-warehouse-mgr/adv-calc-columns.md).

<!-- Getting Started -->

## Guida introduttiva

### Colonne da tracciare

* Tabella `audits`
* `_id`
* `created_at`
* `id`
* `ticket_id`
* `_updated_at`

* Tabella `audits_~_events`
* `_sub_id`
* `_id_of_parent`
* `author_id`
* `field_name`
* `public`
* `type`
* `value`

* Tabella `tickets`
* `_id`
* `assignee_id`
* `created_at`
* `id`
* `requester_id`
* `status`
* `updated_at`
* `via_~_source_~_from_~_address`
* `_updated_at`

* Tabella `users`
* `_id`
* `created_at`
* `emails`
* `id`
* `role`
* `updated_at`
* `_updated_at`

### Set di filtri da creare

* Tabella `[!DNL Zendesk] Tickets`
   * `status != deleted`

* `Filter set name`: `Tickets we count`
* `Filter set logic`:

## Colonne calcolate

### Colonne da creare

* Tabella **`[!DNL Zendesk] user's`**
   * `User is agent? (Yes/No) `
   * 
      * `Column type` - `Same Table > Calculation`

      * `Input columns` - `role`, `email`

      * `SQL Calculation` `- case when `A` is not `null` and `A!=`end-user` then `Yes` quando `B` non è `null` e `B` come `%@magento.com` allora `Yes` else `No` end

      * Sostituisci `@magento.com` con il tuo dominio

      * `Datatype` - `String`

* Tabella **`[!DNL Zendesk] audits_~_events`**
   * Selezionare una definizione: `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events.author_id8`
   * [!UICONTROL One]: `[!DNL Zendesk] users.id`

   * Seleziona [!UICONTROL table]: `[!DNL Zendesk] users`
   * Seleziona [!UICONTROL column]: `User is agent? (Yes/No)`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events.author_id = [!DNL Zendesk] users.id`

* **`Author is agent? (Yes/No)`**

* Tabella **`[!DNL Zendesk] audits`**
   * Selezionare una definizione: `Exists`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events._id_of_parent`
   * [!UICONTROL One]: `[!DNL Zendesk] audits._id`

   * Seleziona [!UICONTROL table]: `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]:
   * `field_name` = `status`
   * `type` = `Change`
   * `value` = `solved`

   * Selezionare una definizione: `Exists`
   * Seleziona [!UICONTROL table]: `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]: `Author is agent? (Yes/No)`
   * `type` = `Comment`
   * `public` = `1`

* **`Status changes to solved? (1/0)`**
* **`Is agent comment? (1/0)`**

* Tabella **`[!DNL Zendesk] Tickets`**
   * Selezionare una definizione: `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] tickets.requester_id`
   * [!UICONTROL One]: `[!DNL Zendesk] users.id`

   * Seleziona [!UICONTROL table]: `[!DNL Zendesk] users`
   * Seleziona [!UICONTROL column]: `email`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * Selezionare una definizione: `Joined Column`
   * Seleziona [!UICONTROL table]: `[!DNL Zendesk] users`
   * Seleziona [!UICONTROL column]: `role`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * Selezionare una definizione: `Max`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits.ticket_id`
   * [!UICONTROL One]: `[!DNL Zendesk] tickets.id`

   * Seleziona [!UICONTROL table]: `[!DNL Zendesk] audits`
   * Seleziona [!UICONTROL column]: `created_at`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `status` è cambiato in `solved = 1`

   * Selezionare una definizione: `Min`
   * Seleziona [!UICONTROL table]: `[!DNL Zendesk] audits`
   * Seleziona [!UICONTROL column]: `created_at`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `Is agent comment? = 1`

* `Requester's email`
* `Requester's role`
* `Ticket's latest solved date`
* `First agent response date`
* `Seconds to resolution`
   * 
      * `Column type` - `Same Table > Date Difference`

      * `Ticket's latest solved date` meno `created_at`

* **`Seconds to first response`**
   * 
      * `Column type` - `Same Table > Date Difference`

      * `First agent response date` meno `created_at`

* **`Requester's ticket number`**
   * 
      * `Column type` - `Same Table > Event Number`

      * `Event Owner` - `requester_id`

      * `Event Rank` - `created_at`

* **`Ticket created_at (hour of day)`**
   * 
      * `Column type` - &quot;Stessa tabella > Calcolo&quot;

      * `Input columns` - `created_at`

      * `SQL Calculation` - `to_char(A,'HH24')::int`

      * `Datatype` - Numero intero

* **`Ticket created_at (day of week)`**
   * 
      * `Column type` - &quot;Stessa tabella > Calcolo&quot;

      * `Input columns` - `created_at`

      * `Calculation` - `to_char(A,'D')||'. '||to_char(A,'Day')`

     *`Datatype` - `String`

* Tabella **`customer_entity`**
   * Selezionare una definizione: `Count`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] tickets.email`
   * 
     [!UICONTROL Uno]: `customer_entity.email`

   * Seleziona [!UICONTROL table]: `[!DNL Zendesk] tickets`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`
   * [!UICONTROL Filter]:
   * `Tickets we count`

* **`User's lifetime number of support tickets requested`**
* **`Has user filed a support ticket? (Yes/No)`**
   * 
      * `Column type` - &quot;Stessa tabella > Calcolo&quot;

      * `Input columns` - `User's lifetime number of support tickets requested`

      * `Calculation` - `case when A>0 then 'Yes' else 'No' end`

      * `Datatype` - `String`

* Tabella **`[!DNL Zendesk] Tickets`**
   * Selezionare una definizione: `Joined Column`
   * Seleziona [!UICONTROL table]: `customer_entity`
   * Seleziona [!UICONTROL column]: `User's lifetime number of support tickets requested`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`

* **`Requester's lifetime number of support tickets`**

## Metriche

* **[!DNL Zendesk]nuovi biglietti**
   * `Tickets we count`

* Nella tabella **`[!DNL Zendesk] tickets`**
* Questa metrica esegue **Count**
* Nella colonna **`id`**
* Ordinato per la marca temporale **`created_at`**
* [!UICONTROL Filter]:

* **[!DNL Zendesk]ticket risolti**
   * `Tickets we count`
   * Stato IN `closed, solved`

* Nella tabella **`[!DNL Zendesk] tickets`**
* Questa metrica esegue **Count**
* Nella colonna **`id`**
* Ordinato per la marca temporale **`created_at`**
* [!UICONTROL Filter]:

* **[!DNL Zendesk]utenti distinti che compilano i ticket**
   * `Tickets we count`

* Nella tabella **`[!DNL Zendesk] tickets`**
* Questa metrica esegue **Count Distinct**
* Nella colonna **`requester_id`**
* Ordinato per la marca temporale **`created_at`**
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Tempo medio/mediano di risoluzione ticket**
   * `Tickets we count`
   * Stato IN `closed, solved`

* Nella tabella **`[!DNL Zendesk] tickets`**
* Questa metrica esegue una **media (o mediana)**
* Nella colonna **`Seconds to resolution`**
* Ordinato per la marca temporale **`created_at`**
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Tempo medio/mediano alla prima risposta**
   * Ticket conteggiati
   * stato IN chiuso, risolto

* Nella tabella **`[!DNL Zendesk] tickets`**
* Questa metrica esegue una **media (o mediana)**
* Nella colonna **`Seconds to first response`**
* Ordinato per la marca temporale **`created_at`**
* [!UICONTROL Filter]:

>[!NOTE]
>
>Assicurati di [aggiungere tutte le nuove colonne come dimensioni alle metriche](../../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.

### Rapporti

* **[!UICONTROL New/Open/Pending tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * Stato IN `new, open, pending`

* Metrica `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Closed/Solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * Stato IN `solved, closed`

* Metrica `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to first response]**
   * [!UICONTROL Metric]: `Average time to first response`

* Metrica `A`: `Average time to first response`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to resolution]**
   * [!UICONTROL Metric]: `Average time to resolution`
   * [!UICONTROL Filter]:
   * Stato IN `solved, closed`

* Metrica `A`: `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Tickets by status]**
   * [!UICONTROL Metric]: `New Tickets`

* Metrica `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `status`
* `Chart Type`: `Stacked Column`

* **[!UICONTROL Number of new and solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`

   * [!UICONTROL Metric]: `New Tickets`

* Metrica `A`: `New tickets`
* Metrica `B`: `Solved tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Line`

* **[!UICONTROL Time to first response]**
   * [!UICONTROL Metric]: `Average time to first response`

* Metrica `A`: `Average time to first response`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Time to resolution]**
   * [!UICONTROL Metric]: `Average time to resolution`
   * [!UICONTROL Filter]:
   * Stato IN `solved, closed`

* Metrica `A`: `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Distinct users filing tickets]**
   * [!UICONTROL Metric]: `Distinct users filing tickets`

* Metrica `A`: `Distinct users filing tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Peak ticket days]**
   * [!UICONTROL Metric]: `New Tickets`

* Metrica `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (day of week)`
* `Chart Type`: `Pie`

* **[!UICONTROL Peak ticket hours]**
   * [!UICONTROL Metric]:`New Tickets`

   * `Show top/bottom`: `Top 100% sorted by created_at (hour of the day)`

* Metrica `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (hour of the day)`
* `Chart Type`: `Pie`

* **[!UICONTROL Avg LTV of users who have and have not filed tickets]**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* Metrica `A`: `Average lifetime revenue`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`

* **[!UICONTROL Number of new users who have and have not filed tickets]**
   * 
     [!UICONTROL Metric]: Users

* Metrica `A`: `New users`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`
