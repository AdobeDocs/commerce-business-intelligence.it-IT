---
title: Connetti Google eCommerce
description: Scopri i canali di riferimento più importanti.
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/iBVf-dkbm1NbELZUYjLp1TzypO7Cu55tIzd93lQ1zo0
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
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
source-wordcount: 305
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
