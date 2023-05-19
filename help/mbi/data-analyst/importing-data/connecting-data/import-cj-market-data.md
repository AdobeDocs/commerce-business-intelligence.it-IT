---
title: Importazione dei dati di marketing di un'affiliata CJ (Commission Junction)
description: Scopri come importare dati di affiliazione CJ (Commission Junction) in [!DNL Commerce Intelligence].L Commerce Intelligence].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# Importa [!DNL CJ Affiliate] dati

Per importare [!DNL CJ Affiliate (Commission Junction)] dati in [!DNL Adobe Commerce Intelligence], è sufficiente seguire i passaggi seguenti e allegare il file risultante a una [ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html). Adobe configurerà la tabella di dati del tuo account e ti consentirà di continuare a caricare i dati in modo indipendente.

## Esporta [!DNL CJ Affiliate] Dati

1. Nel tuo [!DNL CJ Affiliate] account, vai a `Reports` scheda.

1. In `Performance` , seleziona `Report Options`.

1. Imposta `Performance By` uguale a `Program`, `Trend` uguale a `Daily`, e `Date Range` è uguale all’intervallo di date sottoposto a controllo.

   ![export-cj-affiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Seleziona `Run Report`.

1. In `File Format` a discesa, seleziona `CSV`.  Clic **[!UICONTROL Download]**.

   ![esporta dati affiliate cj](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. Dopo aver scaricato il file, puoi [carica il file](../connecting-data/using-file-uploader.md) al tuo [!DNL Commerce Intelligence] Data Warehouse.

   Questo crea una tabella nel [!DNL Commerce Intelligence] Data Warehouse che puoi continuare a caricare dati aggiornati in periodicamente. Durante il caricamento del file, segui i requisiti di formattazione elencati in [Utilizzo di Caricamento file](../connecting-data/using-file-uploader.md).
