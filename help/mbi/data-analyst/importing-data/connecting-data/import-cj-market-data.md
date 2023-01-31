---
title: Importazione di dati di marketing di affiliazione CJ (giunzione della Commissione)
description: Impara a importare i dati di CJ Affiliate (Commission Junction) in [!DNL MBI]L MBI].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---

# Importa `CJ Affiliate` dati

Importazione `CJ Affiliate` dati (giunzione della Commissione) [!DNL MBI], segui semplicemente i passaggi seguenti e allega il file risultante a un ticket di supporto. Configureremo la tabella dati del tuo account e ti consentiremo di continuare a caricare i dati in modo indipendente.

## Esporta `CJ Affiliate` Dati

1. Nel tuo `CJ Affiliate` l&#39;account `Reports` scheda .

1. In `Performance` scheda , seleziona `Report Options`.

1. Imposta `Performance By` uguale a `Program`, `Trend` uguale a `Daily`e `Date Range` è uguale all’intervallo di date sottoposto a controllo.

   ![export-cj-affiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Seleziona `Run Report`.

1. In `File Format` a discesa, seleziona `CSV`.  Fai clic su **[!UICONTROL Download]**.

   ![esportare dati di affiliazione cj](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. Dopo aver scaricato il file, puoi [caricare il file](../connecting-data/using-file-uploader.md) al tuo [!DNL MBI] data warehouse.

   In questo modo viene creata una nuova tabella nel [!DNL MBI] data warehouse in cui puoi continuare a caricare nuovi dati periodicamente. Durante il caricamento del file, assicurati di rispettare i requisiti di formattazione elencati in [Utilizzo di File Uploader](../connecting-data/using-file-uploader.md).
