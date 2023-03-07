---
title: Gestione delle dimensioni dati
description: Scopri cos’è una dimensione che può essere utilizzata per filtrare o segmentare i grafici in base a una metrica.
exl-id: 143a4b1e-2e6f-438a-90e6-bdda13b39cb9
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# Gestione delle dimensioni dati

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../administrator/user-management/user-management.md).

Una dimensione è un campo nella stessa tabella di una metrica che può essere utilizzata per filtrare o segmentare i grafici basati su tale metrica. Ad esempio, una metrica dei ricavi può contenere città, stato, paese, stato dell’ordine, codice coupon e altri tipi di dimensioni.

## Aggiungere dimensioni a più metriche

Per aggiungere una o più dimensioni a più metriche contemporaneamente:

1. Sulla barra di navigazione principale, vai a **[!UICONTROL Manage Data > Metrics]**.

1. Nella parte superiore della pagina, fai clic su **[!UICONTROL Add Dimensions To Metric(s)]**.

1. Selezionate la tabella contenente le quote.

1. In `Choose Metric(s) to Add Dimensions` , seleziona le metriche a cui desideri aggiungere dimensioni. Una volta selezionata, la `Choose Dimensions to Add` a destra. Controlla le dimensioni da aggiungere alla metrica selezionata.

   ![](../../assets/Add_Dimensions.png)

1. Se desideri segmentare o raggruppare per una qualsiasi delle dimensioni dati nei rapporti, assicurati di indicarli _Raggruppabile_.

1. Clic **[!UICONTROL Add]**.

## Eliminare dimensioni da più metriche

Per eliminare una o più dimensioni da più metriche:

1. Sulla barra di navigazione principale, vai a **[!UICONTROL Data > Metrics]**.

1. Nella parte superiore della pagina, fai clic su **[!UICONTROL Remove Dimensions From Metric(s)]**.

1. Selezionate la tabella contenente le quote.

1. Seleziona le metriche da cui vuoi rimuovere le dimensioni a sinistra e le dimensioni da rimuovere a destra.

1. Clic **[!UICONTROL Remove]**.

1. Se le dimensioni sono in uso nei rapporti, viene visualizzato un avviso e un elenco di grafici che utilizzano le dimensioni. Clic **[!UICONTROL Delete]** per eliminare le dimensioni selezionate e tutte le relative dipendenze, inclusi i rapporti.

## Gestire le dimensioni nelle metriche

**Per aggiungere dimensioni a una metrica:**

1. Sulla barra di navigazione principale, vai a **[!UICONTROL Data > Metrics]**.

1. Clic **[!UICONTROL Edit]** sulla metrica desideri una nuova dimensione.

1. Sotto `Dimensions` , utilizza la sezione `Add a dimension` per selezionare una dimensione da aggiungere.

>[!NOTE]
>
>Qualsiasi dimensione in base alla quale si desidera filtrare o raggruppare deve essere già tracciata [!DNL MBI]. Se non trovi la dimensione desiderata, potrebbe essere necessario iniziare a tracciare una nuova colonna di dati nel database tramite [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) pagina.


**Per eliminare una o più dimensioni da una metrica:**

1. Sulla barra di navigazione principale, vai a **[!UICONTROL Manage Data > Metrics]**.

1. Clic **[!UICONTROL Edit]** sulla metrica desideri una nuova dimensione.

1. Sotto `Dimensions` , seleziona la casella di controllo nella colonna elimina accanto alle dimensioni da rimuovere.

>[!NOTE]
>
>Anche dopo aver eliminato una dimensione, essa esiste ancora come colonna nella tabella della Data Warehouse. Puoi aggiungerla nuovamente a qualsiasi metrica e creare nuove metriche utilizzando queste dimensioni. Per rimuovere la colonna di dati a cui corrisponde una dimensione da [!DNL MBI], è sufficiente annullare il tracciamento della colonna di dati tramite [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) pagina.

## Documentazione correlata

* [Best practice per la segmentazione e il filtraggio](../../best-practices/segment-filter.md)
