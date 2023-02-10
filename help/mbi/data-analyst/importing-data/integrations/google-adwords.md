---
title: Connetti Adwords Google
description: Scopri come misurare il ROI delle campagne sposando il tuo costo pubblicitario e il valore del ciclo di vita del cliente (CLV) degli utenti acquisiti dalle tue campagne.
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# Connetti [!DNL Google Adwords]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![](../../../assets/Google_Adwords_logo.png)

Avete fatto la vostra ricerca, avete creato i vostri annunci, avete lanciato la vostra campagna. Ora è il momento di analizzare i dati sulla spesa pubblicitaria e vedere se i vostri soldi vengono spesi in modo efficace. Utilizzando i dati di spesa pubblicitaria, puoi [misurare il ROI delle campagne sposando i costi pubblicitari e il valore del ciclo di vita del cliente (CLV)](../../analysis/roi-ad-camp.md) degli utenti acquisiti dalle campagne.

Iniziamo entrando nel nostro [!DNL Google Adwords] credenziali in [!DNL MBI]:

1. Vai alla pagina Connessioni in **Gestisci dati > Integrazioni**.
1. Fai clic su **Aggiungi integrazione**, situata in alto a destra dello schermo.
1. Fai clic sul pulsante **[!DNL Google Adwords]** icona. Verrà aperto il [!DNL Google Adwords] pagina delle credenziali.
1. Inserisci il tuo [!DNL Google Analytics] credenziali. Al termine del processo di autorizzazione, verrai reindirizzato a [!DNL MBI].
1. Verrà visualizzato un elenco di ID profilo. Controlla i profili a cui desideri connetterti [!DNL MBI].

   ![](../../../assets/cnnct-profile.png)

1. Le modifiche vengono salvate automaticamente, quindi fai clic su **[!UICONTROL Back to Connections]** quando hai finito.

Se disponi di più profili e hai bisogno di aiuto per identificare quale sia la `Connecting Multiple Google Analytics profiles` di seguito.

## `Connecting multiple Google Analytics profiles`

È possibile che più siti web siano connessi a un singolo [!DNL Google Analytics] conto, identificato dal proprio [!DNL Google Analytics] ID profilo. In questo caso, avrai la possibilità di includere tutti gli ID profilo in [!DNL MBI]. Controlla gli ID profilo che desideri includere durante il passaggio di selezione del profilo.

**Per identificare l’ID profilo Google Analytics di un particolare sito Web:**

1. Accedi a [!DNL Google Analytics]
1. Vai al sito web particolare [!DNL Google Analytics] dashboard
1. Osserva l’URL : l’ID profilo corrisponde agli 8 numeri seguenti `p` alla fine della riga:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## Disconnessione [!DNL Google Adwords]

1. Visita il tuo [!DNL Google] [impostazioni account](https://www.google.com/accounts/) pagina.
1. Sotto la `Security` e fai clic su **[!UICONTROL edit]** accanto a `Authorizing` applicazioni e siti.
1. Fai clic su **[!UICONTROL revoke access]** accanto a [!DNL MBI].

## Correlati

* [Riautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [Tracciare l’origine di riferimento dell’ordine tramite [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [Tracciare l’origine del riferimento utente nel database](../../analysis/google-track-user-acq.md)
* [Scopri le fonti e i canali di acquisizione più importanti](../../analysis/most-value-source-channel.md)
* [Aumenta il ROI delle campagne pubblicitarie](../../analysis/roi-ad-camp.md)
* [Come funziona [!DNL Google Analytics] L’attribuzione UTM funziona?](../../analysis/utm-attributes.md)
