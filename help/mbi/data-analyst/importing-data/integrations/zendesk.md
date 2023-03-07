---
title: Connetti Zendesk
description: Scopri come consolidare il reporting dell’help desk in [!DNL MBI].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# Connetti [!DNL Zendesk]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![](../../../assets/Zendesk_logo.png)

Collegamento [!DNL Zendesk] dati consente di consolidare il reporting dell&#39;help desk in [!DNL MBI]. Questo consente di ottimizzare l&#39;assistenza clienti e monitorare le prestazioni dell&#39;help desk insieme ai ricavi.

Collegamento [!DNL Zendesk] i dati sono un semplice processo in tre fasi:

1. [Apri [!DNL Zendesk] pagina delle credenziali in [!DNL MBI]](#stepone)
1. [Recupera [!DNL Zendesk] Token API](#steptwo)
1. [Immetti il [!DNL Zendesk] info di accesso e token in [!DNL MBI]](#stepthree)

Per completare questa procedura, devi aprire due finestre o schede del browser: una per [!DNL MBI], l&#39;altro per [!DNL Zendesk] account.

## Apri [!DNL Zendesk] pagina delle credenziali in [!DNL MBI] {#stepone}

1. Vai a `Integrations` pagina in **[!UICONTROL Manage Data** > ** Origini dati **> **Integrazioni]**.
1. Clic **[!UICONTROL Add Integration]**, situato sul lato destro dello schermo.
1. Fai clic su [!DNL Zendesk] icona. Verrà aperto il [!DNL Zendesk] pagina delle credenziali.

## Recupera [!DNL Zendesk] Token API {#steptwo}

1. Nella finestra/scheda in cui hai effettuato l’accesso a [!DNL Zendesk] fare clic sull&#39;icona Impostazioni (ingranaggio) nell&#39;angolo inferiore sinistro della schermata.
1. Quando `Settings` viene visualizzato il menu, individuare `Channels` sezione. Clic **[!UICONTROL API]** in questa sezione.
1. In `Token Access` sezione di questa pagina, fai clic sulla casella di controllo accanto a `Enabled`. Viene visualizzato un elenco dei token API attivi.
1. Clic **[!UICONTROL Add New Token]**.
1. Quando richiesto, immetti un’etichetta per il token. L’Adobe consiglia di utilizzare `MBI`quindi, a colpo d’occhio, quale applicazione sta utilizzando il token.
1. Clic **[!UICONTROL Create]**.
1. Viene creato un token API. Copia questo token, che verrà utilizzato nel passaggio successivo.

## Invio [!DNL Zendesk] info di accesso e token API in [!DNL MBI] {#stepthree}

1. Immetti il [!DNL Zendesk] prefisso del sito e indirizzo e-mail di accesso in [!DNL Zendesk] pagina delle credenziali in [!DNL MBI].
1. Immetti il token API.
1. Clic **[!UICONTROL Save & Connect]**. Se la connessione ha esito positivo, viene visualizzata una *Connessione riuscita* Il messaggio viene visualizzato nella parte superiore dello schermo.

## Correlato:

* [Previsto [!DNL Zendesk] dati](../integrations/exp-zendesk-data.md)
* [Reautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
