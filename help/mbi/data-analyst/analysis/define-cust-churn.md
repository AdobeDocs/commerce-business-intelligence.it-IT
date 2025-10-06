---
title: Definire l’abbandono dei clienti
description: Scopri come impostare una dashboard che ti aiuti a definire l’abbandono per i clienti transazionali.
exl-id: fea8f7e9-c84c-4d49-a657-8b75140c113a
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# Abbandono dei clienti transazionali

Questo argomento illustra come impostare una dashboard che ti aiuti a definire l’abbandono per i clienti transazionali.

![Dashboard di abbandono dei clienti che mostra la frequenza di abbandono e le metriche di conservazione](../../assets/churn-deashboard.png)

Questa analisi contiene [colonne calcolate avanzate](../data-warehouse-mgr/adv-calc-columns.md).

## Colonne calcolate

Colonne da creare

* Tabella `customer_entity`
* `Customer's lifetime number of orders`
* Selezionare una definizione: `Count`
* Seleziona [!UICONTROL table]: `sales_flat_order`
* Seleziona [!UICONTROL column]: **`entity_id`**
* [!UICONTROL Path]: sales_flat_order.customer_id = customer_entity.entity_id
* [!UICONTROL Filter]:
* Ordini conteggiati

* Tabella `sales_flat_order`
* `Customer's lifetime number of orders`
* Seleziona una definizione: colonna unita
* Seleziona [!UICONTROL table]: `customer_entity`
* Seleziona [!UICONTROL column]: `Customer's lifetime number of orders`
* [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
* [!UICONTROL Filter]: `Orders we count`

* `Seconds since created_at`
* Selezionare una definizione: `Age`
* Seleziona [!UICONTROL column]: `created_at`

* **`Customer's order number`** è stato creato da un analista come parte del **[ticket DEFINIZIONE ABBANDONO]**
* **`Is customer's last order`** è stato creato da un analista come parte del **[ticket DEFINIZIONE ABBANDONO]**
* **`Seconds since previous order`** è stato creato da un analista come parte del **[ticket DEFINIZIONE ABBANDONO]**
* **`Months since order`** è stato creato da un analista come parte del **[ticket DEFINIZIONE ABBANDONO]**
* **`Months since previous order`** è stato creato da un analista come parte del **[ticket DEFINIZIONE ABBANDONO]**

## Metriche

Nessuna nuova metrica.

>[!NOTE]
>
>Assicurati di [aggiungere tutte le nuove colonne come dimensioni alle metriche](../data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.

## Rapporti

* **Probabilità ordine di ripetizione iniziale**
* Metrica A: Ordini ripetuti in qualsiasi momento
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* Metrica B: Ordini di tutti i tempi
* [!UICONTROL Metric]: numero di ordini

* [!UICONTROL Formula]: probabilità ordine di ripetizione iniziale
* 
  [!UICONTROL Formula]: `A/B`
* 
  [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart type]: `Scalar`

* **Probabilità di ripetizione ordine fornita mesi dall&#39;ordine**
* Metrica A: ripetere gli ordini per mesi dall’ordine precedente (nascondere)
* [!UICONTROL Metric]: `Number of orders`
* 
  [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* Metrica B: Ultimi ordini per mesi dall’ordine (nascondi)
* [!UICONTROL Metric]: `Number of orders`
* 
  [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* Metrica C: Ordini ripetuti in qualsiasi momento (nascondi)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 
  [!UICONTROL Raggruppa per]: `Independent`

* Metrica D: Ultimi ordini in qualsiasi momento (nascondi)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* 
  [!UICONTROL Raggruppa per]: `Independent`

* [!UICONTROL Formula]: probabilità ordine di ripetizione iniziale
* 
  [!UICONTROL Formula]: `(C-A)/(C+D-A-B)`
* 
  [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Months since previous order`
* Mostra top.bottom: prime 24 categorie, ordinate per nome di categoria

* 
  [!UICONTROL Chart type]: `Line`

Il rapporto probabilità ordine ripetuto iniziale rappresenta il totale ordini ripetuti / totale ordini. Ogni ordine è un&#39;opportunità per fare un ordine ripetuto; il numero di ordini ripetuti è il sottoinsieme di quelli che effettivamente lo fanno.

La formula utilizzata è semplificata in (Totale ordini ripetuti dopo X mesi)/ (Totale ordini che hanno almeno X mesi). Ci mostra che storicamente, dato che sono passati X mesi da un ordine, c&#39;è una probabilità Y% che l&#39;utente faccia un altro ordine.

Una volta creato il dashboard, la domanda più comune è: come si utilizza questo valore per determinare una soglia di abbandono?

**Non esiste un&#39;unica risposta corretta.** Tuttavia, Adobe consiglia di trovare il punto in cui la linea interseca il valore che è la metà della percentuale di probabilità di ripetizione iniziale. Questo è il punto in cui si può dire &quot;Se un utente sta per fare un ordine di ripetizione, probabilmente lo avrebbe già fatto a questo punto.&quot; In ultima analisi, l’obiettivo è quello di selezionare la soglia in cui ha senso passare dagli sforzi di &quot;conservazione&quot; a quelli di &quot;riattivazione&quot;.

Dopo aver compilato tutti i rapporti, puoi organizzarli nel dashboard come desideri. Il risultato potrebbe essere simile all’immagine nella parte superiore della pagina

Per qualsiasi domanda durante la creazione di questa analisi, o semplicemente per coinvolgere il team Professional Services, [contatta il supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
