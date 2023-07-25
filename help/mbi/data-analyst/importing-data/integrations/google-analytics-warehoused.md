---
title: Connetti Google Analytics Warehousing
description: Scopri come monitorare il modo in cui i visitatori utilizzano il tuo sito, quali contenuti sono attraenti, dove i visitatori escono e altro ancora.
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Connetti [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] è il servizio di analisi web più utilizzato su internet. Implementazione [!DNL Google Analytics] sul sito web consente di tenere traccia di come i visitatori utilizzano il sito, di quali contenuti sono attraenti, di dove i visitatori escono e altro ancora. [!DNL Google Analytics Warehoused] è un’integrazione separata dalla [!DNL Google Analytics] integrazione. Consente una migliore analisi grazie alla possibilità di [!DNL Google Analytics] dati nella tua Data Warehouse, che è diverso dal feed live del [!DNL Google Analytics] integrazione. Analisi di queste metriche in [!DNL Commerce Intelligence], insieme ad altri dati, migliora lo stato e l’usabilità generali del sito.

## Differenza tra Warehouse GA e integrazione Live

La principale differenza consiste nel fatto che viene memorizzata un’integrazione ([!DNL Google Analytics Warehoused]) e l’altro non è ([!DNL Google Analytics Live]). Nel caso di [!DNL Google Analytics Warehoused], consente la manipolazione del [!DNL Google Analytics] e consente di combinare [!DNL Google Analytics] e altre origini dati per creare rapporti dettagliati.

Osserva [!DNL Google Analytics] campagne pubblicitarie per un esempio di ciò che può essere fatto dal punto di vista della manipolazione. Supponiamo di avere più campagne pubblicitarie per il quarto trimestre con nomi diversi. Le campagne erano il risultato di un’iniziativa di marketing specifica. Con i dati immagazzinati, puoi creare una colonna che trova i nomi delle campagne in questione e restituisce il nome dell’iniziativa del quarto trimestre di `Operation Dumbo`.

L&#39;aspetto combinato consente [!DNL Google Analytics] dati da unire ad altri dati per effettuare analisi. Ad esempio, prendi `Total Time On Site By Ad Campaign` dati da [!DNL Google Analytics] e unisciti a loro contro `Total Spent Per Campaign` dati da [!DNL Facebook Ads] per avere un quadro completo dei costi del coinvolgimento.

Con il [!DNL Google Analytics Live] integrazione, dall&#39;altro, ogni [!DNL Google Analytics] il grafico è simile a un piccolo silo non memorizzato nella Data Warehouse.

## Connessione [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] è un `Premium` Integrazione. [Contatta l’assistenza](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) se hai interesse ad aggiungere questa integrazione all’abbonamento.

1. Vai a `Connections` pagina in **[!UICONTROL Admin** > **Integrations]**.
1. Clic **[!UICONTROL Add an Integration]**, situato sul lato destro.
1. Fai clic su [!DNL Google Analytics Warehoused] icona. Verrà aperto il [!DNL Google Analytics] pagina delle credenziali.
1. Immetti il [!DNL Google Analytics] credenziali. Al termine del processo di autorizzazione, verrai reindirizzato nuovamente a [!DNL Commerce Intelligence].
1. Viene visualizzato un elenco di ID profilo. Controlla i profili a cui desideri connetterti [!DNL Commerce Intelligence]. Se disponi di più profili e hai bisogno di aiuto per identificare quale sia, consulta Connessione multipla [!DNL Google Analytics] nella sezione dei profili.

## Collegamento di più [!DNL Google Analytics] profili

È possibile che più siti Web siano connessi a un unico [!DNL Google Analytics] account, identificato dal proprio [!DNL Google Analytics] ID profilo. In questo caso, puoi includere tutti gli ID profilo in [!DNL Commerce Intelligence]. Controlla gli ID profilo da includere durante il passaggio di selezione del profilo.

Per identificare i [!DNL Google Analytics] ID profilo:

1. Accedi a [!DNL Google Analytics]
1. Vai a quello del sito Web [!DNL Google Analytics] dashboard
1. Controlla l’URL: l’ID profilo corrisponde agli otto numeri seguenti `p` alla fine della riga

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Disconnessione [!DNL Google Analytics Warehoused] da [!DNL Commerce Intelligence] {#disconnect}

1. Visita il [!DNL Google Analytics] [impostazioni account](https://myaccount.google.com/intro) pagina.
1. Sotto `Security` e fai clic su **[!UICONTROL edit]** accanto a `Authorizing` applicazioni e siti.
1. Clic **[!UICONTROL revoke access]** accanto a [!DNL Commerce Intelligence].

## Documentazione correlata

* [Reautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Connessione [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Analisi delle attività del sito web e dei tassi di conversione dei clienti](../../analysis/web-act-cust-conversion.md)
* [Tracciare i dati di acquisizione dell&#39;utente tramite [!DNL Google Analytics] cookie](../../analysis/google-track-user-acq.md)
