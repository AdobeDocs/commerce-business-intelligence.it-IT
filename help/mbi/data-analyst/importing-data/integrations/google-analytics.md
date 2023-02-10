---
title: Google Analytics di connessione
description: Scopri come collegare Google Analytics con [!DNL MBI].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Connetti [!DNL Google Analytics]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] è il servizio di analisi web più utilizzato su Internet. Implementazione [!DNL Google Analytics] nel sito web puoi monitorare come i visitatori utilizzano il tuo sito, quale contenuto è attraente, dove i visitatori escono e altro ancora. Analisi di queste metriche in [!DNL MBI], insieme ad altri dati, migliorerà la salute e l&#39;usabilità complessive del tuo sito.

Iniziamo entrando nel nostro [!DNL Google Analytics] credenziali in [!DNL MBI]:

1. Vai a **[!UICONTROL Manage Data** > **Integrations]** pagina.
1. Fai clic su **[!UICONTROL Add Integration]**, situato sul lato destro dello schermo.
1. Fai clic sul pulsante [!DNL Google Analytics] icona. Verrà aperto il [!DNL Google Analytics] pagina delle credenziali.
1. Inserisci il tuo [!DNL Google Analytics] credenziali. Al termine del processo di autorizzazione, verrai reindirizzato a [!DNL MBI].
1. Verrà visualizzato un elenco di ID profilo. Controlla i profili a cui desideri connetterti [!DNL MBI]. Se disponi di più profili e hai bisogno di aiuto per identificare quale di questi è, consulta Collegamento multiplo [!DNL Google Analytics] di seguito la sezione dei profili.

   ![](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. Le modifiche vengono salvate automaticamente, quindi fai clic su **Torna a Connessioni** quando hai finito.

## Collegamento di più [!DNL Google Analytics] profiles

È possibile che più siti web siano connessi a un singolo [!DNL Google Analytics] conto, identificato dal proprio [!DNL Google Analytics] ID profilo. In questo caso, avrai la possibilità di includere tutti gli ID profilo in [!DNL MBI]. Controlla gli ID profilo che desideri includere durante il passaggio di selezione del profilo.

Per identificare un particolare sito web [!DNL Google Analytics] ID profilo:

1. Accedi a [!DNL Google Analytics]
1. Vai al sito web particolare [!DNL Google Analytics] dashboard
1. Osserva l’URL : l’ID profilo corrisponde agli 8 numeri seguenti `p` alla fine della riga:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Disconnessione [!DNL Google Analytics] da [!DNL MBI] {#disconnect}

1. Visita il tuo [!DNL Google Analytics] [impostazioni account](https://www.google.com/accounts/) pagina.
1. Sotto la `Security` e fai clic su **[!UICONTROL edit]** accanto a `Authorizing` applicazioni e siti.
1. Fai clic su **[!UICONTROL revoke access]** accanto a [!DNL MBI].

## Correlati:

* [Riautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [Collegamento [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Analisi dell’attività del sito web e dei tassi di conversione dei clienti](../../analysis/web-act-cust-conversion.md)
* [Tracciare i dati di acquisizione degli utenti utilizzando [!DNL Google Analytics] cookie](../../analysis/google-track-user-acq.md)
