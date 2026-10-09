---
title: Convalida dei dati in Mixpanel
description: Scopri come verificare di aver sincronizzato tutti gli stessi dati disponibili direttamente in Mixpanel.
exl-id: d18ce954-26fe-4440-ad8b-4f266c007b2f
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: 'https://experienceleague.adobe.com/D6qvHVgPX0WEbKZSYel4siWMLTu9BloFBQMTxXxnbY0'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: 4d217dbe-2c9a-5839-94d7-471fd31623b7
    internal-label: Data Integration
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '135'
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

