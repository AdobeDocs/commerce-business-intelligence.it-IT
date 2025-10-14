---
title: Importazione dei dati di condivisione dei collegamenti
description: Scopri come importare i dati di condivisione collegamenti in  [!DNL Commerce Intelligence].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '94'
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
