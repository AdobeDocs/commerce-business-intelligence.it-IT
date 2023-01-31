---
title: Tracciamento degli obiettivi rispetto alle metriche
description: Scopri come impostare un dashboard che ti aiuterà a tenere traccia degli obiettivi aziendali rispetto ai dati effettivi, inclusi i ricavi, i nuovi utenti registrati e gli ordini nel tempo.
exl-id: 9d621f40-f9c2-4310-bd96-a46ab7159930
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Tracciamento degli obiettivi rispetto alle metriche delle prestazioni

Una grande maggioranza dei nostri clienti spesso vorrebbe tenere traccia dei loro **obiettivi aziendali** ma non si rende conto che ciò è possibile in [!DNL MBI]. In questo articolo, mostriamo come impostare un dashboard che ti aiuterà a tenere traccia dei tuoi obiettivi aziendali rispetto ai tuoi dati effettivi, inclusi i ricavi, i nuovi utenti registrati e gli ordini nel tempo. Vi mostriamo anche come confrontare le prestazioni anno dopo anno, il tutto in un dashboard come questo:

![](../../assets/Goals-_dashboard_2.png)

Prima di iniziare, vuoi acquisire familiarità con i nostri [caricatore di file](../importing-data/connecting-data/using-file-uploader.md) e assicurati di aver definito i tuoi obiettivi aziendali per un determinato periodo di tempo.

## Introduzione

Devi innanzitutto caricare un file contenente specifiche destinazioni giornaliere/mensili/trimestrali per la tua azienda.

È possibile utilizzare [caricatore di file](../importing-data/connecting-data/using-file-uploader.md) e l&#39;immagine seguente per formattare il file. I target più comuni tracciati dai nostri clienti [!DNL MBI] includono Ordini, Entrate e Nuovi conti registrati.

![](../../assets/Goals-_Excel.png)

## Metriche

Devi creare una nuova metrica per ogni target. Ad esempio, se carichi destinazioni di ricavi e ordini mensili, dovrai creare due nuove metriche:

* **Obiettivo delle entrate mensili**
* In **`Monthly goals`** tabella
* Questa metrica esegue un **Somma**
* Sulla **`Revenue target`** column
* Ordinato dal **`Month`** timestamp

* **Obiettivo degli ordini mensili**
* In **`Monthly goals`** tabella
* Questa metrica esegue un **Somma**
* Sulla **`Orders target`** column
* Ordinato dal **`Month`** timestamp

* **Destinazione nuovi account registrati mensili**
* In **`Monthly goals`** tabella
* Questa metrica esegue un **Somma**
* Sulla **`New registered accounts target`** column
* Ordinato dal **`Month`** timestamp

## Rapporti

Come sempre, è utile disporre di una combinazione di valori statici e grafici quando si analizzano i target. Di seguito sono riportati tre rapporti di esempio per aiutarti a monitorare le prestazioni dei ricavi.

* **Ricavi rimasti per raggiungere l&#39;obiettivo**
* Metrica `A`: `Revenue`
* 

   [!UICONTROL Metric]: `Revenue`

* Metrica `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* [!UICONTROL Formula]: `Revenue left to achieve target`
* 
   [!Formula UICONTROL]: `(B-A)`
* 

   [!UICONTROL Format]: `Number`

* [!UICONTROL Time period]: (a prescindere dal periodo di tempo desiderato)
* 
   [!UICONTROL Interval]: `Month`
* 

   [!UICONTROL Tipo di grafico]: `Scalar`

* **Obiettivi di profitto**
* Metrica `A`: `Revenue`
* 

   [!UICONTROL Metric]: `Revenue`

* Metrica `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* Metrica `C`: `Revenue (amount change since previous year)` (nascondere)
* 
   [!UICONTROL Metric]: `Revenue`
* [!UICONTROL Perspective]: `Amount change vs. Previous year`

* [!UICONTROL Formula]: (Questo mese l&#39;anno scorso)
* 
   [!Formula UICONTROL]: `(A-C)`
* 

   [!UICONTROL Format]: `Currency`

* Disattiva `Multiple Y-Axes`
* [!UICONTROL Time period]: (a prescindere dal periodo di tempo desiderato)*
* 
   [!UICONTROL Interval]: `Month`
* [!UICONTROL Chart Type]: `Line Chart`

Una volta completati i rapporti di cui sopra per le destinazioni di ricavi, puoi creare rapporti identici per gli obiettivi intorno agli ordini, agli account registrati o a qualsiasi altro valore incluso nel caricamento del file degli obiettivi.

Dopo aver compilato tutti i rapporti, puoi organizzarli nel dashboard come desideri. Il risultato finale potrebbe assomigliare all&#39;immagine nella parte superiore della pagina.
