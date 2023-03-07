---
title: Creare colonne calcolate
description: Scopri come consolidare i dati da diverse origini.
exl-id: 668cbc77-6a96-4687-9f40-3635b1be5c66
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%

---

# Crea colonne calcolate

Nell’analisi dei dati, è utile consolidare i dati provenienti da origini diverse. Raggruppare i ricavi per origine di acquisizione, collegando i dati dalla tabella e dalle Google Analytics degli ordini? Oppure, raggruppare i ricavi per genere di cliente o unire un attributo di cliente ai dati delle transazioni per la segmentazione?

Questa guida ti insegna come fare proprio questo. Prima di iniziare, Adobe consiglia di consultare [Guida ai tipi di colonna calcolati](../../data-analyst/data-warehouse-mgr/calc-column-types.md). Il _Guida ai tipi di colonna calcolati_ illustra i tipi di colonne che è possibile creare in Gestione Date Warehouse, insieme alle relative definizioni ed esempi.

1. Per iniziare, fai clic su **[!DNL Manage Data > Data Warehouse]** nella barra laterale.

1. Fare clic sulla tabella in cui si desidera creare una colonna. Ad esempio, se desideri creare un’ `Customer Gender` per la segmentazione dei ricavi, è necessario selezionare la `sales_flat_order` tabella.

1. Viene visualizzato lo schema di tabella. Clic **[!UICONTROL Create New Column]**.

1. Assegna un nome alla colonna, ad esempio: `Customer Gender`.

1. Selezionare la definizione della colonna. Qui è dove [Guida ai tipi di colonne calcolate](../data-warehouse-mgr/calc-column-types.md) è utile!

1. Per alcuni tipi di colonne, sono necessarie ulteriori informazioni per creare correttamente la colonna:
   * Per `One to Many` (uniti) e `Many to One` (aggregato), è necessario selezionare le tabelle e le colonne.
   * Per un `Same Table calculation`, è necessario selezionare il campo data desiderato dal menu a discesa.

Se stai creando un `One to Many` (uniti) o `Many to One` (aggregato), è necessario selezionare un percorso per collegare le due tabelle. In questo passaggio è possibile utilizzare un percorso esistente o crearne uno esistente.

>[!NOTE]
>
>Ricordati di definire correttamente la tabella come tante o una.

* Se lo desideri, puoi applicare [filtri](../../data-user/reports/ess-manage-data-filters.md) alla nuova colonna.
* Al termine, fai clic su **[!UICONTROL Save]**.

Tutto qui! La nuova colonna viene visualizzata nella tabella corrente con `Pending` stato. Al termine del prossimo aggiornamento, la colonna sarà disponibile per l’utilizzo in metriche e rapporti.

## Mappa di riferimento utile {#map}

Se non riesci a ricordare quali sono tutti gli input durante la creazione di una colonna calcolata, prova a tenere a portata di mano questa mappa di riferimento durante la creazione di:

![](../../assets/Calculated_Columns_Example.png)

## Documentazione correlata

* [Tipi di colonne calcolate](../data-warehouse-mgr/calc-column-types.md)
* [Tipi di colonne calcolate avanzate](../data-warehouse-mgr/adv-calc-columns.md)
* [Generazione [!DNL Google ECommerce] dimensioni con dati di ordini e clienti](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
