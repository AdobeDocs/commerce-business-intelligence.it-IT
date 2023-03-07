---
title: Rapporti helpdesk per Zendesk
description: Scopri i canali di riferimento più importanti.
exl-id: b6142ef2-2be8-401f-ac35-f86fc68d204e
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Rapporti dell&#39;helpdesk per [!DNL Zendesk]

>[!NOTE]
>
>Questa opzione è disponibile solo per i client che si trovano in `Pro` pianificare e utilizzare la nuova architettura. Sei sulla nuova architettura se disponi di `Data Warehouse Views` sezione disponibile dopo la selezione `Manage Data` dalla barra degli strumenti principale.

Consolidamento delle [!DNL Zendesk] i dati contenuti nel database transazionale sono un modo eccellente per comprendere meglio come i clienti interagiscono con i team di vendita o di successo dei clienti. Consente inoltre di conoscere il tipo di clienti che utilizzano la piattaforma di supporto. Questo articolo illustra come impostare una dashboard per ottenere rapporti granulari sul [!DNL Zendesk] prestazioni e tempi di connessione dei clienti transazionali.

Prima di iniziare, è necessario connettere il [[!DNL Zendesk]](../integrations/zendesk.md). Questa analisi contiene [colonne calcolate avanzate](../../data-warehouse-mgr/adv-calc-columns.md).

<!-- Getting Started -->

## Guida introduttiva

### Colonne da tracciare

* `audits` tabella
* `_id`
* `created_at`
* `id`
* `ticket_id`
* `_updated_at`

* `audits_~_events` tabella
* `_sub_id`
* `_id_of_parent`
* `author_id`
* `field_name`
* `public`
* `type`
* `value`

* `tickets` tabella
* `_id`
* `assignee_id`
* `created_at`
* `id`
* `requester_id`
* `status`
* `updated_at`
* `via_~_source_~_from_~_address`
* `_updated_at`

* `users` tabella
* `_id`
* `created_at`
* `emails`
* `id`
* `role`
* `updated_at`
* `_updated_at`

### Set di filtri da creare

* `[!DNL Zendesk] Tickets` tabella
   * `status != deleted`

* `Filter set name`: `Tickets we count`
* `Filter set logic`:

## Colonne calcolate

### Colonne da creare

* **`[!DNL Zendesk] user's`** tabella
   * `User is agent? (Yes/No) `
   * 
      * `Column type` - `Same Table > Calculation`

      * `Input columns` - `role`, `email`

      * `SQL Calculation` `- case when `A` is not `nulle` and `R!=`end-user` allora `Yes` quando `B` non è `null` e `B` mi piace `%@magento.com` allora `Yes` else `No` fine

      * Sostituisci `@magento.com` con il tuo dominio

      * `Datatype` - `String`

* **`[Zendesk] audits_~_events`** tabella
   * Seleziona una definizione: `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] audits_~_events.author_id8`
   * [!UICONTROL One]: `[Zendesk] users.id`

   * Seleziona un [!UICONTROL table]: `[Zendesk] users`
   * Seleziona un [!UICONTROL column]: `User is agent? (Yes/No)`
   * [!UICONTROL Path]: `[Zendesk] audits_~_events.author_id = [!DNL Zendesk] users.id`

* **`Author is agent? (Yes/No)`**

