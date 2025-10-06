---
title: Connetti Google eCommerce
description: Scopri i canali di riferimento più importanti.
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# Connetti [!DNL Google ECommerce]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![Logo Google eCommerce](../../../assets/google-ecommerce-logo.png)

Il flusso del traffico e degli ordini è costante, il che significa che puoi raggiungere e acquisire in modo efficace i clienti. Ma quali sono i canali di riferimento più importanti? Qual è il valore medio del ciclo di vita dei clienti acquisiti da un&#39;origine rispetto a un&#39;altra? Collegando i dati di origine per la segnalazione degli ordini da [!DNL Google ECommerce] a [!DNL Commerce Intelligence], puoi creare analisi che ti aiutino a identificare i [canali di marketing più importanti](../../../data-analyst/analysis/most-value-source-channel.md).

Inizia immettendo le tue credenziali di [!DNL Google ECommerce] in [!DNL Commerce Intelligence]:

1. Passare alla pagina `Connections` in **[!UICONTROL Admin** > **Connections]**.

1. Fare clic su **[!UICONTROL Add a New Source]**, che si trova sul lato destro della schermata sopra la tabella `Data Sources`.

1. Fare clic sull&#39;icona [!DNL Google ECommerce]. Verrà aperta la pagina delle credenziali [!DNL Google ECommerce].

1. Immetti le tue credenziali di [!DNL Google Analytics]. Al termine del processo di autorizzazione, verrà eseguito il reindirizzamento a [!DNL Commerce Intelligence].

1. Viene visualizzato un elenco di ID profilo. Controllare i profili a cui connettersi [!DNL Commerce Intelligence].

   Se disponi di più profili e hai bisogno di aiuto per identificare quale sia, consulta la sezione seguente **Connessione di più profili [!DNL Google Analytics].

   ![Modulo con opzioni per la connessione di più profili Google Analytics](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. Le modifiche vengono salvate automaticamente, quindi fare clic su **[!UICONTROL Back to Connections]** al termine dell&#39;operazione.

## Connessione di più profili [!DNL Google Analytics] a [!DNL Commerce Intelligence]

È possibile che più siti Web siano connessi a un unico account [!DNL Google Analytics], identificato dal proprio ID profilo [!DNL Google Analytics]. In questo caso, puoi includere tutti gli ID profilo in [!DNL Commerce Intelligence]. Controlla gli ID profilo da includere durante il passaggio di selezione del profilo.

Per identificare l&#39;ID profilo [!DNL Google Analytics] di un particolare sito Web:

1. Accedi a [!DNL Google Analytics].
1. Passare alla dashboard [!DNL Google Analytics] del sito Web specifico.
1. Controlla l&#39;URL: l&#39;ID profilo corrisponde agli otto numeri seguenti `p` alla fine della riga.

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Disconnessione di [!DNL Google ECommerce] da [!DNL Commerce Intelligence] {#disconnect}

1. Visita la pagina delle [!DNL Google Analytics] [impostazioni account](https://www.google.com/account/about/?hl=en).
1. Nella sezione `Security`, fare clic su **[!UICONTROL edit]** accanto a `Authorizing` applicazioni e siti.
1. Fai clic su **[!UICONTROL revoke access]** accanto a [!DNL Commerce Intelligence].

## Correlato:

* [Previsti [!DNL Google ECommerce] dati](../integrations/google-ecommerce-data.md)
* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=it)
* [Configurazione [!DNL Google ECommerce] tracciamento](https://support.google.com/analytics/answer/1009612?hl=en)
* [Scopri le fonti e i canali di acquisizione più importanti](../../analysis/most-value-source-channel.md)
* [Aumentare il ROI nelle campagne pubblicitarie](../../analysis/roi-ad-camp.md)
