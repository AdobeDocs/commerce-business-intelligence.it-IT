---
title: Importazione dei dati di condivisione dei collegamenti
description: Scopri come importare i dati di condivisione dei collegamenti in [!DNL Commerce Intelligence].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# Importa [!DNL Linkshare] dati

Per portare [!DNL Linkshare] dati in [!DNL Adobe Commerce Intelligence], è necessario eseguire due operazioni:

1. [Esportare i dati di condivisione dei collegamenti in ](#export)
1. [Carica il foglio di calcolo in [!DNL Commerce Intelligence]](../connecting-data/using-file-uploader.md)

## Esporta dati da condivisione collegamenti {#export}

1. Nel tuo [!DNL Linkshare] account, vai a **[!UICONTROL Reports** > **Run Reports].**

1. In `Report` a discesa, seleziona **[!UICONTROL Sales & Activity Report]**.

1. Lascia tutte le altre opzioni a discesa come selezione predefinita.

1. In `Date Range` a discesa, seleziona l’opzione (`Sun - Sat`, `Mon - Sun`) corrisponde al tuo `Start of Week` impostazioni in [!DNL Commerce Intelligence].

1. Cancella `Compare Year-Over-Year Data` casella di controllo.

1. Sotto `Data Type`, seleziona `Transaction Date`.

   ![import\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. Clic **[!UICONTROL View Report]**.

1. Clic **[!UICONTROL Download]**.

   A questo punto, un `.csv` e scaricato.

Dopo il download, puoi caricarlo in [!DNL Commerce Intelligence] utilizzando [`File Upload` funzionalità](../connecting-data/using-file-uploader.md).
