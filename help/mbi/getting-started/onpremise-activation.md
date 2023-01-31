---
title: Attivazione della [!DNL MBI] Account per sottoscrizioni on-premise
description: Scopri come attivare la [!DNL MBI] account per sottoscrizioni on-premise.
exl-id: 0efac7b4-2457-48c7-947a-d2776b90a1dd
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# Attiva il tuo [!DNL MBI] Account per sottoscrizioni on-premise

Per attivare [!DNL MBI] per gli abbonamenti on-premise, crea prima un [!DNL MBI] account, quindi collegare [!DNL MBI] nel database Commerce. Per informazioni sull&#39;attivazione in `Cloud Starter` progetti, vedi [Attivazione della [!DNL MBI] Account per `Cloud Starter` Abbonamenti](../getting-started/cloud-activation.md).

1. Crea il tuo [!DNL MBI] Conto.

   - Vai a [https://account.magento.com/customer/account/login](https://account.magento.com/customer/account/login)

   - Vai a **[!UICONTROL My Account** > **My [!DNL MBI] Instances]**.

   - Fai clic su **[!UICONTROL Create Instance]**. Se non trovi questo pulsante, contatta il tuo Customer Success Manager o Customer Technical Advisor.

   - Immetti le informazioni per creare il tuo account.

   ![](../assets/create-account-2.png)

   - Vai alla tua casella in entrata e verifica il tuo indirizzo e-mail. Se non hai ricevuto un&#39;e-mail, [contattare il supporto](../guide-overview.md).

   - Crea la tua password.

   ![](../assets/create-account-4.png)

   - Dopo aver creato il tuo account, puoi aggiungere gli utenti al tuo nuovo account. È ora possibile aggiungere gli amministratori tecnici per eseguire le seguenti operazioni.

   ![](../assets/create-account-5.png)

1. Immetti le informazioni sul tuo negozio per impostare le tue preferenze.

   ![](../assets/create-account-6.png)

1. Connetti [!DNL MBI] al database Commerce tramite una connessione crittografata.

   Commerce consiglia vivamente di connettersi utilizzando un [`SSH tunnel`](../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md). Tuttavia, se questa non è un&#39;opzione, puoi comunque collegare [!DNL MBI] al database utilizzando un [`direct connection`](../data-analyst/importing-data/integrations/mysql-via-a-direct-connection.md).

1. Dopo la connessione [!DNL MBI] al database Commerce, contatta il tuo Customer Success Manager per coordinare i passaggi successivi, ad esempio la configurazione di integrazioni e altri passaggi di configurazione.

1. Al termine della configurazione, puoi [accedere](../getting-started/sign-in.md) al tuo [!DNL MBI] conto.
