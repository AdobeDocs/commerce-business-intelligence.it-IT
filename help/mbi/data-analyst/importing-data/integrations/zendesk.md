---
title: Connetti Zendesk
description: Scopri come consolidare il reporting dell’help desk in [!DNL MBI].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Connetti [!DNL Zendesk]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![](../../../assets/Zendesk_logo.png)

Collegamento del [!DNL Zendesk] i dati consentono di consolidare i rapporti dell&#39;help desk in [!DNL MBI]. Questo consente di ottimizzare l&#39;assistenza clienti e monitorare le prestazioni dell&#39;help desk insieme ai ricavi.

Collegamento del [!DNL Zendesk] i dati sono un semplice processo in tre fasi:

1. [Apri [!DNL Zendesk] pagina delle credenziali in [!DNL MBI]](#stepone)
1. [Recupera il tuo [!DNL Zendesk] Token API](#steptwo)
1. [Inserisci il tuo [!DNL Zendesk] informazioni di accesso e token in [!DNL MBI]](#stepthree)

Per completare questo processo, dovrai aprire due finestre o schede del browser, una per [!DNL MBI], l&#39;altro per il tuo [!DNL Zendesk] conto.

## Apri [!DNL Zendesk] pagina delle credenziali in [!DNL MBI] {#stepone}

1. Vai a `Integrations` pagina sotto **[!UICONTROL Manage Data** > ** Origini dati **> **Integrazioni]**.
1. Fai clic su **[!UICONTROL Add Integration]**, situato sul lato destro dello schermo.
1. Fai clic sul pulsante [!DNL Zendesk] icona. Verrà aperto il [!DNL Zendesk] pagina delle credenziali.

## Recupera il tuo [!DNL Zendesk] Token API {#steptwo}

1. Nella finestra/scheda in cui hai effettuato l’accesso al tuo [!DNL Zendesk] , fai clic sull’icona Impostazioni (ingranaggio) nell’angolo in basso a sinistra dello schermo.
1. Quando il `Settings` visualizza il menu, individuare `Channels` sezione . Fai clic su **[!UICONTROL API]** in questa sezione.
1. In `Token Access` in questa sezione della pagina, fai clic sulla casella di controllo accanto a `Enabled`. Verrà visualizzato un elenco di token API attivi.
1. Fai clic su **[!UICONTROL Add New Token]**.
1. Quando richiesto, immetti un’etichetta per il token. Si consiglia di utilizzare `MBI`, quindi saprete subito quale applicazione utilizza il token.
1. Fai clic su **[!UICONTROL Create]**.
1. Verrà creato un token API. Copia questo token; verrà utilizzato nel passaggio successivo.

## Invio [!DNL Zendesk] informazioni di accesso e token API in [!DNL MBI] {#stepthree}

1. Inserisci il tuo [!DNL Zendesk] prefisso del sito ed e-mail di accesso nel [!DNL Zendesk] pagina delle credenziali in [!DNL MBI].
1. Immetti il token API.
1. Fai clic su **[!UICONTROL Save & Connect]**. Se la connessione ha esito positivo, un *Connessione riuscita.* il messaggio viene visualizzato nella parte superiore dello schermo.

## Correlati:

* [Previsto [!DNL Zendesk] dati](../integrations/exp-zendesk-data.md)
* [Riautenticazione delle integrazioni](https://support.magento.com/hc/en-us/articles/360016733151)
