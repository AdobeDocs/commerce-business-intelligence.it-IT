---
title: Tracciamento degli obiettivi rispetto alle metriche
description: Scopri come impostare una dashboard che ti aiuti a tenere traccia degli obiettivi aziendali in base ai dati effettivi, inclusi ricavi, nuovi utenti registrati e ordini nel tempo.
exl-id: 9d621f40-f9c2-4310-bd96-a46ab7159930
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Tracciamento degli obiettivi rispetto alle metriche delle prestazioni

La maggior parte dei clienti desidera tenere traccia delle proprie **obiettivi aziendali**, ma non capire che questo è possibile in [!DNL Adobe Commerce Intelligence]. In questo argomento viene illustrato come impostare una dashboard che consenta di tenere traccia degli obiettivi aziendali in base ai dati effettivi, inclusi ricavi, nuovi utenti registrati e ordini nel tempo. Scopri anche come confrontare le prestazioni anno su anno, il tutto in una dashboard come questa:

![](../../assets/Goals-_dashboard_2.png)

Prima di iniziare, è necessario rivedere [caricatore di file](../importing-data/connecting-data/using-file-uploader.md) e assicurati di aver definito gli obiettivi aziendali per un dato periodo.

## Guida introduttiva

Devi innanzitutto caricare un file contenente i target giornalieri/mensili/trimestrali specifici per la tua azienda.

È possibile utilizzare [caricatore di file](../importing-data/connecting-data/using-file-uploader.md) e l&#39;immagine seguente per formattare il file. I target più comuni tracciati dai client [!DNL Commerce Intelligence] includono Ordini, Ricavi e Nuovi conti registrati.

![](../../assets/Goals-_Excel.png)

## Metriche

Crea una nuova metrica per ogni destinazione. Ad esempio, se carichi gli obiettivi mensili di ricavi e ordini, devi creare due nuove metriche:

* **Obiettivo di ricavo mensile**
* In **`Monthly goals`** tabella
* Questa metrica esegue una **Somma**
* Il giorno **`Revenue target`** colonna
* Ordinato da **`Month`** timestamp

* **Obiettivo ordini mensili**
* In **`Monthly goals`** tabella
* Questa metrica esegue una **Somma**
* Il giorno **`Orders target`** colonna
* Ordinato da **`Month`** timestamp

* **Destinazione nuovi account registrati mensili**
* In **`Monthly goals`** tabella
* Questa metrica esegue una **Somma**
* Il giorno **`New registered accounts target`** colonna
* Ordinato da **`Month`** timestamp

## Rapporti

Nell’analisi dei target, è utile disporre di una combinazione di valori statici e grafici visivi. Di seguito sono riportati tre rapporti di esempio per iniziare a monitorare le prestazioni dei ricavi.

* **Ricavi rimasti per raggiungere l&#39;obiettivo**
* Metrica `A`: `Revenue`
* 
  [!UICONTROL Metric]: `Revenue`

* Metrica `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* [!UICONTROL Formula]: `Revenue left to achieve target`
* 
  [!UICONTROL Formula]: `(B-A)`
* 
  [!UICONTROL Format]: `Number`

* [!UICONTROL Time period]: (qualunque sia il periodo di tempo rilevante desiderato)
* 
  [!UICONTROL Interval]: `Month`
* 
  [!UICONTROL Chart Type]: `Scalar`

* **Obiettivi di ricavo**
* Metrica `A`: `Revenue`
* 
  [!UICONTROL Metric]: `Revenue`

* Metrica `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* Metrica `C`: `Revenue (amount change since previous year)` (nascondi)
* 
  [!UICONTROL Metric]: `Revenue`
* [!UICONTROL Perspective]: `Amount change vs. Previous year`

* [!UICONTROL Formula]: (questo mese, ultimo anno)
* 
  [!UICONTROL Formula]: `(A-C)`
* 
  [!UICONTROL Format]: `Currency`

* Disattiva `Multiple Y-Axes`
* [!UICONTROL Time period]: (qualunque sia il periodo di tempo rilevante desiderato)*
* 
  [!UICONTROL Interval]: `Month`
* [!UICONTROL Chart Type]: `Line Chart`

Una volta completati i rapporti di cui sopra per gli obiettivi di ricavo, puoi creare rapporti identici per gli obiettivi in base agli ordini, ai conti registrati o a qualsiasi altro valore incluso nel caricamento del file degli obiettivi.

Dopo aver compilato tutti i rapporti, puoi organizzarli nel dashboard come desideri. Il risultato potrebbe essere simile all’immagine nella parte superiore della pagina.
