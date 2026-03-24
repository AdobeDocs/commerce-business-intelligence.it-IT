---
title: Importazione dei dati di condivisione dei collegamenti
description: Scopri come importare i dati di condivisione collegamenti in  [!DNL Commerce Intelligence].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/TsQYXEwH-8m1rpKg6It8wa-B2eQH0oqDkLcgx-tRBWU
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 94
ht-degree: 0%

---

# Importa dati [!DNL Linkshare]

Per inserire i dati di [!DNL Linkshare] in [!DNL Adobe Commerce Intelligence], è necessario eseguire due operazioni:

1. [Esportare i dati di condivisione dei collegamenti in &#x200B;](#export)
1. [Carica il foglio di calcolo in [!DNL Commerce Intelligence]](../connecting-data/using-file-uploader.md)

## Esporta dati da condivisione collegamenti {#export}

1. Nel tuo account [!DNL Linkshare], vai a **[!UICONTROL Reports** > **Run Reports].**

1. Nel menu a discesa `Report`, seleziona **[!UICONTROL Sales & Activity Report]**.

1. Lascia tutte le altre opzioni a discesa come selezione predefinita.

1. Nel menu a discesa `Date Range`, selezionare l&#39;opzione (`Sun - Sat`, `Mon - Sun`) corrispondente alle impostazioni di `Start of Week` in [!DNL Commerce Intelligence].

1. Deselezionare la casella di controllo `Compare Year-Over-Year Data`.

1. In `Data Type`, selezionare `Transaction Date`.

   ![importazione\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. Fare clic su **[!UICONTROL View Report]**.

1. Fare clic su **[!UICONTROL Download]**.

   A questo punto, è stato scaricato un file `.csv`.

Dopo aver scaricato il file, è possibile caricarlo in [!DNL Commerce Intelligence] utilizzando la funzionalità [`File Upload`](../connecting-data/using-file-uploader.md).
