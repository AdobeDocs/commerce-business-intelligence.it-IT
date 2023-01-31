---
title: Analisi del valore del ciclo di vita previsto (LTV) (base)
description: Scopri come creare analisi per comprendere il valore del ciclo di vita dei clienti correnti e come prevedere in che modo il valore del ciclo di vita aumenterà con più ordini.
exl-id: e6f02cf6-f542-4768-969c-3ec998a7caa9
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# Analisi del valore del ciclo di vita prevista

Prevedere il valore del ciclo di vita dei clienti in quanto fanno più ordini è uno degli aspetti più importanti di qualsiasi attività di qualsiasi dimensione.

Di seguito sono riportati i passaggi per creare analisi per comprendere il valore del ciclo di vita del cliente corrente e prevedere in che modo il valore del ciclo di vita aumenterà con più ordini:

![valore del ciclo di vita previsto](../../assets/expected_ltv_720.png)

## Creazione di una metrica

Il primo passaggio consiste nel creare una nuova metrica con i seguenti passaggi:
* Passa a **[!UICONTROL Manage Data > Metrics]**
   * Visualizza il **[!UICONTROL Avg lifetime revenue]**.

   >[!NOTE]
   >
   >Tabella su cui è basata questa metrica (probabilmente `customer_entity` o `sales_order` a seconda della capacità del negozio di accettare il pagamento degli ospiti.)

   * Fai clic su **[!UICONTROL Create New Metric]** e selezionare la tabella dall&#39;alto.
   * Questa metrica esegue un **mediana** sulla `Customer's lifetime revenue` colonna, ordinata da `created_at`.
      * [!UICONTROL Filters]:
         * Aggiungi il `Customers we count (Saved Filter Set)` o `Registered accounts we count`)
   * Assegna un nome alla metrica, ad esempio `Median lifetime revenue`.



## Creazione del dashboard

Una volta creata la metrica, puoi **creare un dashboard** facendo questo:
* Passa a **[!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
* Assegna al dashboard un nome come `Expected LTV`.

* In questo caso creeremo e aggiungeremo tutti i rapporti.

## Creazione di report

* Se non lo hai già fatto, effettua il check-out [questo video](https://fast.wistia.net/embed/iframe/24zz7wmjrt) informazioni sull’utilizzo di **[!UICONTROL Visual Report Builder] creazione di grafici, tabelle e valori scalari.

>[!NOTE]
>
>On **[!UICONTROL Time Period:]**, il periodo di tempo per ogni rapporto è elencato come `All-time`. Sentitevi liberi di modificarlo per soddisfare le vostre esigenze di analisi. È consigliabile che tutti i rapporti di questo dashboard coprano lo stesso periodo di tempo, ad esempio `All time`, `Year-to-date`oppure `Last 365 days`.

* **[!UICONTROL Average LTV (all)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL intervallo]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average LTV (customers / non-guest checkout)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Aggiungi [!UICONTROL filters]:
         * [`A`] `Customer's group code` **Diverso da** `Not Logged In`
         * [`B`] `Customer's lifetime number of orders` **Maggiore di**`0`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL intervallo]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`


* **[!UICONTROL Average and Median LTV]**
   * Metrica `1`: `Avg lifetime revenue`
   * Metrica `2`: `Median lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * 
      [!UICONTROL Tipo di grafico]: `Line`
   * Deseleziona `Multiple Y-Axes`

* **LTV per numero di ordini nel corso della vita**
   * Metrica `1`: `Avg lifetime revenue`
   * Metrica `2`: `New customers`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL intervallo]: `None`
   * [!UICONTROL Group by]: `Customer's lifetime number of orders`
   * 

      [!UICONTROL Tipo di grafico]: `Line`
   >[!NOTE]
   >
   >Non aggiungere tutti i valori per `Customer's lifetime number of orders`, guarda invece a un punto in cui il numero di nuovi clienti raggiunge un numero limitato e aggiungi manualmente a quel punto il numero di ordine nel ciclo di vita di ciascun cliente. Ad esempio, se ci sono 200 clienti in un ordine, 75 in due, 15 in tre e 3 in quattro, aggiungi *1, 2 e 3*.

* Aggiungi l&#39;esistente [!UICONTROL Avg customer lifetime revenue by cohort] rapporto.

Dopo aver creato i rapporti, fai riferimento all’immagine nella parte superiore di questo argomento per scoprire come organizzare i rapporti sul dashboard.
