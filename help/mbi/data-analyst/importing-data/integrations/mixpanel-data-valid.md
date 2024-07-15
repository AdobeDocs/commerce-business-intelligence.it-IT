---
title: Convalida dei dati in Mixpanel
description: Scopri come verificare di aver sincronizzato tutti gli stessi dati disponibili direttamente in Mixpanel.
exl-id: d18ce954-26fe-4440-ad8b-4f266c007b2f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---

# Convalida dati in [!DNL Mixpanel]

Quando [!DNL Adobe Commerce Intelligence] si connette per la prima volta ai dati di [!DNL Mixpanel], l&#39;Account Manager o l&#39;analista potrebbe richiedere di fornire esportazioni di dati da [!DNL Mixpanel] a scopo di convalida. Ciò ti consente di confermare che hai sincronizzato tutti gli stessi dati disponibili direttamente in [!DNL Mixpanel].

## Processo di esportazione dati: `Events`

1. Visita la sezione `Segmentation` e visualizza `Your Top Events`.

   ![](../../../assets/your-top-events.png)

1. Seleziona `Past 96 Hours` per l&#39;intervallo di tempo

   ![](../../../assets/past-96-hours.png)

1. Scorri fino alla parte inferiore destra del report ed esporta un file `.csv`:

   ![](../../../assets/export-csv-mixpanel.png)

1. Invia il file `.csv` all&#39;account manager o all&#39;analista con cui stai lavorando in questo processo di convalida.
