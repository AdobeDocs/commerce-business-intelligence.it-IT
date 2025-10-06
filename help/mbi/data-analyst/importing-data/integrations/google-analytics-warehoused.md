---
title: Connetti Google Analytics Warehousing
description: Scopri come monitorare il modo in cui i visitatori utilizzano il tuo sito, quali contenuti sono attraenti, dove i visitatori escono e altro ancora.
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# Connetti [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![Logo Google Analytics](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] è il servizio di analisi Web più utilizzato su Internet. L&#39;implementazione di [!DNL Google Analytics] sul sito Web consente di tenere traccia di come i visitatori utilizzano il sito, quali contenuti sono interessanti, dove i visitatori escono e altro ancora. [!DNL Google Analytics Warehoused] è un&#39;integrazione separata dall&#39;integrazione esistente di [!DNL Google Analytics]. Consente una migliore analisi grazie alla presenza dei dati [!DNL Google Analytics] nel Data Warehouse, che è diverso dal feed live dell&#39;integrazione [!DNL Google Analytics] esistente. L&#39;analisi di queste metriche in [!DNL Commerce Intelligence], insieme ad altre parti di dati, migliora lo stato e l&#39;usabilità complessivi del sito.

## Differenza tra Warehouse GA e integrazione Live

Il principale elemento di differenziazione è che un&#39;integrazione è archiviata ([!DNL Google Analytics Warehoused]) e l&#39;altra non è ([!DNL Google Analytics Live]). Nel caso di [!DNL Google Analytics Warehoused], ciò consente la manipolazione dei dati di [!DNL Google Analytics] e consente di combinare [!DNL Google Analytics] e altre origini dati per creare report approfonditi.

Osserva le [!DNL Google Analytics] campagne pubblicitarie per un esempio di cosa si può fare dal punto di vista della manipolazione. Supponiamo di avere più campagne pubblicitarie per il quarto trimestre con nomi diversi. Le campagne erano il risultato di un’iniziativa di marketing specifica. Con i dati immagazzinati, puoi creare una colonna che trovi i nomi delle campagne in questione e restituisca il nome dell&#39;iniziativa del quarto trimestre di `Operation Dumbo`.

L&#39;aspetto combinato consente di unire i dati di [!DNL Google Analytics] ad altri dati per eseguire analisi. Prendi ad esempio `Total Time On Site By Ad Campaign` dati da [!DNL Google Analytics] e unisciti a `Total Spent Per Campaign` dati da [!DNL Facebook Ads] per ottenere un quadro completo del costo del coinvolgimento.

Con l&#39;integrazione di [!DNL Google Analytics Live], invece, ogni grafico [!DNL Google Analytics] è come un piccolo silo non memorizzato nel Data Warehouse.

## Connessione a [!DNL Google Analytics Warehoused] in corso

>[!INFO]
>
>[!DNL Google Analytics Warehoused] è un&#39;integrazione `Premium`. [Contatta il supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=it) se hai interesse ad aggiungere questa integrazione alla sottoscrizione.

1. Passare alla pagina `Connections` in **[!UICONTROL Admin** > **Integrations]**.
1. Fare clic su **[!UICONTROL Add an Integration]**, che si trova sul lato destro.
1. Fare clic sull&#39;icona [!DNL Google Analytics Warehoused]. Verrà aperta la pagina delle credenziali [!DNL Google Analytics].
1. Immetti le tue credenziali di [!DNL Google Analytics]. Al termine del processo di autorizzazione, l&#39;utente viene reindirizzato a [!DNL Commerce Intelligence].
1. Viene visualizzato un elenco di ID profilo. Controllare i profili a cui connettersi [!DNL Commerce Intelligence]. Se disponi di più profili e hai bisogno di aiuto per identificare quale sia, consulta la sezione Connessione di più profili [!DNL Google Analytics] di seguito.

## Connessione di più profili [!DNL Google Analytics]

È possibile che più siti Web siano connessi a un unico account [!DNL Google Analytics], identificato dal proprio ID profilo [!DNL Google Analytics]. In questo caso, puoi includere tutti gli ID profilo in [!DNL Commerce Intelligence]. Controlla gli ID profilo da includere durante il passaggio di selezione del profilo.

Per identificare l&#39;ID profilo [!DNL Google Analytics] di un particolare sito Web:

1. Accedi a [!DNL Google Analytics]
1. Passa alla dashboard [!DNL Google Analytics] del sito Web specifico
1. Controlla l&#39;URL: l&#39;ID profilo corrisponde agli otto numeri seguenti `p` alla fine della riga

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Disconnessione di [!DNL Google Analytics Warehoused] da [!DNL Commerce Intelligence] {#disconnect}

1. Visita la pagina delle [!DNL Google Analytics] [impostazioni account](https://myaccount.google.com/intro).
1. Nella sezione `Security` e fare clic su **[!UICONTROL edit]** accanto a `Authorizing` applicazioni e siti.
1. Fai clic su **[!UICONTROL revoke access]** accanto a [!DNL Commerce Intelligence].

## Documentazione correlata

* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=it)
* [Connessione in corso  [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Analisi delle attività del sito web e dei tassi di conversione dei clienti](../../analysis/web-act-cust-conversion.md)
* [Tieni traccia dei dati di acquisizione dell&#39;utente utilizzando  [!DNL Google Analytics] cookie](../../analysis/google-track-user-acq.md)
