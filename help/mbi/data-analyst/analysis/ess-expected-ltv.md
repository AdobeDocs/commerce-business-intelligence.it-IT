---
title: Analisi del valore del ciclo di vita previsto (LTV) (base)
description: Scopri come creare analisi per comprendere il valore del ciclo di vita dei clienti attuali e prevedere in che modo il valore del ciclo di vita aumenta con un numero maggiore di ordini.
exl-id: e6f02cf6-f542-4768-969c-3ec998a7caa9
role: Admin, User
feature: Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/bGbpknj6UfM8k995EnptIRfwZsvYTNo8-kzF9HrALQk
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: bd989d82-1e15-4534-88db-f1f51dd77ffaid: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 338
ht-degree: 0%

---

# Analisi del valore del ciclo di vita previsto

Prevedere il valore del ciclo di vita dei clienti quando effettuano più ordini è uno degli aspetti più importanti di qualsiasi azienda di qualsiasi dimensione.

Di seguito sono riportati i passaggi per creare analisi che consentano di comprendere il valore del ciclo di vita dei clienti attuali e prevedere in che modo il valore del ciclo di vita aumenta con un numero maggiore di ordini.

![valore di durata previsto](../../assets/expected_ltv_720.png)

## Creazione di una metrica

Il primo passaggio consiste nel creare una nuova metrica con i passaggi seguenti:
* Passa a **[!UICONTROL Manage Data > Metrics]**
   * Visualizza **[!UICONTROL Avg lifetime revenue]** esistente.

  >[!NOTE]
  >
  >La tabella su cui è costruita questa metrica (probabilmente `customer_entity` o `sales_order` a seconda della capacità dell&#39;archivio di accettare l&#39;estrazione guest).

   * Fare clic su **[!UICONTROL Create New Metric]** e selezionare la tabella dall&#39;alto.
   * Questa metrica esegue una **mediana** nella colonna `Customer's lifetime revenue`, ordinata da `created_at`.
      * [!UICONTROL Filters]:
         * Aggiungi `Customers we count (Saved Filter Set)` (o `Registered accounts we count`)

   * Assegnare un nome alla metrica, ad esempio `Median lifetime revenue`.

## Creazione del dashboard

Una volta creata la metrica, puoi **creare un dashboard** effettuando le seguenti operazioni:
* Passa a **[!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
* Assegna al dashboard un nome come `Expected LTV`.

* Qui puoi creare e aggiungere tutti i rapporti.

## Creazione di rapporti

>[!NOTE]
>
>Il **[!UICONTROL Time Period:]**, il periodo di tempo per ogni report è elencato come `All-time`. Puoi modificarlo in base alle tue esigenze di analisi. Adobe consiglia che tutti i rapporti in questo dashboard riguardino lo stesso periodo di tempo, ad esempio `All time`, `Year-to-date` o `Last 365 days`.

* **[!UICONTROL Average LTV (all)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average LTV (customers / non-guest checkout)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Aggiungi [!UICONTROL filters]:
         * [`A`] `Customer's group code` **Diverso Da** `Not Logged In`
         * [`B`] `Customer's lifetime number of orders` **Maggiore Di**`0`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average and Median LTV]**
   * Metrica `1`: `Avg lifetime revenue`
   * Metrica `2`: `Median lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * 
     [!UICONTROL Chart Type]: `Line`
   * Deseleziona `Multiple Y-Axes`

* **LTV per numero di ordini a vita**
   * Metrica `1`: `Avg lifetime revenue`
   * Metrica `2`: `New customers`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * [!UICONTROL Group by]: `Customer's lifetime number of orders`
   * 
     [!UICONTROL Chart Type]: `Line`

  >[!NOTE]
  >
  >Non aggiungere tutti i valori per `Customer's lifetime number of orders`. Osservare invece un punto in cui il numero di nuovi clienti raggiunge un numero limitato e aggiungere manualmente il numero di ordini del ciclo di vita di ogni cliente a tale punto. Ad esempio, se ci sono 200 clienti in un ordine, 75 in due, 15 in tre e 3 in quattro, aggiungere *1, 2 e 3*.

* Aggiungi il report [!UICONTROL Avg customer lifetime revenue by cohort] esistente.

Dopo aver generato i rapporti, consulta l’immagine nella parte superiore di questo argomento per informazioni su come organizzare i rapporti sul dashboard.
