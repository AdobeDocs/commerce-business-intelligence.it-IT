---
title: Rapporti per l'help desk per Zendesk
description: Scopri i tuoi canali di riferimento più importanti.
exl-id: b6142ef2-2be8-401f-ac35-f86fc68d204e
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Report dell&#39;help desk per [!DNL Zendesk]

>[!NOTE]
>
>Questa opzione è disponibile solo per i client che si trovano nella `Pro` pianificare e utilizzare la nuova architettura. Se hai la `Data Warehouse Views` sezione disponibile dopo la selezione `Manage Data` dalla barra degli strumenti principale.

Consolidamento del [!DNL Zendesk] i dati con il database sulle transazioni sono un modo eccellente per comprendere meglio come i clienti interagiscono con i team di vendita o di successo dei clienti e che tipo di clienti utilizzano la piattaforma di supporto. In questo articolo viene illustrato come impostare una dashboard per ottenere rapporti granulari sulle [!DNL Zendesk] prestazioni e collegamento nei clienti transazionali.

Prima di iniziare, è necessario collegare il [[!DNL Zendesk]](../integrations/zendesk.md). Questa analisi contiene [colonne calcolate avanzate](../../data-warehouse-mgr/adv-calc-columns.md).

<!-- Getting Started -->

## Introduzione

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

### Filtrare i set da creare

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

      * `SQL Calculation` `- case when `A` is not `null` and `A!=`end-user` then `Yes` quando `B` non `null` e `B` like `%@magento.com` then `Yes` else `No` end

      * Sostituisci `@magento.com` con il tuo dominio

      * `Datatype` - `String`

* **`[Zendesk] audits_~_events`** tabella
   * Seleziona una definizione: `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] audits_~_events.author_id8`
   * [!UICONTROL One]: `[Zendesk] users.id`

   * Seleziona una [!UICONTROL table]: `[Zendesk] users`
   * Seleziona una [!UICONTROL column]: `User is agent? (Yes/No)`
   * [!UICONTROL Path]: `[Zendesk] audits_~_events.author_id = [!DNL Zendesk] users.id`

* **`Author is agent? (Yes/No)`**

* **`[Zendesk] audits`** tabella
   * Seleziona una definizione: `Exists`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] audits_~_events._id_of_parent`
   * [!UICONTROL One]: `[Zendesk] audits._id`

   * Seleziona una [!UICONTROL table]: `[Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[Zendesk] audits_~_events._id_of_parent = [Zendesk] audits._id`
   * [!UICONTROL Filter]:
   * `field_name` = `status`
   * `type` = `Change`
   * `value` = `solved`

   * Seleziona una definizione: `Exists`
   * Seleziona una [!UICONTROL table]: `[Zendesk] audits_~_events`
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

   * Seleziona una [!UICONTROL table]: `[Zendesk] users`
   * Seleziona una [!UICONTROL column]: `email`
   * [!UICONTROL Path]: `[Zendesk] tickets.requester_id = [Zendesk] users.id`

   * Seleziona una definizione: `Joined Column`
   * Seleziona una [!UICONTROL table]: `[Zendesk] users`
   * Seleziona una [!UICONTROL column]: `role`
   * [!UICONTROL Path]: `[Zendesk] tickets.requester_id = [Zendesk] users.id`

   * Seleziona una definizione: `Max`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] audits.ticket_id`
   * [!UICONTROL One]: `[Zendesk] tickets.id`

   * Seleziona una [!UICONTROL table]: `[Zendesk] audits`
   * Seleziona una [!UICONTROL column]: `created_at`
   * [!UICONTROL Path]: `[Zendesk] audits.ticket_id = [Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `status` modificato in `solved = 1`

   * Seleziona una definizione: `Min`
   * Seleziona una [!UICONTROL table]: `[Zendesk] audits`
   * Seleziona una [!UICONTROL column]: `created_at`
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

      [!UICONTROL One]: `customer_entity.email`

   * Seleziona una [!UICONTROL table]: `[Zendesk] tickets`
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
   * Seleziona una [!UICONTROL table]: `customer_entity`
   * Seleziona una [!UICONTROL column]: `User's lifetime number of support tickets requested`
   * [!UICONTROL Path]: `[Zendesk] tickets.email = customer_entity.email`

* **`Requester's lifetime number of support tickets`**

## Metriche

* **[!DNL Zendesk]Nuovi biglietti**
   * `Tickets we count`

* In **`[Zendesk] tickets`** tabella
* Questa metrica esegue un **Conteggio**
* Sulla **`id`** column
* Ordinato dal **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Biglietti risolti**
   * `Tickets we count`
   * status IN `closed, solved`

* In **`[Zendesk] tickets`** tabella
* Questa metrica esegue un **Conteggio**
* Sulla **`id`** column
* Ordinato dal **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Utenti univoci che registrano i ticket**
   * `Tickets we count`

* In **`[Zendesk] tickets`** tabella
* Questa metrica esegue un **Conteggio valori univoci**
* Sulla **`requester_id`** column
* Ordinato dal **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Tempo medio/medio di risoluzione del biglietto**
   * `Tickets we count`
   * status IN `closed, solved`

* In **`[Zendesk] tickets`** tabella
* Questa metrica esegue un **Media (o Mediana)**
* Sulla **`Seconds to resolution`** column
* Ordinato dal **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Tempo medio/medio per la prima risposta**
   * Biglietti che contiamo
   * stato IN chiuso, risolto

* In **`[Zendesk] tickets`** tabella
* Questa metrica esegue un **Media (o Mediana)**
* Sulla **`Seconds to first response`** column
* Ordinato dal **`created_at`** timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>Assicurati di [aggiungi tutte le nuove colonne come dimensioni alle metriche](../../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.

### Rapporti

* **[!UICONTROL New/Open/Pending tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * status IN `new, open, pending`

* Metrica `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Closed/Solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * status IN `solved, closed`

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
   * status IN `solved, closed`

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
   * status IN `solved, closed`

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
