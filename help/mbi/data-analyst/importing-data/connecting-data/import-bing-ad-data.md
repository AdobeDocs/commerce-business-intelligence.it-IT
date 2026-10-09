---
title: Importare dati sulla spesa pubblicitaria di Bing
description: Scopri come importare in [!DNL Commerce Intelligence] i dati sulla spesa pubblicitaria di Bing per l'analisi.
exl-id: c8dec4b4-74ce-41b2-a77d-403fe44e2816
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: 'https://experienceleague.adobe.com/66UAmNWDCkiflHxsq9X1MlkwEgzC5Cl1HfRirNd8AHM'
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
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%
---
# Importa dati [!DNL Bing]

Per importare i dati di spesa pubblicitaria [!DNL Bing] in [!DNL Adobe Commerce Intelligence] per l&#39;analisi, è sufficiente esportare i dati da [!DNL Bing Ads Editor] in formato `.csv` e caricarli in [!DNL Commerce Intelligence] come descritto nei passaggi seguenti.

## [!DNL Bing Ads Editor]

Per esportare i dati di [!DNL Bing Ads], è necessario che [!DNL Bing Ads Editor] sia installato. È possibile trovare un download gratuito di [[!DNL Bing Ads Editor]](https://about.ads.microsoft.com/en-us/solutions/tools/editor).

## Esportazione dati [!DNL Bing Ads]

1. Nel riquadro `Browser` di [!DNL Bing Ads Editor] fare clic con il pulsante destro del mouse sulla campagna o sul gruppo di annunci che si desidera esportare e scegliere **[!UICONTROL Export]**.
1. Nella finestra di dialogo `Export` fare clic su **[!UICONTROL Export]**.
1. Nella finestra di dialogo `Save As` fare clic sulla cartella in cui si desidera salvare il file di esportazione.
1. Nella casella `File name` scegliere un nome per l&#39;esportazione del file.
1. Fare clic su **[!UICONTROL Save]**.
1. Dopo aver scaricato il file, [contatta l&#39;assistenza](https://experienceleague.adobe.com/it/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies) per eseguire un primo caricamento per tuo conto e impostare le dimensioni di back-end necessarie.
