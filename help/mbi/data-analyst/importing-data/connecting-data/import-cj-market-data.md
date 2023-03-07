---
title: Importazione dei dati di marketing di un'affiliata CJ (Commission Junction)
description: Scopri come importare dati di affiliazione CJ (Commission Junction) in [!DNL MBI].L MBI].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# Importa `CJ Affiliate` dati

Per importare `CJ Affiliate` (Commission Junction) data in [!DNL MBI], è sufficiente seguire i passaggi riportati di seguito e allegare il file risultante a un ticket di supporto. Adobe configurerà la tabella di dati del tuo account e ti consentirà di continuare a caricare i dati in modo indipendente.

## Esporta `CJ Affiliate` Dati

1. Nel tuo `CJ Affiliate` account, vai a `Reports` scheda.

1. In `Performance` , seleziona `Report Options`.

1. Imposta `Performance By` uguale a `Program`, `Trend` uguale a `Daily`, e `Date Range` è uguale all’intervallo di date sottoposto a controllo.

   ![export-cj-affiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Seleziona `Run Report`.

1. In `File Format` a discesa, seleziona `CSV`.  Clic **[!UICONTROL Download]**.

   ![esporta dati affiliate cj](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. Dopo aver scaricato il file, puoi [carica il file](../connecting-data/using-file-uploader.md) al tuo [!DNL MBI] Data Warehouse.

   Questo crea una tabella nel [!DNL MBI] Data Warehouse che puoi continuare a caricare dati aggiornati in periodicamente. Durante il caricamento del file, assicurati di rispettare i requisiti di formattazione elencati in [Utilizzo di Caricamento file](../connecting-data/using-file-uploader.md).
