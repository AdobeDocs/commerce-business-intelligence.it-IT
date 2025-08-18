---
title: Importazione dei dati di marketing di un'affiliata CJ (Commission Junction)
description: Scopri come importare dati di affiliazione CJ (Commission Junction) in  [!DNL Commerce Intelligence].L Commerce Intelligence].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# Importa dati [!DNL CJ Affiliate]

Per importare i dati di [!DNL CJ Affiliate (Commission Junction)] in [!DNL Adobe Commerce Intelligence], è sufficiente seguire la procedura seguente e allegare il file risultante a un [ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html). Adobe configurerà la tabella dati del tuo account e ti consentirà di continuare a caricare i dati in modo indipendente.

## Esporta dati [!DNL CJ Affiliate]

1. Nel tuo account [!DNL CJ Affiliate], passa alla scheda `Reports`.

1. Nella scheda `Performance`, selezionare `Report Options`.

1. Imposta `Performance By` uguale a `Program`, `Trend` uguale a `Daily` e `Date Range` uguale all&#39;intervallo di date sottoposto a controllo.

   ![export-cj-affiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Selezionare `Run Report`.

1. Nel menu a discesa `File Format`, seleziona `CSV`.  Fare clic su **[!UICONTROL Download]**.

   ![esporta dati affiliate cj](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. Dopo aver scaricato il file, puoi [caricarlo](../connecting-data/using-file-uploader.md) nel tuo Data Warehouse [!DNL Commerce Intelligence].

   In questo modo viene creata una tabella nel Data Warehouse [!DNL Commerce Intelligence] in cui è possibile continuare a caricare dati aggiornati periodicamente. Durante il caricamento del file, attieniti ai requisiti di formattazione elencati in [Utilizzo di Caricamento file](../connecting-data/using-file-uploader.md).
