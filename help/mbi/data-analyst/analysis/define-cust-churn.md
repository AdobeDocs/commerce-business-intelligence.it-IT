---
title: Definire il tasso di abbandono dei clienti
description: Scopri come impostare un dashboard che ti aiuterà a definire l’abbandono per i clienti transazionali.
exl-id: fea8f7e9-c84c-4d49-a657-8b75140c113a
source-git-commit: 3557e6370fae637cd74550b2806847bebe61d5d3
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# Abbandono dei clienti transazionali

In questo articolo viene illustrato come impostare un dashboard che ti aiuti a definire l’abbandono per i clienti transazionali.

![](../../assets/churn-deashboard.png)

Questa analisi contiene [colonne calcolate avanzate](../data-warehouse-mgr/adv-calc-columns.md).

## Colonne calcolate

Colonne da creare

* `customer_entity` tabella
* `Customer's lifetime number of orders`
* Seleziona una definizione: `Count`
* Seleziona una [!UICONTROL table]: `sales_flat_order`
* Seleziona una [!UICONTROL column]: **`entity_id`**
* [!UICONTROL Path]: sales_flat_order.customer_id = customer_entity.entity_id
* [!UICONTROL Filter]:
* Ordini contati

* `sales_flat_order` tabella
* `Customer's lifetime number of orders`
* Seleziona una definizione: Colonna unita
* Seleziona una [!UICONTROL table]: `customer_entity`
* Seleziona una [!UICONTROL column]: `Customer's lifetime number of orders`
* [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
* [!UICONTROL Filter]: `Orders we count`

* `Seconds since created_at`
* Seleziona una definizione: `Age`
* Seleziona una [!UICONTROL column]: `created_at`

* **`Customer's order number`** verrà creato da un analista come parte del **[DEFINIZIONE DELLA CHURN]** biglietto
* **`Is customer's last order`** verrà creato da un analista come parte del **[DEFINIZIONE DELLA CHURN]** biglietto
* **`Seconds since previous order`** verrà creato da un analista come parte del **[DEFINIZIONE DELLA CHURN]** biglietto
* **`Months since order`** verrà creato da un analista come parte del **[DEFINIZIONE DELLA CHURN]** biglietto
* **`Months since previous order`** verrà creato da un analista come parte del **[DEFINIZIONE DELLA CHURN]** biglietto

## Metriche

Nessuna nuova metrica!

>[!NOTE]
>
>Assicurati di [aggiungi tutte le nuove colonne come dimensioni alle metriche](../data-warehouse-mgr/manage-data-dimensions-metrics.md) prima di creare nuovi rapporti.

## Rapporti

* **Probabilità dell&#39;ordine di ripetizione iniziale**
* Metrica A: Tutti gli ordini ripetuti
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* Metrica B: Tutti gli ordini temporali
* [!UICONTROL Metric]: Numero di ordini

* [!UICONTROL Formula]: Probabilità dell&#39;ordine di ripetizione iniziale
* 
   [!Formula UICONTROL]: `A/B`
* 

   [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 

   [!UICONTROL Chart type]: `Scalar`

* **Probabilità dell&#39;ordine di ripetizione in base a mesi dall&#39;ordine**
* Metrica A: Ripeti gli ordini per mesi dall&#39;ordine precedente (nascondi)
* [!UICONTROL Metric]: `Number of orders`
* 
   [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* Metrica B: Ultimi ordini per mesi dall&#39;ordine (nascondere)
* [!UICONTROL Metric]: `Number of orders`
* 
   [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* Metrica C: Tutti gli ordini ripetuti (nascondere)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 

   [!UICONTROL Group by]: `Independent`

* Metrica D: Tutti gli ultimi ordini (nascondere)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* 

   [!UICONTROL Group by]: `Independent`

* [!UICONTROL Formula]: Probabilità dell&#39;ordine di ripetizione iniziale
* 
   [!Formula UICONTROL]: `(C-A)/(C+D-A-B)`
* 

   [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Months since previous order`
* Mostra top.bottom: Prime 24 categorie, ordinate per nome categoria

* 

   [!UICONTROL Chart type]: `Line`

Il rapporto di probabilità iniziale dell&#39;ordine di ripetizione rappresenta il rapporto Totale ordini ripetuti/Ordini totali. Ogni ordine è un&#39;opportunità per fare un ordine ripetuto; il numero di ordini di ripetizione è il sottoinsieme di quelli che effettivamente lo fanno.

La formula che usiamo semplifica (Totale ordini ripetuti che si sono verificati dopo X mesi)/ (Totale ordini che hanno almeno X mesi). Ci mostra che storicamente, dato che è stato X mesi da un ordine, c&#39;è una probabilità del Y% che l&#39;utente effettui un altro ordine.

Una volta costruito il dashboard, la domanda più comune che riceviamo è: Come si determina la soglia di abbandono?

**Non c&#39;è &quot;una risposta giusta&quot; a questo.** Tuttavia, si consiglia di trovare il punto in cui la linea attraversa il valore che è la metà del tasso di probabilità di ripetizione iniziale. Questo è il punto in cui possiamo dire &quot;Se un utente avesse intenzione di fare un ordine ripetuto, probabilmente l&#39;avrebbe già fatto&quot;. In definitiva, l&#39;obiettivo è quello di selezionare la soglia in cui ha senso passare dagli sforzi di &quot;conservazione&quot; a quelli di &quot;riattivazione&quot;.

Dopo aver compilato tutti i rapporti, puoi organizzarli nel dashboard come desideri. Il risultato finale potrebbe assomigliare all&#39;immagine nella parte superiore della pagina

In caso di domande durante la creazione di questa analisi, o se desideri semplicemente coinvolgere il nostro team di servizi professionali, [contattare il supporto](../../guide-overview.md).
