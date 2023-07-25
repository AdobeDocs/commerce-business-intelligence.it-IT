---
title: Connetti Facebook Ads
description: Scopri come analizzare i dati di spesa degli annunci e vedere se i tuoi soldi vengono spesi in modo efficace.
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# Connetti [!DNL Facebook Ads]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![](../../../assets/facebook-ads-logo.png)

Hai fatto la tua ricerca, creato i tuoi annunci, lanciato la tua campagna su [!DNL Facebook]. Ora è il momento di analizzare i dati di spesa degli annunci e verificare se i soldi vengono spesi in modo efficace. Utilizzando i dati sulla spesa pubblicitaria, puoi [misurare il ROI delle campagne sposando i costi pubblicitari e il valore del ciclo di vita del cliente (CLV)](../../../data-analyst/analysis/roi-ad-camp.md) degli utenti acquisiti dalle campagne.

Collegamento [!DNL Facebook Ad] dati a [!DNL Commerce Intelligence] è un semplice processo in tre fasi:

1. [Aggiungi [!DNL Facebook] come origine dati in [!DNL Commerce Intelligence]](#stepone)
1. [Consenti [!DNL Commerce Intelligence] accesso al tuo [!DNL Facebook Ads] dati](#steptwo)
1. [Seleziona [!DNL Facebook Ads] Account per il richiamo dei dati](#stepthree)

## Aggiungi [!DNL Facebook] come origine dati in [!DNL Commerce Intelligence] {#stepone}

1. Per aggiungere [!DNL Facebook] integrazione al tuo [!DNL Commerce Intelligence]account, passa a `Connections` pagina in **[!UICONTROL Manage Data** > **Integrations]**.
1. Clic **[!UICONTROL Add Integration]**, a destra.
1. Fai clic su [!DNL Facebook] icona. Viene visualizzata la [!DNL Facebook] pagina di autorizzazione.
1. Clic **[!UICONTROL Authorize]**.

## Consenti [!DNL Commerce Intelligence] accesso al tuo [!DNL Facebook Ads] dati {#steptwo}

Dopo aver fatto clic su **[!DNL Facebook Authorize]**, viene visualizzata una piccola finestra a comparsa:

![](../../../assets/Facebook_Access_Popup.png)

Segui una serie di passaggi per consentire [!DNL Commerce Intelligence] per accedere ai dati dal tuo profilo pubblico, [!DNL Facebook Ads] e, statistiche correlate. Clic **[!UICONTROL OK]** su questi passaggi per continuare.

## Seleziona [!DNL Facebook Ads] Account per il richiamo dei dati {#stepthree}

1. Al termine dell’autenticazione, ti verrà richiesto di selezionare [!DNL Facebook Ads] Account da cui desideri estrarre i dati. Seleziona gli account desiderati facendo clic sulla casella di controllo in `Connect` colonna.

   ![](../../../assets/Facebook_Ad_Accounts.png)

1. Clic **[!UICONTROL Save Connections]**.

   Se la connessione ha esito positivo, viene visualizzata una *Connessione riuscita* viene visualizzato nella parte superiore della pagina.

## Cosa succede dopo? {#next}

Assicurati di tenere traccia di [!DNL Facebook] campagne in [!DNL Google Analytics]. Ciò garantisce che `utm\_campaign` campo in [!DNL Google Analytics] è compilato correttamente per il tuo [!DNL Facebook] campagne.

## Correlato

* [Reautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Connetti [!DNL Google Adwords] account](../integrations/google-ecommerce.md)
* [Tracciare l’origine di riferimento dell’ordine tramite [!DNL Google eCommerce]](../integrations/google-ecommerce.md)
* [Tracciare l&#39;origine di riferimento dell&#39;utente nel database](../../analysis/google-track-user-acq.md)
* [Tenere traccia dei dati relativi a dispositivi utente, browser e sistema operativo nel database](../../analysis/track-usr-dev-browser.md)
* [Scopri le fonti e i canali di acquisizione più importanti](../../analysis/most-value-source-channel.md)
* [Aumentare il ROI nelle campagne pubblicitarie](../../analysis/roi-ad-camp.md)
* [In che modo [!DNL Google Analytics] Lavoro di attribuzione UTM?](../../analysis/utm-attributes.md)
