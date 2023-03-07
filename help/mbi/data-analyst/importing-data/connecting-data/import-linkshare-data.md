---
title: Importazione dei dati di condivisione dei collegamenti
description: Scopri come importare i dati di condivisione dei collegamenti in [!DNL MBI].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# Importa `Linkshare` dati

Per portare `Linkshare` dati in [!DNL MBI], è necessario eseguire due operazioni:

1. [Esportare i dati di condivisione dei collegamenti in ](#export)
1. [Carica il foglio di calcolo in [!DNL MBI]](../connecting-data/using-file-uploader.md)

## Esporta dati da condivisione collegamenti {#export}

1. Nel tuo `Linkshare` account, vai a **[!UICONTROL Reports** > **Run Reports].**

1. In `Report` a discesa, seleziona **[!UICONTROL Sales & Activity Report]**.

1. Lascia tutte le altre opzioni a discesa come selezione predefinita.

1. In `Date Range` a discesa, seleziona l’opzione (`Sun - Sat`, `Mon - Sun`) corrisponde al tuo `Start of Week` impostazioni in [!DNL MBI].

1. Cancella `Compare Year-Over-Year Data` casella di controllo.

1. Sotto `Data Type`, seleziona `Transaction Date`.

   ![import\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. Clic **[!UICONTROL View Report]**.

1. Clic **[!UICONTROL Download]**.

   A questo punto, un `.csv` e scaricato.

Dopo il download, puoi caricarlo in [!DNL MBI] utilizzando [`File Upload` funzionalità](../connecting-data/using-file-uploader.md).
