---
title: Connetti Google Analytics
description: Scopri come connettere Google Analytics con  [!DNL Commerce Intelligence].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Connetti [!DNL Google Analytics]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![Logo Google Analytics](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] è il servizio di analisi Web più utilizzato su Internet. L&#39;implementazione di [!DNL Google Analytics] sul sito Web consente di tenere traccia di come i visitatori utilizzano il sito, quali contenuti sono interessanti, dove i visitatori escono e altro ancora. L&#39;analisi di queste metriche in [!DNL Commerce Intelligence], insieme ad altre parti di dati, migliora lo stato e l&#39;usabilità complessivi del sito.

Inizia immettendo le tue credenziali di [!DNL Google Analytics] in [!DNL Commerce Intelligence]:

1. Vai a **[!UICONTROL Manage Data** > **Integrations]**.

1. Fare clic su **[!UICONTROL Add Integration]**, che si trova sul lato destro della schermata.

1. Fare clic sull&#39;icona [!DNL Google Analytics]. Verrà aperta la pagina delle credenziali [!DNL Google Analytics].

1. Immetti le tue credenziali di [!DNL Google Analytics]. Al termine del processo di autorizzazione, verrà eseguito il reindirizzamento a [!DNL Commerce Intelligence].

1. Viene visualizzato un elenco di ID profilo. Controllare i profili a cui connettersi [!DNL Commerce Intelligence]. Se disponi di più profili e hai bisogno di aiuto per identificare quale sia, consulta la sezione Connessione di più profili [!DNL Google Analytics] di seguito.

   ![Pagina amministrazione Google Analytics con ID profilo nell&#39;URL](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. Le modifiche vengono salvate automaticamente, quindi al termine fai clic su **Torna a connessioni**.

## Connessione di più profili [!DNL Google Analytics]

È possibile che più siti Web siano connessi a un unico account [!DNL Google Analytics], identificato dal proprio ID profilo [!DNL Google Analytics]. In questo caso, puoi includere tutti gli ID profilo in [!DNL Commerce Intelligence]. Controlla gli ID profilo da includere durante il passaggio di selezione del profilo.

Per identificare l&#39;ID profilo [!DNL Google Analytics] di un particolare sito Web:

1. Accedi a [!DNL Google Analytics]
1. Passa alla dashboard [!DNL Google Analytics] del sito Web specifico
1. Controlla l&#39;URL: l&#39;ID profilo corrisponde agli otto numeri seguenti `p` alla fine della riga:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Disconnessione di [!DNL Google Analytics] da [!DNL Commerce Intelligence] {#disconnect}

1. Visita la pagina delle [!DNL Google Analytics] [impostazioni account](https://accounts.google.com/).
1. Nella sezione `Security` e fare clic su **[!UICONTROL edit]** accanto a `Authorizing` applicazioni e siti.
1. Fai clic su **[!UICONTROL revoke access]** accanto a [!DNL Commerce Intelligence].

## Correlato:

* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Connessione in corso  [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Analisi delle attività del sito web e dei tassi di conversione dei clienti](../../analysis/web-act-cust-conversion.md)
* [Tieni traccia dei dati di acquisizione dell&#39;utente utilizzando  [!DNL Google Analytics] cookie](../../analysis/google-track-user-acq.md)
