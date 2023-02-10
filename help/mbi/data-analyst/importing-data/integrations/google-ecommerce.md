---
title: Connetti Google ECommerce
description: Scopri i tuoi canali di riferimento più importanti.
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Connetti [!DNL Google ECommerce]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![](../../../assets/google-ecommerce-logo.png)

Hai un flusso costante di traffico e ordini, il che significa che stai raggiungendo e acquisendo efficacemente i clienti. Ma quali sono i tuoi canali di riferimento più preziosi? qual è il valore medio del ciclo di vita dei clienti acquisiti da un’origine rispetto a un’altra? Collegando i dati di origine dei riferimenti dell&#39;ordine da [!DNL Google ECommerce] a [!DNL MBI], puoi creare analisi che ti aiuteranno a identificare il tuo [canali di marketing più importanti](../../../data-analyst/analysis/most-value-source-channel.md).

Iniziamo entrando nel nostro [!DNL Google ECommerce] credenziali in [!DNL MBI]:

1. Vai a `Connections` pagina sotto **[!UICONTROL Admin** > **Connections]**.
1. Fai clic su **[!UICONTROL Add a New Source]**, situato sul lato destro dello schermo sopra il `Data Sources` tabella.
1. Fai clic sul pulsante [!DNL Google ECommerce] icona. Verrà aperto il [!DNL Google ECommerce] pagina delle credenziali.
1. Inserisci il tuo [!DNL Google Analytics] credenziali. Al termine del processo di autorizzazione, verrai reindirizzato a [!DNL MBI].
1. Verrà visualizzato un elenco di ID profilo. Controlla i profili a cui desideri connetterti [!DNL MBI].

   Se disponi di più profili e hai bisogno di aiuto per identificare quale di questi è, fai riferimento al **Collegamento di più profili [!DNL Google Analytics] di seguito la sezione dei profili.

   ![](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. Le modifiche vengono salvate automaticamente, quindi fai clic su **[!UICONTROL Back to Connections]** quando hai finito.

## Collegamento di più [!DNL Google Analytics] profili a [!DNL MBI]

È possibile che più siti web siano connessi a un singolo [!DNL Google Analytics] conto, identificato dal proprio [!DNL Google Analytics] ID profilo. In questo caso, avrai la possibilità di includere tutti gli ID profilo in [!DNL MBI]. Controlla gli ID profilo che desideri includere durante il passaggio di selezione del profilo.

Per identificare un particolare sito web [!DNL Google Analytics] ID profilo:

1. Accedi a [!DNL Google Analytics]
1. Vai al sito web particolare [!DNL Google Analytics] dashboard
1. Osserva l’URL : l’ID profilo corrisponde agli 8 numeri seguenti `p` alla fine della linea

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Disconnessione [!DNL Google ECommerce] da [!DNL MBI] {#disconnect}

1. Visita il tuo [!DNL Google Analytics] [impostazioni account](https://www.google.com/accounts/) pagina.
1. Sotto la `Security` sezione, fai clic su **[!UICONTROL edit]** accanto a `Authorizing` applicazioni e siti.
1. Fai clic su **[!UICONTROL revoke access]** accanto a [!DNL MBI].

## Correlati:

* [Previsto [!DNL Google ECommerce] dati](../integrations/google-ecommerce-data.md)
* [Riautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [Configurazione [!DNL Google ECommerce] tracking](https://support.google.com/analytics/answer/1009612?hl=en)
* [Scopri le fonti e i canali di acquisizione più importanti](../../analysis/most-value-source-channel.md)
* [Aumenta il ROI delle campagne pubblicitarie](../../analysis/roi-ad-camp.md)
