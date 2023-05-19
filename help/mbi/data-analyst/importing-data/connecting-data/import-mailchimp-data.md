---
title: Importa dati MailChimp
description: Scopri come importare dati MailChimp in [!DNL Commerce Intelligence].
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Importa [!DNL Mailchimp] dati

Per avere un quadro completo delle tue attività di campagna, puoi importare il tuo [!DNL Mailchimp] inviare i dati della campagna e-mail a [!DNL Commerce Intelligence]. Per completare l&#39;importazione, è necessario eseguire le operazioni seguenti per ogni [!DNL Mailchimp] campagna di cui disponi:

## Esporta dati di apertura {#opens}

1. Dopo l’accesso a [!DNL Mailchimp], passare alla `Campaigns` scheda.

   ![importa mailchimp 1](../../../assets/import-mailchimp-1.png)

1. Clic **[!UICONTROL View Report]**, accanto al nome della campagna.

   ![importa mailchimp 2](../../../assets/import-mailchimp-2.png)

1. Fai clic su **[!UICONTROL Opened]** numero.

   ![importa mailchimp 3](../../../assets/import-mailchimp-3.png)

1. Clic **[!UICONTROL Export]** e salva `.csv` file.

   È necessario aggiungere `primary key`, `date (mm/dd/yyyy)`, e `campaign name` in questo file. Assicurati che le `primary keys` sono univoci per ogni riga.

   ![importa mailchimp 4](../../../assets/import-mailchimp-4.png)

## Esporta dati clic {#clicks}

1. Torna a `View Report` schermata per la campagna.

1. Fai clic sul numero che `Clicked`.

   ![importa mailchimp 5](../../../assets/import-mailchimp-5.png)

1. Fai clic sul numero sotto al `Total Clicks` OPPURE `Unique Clicks` colonna.

   ![importa mailchimp 6](../../../assets/import-mailchimp-6.png)

1. Clic **[!UICONTROL Export]** e salva `.csv` file.

   È necessario aggiungere `Primary Key`, `date (mm/dd/yyyy)`, `campaign name`, e `URL` in questo file. Non è necessario aggiungere l’URL completo, solo un elemento che consente di sapere cosa è stato fatto clic.

   ![importa mailchimp 7](../../../assets/import-mailchimp-7.png)

1. Ripeti i passaggi 3 e 4 per ogni URL su cui hai fatto clic nell’e-mail, combinando tutti i dati nello stesso `.csv` al termine.

## Esporta dati inviati {#sent}

1. Accedi a `Campaigns` scheda di [!DNL Mailchimp].

1. Clic **[!UICONTROL View Report]** accanto al nome della campagna.

1. Fai clic sul numero accanto a `Recipients`.

   ![importa mailchimp 8](../../../assets/import-mailchimp-8.png)

1. Clic **[!UICONTROL Export]** e salva `.csv` file.

   È necessario aggiungere `Primary Key`, `date (mm/dd/yyyy)`, e `campaign name` in questo file.

   ![importa mailchimp 9](../../../assets/import-mailchimp-9.png)

## Prepara i file per il caricamento in [!DNL Commerce Intelligence] {#upload}

Ogni file - `Opens`, `Clicks`, e `Sent` - deve essere caricato in [!DNL Commerce Intelligence] come file separato. L’Adobe consiglia di denominare i file utilizzando questa convenzione di denominazione: `MailChimp\_ACTION\_DATE`. Sostituisci `ACTION` con `Open`, `Click`, o `Sent`, e sostituisci `DATE` con la data di esportazione.

Quando sei pronto a caricare i file, utilizza [`File Upload` funzionalità](../connecting-data/using-file-uploader.md) per inserire i dati nella Data Warehouse.
