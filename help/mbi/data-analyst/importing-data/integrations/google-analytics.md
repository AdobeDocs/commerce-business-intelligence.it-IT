---
title: Connetti Google Analytics
description: Scopri come collegare le Google Analytics con [!DNL MBI].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
source-git-commit: 8de036e2717aedef95a8bb908898fd9b9bc9c3fa
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Connetti [!DNL Google Analytics]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] è il servizio di analisi web più utilizzato su internet. Implementazione [!DNL Google Analytics] sul sito web consente di tenere traccia di come i visitatori utilizzano il sito, di quali contenuti sono attraenti, di dove i visitatori escono e altro ancora. Analisi di queste metriche in [!DNL MBI], insieme ad altri dati, migliora lo stato e l’usabilità generali del sito.

Per iniziare, immetti il [!DNL Google Analytics] credenziali in [!DNL MBI]:

1. Vai a **[!UICONTROL Manage Data** > **Integrations]** pagina.
1. Clic **[!UICONTROL Add Integration]**, situato sul lato destro dello schermo.
1. Fai clic su [!DNL Google Analytics] icona. Verrà aperto il [!DNL Google Analytics] pagina delle credenziali.
1. Immetti il [!DNL Google Analytics] credenziali. Al termine del processo di autorizzazione, verrai reindirizzato nuovamente a [!DNL MBI].
1. Viene visualizzato un elenco di ID profilo. Controlla i profili a cui desideri connetterti [!DNL MBI]. Se disponi di più profili e hai bisogno di aiuto per identificare quale sia, consulta Connessione multipla [!DNL Google Analytics] nella sezione dei profili.

   ![](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. Le modifiche vengono salvate automaticamente, quindi fai clic su **Torna a Connessioni** quando hai finito.

## Collegamento di più [!DNL Google Analytics] profili

È possibile che più siti Web siano connessi a un unico [!DNL Google Analytics] account, identificato dal proprio [!DNL Google Analytics] ID profilo. In questo caso, puoi includere tutti gli ID profilo in [!DNL MBI]. Controlla gli ID profilo da includere durante il passaggio di selezione del profilo.

Per identificare i [!DNL Google Analytics] ID profilo:

1. Accedi a [!DNL Google Analytics]
1. Vai a quello del sito Web [!DNL Google Analytics] dashboard
1. Controlla l’URL: l’ID profilo corrisponde agli otto numeri seguenti `p` alla fine della riga:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Disconnessione [!DNL Google Analytics] da [!DNL MBI] {#disconnect}

1. Visita il [!DNL Google Analytics] [impostazioni account](https://accounts.google.com/) pagina.
1. Sotto `Security` e fai clic su **[!UICONTROL edit]** accanto a `Authorizing` applicazioni e siti.
1. Clic **[!UICONTROL revoke access]** accanto a [!DNL MBI].

## Correlato:

* [Reautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [Connessione [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Analisi delle attività del sito web e dei tassi di conversione dei clienti](../../analysis/web-act-cust-conversion.md)
* [Tracciare i dati di acquisizione dell&#39;utente tramite [!DNL Google Analytics] cookie](../../analysis/google-track-user-acq.md)
