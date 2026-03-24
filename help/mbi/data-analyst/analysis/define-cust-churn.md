---
title: Definire l’abbandono dei clienti
description: Scopri come impostare una dashboard che ti aiuti a definire l’abbandono per i clienti transazionali.
exl-id: fea8f7e9-c84c-4d49-a657-8b75140c113a
role: Admin, Developer, User
feature: Data Warehouse Manager, Reports, Dashboards
TQID: https://experienceleague.adobe.com/eDJBh7FlhuKjBa5ft4sqAfZavmBk4V9m-Iu-26cG2VI
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 482
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
