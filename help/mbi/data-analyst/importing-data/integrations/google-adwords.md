---
title: Connetti Google Adwords
description: Scopri come misurare il ROI delle campagne sposando i costi pubblicitari e il valore del ciclo di vita del cliente (Customer Lifetime Value, CLV) degli utenti acquisiti dalle campagne.
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# Connetti [!DNL Google Adwords]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![](../../../assets/Google_Adwords_logo.png)

Avete fatto la vostra ricerca, creato i vostri annunci, lanciato il vostro [!DNL Google] campagna. Ora è il momento di analizzare i dati di spesa degli annunci e verificare se i soldi vengono spesi in modo efficace. Utilizzando i dati sulla spesa pubblicitaria, puoi [misurare il ROI delle campagne sposando i costi pubblicitari e il valore del ciclo di vita del cliente (CLV)](../../analysis/roi-ad-camp.md) degli utenti acquisiti dalle campagne.

Per iniziare, immetti il [!DNL Google Adwords] credenziali in [!DNL Commerce Intelligence].

1. Vai a `Connections` pagina in **Gestisci dati > Integrazioni**.
1. Clic **Aggiungi integrazione**, situato nella parte superiore destra dello schermo.
1. Fai clic su **[!DNL Google Adwords]** icona. Verrà aperto il [!DNL Google Adwords] pagina delle credenziali.
1. Immetti il [!DNL Google Analytics] credenziali. Al termine del processo di autorizzazione, verrai reindirizzato nuovamente a [!DNL Commerce Intelligence].
1. Viene visualizzato un elenco di ID profilo. Controlla i profili a cui desideri connetterti [!DNL Commerce Intelligence].

   ![](../../../assets/cnnct-profile.png)

1. Le modifiche vengono salvate automaticamente, quindi fai clic su **[!UICONTROL Back to Connections]** quando hai finito.

Se disponi di più profili e hai bisogno di aiuto per identificare quale sia, fai riferimento alla `Connecting Multiple Google Analytics profiles` sezione successiva.

## Collegamento di più [!DNL Google Analytics] profili

È possibile che più siti Web siano connessi a un unico [!DNL Google Analytics] account, identificato dal proprio [!DNL Google Analytics] ID profilo. In questo caso, puoi includere tutti gli ID profilo in [!DNL Commerce Intelligence]. Controlla gli ID profilo che vuoi includere durante il passaggio di selezione del profilo.

**Per identificare l&#39;ID profilo Google Analytics di un particolare sito Web:**

1. Accedi a [!DNL Google Analytics]
1. Vai a quello del sito Web [!DNL Google Analytics] dashboard
1. Controlla l’URL: l’ID profilo corrisponde agli otto numeri seguenti `p` alla fine della riga:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## Disconnessione [!DNL Google Adwords]

1. Visita il [!DNL Google] [impostazioni account](https://www.google.com/account/about/?hl=en) pagina.
1. Sotto `Security` , fare clic su **[!UICONTROL edit]** accanto a `Authorizing` applicazioni e siti.
1. Clic **[!UICONTROL revoke access]**.

## Correlato

* [Reautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Tracciare l’origine di riferimento dell’ordine tramite [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [Tracciare l&#39;origine di riferimento dell&#39;utente nel database](../../analysis/google-track-user-acq.md)
* [Scopri le fonti e i canali di acquisizione più importanti](../../analysis/most-value-source-channel.md)
* [Aumentare il ROI nelle campagne pubblicitarie](../../analysis/roi-ad-camp.md)
* [In che modo [!DNL Google Analytics] Lavoro di attribuzione UTM?](../../analysis/utm-attributes.md)
