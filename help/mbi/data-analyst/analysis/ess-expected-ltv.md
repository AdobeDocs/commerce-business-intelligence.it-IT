---
title: Analisi del valore del ciclo di vita previsto (LTV) (base)
description: Scopri come creare analisi per comprendere il valore del ciclo di vita dei clienti attuali e prevedere in che modo il valore del ciclo di vita aumenta con un numero maggiore di ordini.
exl-id: e6f02cf6-f542-4768-969c-3ec998a7caa9
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# Analisi del valore del ciclo di vita previsto

Prevedere il valore del ciclo di vita dei clienti quando effettuano più ordini è uno degli aspetti più importanti di qualsiasi azienda di qualsiasi dimensione.

Di seguito sono riportati i passaggi per creare analisi che consentano di comprendere il valore del ciclo di vita dei clienti attuali e prevedere in che modo il valore del ciclo di vita aumenta con un numero maggiore di ordini.

![valore del ciclo di vita previsto](../../assets/expected_ltv_720.png)

## Creazione di una metrica

Il primo passaggio consiste nel creare una nuova metrica con i passaggi seguenti:
* Accedi a **[!UICONTROL Manage Data > Metrics]**
   * Visualizza il **[!UICONTROL Avg lifetime revenue]**.

   >[!NOTE]
   >
   >La tabella su cui è costruita questa metrica (probabilmente `customer_entity` o `sales_order` a seconda della capacità del tuo negozio di accettare il pagamento come ospite.).

   * Clic **[!UICONTROL Create New Metric]** e seleziona la tabella dall’alto.
   * Questa metrica esegue una **Mediana** il `Customer's lifetime revenue` colonna, ordinata per `created_at`.
      * [!UICONTROL Filters]:
         * Aggiungi il `Customers we count (Saved Filter Set)` (o `Registered accounts we count`)
   * Assegna un nome alla metrica, ad esempio `Median lifetime revenue`.



## Creazione del dashboard

Una volta creata la metrica, puoi **creare un dashboard** in questo modo:
* Accedi a **[!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
* Assegna al dashboard un nome come `Expected LTV`.

* Qui puoi creare e aggiungere tutti i rapporti.

## Creazione di rapporti

>[!NOTE]
>
>On **[!UICONTROL Time Period:]**, il periodo di tempo per ogni rapporto è elencato come `All-time`. Puoi modificarlo in base alle tue esigenze di analisi. L’Adobe consiglia che tutti i rapporti su questo dashboard riguardino lo stesso periodo di tempo, ad esempio `All time`, `Year-to-date`, o `Last 365 days`.

* **[!UICONTROL Average LTV (all)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Interval]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average LTV (customers / non-guest checkout)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Aggiungi [!UICONTROL filters]:
         * [`A`] `Customer's group code` **Diverso da** `Not Logged In`
         * [`B`] `Customer's lifetime number of orders` **Maggiore di**`0`
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
   >Non aggiungere tutti i valori per `Customer's lifetime number of orders`. Osservare invece un punto in cui il numero di nuovi clienti raggiunge un numero limitato e aggiungere manualmente il numero di ordini del ciclo di vita di ogni cliente a tale punto. Ad esempio, se ci sono 200 clienti in un ordine, 75 in due, 15 in tre e 3 in quattro, aggiungi *1, 2 e 3*.

* Aggiungi il [!UICONTROL Avg customer lifetime revenue by cohort] rapporto.

Dopo aver generato i rapporti, consulta l’immagine nella parte superiore di questo argomento per informazioni su come organizzare i rapporti sul dashboard.
