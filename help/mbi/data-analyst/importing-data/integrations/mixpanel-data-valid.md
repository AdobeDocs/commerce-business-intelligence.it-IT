---
title: Convalida dei dati in Mixpanel
description: Scopri come verificare di aver sincronizzato tutti gli stessi dati disponibili direttamente in Mixpanel.
exl-id: d18ce954-26fe-4440-ad8b-4f266c007b2f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---

# Convalida dati in [!DNL Mixpanel]

Quando [!DNL Adobe Commerce Intelligence] si connette per la prima volta ai dati di [!DNL Mixpanel], l&#39;Account Manager o l&#39;analista potrebbe richiedere di fornire esportazioni di dati da [!DNL Mixpanel] a scopo di convalida. Ciò ti consente di confermare che hai sincronizzato tutti gli stessi dati disponibili direttamente in [!DNL Mixpanel].

## Processo di esportazione dati: `Events`

1. Visita la sezione `Segmentation` e visualizza `Your Top Events`.

   ![Dashboard mixpanel con i tuoi eventi principali](../../../assets/your-top-events.png)

1. Seleziona `Past 96 Hours` per l&#39;intervallo di tempo

   ![Selettore intervallo di tempo Mixpanel che mostra l&#39;opzione delle ultime 96 ore](../../../assets/past-96-hours.png)

1. Scorri fino alla parte inferiore destra del report ed esporta un file `.csv`:

   ![Opzione esporta in formato CSV nel menu](../../../assets/export-csv-mixpanel.png)

1. Invia il file `.csv` all&#39;account manager o all&#39;analista con cui stai lavorando in questo processo di convalida.
