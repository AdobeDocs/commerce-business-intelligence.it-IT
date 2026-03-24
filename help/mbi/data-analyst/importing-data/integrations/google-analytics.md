---
title: Connetti Google Analytics
description: Scopri come connettere Google Analytics con  [!DNL Commerce Intelligence].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/wSR5SWYSfmNZkzp5QxTUwv6QSsynXYofmRkKbvMsohs
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 283
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

* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=it)
* [Connessione in corso  [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Analisi delle attività del sito web e dei tassi di conversione dei clienti](../../analysis/web-act-cust-conversion.md)
* [Tieni traccia dei dati di acquisizione dell&#39;utente utilizzando  [!DNL Google Analytics] cookie](../../analysis/google-track-user-acq.md)
