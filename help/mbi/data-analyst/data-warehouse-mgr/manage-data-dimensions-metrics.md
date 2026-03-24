---
title: Gestione delle dimensioni dati
description: Scopri cos’è una dimensione che può essere utilizzata per filtrare o segmentare i grafici in base a una metrica.
exl-id: 143a4b1e-2e6f-438a-90e6-bdda13b39cb9
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/0q2fVRWwNd21eyyO7WyYKlENLArkw325oq4YLNIRfLg
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12bid: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 419
ht-degree: 0%

---

# Gestione delle dimensioni dati

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../administrator/user-management/user-management.md).

Una dimensione è un campo nella stessa tabella di una metrica che può essere utilizzata per filtrare o segmentare i grafici basati su tale metrica. Ad esempio, una metrica dei ricavi può contenere città, stato, paese, stato dell’ordine, codice coupon e altri tipi di dimensioni.

## Aggiungere dimensioni a più metriche

Per aggiungere una o più dimensioni a più metriche contemporaneamente:

1. Vai a **[!UICONTROL Manage Data > Metrics]**.

1. Fare clic su **[!UICONTROL Add Dimensions To Metric(s)]**.

1. Selezionate la tabella contenente le quote.

1. Nella colonna `Choose Metric(s) to Add Dimensions` selezionare le metriche a cui si desidera aggiungere le dimensioni. Una volta selezionata, la colonna `Choose Dimensions to Add` viene visualizzata a destra. Controlla le dimensioni da aggiungere alla metrica selezionata.

   ![Finestra di dialogo Aggiungi dimensioni con le opzioni di dimensione disponibili](../../assets/Add_Dimensions.png)

1. Se desideri segmentare o raggruppare per una qualsiasi delle dimensioni dati nei rapporti, assicurati di indicare che sono _Raggruppabili_.

1. Fare clic su **[!UICONTROL Add]**.

## Eliminare dimensioni da più metriche

Per eliminare una o più dimensioni da più metriche:

1. Vai a **[!UICONTROL Data > Metrics]**.

1. Fare clic su **[!UICONTROL Remove Dimensions From Metric(s)]**.

1. Selezionate la tabella contenente le quote.

1. Seleziona le metriche da cui vuoi rimuovere le dimensioni a sinistra e le dimensioni da rimuovere a destra.

1. Fare clic su **[!UICONTROL Remove]**.

1. Se le dimensioni sono in uso nei rapporti, viene visualizzato un avviso con l’elenco dei grafici che utilizzano le dimensioni. Fare clic su **[!UICONTROL Delete]** per eliminare le dimensioni selezionate e tutte le relative dipendenze, inclusi i report.

## Gestire le dimensioni nelle metriche

**Per aggiungere dimensioni in una metrica:**

1. Vai a **[!UICONTROL Data > Metrics]**.

1. Fare clic su **[!UICONTROL Edit]** sulla metrica per la quale si desidera una nuova dimensione.

1. Nella sezione `Dimensions`, utilizza il menu a discesa `Add a dimension` per selezionare una dimensione da aggiungere.

>[!NOTE]
>
>Qualsiasi dimensione in base alla quale si desidera filtrare o raggruppare deve essere già tracciata in [!DNL Commerce Intelligence]. Se non trovi la dimensione desiderata, potresti dover iniziare a monitorare una nuova colonna di dati nel database tramite la pagina [Data Warehouse](../data-warehouse-mgr/tour-dwm.md).


**Per eliminare una o più dimensioni da una metrica:**

1. Vai a **[!UICONTROL Manage Data > Metrics]**.

1. Fare clic su **[!UICONTROL Edit]** sulla metrica per la quale si desidera una nuova dimensione.

1. Nella sezione `Dimensions`, seleziona la casella di controllo nella colonna Elimina accanto alle dimensioni da rimuovere.

>[!NOTE]
>
>Anche dopo l’eliminazione di una dimensione, questa esiste ancora come colonna nella tabella del Data Warehouse. Puoi aggiungerla nuovamente a qualsiasi metrica e creare nuove metriche utilizzando queste dimensioni. Per rimuovere la colonna di dati a cui corrisponde una dimensione da [!DNL Commerce Intelligence], è sufficiente annullare il tracciamento della colonna di dati tramite la pagina [Data Warehouse](../data-warehouse-mgr/tour-dwm.md).

## Documentazione correlata

* [Best practice per la segmentazione e il filtraggio](../../best-practices/segment-filter.md)
