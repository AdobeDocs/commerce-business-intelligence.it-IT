---
title: Importazione di dati di Linkshare
description: Scopri come importare i dati di Linkshare in [!DNL MBI].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Importa `Linkshare` dati

Per portare `Linkshare` dati [!DNL MBI], è necessario eseguire due operazioni:

1. [Esporta i dati di Condivisione collegamenti in ](#export)
1. [Carica il foglio di calcolo in [!DNL MBI]](../connecting-data/using-file-uploader.md)

## Esportare dati da Linkshare {#export}

1. Nel tuo `Linkshare` account, vai a **[!UICONTROL Reports** > **Run Reports].**

1. In `Report` a discesa, seleziona **[!UICONTROL Sales & Activity Report]**.

1. Lascia come selezione predefinita tutte le altre opzioni del menu a discesa.

1. In `Date Range` a discesa, seleziona l’opzione (`Sun - Sat`, `Mon - Sun`) corrisponde al `Start of Week` impostazioni in [!DNL MBI].

1. Elimina `Compare Year-Over-Year Data` casella di controllo.

1. Sotto `Data Type`, seleziona `Transaction Date`.

   ![importazione\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. Fai clic su **[!UICONTROL View Report]**.

1. Fai clic su **[!UICONTROL Download]**.

   A questo punto, un `.csv` Il file verrà creato e scaricato.

Dopo aver scaricato il file, puoi caricarlo in [!DNL MBI] utilizzando [`File Upload` caratteristica](../connecting-data/using-file-uploader.md).
