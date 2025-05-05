---
title: Connetti Facebook Ads
description: Scopri come analizzare i dati di spesa degli annunci e vedere se i tuoi soldi vengono spesi in modo efficace.
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# Connetti [!DNL Facebook Ads]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![](../../../assets/facebook-ads-logo.png)

Hai fatto la tua ricerca, creato i tuoi annunci, lanciato la tua campagna il [!DNL Facebook]. Ora è il momento di analizzare i dati di spesa degli annunci e verificare se i soldi vengono spesi in modo efficace. Utilizzando i dati di spesa degli annunci, puoi [misurare il ROI delle campagne unendo i costi pubblicitari e il valore del ciclo di vita del cliente (CLV)](../../../data-analyst/analysis/roi-ad-camp.md) degli utenti acquisiti dalle campagne.

La connessione dei dati di [!DNL Facebook Ad] a [!DNL Commerce Intelligence] è un semplice processo in tre fasi:

1. [Aggiungi [!DNL Facebook] come origine dati in [!DNL Commerce Intelligence]](#stepone)
1. [Consenti [!DNL Commerce Intelligence] accesso ai tuoi [!DNL Facebook Ads] dati](#steptwo)
1. [Seleziona [!DNL Facebook Ads] account per estrarre i dati](#stepthree)

## Aggiungi [!DNL Facebook] come origine dati in [!DNL Commerce Intelligence] {#stepone}

1. Per aggiungere l&#39;integrazione di [!DNL Facebook] all&#39;account [!DNL Commerce Intelligence], passare alla pagina `Connections` in **[!UICONTROL Manage Data** > **Integrations]**.
1. Fai clic su **[!UICONTROL Add Integration]**, a destra.
1. Fare clic sull&#39;icona [!DNL Facebook]. Viene visualizzata la pagina di autorizzazione [!DNL Facebook].
1. Fare clic su **[!UICONTROL Authorize]**.

## Consenti a [!DNL Commerce Intelligence] l&#39;accesso ai tuoi dati di [!DNL Facebook Ads] {#steptwo}

Dopo aver fatto clic su **[!DNL Facebook Authorize]**, verrà visualizzata una piccola finestra popup:

![](../../../assets/Facebook_Access_Popup.png)

Segui una serie di passaggi per consentire a [!DNL Commerce Intelligence] di accedere ai dati dal tuo profilo pubblico, [!DNL Facebook Ads] e statistiche correlate. Fare clic su **[!UICONTROL OK]** in questi passaggi per continuare.

## Seleziona account [!DNL Facebook Ads] per il richiamo dei dati {#stepthree}

1. Al termine dell&#39;autenticazione, verrà richiesto di selezionare gli account [!DNL Facebook Ads] da cui si desidera estrarre i dati. Selezionare gli account desiderati facendo clic sulla casella di controllo nella colonna `Connect`.

   ![](../../../assets/Facebook_Ad_Accounts.png)

1. Fare clic su **[!UICONTROL Save Connections]**.

   Se la connessione ha esito positivo, *Connessione riuscita.Il messaggio* viene visualizzato nella parte superiore della pagina.

## Cosa succede dopo? {#next}

Assicurati di monitorare [!DNL Facebook] campagne in [!DNL Google Analytics]. In questo modo il campo `utm\_campaign` in [!DNL Google Analytics] viene popolato correttamente per le campagne [!DNL Facebook].

## Correlato

* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=it)
* [Connetti il tuo account  [!DNL Google Adwords] ](../integrations/google-ecommerce.md)
* [Tracciare l&#39;origine di riferimento dell&#39;ordine tramite [!DNL Google eCommerce]](../integrations/google-ecommerce.md)
* [Tracciare l&#39;origine di riferimento dell&#39;utente nel database](../../analysis/google-track-user-acq.md)
* [Tenere traccia dei dati relativi a dispositivi utente, browser e sistema operativo nel database](../../analysis/track-usr-dev-browser.md)
* [Scopri le fonti e i canali di acquisizione più importanti](../../analysis/most-value-source-channel.md)
* [Aumentare il ROI nelle campagne pubblicitarie](../../analysis/roi-ad-camp.md)
* [Come funziona l&#39;attribuzione  [!DNL Google Analytics] UTM?](../../analysis/utm-attributes.md)
