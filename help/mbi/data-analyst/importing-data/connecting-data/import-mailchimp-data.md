---
title: Importa dati MailChimp
description: Impara a importare i dati di MailChimp in [!DNL MBI].
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Importa `MailChimp` dati

Per ottenere un quadro completo dei tuoi sforzi di campagna, puoi importare il tuo `MailChimp` inviare dati della campagna e-mail a [!DNL MBI]. Per completare l’importazione, è necessario effettuare le seguenti operazioni per ogni `MailChimp` campagna disponibile:

## Esportare i dati Aperture {#opens}

1. Dopo aver effettuato l’accesso a `MailChimp`, vai al `Campaigns` scheda .

   ![import mailchimp 1](../../../assets/import-mailchimp-1.png)

1. Fai clic su **[!UICONTROL View Report]**, accanto al nome della campagna.

   ![import mailchimp 2](../../../assets/import-mailchimp-2.png)

1. Fai clic sul pulsante **[!UICONTROL Opened]** numero.

   ![import mailchimp 3](../../../assets/import-mailchimp-3.png)

1. Fai clic su **[!UICONTROL Export]** e salva il `.csv` file.

   Dovrai aggiungere `primary key`, `date (mm/dd/yyyy)`e `campaign name` in questo file. Assicurati che `primary keys` sono univoci per ogni riga.

   ![import mailchimp 4](../../../assets/import-mailchimp-4.png)

## Esportare i dati dei clic {#clicks}

1. Torna alla pagina `View Report` per la campagna.

1. Fai clic sul numero `Clicked`.

   ![import mailchimp 5](../../../assets/import-mailchimp-5.png)

1. Fai clic sul numero sotto il `Total Clicks` O `Unique Clicks` colonna.

   ![import mailchimp 6](../../../assets/import-mailchimp-6.png)

1. Fai clic su **[!UICONTROL Export]** e salva il `.csv` file.

   Dovrai aggiungere `Primary Key`, `date (mm/dd/yyyy)`, `campaign name`e `URL` in questo file. Non è necessario aggiungere l’URL completo, ma solo qualcosa che ti informerà di ciò che è stato fatto clic.

   ![Importa mailchimp 7](../../../assets/import-mailchimp-7.png)

1. Ripeti i passaggi 3 e 4 per ogni URL selezionato nell’e-mail, combinando tutti i dati nello stesso `.csv` al termine.

## Esportare i dati inviati {#sent}

1. Vai in `Campaigns` scheda di MailChimp.

1. Fai clic su **[!UICONTROL View Report]** accanto al nome della campagna.

1. Fai clic sul numero accanto a `Recipients`.

   ![import mailchimp 8](../../../assets/import-mailchimp-8.png)

1. Fai clic su **[!UICONTROL Export]** e salva il `.csv` file.

   Dovrai aggiungere `Primary Key`, `date (mm/dd/yyyy)`e `campaign name` in questo file.

   ![Importa mailchimp 9](../../../assets/import-mailchimp-9.png)

## Preparare i file da caricare in [!DNL MBI] {#upload}

Ogni file - `Opens`, `Clicks`e `Sent` - deve essere caricato su [!DNL MBI] come file separato. È inoltre consigliabile denominare i file utilizzando questa convenzione di denominazione: `MailChimp\_ACTION\_DATE`. Sostituisci `ACTION` con `Open`, `Click`oppure `Sent`e sostituiscono `DATE` con la data di esportazione.

Quando sei pronto a caricare i file, utilizza il [`File Upload` caratteristica](../connecting-data/using-file-uploader.md) per inserire i dati nel data warehouse.
