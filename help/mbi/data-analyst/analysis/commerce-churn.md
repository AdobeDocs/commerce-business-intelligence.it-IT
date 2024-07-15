---
title: Abbandono Commerce
description: Scopri come generare e analizzare la frequenza di abbandono di Commerce.
exl-id: 8775cf0a-114d-4b48-8bd2-fc1700c59a12
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 2%

---

# Frequenza di abbandono

In questo argomento viene illustrato come calcolare una **frequenza di abbandono** per i **clienti commerce**. A differenza di SaaS o delle società di abbonamento tradizionali, i clienti commerce in genere non hanno un **&quot;evento di abbandono&quot;** concreto per mostrare che non dovrebbero più contare verso i tuoi clienti attivi. Per questo motivo, le istruzioni di seguito consentono di definire un cliente come &quot;abbandonato&quot; in base a una determinata quantità di tempo trascorso dal suo ultimo ordine.

![](../../assets/Churn_rate_image.png)

Molti clienti desiderano assistenza per iniziare a concettualizzare **l&#39;intervallo di tempo** da utilizzare in base ai propri dati. Se desideri utilizzare il comportamento storico del cliente per definire questo **intervallo di abbandono**, puoi acquisire familiarità con l&#39;[argomento definizione dell&#39;abbandono](../analysis/define-cust-churn.md). Quindi, puoi utilizzare i risultati nella formula per il tasso di abbandono nelle istruzioni seguenti.

## Colonne calcolate

Colonne da creare

* Tabella **`customer_entity`**
* **`Customer's last order date`**
   * Seleziona [!UICONTROL definition]: `Max`
   * Seleziona [!UICONTROL table]: `sales_flat_order`
   * Seleziona [!UICONTROL column]: `created_at`
   * `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]: `Orders we count`

* **`Seconds since customer's last order date`**
   * Seleziona [!UICONTROL definition]: `Age`
   * Seleziona [!UICONTROL column]: `Customer's last order date`

>[!NOTE]
>
>Assicurati di [aggiungere tutte le nuove colonne come dimensioni alle metriche](../data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.

## Metriche

* **Nuovi clienti (per data primo ordine)**
   * Clienti conteggiati

>[!NOTE]
>
>Questa metrica potrebbe esistere sul tuo account.

* Nella tabella **`customer_entity`**
* Questa metrica esegue **Count**
* Nella colonna **`entity_id`**
* Ordinato per la marca temporale **`Customer's first order date`**
* [!UICONTROL Filter]:

* **Nuovi clienti (per data ultimo ordine)**
   * Clienti conteggiati

  >[!NOTE]
  >
  >Questa metrica potrebbe esistere sul tuo account.

* Nella tabella **`customer_entity`**
* Questa metrica esegue **Count**
* Nella colonna **`entity_id`**
* Ordinato per la marca temporale **`Customer's last order date`**
* [!UICONTROL Filter]:

>[!NOTE]
>
>Assicurati di [aggiungere tutte le nuove colonne come dimensioni alle metriche](../data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.

## Rapporti

* **Frequenza di abbandono**
   * [!UICONTROL Metric]: nuovi clienti (per data primo ordine)
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
     [!UICONTROL Perspective]: `Cumulative`
   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]:
   * Secondi trascorsi dall&#39;ultima data dell&#39;ordine del cliente >= [Limite predefinito per i clienti abbandonati ]**`^`**
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

Di seguito sono riportati alcuni mesi comuni > seconde conversioni, ma google fornisce altri valori, tra cui settimana > secondi conversioni per eventuali valori personalizzati che potresti cercare.

| **Mesi** | **Secondi** |
|---|---|
| 3 | 7.776.000 |
| 6 | 15.552.000 |
| 9 | 23.328.000 |
| 12 | 31.104.000 |

Dopo aver compilato tutti i rapporti, puoi organizzarli nel dashboard come desideri. Il risultato potrebbe essere simile al dashboard di esempio riportato sopra.
