---
title: Gestione delle dimensioni dati
description: Scopri cos’è una dimensione che può essere utilizzata per filtrare o segmentare i grafici in base a una metrica.
exl-id: 143a4b1e-2e6f-438a-90e6-bdda13b39cb9
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '412'
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

   ![](../../assets/Add_Dimensions.png)

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
>Anche dopo aver eliminato una dimensione, essa esiste ancora come colonna nella tabella della Data Warehouse. Puoi aggiungerla nuovamente a qualsiasi metrica e creare nuove metriche utilizzando queste dimensioni. Per rimuovere la colonna di dati a cui corrisponde una dimensione da [!DNL Commerce Intelligence], è sufficiente annullare il tracciamento della colonna di dati tramite la pagina [Data Warehouse](../data-warehouse-mgr/tour-dwm.md).

## Documentazione correlata

* [Best practice per la segmentazione e il filtraggio](../../best-practices/segment-filter.md)
