---
title: Rapporti annuali, mensili e settimanali
description: Scopri come visualizzare facilmente le tendenze nel tempo e cambiare la prospettiva per i periodi di tempo che potresti voler confrontare.
exl-id: 74cf11c3-7ce0-477f-9a28-9d782e5da3d9
role: Admin, Developer, Leader, User
feature: Reports, Dashboards
TQID: https://experienceleague.adobe.com/KHFNcuiZONPjk6D4ijyAfcPSrP84xWMOcTub80REqPM
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 301
ht-degree: 0%

---

# Generazione di rapporti su periodi di tempo

>[!NOTE]
>
>Questo argomento contiene istruzioni per i client che utilizzano l&#39;architettura originale e la nuova architettura. Ti trovi nella [nuova architettura](../../administrator/account-management/new-architecture.md) se disponi della sezione [!DNL _Visualizzazioni Data Warehouse_] dopo aver selezionato [!DNL Manage Data] dalla barra degli strumenti principale.

Il generatore di rapporti consente di visualizzare facilmente le tendenze nel tempo e di cambiare la prospettiva per i periodi di tempo che potrebbe essere utile confrontare. Questo argomento illustra come impostare una dashboard per andare a un livello più approfondito e consentire di creare rapporti per l’analisi settimana per settimana, mese per mese e anno per anno.

![Dashboard che mostra confronti settimana-su-settimana, mese-su-mese e anno-su-anno](../../assets/Wow__mom__yoy.png)

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
     ![Creare un&#39;interfaccia colonna calcolata in Data Warehouse Manager](../../assets/new-arch-create-calc.png)

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
