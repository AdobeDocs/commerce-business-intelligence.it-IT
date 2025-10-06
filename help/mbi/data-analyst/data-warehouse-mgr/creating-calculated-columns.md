---
title: Creare colonne calcolate
description: Scopri come consolidare i dati da diverse origini.
exl-id: 668cbc77-6a96-4687-9f40-3635b1be5c66
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# Crea colonne calcolate

Nell’analisi dei dati, è utile consolidare i dati provenienti da origini diverse. Raggruppare i ricavi per origine di acquisizione, collegando i dati dalla tabella `orders` e i dati [!DNL Google Analytics]? Puoi raggruppare i ricavi per genere del cliente o aggiungere un attributo del cliente ai dati della transazione per la segmentazione. Questo argomento illustra come eseguire questa operazione.

Prima di iniziare, Adobe consiglia di consultare la [Guida ai tipi di colonna calcolati](../../data-analyst/data-warehouse-mgr/calc-column-types.md) per informazioni sui tipi di colonne che è possibile creare in Data Warehouse Manager, insieme alle relative definizioni ed esempi.

1. Per iniziare, fare clic su **[!DNL Manage Data > Data Warehouse]**.

1. Fare clic sulla tabella in cui si desidera creare una colonna. Ad esempio, se desideri creare una colonna `Customer Gender` per la segmentazione dei ricavi, seleziona la tabella `sales_flat_order`.

1. Viene visualizzato lo schema di tabella. Fare clic su **[!UICONTROL Create New Column]**.

1. Assegna un nome alla colonna. Ad esempio, `Customer Gender`.

1. Selezionare la definizione della colonna. Qui la [guida dei tipi di colonna calcolati](../data-warehouse-mgr/calc-column-types.md) si rivela utile.

1. Per alcuni tipi di colonne, sono necessarie ulteriori informazioni per creare correttamente la colonna:

   * Per `One to Many` colonne (unite) e `Many to One` colonne (aggregate), è necessario selezionare le tabelle e le colonne.

   * Per `Same Table calculation`, è necessario selezionare il campo data desiderato dal menu a discesa.

Se si sta creando una colonna `One to Many` (unita in join) o `Many to One` (aggregata), è necessario selezionare un percorso per connettere le due tabelle. In questo passaggio è possibile utilizzare un percorso esistente o crearne uno esistente.

>[!NOTE]
>
>Ricordati di definire correttamente la tabella come tante o una.

* Se lo desideri, puoi applicare [filtri](../../data-user/reports/ess-manage-data-filters.md) alla nuova colonna.

* Al termine, fare clic su **[!UICONTROL Save]**.

La nuova colonna viene visualizzata nella tabella corrente con lo stato `Pending`. Al termine del prossimo aggiornamento, la colonna sarà disponibile per l’utilizzo in metriche e rapporti.

## Mappa di riferimento utile {#map}

Se non riesci a ricordare quali sono tutti gli input durante la creazione di una colonna calcolata, prova a tenere a portata di mano questa mappa di riferimento durante la creazione di:

![Esempio di configurazione delle colonne calcolate in Data Warehouse Manager](../../assets/Calculated_Columns_Example.png)

## Documentazione correlata

* [Tipi di colonne calcolate](../data-warehouse-mgr/calc-column-types.md)
* [Tipi di colonne calcolate avanzate](../data-warehouse-mgr/adv-calc-columns.md)
* [Creazione di  [!DNL Google ECommerce]  dimensioni con i dati dell&#39;ordine e del cliente](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
