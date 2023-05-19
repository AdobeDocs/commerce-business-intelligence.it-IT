---
title: Rapporti annuali, mensili e settimanali
description: Scopri come visualizzare facilmente le tendenze nel tempo e cambiare la prospettiva per i periodi di tempo che potresti voler confrontare.
exl-id: 74cf11c3-7ce0-477f-9a28-9d782e5da3d9
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Generazione di rapporti su periodi di tempo

>[!NOTE]
>
>Questo argomento contiene istruzioni per i client che utilizzano l&#39;architettura originale e la nuova architettura. Sei sul [nuova architettura](../../administrator/account-management/new-architecture.md) se ha la [!DNL _Data Warehouse visualizzazioni_] sezione disponibile dopo la selezione [!DNL Manage Data] dalla barra degli strumenti principale.

Il generatore di rapporti consente di visualizzare facilmente le tendenze nel tempo e di cambiare la prospettiva per i periodi di tempo che potrebbe essere utile confrontare. Questo argomento illustra come impostare una dashboard per andare a un livello più approfondito e consentire di creare rapporti per l’analisi settimana per settimana, mese per mese e anno per anno.

![](../../assets/Wow__mom__yoy.png)

Prima di iniziare, è necessario rivedere le prospettive in modo più dettagliato [qui](../../tutorials/using-visual-report-builder.md) e opzioni di tempo indipendenti [qui](../../tutorials/time-options-visual-rpt-bldr.md).

Questa analisi contiene [colonne calcolate avanzate](../data-warehouse-mgr/adv-calc-columns.md).

## Colonne calcolate

* **`Sales_flat_order`** tabella
* **Architettura originale:** le colonne seguenti vengono create da un analista come parte del `[YoY WoW MoM ANALYSIS]` ticket
* `created_at (month-day)`
* `created_at (month)`
* `created_at (day of the month)`
* `created_at (day of the week)`
* `created_at (hour of the day)`

* **Nuova architettura:** Di seguito sono elencate le istruzioni SQL con la foto di un esempio per la creazione di questo calcolo
   * `created_at (month-day)` [!UICONTROL Calculation]: **to_char(A, &#39;mm-gg&#39;)**
   * `created_at (month)` [!UICONTROL Calculation]: **to_char(A, &#39;mm-mese&#39;)**
   * `created_at (day of the month)`&lt; [!UICONTROL Calculation]: **to_char(A, &#39;gg&#39;)**
   * `created_at (day of the week)` [!UICONTROL Calculation]: **to_char(A, &#39;d-Day&#39;)**
   * **`created_at (hour of the day)` [!UICONTROL Calculation]: **to_char(A, &#39;hh24&#39;)**

      ![](../../assets/new-arch-create-calc.png)

## Metriche

Nessuno.

>[!NOTE]
>
>Assicurati di [aggiungere tutte le nuove colonne come dimensioni alle metriche](../data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.

## Rapporti

* **Grafico a Y**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 years ago to 1 year ago`

   * [!UICONTROL Show top/bottom]: primo 100% ordinato per **`created_at (month-day)`***

* Metrica `A`: `This year`
* Metrica `B`: `Last year`
* [!UICONTROL Time period]: `1 year ago to 0 years ago`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (month-day)`
* 
   [!UICONTROL Chart Type]: `Line`

* **Grafico MoM**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * Opzioni tempo: `Time range (Custom)`: `2 months ago to 1 month ago`

   * Mostra in alto/in basso: Primi 100% in ordine **`created_at (day of month)`***

* Metrica `A`: questo mese*
* Metrica `B`: ultimo mese*
* [!UICONTROL Time period]: da un mese fa a 0 mesi fa
* 
   [!UICONTROL Interval]: None
* [!UICONTROL Group by]: `created_at (day of month)`
* 
   [!UICONTROL Chart Type]: Line

* **Grafico a W**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 weeks ago to 1 week ago`

   * [!UICONTROL Show top/bottom]: primo 100% ordinato per `created_at (day of week)`

* Metrica `A`: `This week`
* Metrica `B`: `Last week`
* [!UICONTROL Time period]: `1 week ago to 0 weeks ago`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (day of week)`
* 
   [!UICONTROL Chart Type]: `Line`

* **Grafico DoD**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 days ago to 1 day ago`

   * [!UICONTROL Show top/bottom]: primo 100% ordinato per `created_at (hour of day)`

* Metrica `A`: `Today`
* Metrica B: `Yesterday`
* [!UICONTROL Time period]: `1 day ago to 0 days ago`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (hour of day)`
* 
   [!UICONTROL Chart Type]: `Line`

Dopo aver compilato tutti i rapporti, puoi organizzarli nel dashboard come desideri. Il risultato potrebbe essere simile all’immagine nella parte superiore della pagina.
