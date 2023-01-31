---
title: Connetti annunci Facebook
description: Scopri come analizzare i dati sulla spesa pubblicitaria e verificare se i tuoi soldi vengono spesi in modo efficace.
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# Connetti [!DNL Facebook Ads]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![](../../../assets/Facebook_Logo.png)

Hai fatto la tua ricerca, hai creato i tuoi annunci, hai lanciato la tua campagna su [!DNL Facebook]. Ora è il momento di analizzare i dati sulla spesa pubblicitaria e vedere se i vostri soldi vengono spesi in modo efficace. Utilizzando i dati di spesa pubblicitaria, puoi [misurare il ROI delle campagne sposando i costi pubblicitari e il valore del ciclo di vita del cliente (CLV)](../../../data-analyst/analysis/roi-ad-camp.md) degli utenti acquisiti dalle campagne.

Collegamento dei dati degli annunci Facebook a [!DNL MBI] è un semplice processo in tre fasi:

1. [Aggiungi [!DNL Facebook] come origine dati in [!DNL MBI]](#stepone)
1. [Consenti [!DNL MBI] accesso al [!DNL Facebook Ads] dati](#steptwo)
1. [Seleziona [!DNL Facebook Ads] Account per l’estrazione dei dati](#stepthree)

## Aggiungi [!DNL Facebook] come origine dati in [!DNL MBI] {#stepone}

1. Per aggiungere la [!DNL Facebook] integrazione con il tuo account, passa alla `Connections` pagina sotto **[!UICONTROL Manage Data** > **Integrations]**.
1. Fai clic su **[!UICONTROL Add Integration]**, situato sul lato destro dello schermo sopra i dati `Sources` tabella.
1. Fai clic sul pulsante [!DNL Facebook] icona. Verrà visualizzata la [!DNL Facebook] pagina di autorizzazione.
1. Fai clic su **[!UICONTROL Authorize]**.

## Consenti [!DNL MBI] accesso al [!DNL Facebook Ads] dati {#steptwo}

Dopo aver fatto clic su **[!DNL Facebook Authorize]**, viene visualizzata una piccola finestra a comparsa:

![](../../../assets/Facebook_Access_Popup.png)

Seguirai una serie di passaggi per consentire [!DNL MBI] per accedere ai dati dal tuo profilo pubblico, [!DNL Facebook Ads] e statistiche correlate. Fai clic su **[!UICONTROL OK]** su questi passaggi per continuare.

## Seleziona [!DNL Facebook Ads] Account per l’estrazione dei dati {#stepthree}

1. Al termine dell&#39;autenticazione, ti verrà richiesto di selezionare il [!DNL Facebook Ads] Account da cui si desidera estrarre i dati. Seleziona gli account desiderati facendo clic sulla casella di controllo nel `Connect` colonna.

   ![](../../../assets/Facebook_Ad_Accounts.png)

1. Fai clic su **[!UICONTROL Save Connections]**.

   Se la connessione ha esito positivo, un *Connessione riuscita.* il messaggio viene visualizzato nella parte superiore della pagina.

## cosa succede dopo? {#next}

Assicurati di tenere traccia [!DNL Facebook] campagne [!DNL Google Analytics] come da [tutorial](https://www.facebook.com/business/google-analytics). In tal modo, `utm\_campaign` campo [!DNL Google Analytics] è popolato correttamente per il [!DNL Facebook] campagne.

## Correlati

* [Riautenticazione delle integrazioni](https://support.magento.com/hc/en-us/articles/360016733151)
* [Collega il tuo [!DNL Google Adwords] account](../integrations/google-ecommerce.md)
* [Tracciare l’origine di riferimento dell’ordine tramite [!DNL Google eCommerce]](../integrations/google-ecommerce.md)
* [Tracciare l’origine del riferimento utente nel database](../../analysis/google-track-user-acq.md)
* [Tieni traccia dei dati di dispositivi utente, browser e sistemi operativi nel database](../../analysis/track-usr-dev-browser.md)
* [Scopri le fonti e i canali di acquisizione più importanti](../../analysis/most-value-source-channel.md)
* [Aumenta il ROI delle campagne pubblicitarie](../../analysis/roi-ad-camp.md)
* [Come funziona [!DNL Google Analytics] L’attribuzione UTM funziona?](../../analysis/utm-attributes.md)
