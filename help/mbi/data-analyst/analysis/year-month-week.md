---
title: Rapporti annuali, mensili e settimanali
description: Scopri come visualizzare facilmente le tendenze nel tempo e cambiare la prospettiva per i periodi di tempo che potresti voler confrontare.
exl-id: 74cf11c3-7ce0-477f-9a28-9d782e5da3d9
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Generazione di rapporti su periodi di tempo

>[!NOTE]
>
>Questo argomento contiene istruzioni per i client che utilizzano l&#39;architettura originale e la nuova architettura. Ti trovi nella [nuova architettura](../../administrator/account-management/new-architecture.md) se disponi della sezione [!DNL _Data Warehouse visualizzazioni_] dopo aver selezionato [!DNL Manage Data] dalla barra degli strumenti principale.

Il generatore di rapporti consente di visualizzare facilmente le tendenze nel tempo e di cambiare la prospettiva per i periodi di tempo che potrebbe essere utile confrontare. Questo argomento illustra come impostare una dashboard per andare a un livello più approfondito e consentire di creare rapporti per l’analisi settimana per settimana, mese per mese e anno per anno.

![](../../assets/Wow__mom__yoy.png)

Prima di iniziare, è necessario rivedere le prospettive di esplorazione in modo più dettagliato [qui](../../tutorials/using-visual-report-builder.md) e le opzioni di tempo indipendenti [qui](../../tutorials/time-options-visual-rpt-bldr.md).

Questa analisi contiene [colonne calcolate avanzate](../data-warehouse-mgr/adv-calc-columns.md).

## Colonne calcolate

* Tabella **`Sales_flat_order`**
* **Architettura originale:** le colonne seguenti sono state create da un analista come parte del ticket `[YoY WoW MoM ANALYSIS]`
* `created_at (month-day)`
* `created_at (month)`
* `created_at (day of the month)`
* `created_at (day of the week)`
* `created_at (hour of the day)`

* **Nuova architettura:** SQL elencato di seguito con la foto di un esempio per la creazione di questo calcolo
   * `created_at (month-day)` [!UICONTROL Calculation]: **to_char(A, &#39;mm-dd&#39;)**
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

* **Grafico YoY**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 years ago to 1 year ago`

   * [!UICONTROL Show top/bottom]: primi 100% in base a **`created_at (month-day)`***

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
   * Opzioni ora: `Time range (Custom)`: `2 months ago to 1 month ago`

   * Mostra in alto/in basso: primi 100% in base a **`created_at (day of month)`***

* Metrica `A`: questo mese*
* Metrica `B`: ultimo mese*
* [!UICONTROL Time period]: da un mese fa a 0 mesi fa
* 
  [!UICONTROL Interval]: None
* [!UICONTROL Group by]: `created_at (day of month)`
* 
  [!UICONTROL Chart Type]: Line

* **Grafico W**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 weeks ago to 1 week ago`

   * [!UICONTROL Show top/bottom]: primi 100% ordinati per `created_at (day of week)`

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

   * [!UICONTROL Show top/bottom]: primi 100% ordinati per `created_at (hour of day)`

* Metrica `A`: `Today`
* Metrica B: `Yesterday`
* [!UICONTROL Time period]: `1 day ago to 0 days ago`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (hour of day)`
* 
  [!UICONTROL Chart Type]: `Line`

Dopo aver compilato tutti i rapporti, puoi organizzarli nel dashboard come desideri. Il risultato potrebbe essere simile all’immagine nella parte superiore della pagina.
