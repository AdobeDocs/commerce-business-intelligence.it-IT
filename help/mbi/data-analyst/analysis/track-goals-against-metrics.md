---
title: Tracciamento degli obiettivi rispetto alle metriche
description: Scopri come impostare una dashboard che ti aiuti a tenere traccia degli obiettivi aziendali in base ai dati effettivi, inclusi ricavi, nuovi utenti registrati e ordini nel tempo.
exl-id: 9d621f40-f9c2-4310-bd96-a46ab7159930
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards, Reports
TQID: https://experienceleague.adobe.com/gT-FJxqVg3X9fuXe-4kWErttYJ6qSMD4eqNvOITNNtQ
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 402
ht-degree: 0%

---

# Tracciamento degli obiettivi rispetto alle metriche delle prestazioni

La maggior parte dei client desidera tenere traccia dei propri **obiettivi aziendali**, ma non si rende conto che ciò è possibile in [!DNL Adobe Commerce Intelligence]. In questo argomento viene illustrato come impostare una dashboard che consenta di tenere traccia degli obiettivi aziendali in base ai dati effettivi, inclusi ricavi, nuovi utenti registrati e ordini nel tempo. Scopri anche come confrontare le prestazioni anno su anno, il tutto in una dashboard come questa:

![Dashboard che mostra il tracciamento degli obiettivi rispetto alle prestazioni effettive delle metriche](../../assets/Goals-_dashboard_2.png)

Prima di iniziare, è necessario esaminare lo strumento di caricamento [file](../importing-data/connecting-data/using-file-uploader.md) e assicurarsi di aver definito gli obiettivi aziendali per un determinato periodo.

## Guida introduttiva

Devi innanzitutto caricare un file contenente i target giornalieri/mensili/trimestrali specifici per la tua azienda.

Per formattare il file è possibile utilizzare [uploader file](../importing-data/connecting-data/using-file-uploader.md) e l&#39;immagine seguente. Le destinazioni più comuni monitorate dai client in [!DNL Commerce Intelligence] includono Ordini, Ricavi e Nuovi account registrati.

![Modello di foglio di calcolo Excel per monitorare obiettivi e metriche](../../assets/Goals-_Excel.png)

## Metriche

Crea una nuova metrica per ogni destinazione. Ad esempio, se carichi gli obiettivi mensili di ricavi e ordini, devi creare due nuove metriche:

* **Destinazione ricavi mensile**
* Nella tabella **`Monthly goals`**
* Questa metrica esegue una **somma**
* Nella colonna **`Revenue target`**
* Ordinato per la marca temporale **`Month`**

* **Destinazione ordini mensili**
* Nella tabella **`Monthly goals`**
* Questa metrica esegue una **somma**
* Nella colonna **`Orders target`**
* Ordinato per la marca temporale **`Month`**

* **Destinazione mensile nuovi account registrati**
* Nella tabella **`Monthly goals`**
* Questa metrica esegue una **somma**
* Nella colonna **`New registered accounts target`**
* Ordinato per la marca temporale **`Month`**

## Rapporti

Nell’analisi dei target, è utile disporre di una combinazione di valori statici e grafici visivi. Di seguito sono riportati tre rapporti di esempio per iniziare a monitorare le prestazioni dei ricavi.

* **Ricavi rimanenti per raggiungere la destinazione**
* Metrica `A`: `Revenue`
* &#x200B;
  [!UICONTROL Metric]: `Revenue`

* Metrica `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* [!UICONTROL Formula]: `Revenue left to achieve target`
* &#x200B;
  [!UICONTROL Formula]: `(B-A)`
* &#x200B;
  [!UICONTROL Format]: `Number`

* [!UICONTROL Time period]: (qualsiasi periodo di tempo rilevante si desideri)
* &#x200B;
  [!UICONTROL Interval]: `Month`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`

* **Destinazioni ricavi**
* Metrica `A`: `Revenue`
* &#x200B;
  [!UICONTROL Metric]: `Revenue`

* Metrica `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* Metrica `C`: `Revenue (amount change since previous year)` (nascondere)
* &#x200B;
  [!UICONTROL Metric]: `Revenue`
* [!UICONTROL Perspective]: `Amount change vs. Previous year`

* [!UICONTROL Formula]: (questo mese l&#39;anno scorso)
* &#x200B;
  [!UICONTROL Formula]: `(A-C)`
* &#x200B;
  [!UICONTROL Format]: `Currency`

* Disattiva `Multiple Y-Axes`
* [!UICONTROL Time period]: (qualunque sia il periodo di tempo rilevante desiderato)*
* &#x200B;
  [!UICONTROL Interval]: `Month`
* [!UICONTROL Chart Type]: `Line Chart`

Una volta completati i rapporti di cui sopra per gli obiettivi di ricavo, puoi creare rapporti identici per gli obiettivi in base agli ordini, ai conti registrati o a qualsiasi altro valore incluso nel caricamento del file degli obiettivi.

Dopo aver compilato tutti i rapporti, puoi organizzarli nel dashboard come desideri. Il risultato potrebbe essere simile all’immagine nella parte superiore della pagina.
