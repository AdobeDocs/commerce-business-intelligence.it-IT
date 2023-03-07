---
title: Connetti Google eCommerce
description: Scopri i canali di riferimento più importanti.
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
source-git-commit: 8de036e2717aedef95a8bb908898fd9b9bc9c3fa
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# Connetti [!DNL Google ECommerce]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![](../../../assets/google-ecommerce-logo.png)

Il flusso del traffico e degli ordini è costante, il che significa che puoi raggiungere e acquisire in modo efficace i clienti. Ma quali sono i canali di riferimento più importanti? Qual è il valore medio del ciclo di vita dei clienti acquisiti da un&#39;origine rispetto a un&#39;altra? Collegando i dati di origine per il riferimento dell’ordine da [!DNL Google ECommerce] a [!DNL MBI], puoi creare analisi che ti aiutino a identificare [canali di marketing più importanti](../../../data-analyst/analysis/most-value-source-channel.md).

Per iniziare, immetti il [!DNL Google ECommerce] credenziali in [!DNL MBI]:

1. Vai a `Connections` pagina in **[!UICONTROL Admin** > **Connections]**.
1. Clic **[!UICONTROL Add a New Source]**, situato sul lato destro dello schermo sopra la `Data Sources` tabella.
1. Fai clic su [!DNL Google ECommerce] icona. Verrà aperto il [!DNL Google ECommerce] pagina delle credenziali.
1. Immetti il [!DNL Google Analytics] credenziali. Al termine del processo di autorizzazione, verrai reindirizzato nuovamente a [!DNL MBI].
1. Viene visualizzato un elenco di ID profilo. Controlla i profili a cui desideri connetterti [!DNL MBI].

   Se disponi di più profili e hai bisogno di aiuto per identificare quale sia, consulta **Connessione multipla [!DNL Google Analytics] nella sezione dei profili.

   ![](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. Le modifiche vengono salvate automaticamente, quindi fai clic su **[!UICONTROL Back to Connections]** quando hai finito.

## Collegamento di più [!DNL Google Analytics] profili da [!DNL MBI]

È possibile che più siti Web siano connessi a un unico [!DNL Google Analytics] account, identificato dal proprio [!DNL Google Analytics] ID profilo. In questo caso, puoi includere tutti gli ID profilo in [!DNL MBI]. Controlla gli ID profilo da includere durante il passaggio di selezione del profilo.

Per identificare i [!DNL Google Analytics] ID profilo:

1. Accedi a [!DNL Google Analytics]
1. Vai a quello del sito Web [!DNL Google Analytics] dashboard
1. Controlla l’URL: l’ID profilo corrisponde agli otto numeri seguenti `p` alla fine della riga

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Disconnessione [!DNL Google ECommerce] da [!DNL MBI] {#disconnect}

1. Visita il [!DNL Google Analytics] [impostazioni account](https://www.google.com/account/about/?hl=en) pagina.
1. Sotto `Security` , fare clic su **[!UICONTROL edit]** accanto a `Authorizing` applicazioni e siti.
1. Clic **[!UICONTROL revoke access]** accanto a [!DNL MBI].

## Correlato:

* [Previsto [!DNL Google ECommerce] dati](../integrations/google-ecommerce-data.md)
* [Reautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [Configurazione [!DNL Google ECommerce] tracciamento](https://support.google.com/analytics/answer/1009612?hl=en)
* [Scopri le fonti e i canali di acquisizione più importanti](../../analysis/most-value-source-channel.md)
* [Aumentare il ROI nelle campagne pubblicitarie](../../analysis/roi-ad-camp.md)
