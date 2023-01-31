---
title: Gestione delle dimensioni dati
description: Scopri come vengono generati i dati e cosa causa esattamente l’inserimento di una nuova riga in uno dei Servizi di commercio di base in che modo vengono registrate le azioni quali l’acquisto o la creazione di un account nel database Commerce.
exl-id: 143a4b1e-2e6f-438a-90e6-bdda13b39cb9
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# Gestione delle dimensioni dati

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../administrator/user-management/user-management.md).

Una dimensione è un campo nella stessa tabella di una metrica che può essere utilizzato per filtrare o segmentare i grafici in base a tale metrica. Ad esempio, una metrica Ricavo può contenere città, stato, paese, stato dell’ordine, codice coupon e altri tipi di dimensioni.

## Aggiungere dimensioni a più metriche

Per aggiungere una o più dimensioni a più metriche contemporaneamente:

1. Nella barra di navigazione principale, vai a **[!UICONTROL Manage Data > Metrics]**.

1. Nella parte superiore della pagina, fai clic su **[!UICONTROL Add Dimensions To Metric(s)]**.

1. Scegli la tabella che contiene le dimensioni.

1. In `Choose Metric(s) to Add Dimensions` seleziona le metriche a cui desideri aggiungere dimensioni. Una volta selezionato, il `Choose Dimensions to Add` a destra. Seleziona le dimensioni da aggiungere alla metrica selezionata.

   ![](../../assets/Add_Dimensions.png)

1. Se desideri segmentare o raggruppare in base a una qualsiasi delle dimensioni dati nei rapporti, assicurati di indicarle come _Raggruppabile_.

1. Fai clic su **[!UICONTROL Add]**.

## Eliminare dimensioni da più metriche

Per eliminare una o più dimensioni da più metriche:

1. Nella barra di navigazione principale, vai a **[!UICONTROL Data > Metrics]**.

1. Nella parte superiore della pagina, fai clic su **[!UICONTROL Remove Dimensions From Metric(s)]**.

1. Scegli la tabella che contiene le dimensioni.

1. Seleziona le metriche da cui vuoi rimuovere le dimensioni da a sinistra e quelle da rimuovere a destra.

1. Fai clic su **[!UICONTROL Remove]**.

1. Se le dimensioni sono in uso nei rapporti, viene visualizzato un avviso e un elenco di grafici che utilizzano le dimensioni. Fai clic su **[!UICONTROL Delete]** per eliminare le dimensioni controllate e tutti i relativi dipendenti, inclusi i rapporti.

## Gestione delle dimensioni nelle metriche

**Per aggiungere dimensioni in una metrica:**

1. Nella barra di navigazione principale, vai a **[!UICONTROL Data > Metrics]**.

1. Fai clic su **[!UICONTROL Edit]** sulla metrica che desideri una nuova dimensione.

1. Sotto la `Dimensions` utilizza `Add a dimension` menu a discesa per selezionare una dimensione da aggiungere.

>[!NOTE]
>
>Qualsiasi dimensione per la quale desideri filtrare o raggruppare deve essere già monitorata [!DNL MBI]. Se non trovi la dimensione desiderata, potrebbe essere necessario avviare il tracciamento di una nuova colonna di dati nel database tramite [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) pagina.


**Per eliminare le dimensioni da una metrica:**

1. Nella barra di navigazione principale, vai a **[!UICONTROL Manage Data > Metrics]**.

1. Fai clic su **[!UICONTROL Edit]** sulla metrica che desideri una nuova dimensione.

1. Sotto la `Dimensions` seleziona la casella di controllo nella colonna Elimina accanto alle dimensioni da rimuovere.

>[!NOTE]
>
>Anche dopo l’eliminazione di una dimensione, esiste ancora come colonna sulla tabella nel data warehouse. Puoi aggiungerla nuovamente a qualsiasi metrica e generare nuove metriche utilizzando queste dimensioni. Per rimuovere la colonna di dati a cui corrisponde una dimensione [!DNL MBI], è sufficiente annullare il tracciamento della colonna di dati tramite [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) pagina.

## Documentazione correlata

* [Best practice per segmentazione e filtro](../../best-practices/segment-filter.md)
