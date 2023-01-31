---
title: Churn Commercio
description: Scopri come generare e analizzare il tasso di abbandono di Commerce.
exl-id: 8775cf0a-114d-4b48-8bd2-fc1700c59a12
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# Tasso di abbandono

In questo argomento, dimostriamo come calcolare un **tasso di abbandono** per **clienti commerciali**. A differenza di SaaS o di società di abbonamento tradizionali, i clienti di commercio generalmente non hanno un **&quot;evento di abbandono&quot;** per mostrare che non devono più contare verso i clienti attivi. Per questo motivo, le istruzioni riportate di seguito ti consentono di definire un cliente come &quot;eseguito&quot; in base a un determinato lasso di tempo trascorso dal suo ultimo ordine.

![](../../assets/Churn_rate_image.png)

Molti clienti desiderano assistenza per iniziare a concepire cosa **arco temporale** dovrebbero utilizzare in base ai loro dati. Se desideri utilizzare il comportamento storico dei clienti per definire questo **arco temporale di abbandono**, potresti voler acquisire familiarità con il [definizione di abbandono](../analysis/define-cust-churn.md) articolo. Quindi, puoi utilizzare i risultati nella formula per il tasso di abbandono nelle istruzioni riportate di seguito.

## Colonne calcolate

Colonne da creare

* **`customer_entity`** tabella
* **`Customer's last order date`**
   * Seleziona una [!UICONTROL definition]: `Max`
   * Seleziona [!UICONTROL table]: `sales_flat_order`
   * Seleziona [!UICONTROL column]: `created_at`
   * `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]: `Orders we count`

* **`Seconds since customer's last order date`**
   * Seleziona una [!UICONTROL definition]: `Age`
   * Seleziona [!UICONTROL column]: `Customer's last order date`

>[!NOTE]
>
>Assicurati di [aggiungi tutte le nuove colonne come dimensioni alle metriche](../data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.

## Metriche

* **Nuovi clienti (per data primo ordine)**
   * Clienti contati

>[!NOTE]
>
>Questa metrica potrebbe già esistere sul tuo account.

* In **`customer_entity`** tabella
* Questa metrica esegue un **Conteggio**
* Sulla **`entity_id`** column
* Ordinato dal **`Customer's first order date`** timestamp
* [!UICONTROL Filter]:

* **Nuovi clienti (per data ultimo ordine)**
   * Clienti contati

>[!NOTE]
>
>Questa metrica potrebbe già esistere sul tuo account.

* In **`customer_entity`** tabella
* Questa metrica esegue un **Conteggio**
* Sulla **`entity_id`** column
* Ordinato dal **`Customer's last order date`** timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>Assicurati di [aggiungi tutte le nuove colonne come dimensioni alle metriche](../data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.

## Rapporti

* **Tasso di abbandono**
   * [!UICONTROL Metric]: Nuovi clienti (per data primo ordine)
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
      [!UICONTROL Perspective]: `Cumulative`
   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]:
   * Secondi dall&#39;ultima data dell&#39;ordine del cliente >= [Taglio definito automaticamente per i clienti con scadenza ]**`^`**
   * `Lifetime number of orders Greater Than 0`

   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
      [!UICONTROL Perspective]: Cumulative
   * [!UICONTROL Formula]: `(B / ((A + B) - C)`
   * 

      [!UICONTROL Format]: Percentage

* *Metrica `A`:`New customers cumulative`*
* *Metrica `B`:`Churned customers by last order date`*
* *Metrica `C`:`Customers by last order date cumulative`*
* *`Formula`:`Repeat order probability`*
* *`Time period`:`All time (or custom range)`*
* *`Group by`:`Customer's order number`*
* *`Chart Type`:`Column`*

Di seguito sono riportate alcune conversioni mese > secondo, ma google fornisce altri valori, tra cui settimana > secondi di conversioni per eventuali valori personalizzati che si potrebbero cercare.

| **Mesi** | **Seconds** |
|---|---|
| 3 | 7.776.000 |
| 6 | 15.552.000 |
| 9 | 23.328.000 |
| 12 | 31.104.000 |

Dopo aver compilato tutti i rapporti, puoi organizzarli nel dashboard come desideri. Il risultato finale potrebbe assomigliare al dashboard di esempio riportato sopra.
