---
title: Importa dati MailChimp
description: Scopri come importare i dati di MailChimp in  [!DNL Commerce Intelligence].
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/HJJYKfqc1sbslQimSNituG6Pm6wi6QpU-vn6GtKvV-Y
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
source-wordcount: 274
ht-degree: 0%

---

# Importa dati [!DNL Mailchimp]

Per ottenere un quadro completo delle tue attività di campagna, puoi importare i dati della tua campagna e-mail di [!DNL Mailchimp] in [!DNL Commerce Intelligence]. Per completare l&#39;importazione, eseguire le operazioni seguenti per ogni campagna [!DNL Mailchimp]:

## Esporta dati di apertura {#opens}

1. Dopo aver effettuato l&#39;accesso a [!DNL Mailchimp], passare alla scheda `Campaigns`.

   ![importa mailchimp 1](../../../assets/import-mailchimp-1.png)

1. Fare clic su **[!UICONTROL View Report]** accanto al nome della campagna.

   ![importa mailchimp 2](../../../assets/import-mailchimp-2.png)

1. Fare clic sul numero **[!UICONTROL Opened]**.

   ![importa mailchimp 3](../../../assets/import-mailchimp-3.png)

1. Fare clic su **[!UICONTROL Export]** e salvare il file `.csv`.

   Aggiungere `primary key`, `date (mm/dd/yyyy)` e `campaign name` colonne a questo file. Assicurarsi che `primary keys` siano univoci per ogni riga.

   ![importa mailchimp 4](../../../assets/import-mailchimp-4.png)

## Esporta dati clic {#clicks}

1. Tornare alla schermata `View Report` per la campagna.

1. Fare clic sul numero `Clicked`.

   ![importa mailchimp 5](../../../assets/import-mailchimp-5.png)

1. Fare clic sul numero sotto la colonna `Total Clicks` OPPURE `Unique Clicks`.

   ![importa mailchimp 6](../../../assets/import-mailchimp-6.png)

1. Fare clic su **[!UICONTROL Export]** e salvare il file `.csv`.

   Aggiungere `Primary Key`, `date (mm/dd/yyyy)`, `campaign name` e `URL` colonne a questo file. Non è necessario aggiungere l’URL completo, solo un elemento che consente di sapere cosa è stato fatto clic.

   ![importa mailchimp 7](../../../assets/import-mailchimp-7.png)

1. Ripeti i passaggi 3 e 4 per ogni URL su cui hai fatto clic nell&#39;e-mail, combinando tutti i dati nello stesso file `.csv` al termine.

## Esporta dati inviati {#sent}

1. Passa alla scheda `Campaigns` di [!DNL Mailchimp].

1. Fai clic su **[!UICONTROL View Report]** accanto al nome della campagna.

1. Fare clic sul numero accanto a `Recipients`.

   ![importa mailchimp 8](../../../assets/import-mailchimp-8.png)

1. Fare clic su **[!UICONTROL Export]** e salvare il file `.csv`.

   Aggiungere `Primary Key`, `date (mm/dd/yyyy)` e `campaign name` colonne a questo file.

   ![importa mailchimp 9](../../../assets/import-mailchimp-9.png)

## Prepara i file per il caricamento in [!DNL Commerce Intelligence] {#upload}

Ogni file - `Opens`, `Clicks` e `Sent` - deve essere caricato in [!DNL Commerce Intelligence] come file separato. Adobe consiglia di denominare i file utilizzando questa convenzione di denominazione: `MailChimp\_ACTION\_DATE`. Sostituisci `ACTION` con `Open`, `Click` o `Sent` e sostituisci `DATE` con la data di esportazione.

Quando sei pronto a caricare i file, utilizza la funzionalità [`File Upload`](../connecting-data/using-file-uploader.md) per inserire i dati nel tuo Data Warehouse.
