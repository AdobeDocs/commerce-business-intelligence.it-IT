---
title: Connetti Google Analytics warehouse
description: Scopri come i visitatori utilizzano il tuo sito, quali contenuti sono attraenti, dove i visitatori escono e altro ancora.
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---

# Connetti [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] è il servizio di analisi web più utilizzato su Internet. Implementazione [!DNL Google Analytics] nel sito web puoi monitorare come i visitatori utilizzano il tuo sito, quale contenuto è attraente, dove i visitatori escono e altro ancora. [!DNL Google Analytics Warehoused] è un’integrazione separata dal [!DNL Google Analytics] integrazione. Consentirà una migliore analisi grazie alla [!DNL Google Analytics] i dati presenti nella Data Warehouse, diversi dal feed live dell’esistente [!DNL Google Analytics] integrazione. Analisi di queste metriche in [!DNL MBI], insieme ad altri dati, migliorerà la salute e l&#39;usabilità complessive del tuo sito.

## Differenza tra GA Warehouse e Live Integration

Il principale fattore di differenziazione consiste nell&#39;archiviazione di un&#39;integrazione ([!DNL Google Analytics Warehoused]) e l&#39;altro non è ([!DNL Google Analytics Live]). Nel caso di [!DNL Google Analytics Warehoused], questo consente la manipolazione del [!DNL Google Analytics] e consente di combinare [!DNL Google Analytics] e altre origini dati per creare rapporti approfonditi.

Diamo un&#39;occhiata [!DNL Google Analytics] campagne pubblicitarie per un esempio di ciò che può essere fatto da un punto di vista di manipolazione. Supponiamo di avere più campagne pubblicitarie per Q4 con nomi diversi. Le campagne sono il risultato di una specifica iniziativa di marketing. Con i dati memorizzati, possiamo creare una nuova colonna che trovi i nomi delle campagne in questione e restituisca il nome dell&#39;iniziativa Q4 di `Operation Dumbo`.

L&#39;aspetto combinato consente [!DNL Google Analytics] dati da unire ad altri dati per effettuare analisi. Ad esempio, `Total Time On Site By Ad Campaign` dati da [!DNL Google Analytics] e unisciti `Total Spent Per Campaign` dati da [!DNL Facebook Ads] per avere un quadro completo di quanto impegno vi sta costando.

Con la [!DNL Google Analytics Live] l&#39;integrazione, d&#39;altra parte, [!DNL Google Analytics] grafico è come un piccolo silo che non è memorizzato nel tuo [!DNL MBI] data warehouse.

## Collegamento [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] è un `Premium` Integrazione. [Contatta il supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) se hai interesse ad aggiungere questa integrazione alla tua sottoscrizione.

1. Vai a `Connections` pagina sotto **[!UICONTROL Admin** > **Integrations]**.
1. Fai clic su **[!UICONTROL Add a Add Integration]**, situato sul lato destro dello schermo.
1. Fai clic sul pulsante [!DNL Google Analytics Warehoused] icona. Verrà aperto il [!DNL Google Analytics] pagina delle credenziali.
1. Inserisci il tuo [!DNL Google Analytics] credenziali. Al termine del processo di autorizzazione, verrai reindirizzato a [!DNL MBI].
1. Verrà visualizzato un elenco di ID profilo. Controlla i profili a cui desideri connetterti [!DNL MBI]. Se disponi di più profili e hai bisogno di aiuto per identificare quale di questi è, consulta Collegamento multiplo [!DNL Google Analytics] di seguito la sezione dei profili.

## Collegamento di più [!DNL Google Analytics] profiles

È possibile che più siti web siano connessi a un singolo [!DNL Google Analytics] conto, identificato dal proprio [!DNL Google Analytics] ID profilo. In questo caso, avrai la possibilità di includere tutti gli ID profilo in [!DNL MBI]. Controlla gli ID profilo che desideri includere durante il passaggio di selezione del profilo.

Per identificare un particolare sito web [!DNL Google Analytics] ID profilo:

1. Accedi a [!DNL Google Analytics]
1. Vai al sito web particolare [!DNL Google Analytics] dashboard
1. Osserva l’URL : l’ID profilo corrisponde agli 8 numeri seguenti `p` alla fine della linea

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Disconnessione [!DNL Google Analytics Warehoused] da [!DNL MBI] {#disconnect}

1. Visita il tuo [!DNL Google Analytics] [impostazioni account](https://www.google.com/accounts/) pagina.
1. Sotto la `Security` e fai clic su **[!UICONTROL edit]** accanto a `Authorizing` applicazioni e siti.
1. Fai clic su **[!UICONTROL revoke access]** accanto a [!DNL MBI].

## Documentazione correlata

* [Riautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [Collegamento [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Analisi dell’attività del sito web e dei tassi di conversione dei clienti](../../analysis/web-act-cust-conversion.md)
* [Tracciare i dati di acquisizione degli utenti utilizzando [!DNL Google Analytics] cookie](../../analysis/google-track-user-acq.md)
