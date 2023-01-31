---
title: Creare colonne calcolate
description: Scopri come consolidare i dati provenienti da origini diverse.
exl-id: 668cbc77-6a96-4687-9f40-3635b1be5c66
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# Crea colonne calcolate

Quando si analizzano i dati, è utile consolidare i dati provenienti da fonti diverse. Vuoi raggruppare i ricavi per origine di acquisizione, collegando i dati dalla tabella e dalle Google Analytics degli ordini? Oppure cosa succede quando si raggruppano i ricavi per genere cliente o si unisce un attributo cliente ai dati di transazione per la segmentazione?

Questa guida vi insegnerà come farlo. Prima di iniziare, consulta la sezione [Guida ai tipi di colonna calcolati](../../data-analyst/data-warehouse-mgr/calc-column-types.md). La _Guida ai tipi di colonna calcolati_ delinea i tipi di colonne che è possibile creare in Data Warehouse Manager, insieme alle relative definizioni ed esempi.

1. Per iniziare, fai clic su **[!DNL Manage Data > Data Warehouse]** nella barra laterale.

1. Fare clic sulla tabella in cui si desidera creare una colonna. Ad esempio, se desideri creare un `Customer Gender` per la segmentazione dei ricavi, selezioniamo la `sales_flat_order` tabella.

1. Verrà visualizzato lo schema della tabella. Fai clic su **[!UICONTROL Create New Column]**.

1. Assegna un nome alla colonna, ad esempio `Customer Gender`.

1. Seleziona la definizione della colonna. Qui è dove [Guida ai tipi di colonna calcolati](../data-warehouse-mgr/calc-column-types.md) sarà utile!

1. Per alcuni tipi di colonne sono necessarie un po&#39; più di informazioni per creare correttamente la colonna:
   * Per `One to Many` (uniti) e `Many to One` (aggregato) colonne, è necessario selezionare le tabelle e le colonne.
   * Per `Same Table calculation`, devi selezionare il campo data desiderato dal menu a discesa .

Se stai creando un `One to Many` (unito) o `Many to One` (aggregato), per collegare le due tabelle è necessario selezionare un percorso. In questo passaggio, puoi utilizzare un percorso esistente o crearne uno nuovo.

>[!NOTE]
>
>Ricordarsi di definire correttamente la tabella come molti o uno!

* Se lo desideri, puoi applicare [filtri](../../data-user/reports/ess-manage-data-filters.md) nella nuova colonna.
* Al termine, fai clic su **[!UICONTROL Save]**.

Tutto qui! La nuova colonna verrà visualizzata nella tabella corrente con un `Pending` stato. Al termine del prossimo aggiornamento, la colonna sarà disponibile per l’utilizzo in metriche e rapporti.

## Mappa di riferimento di Handy {#map}

Se hai qualche problema a ricordare cosa sono tutti gli input durante la creazione di una colonna calcolata, prova a mantenere questa mappa di riferimento utile durante la creazione:

![](../../assets/Calculated_Columns_Example.png)

## Documentazione correlata

* [Tipi di colonne calcolate](../data-warehouse-mgr/calc-column-types.md)
* [Tipi di colonne calcolate avanzate](../data-warehouse-mgr/adv-calc-columns.md)
* [Costruzione [!DNL Google ECommerce] dimensioni con i dati relativi all’ordine e al cliente](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