* **`[Zendesk] audits`** tabella
   * Seleziona una definizione: `Exists`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] audits_~_events._id_of_parent`
   * [!UICONTROL One]: `[Zendesk] audits._id`

   * Seleziona un [!UICONTROL table]: `[Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[Zendesk] audits_~_events._id_of_parent = [Zendesk] audits._id`
   * [!UICONTROL Filter]:
   * `field_name` = `status`
   * `type` = `Change`
   * `value` = `solved`

   * Seleziona una definizione: `Exists`
   * Seleziona un [!UICONTROL table]: `[Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[Zendesk] audits_~_events._id_of_parent = [Zendesk] audits._id`
   * [!UICONTROL Filter]: `Author is agent? (Yes/No)`
   * `type` = `Comment`
   * `public` = `1`

* **`Status changes to solved? (1/0)`**
* **`Is agent comment? (1/0)`**

* **`[Zendesk] Tickets`** tabella
   * Seleziona una definizione: `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] tickets.requester_id`
   * [!UICONTROL One]: `[Zendesk] users.id`

   * Seleziona un [!UICONTROL table]: `[Zendesk] users`
   * Seleziona un [!UICONTROL column]: `email`
   * [!UICONTROL Path]: `[Zendesk] tickets.requester_id = [Zendesk] users.id`

   * Seleziona una definizione: `Joined Column`
   * Seleziona un [!UICONTROL table]: `[Zendesk] users`
   * Seleziona un [!UICONTROL column]: `role`
   * [!UICONTROL Path]: `[Zendesk] tickets.requester_id = [Zendesk] users.id`

   * Seleziona una definizione: `Max`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] audits.ticket_id`
   * [!UICONTROL One]: `[Zendesk] tickets.id`

   * Seleziona un [!UICONTROL table]: `[Zendesk] audits`
   * Seleziona un [!UICONTROL column]: `created_at`
   * [!UICONTROL Path]: `[Zendesk] audits.ticket_id = [Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `status` è stato modificato in `solved = 1`

   * Seleziona una definizione: `Min`
   * Seleziona un [!UICONTROL table]: `[Zendesk] audits`
   * Seleziona un [!UICONTROL column]: `created_at`
   * [!UICONTROL Path]: `[Zendesk] audits.ticket_id = [Zendesk] tickets.id`
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

      * `Datatype` - Intero

* **`Ticket created_at (day of week)`**
   * 
      * `Column type` - &quot;Stessa tabella > Calcolo&quot;

      * `Input columns` - `created_at`

      * `Calculation` - `to_char(A,'D')||'. '||to_char(A,'Day')`

      *`Datatype` – `String`


* **`customer_entity`** tabella
   * Seleziona una definizione: `Count`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] tickets.email`
   * 

      [!UICONTROL Uno]: `customer_entity.email`

   * Seleziona un [!UICONTROL table]: `[Zendesk] tickets`
   * [!UICONTROL Path]: `[Zendesk] tickets.email = customer_entity.email`
   * [!UICONTROL Filter]:
   * `Tickets we count`

* **`User's lifetime number of support tickets requested`**
* **`Has user filed a support ticket? (Yes/No)`**
   * 
      * `Column type` - &quot;Stessa tabella > Calcolo&quot;

      * `Input columns` - `User's lifetime number of support tickets requested`

      * `Calculation` - `case when A>0 then 'Yes' else 'No' end`

      * `Datatype` – `String`

* **`[Zendesk] Tickets`** tabella
   * Seleziona una definizione: `Joined Column`
   * Seleziona un [!UICONTROL table]: `customer_entity`
   * Seleziona un [!UICONTROL column]: `User's lifetime number of support tickets requested`
   * [!UICONTROL Path]: `[Zendesk] tickets.email = customer_entity.email`

* **`Requester's lifetime number of support tickets`**

## Metriche

* **[!DNL Zendesk]Nuovi biglietti**
   * `Tickets we count`

* In **`[Zendesk] tickets`** tabella
* Questa metrica esegue una **Conteggio**
* Il giorno **`id`** colonna
* Ordinato da **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Ticket risolti**
   * `Tickets we count`
   * stato IN `closed, solved`

* In **`[Zendesk] tickets`** tabella
* Questa metrica esegue una **Conteggio**
* Il giorno **`id`** colonna
* Ordinato da **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Utenti distinti che presentano ticket**
   * `Tickets we count`

* In **`[Zendesk] tickets`** tabella
* Questa metrica esegue una **Count Distinct**
* Il giorno **`requester_id`** colonna
* Ordinato da **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Tempo medio/mediano di risoluzione ticket**
   * `Tickets we count`
   * stato IN `closed, solved`

* In **`[Zendesk] tickets`** tabella
* Questa metrica esegue un **Media (o Mediana)**
* Il giorno **`Seconds to resolution`** colonna
* Ordinato da **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Tempo medio/mediano alla prima risposta**
   * Ticket conteggiati
   * stato IN chiuso, risolto

* In **`[Zendesk] tickets`** tabella
* Questa metrica esegue un **Media (o Mediana)**
* Il giorno **`Seconds to first response`** colonna
* Ordinato da **`created_at`** timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>Assicurati di [aggiungere tutte le nuove colonne come dimensioni alle metriche](../../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.

### Rapporti

* **[!UICONTROL New/Open/Pending tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * stato IN `new, open, pending`

* Metrica `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Closed/Solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * stato IN `solved, closed`

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
   * stato IN `solved, closed`

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
   * stato IN `solved, closed`

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
