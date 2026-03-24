---
title: Importazione dei dati di marketing di un'affiliata CJ (Commission Junction)
description: Scopri come importare dati di affiliazione CJ (Commission Junction) in  [!DNL Commerce Intelligence].L Commerce Intelligence&rbrack;.
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
TQID: https://experienceleague.adobe.com/tZ2fzAKou0fBmkmKD5zdLFBNCSiAGpT3GNgkHp9ptx4
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 141
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
