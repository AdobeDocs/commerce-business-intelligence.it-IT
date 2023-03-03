---
title: Attivazione del [!DNL MBI] Account per sottoscrizioni on-premise
description: Scopri come attivare [!DNL MBI] account per le sottoscrizioni locali.
exl-id: 0efac7b4-2457-48c7-947a-d2776b90a1dd
source-git-commit: 6f018ab220f2ae573cbc9016f9efb83c27a254be
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# Attiva [!DNL MBI] Account per sottoscrizioni on-premise

Per attivare [!DNL MBI] per gli abbonamenti on-premise, crea innanzitutto un [!DNL MBI] account, quindi connetti [!DNL MBI] nel database di Commerce. Per informazioni sull&#39;attivazione in `Cloud Starter` progetti, consulta [Attivazione del [!DNL MBI] Account per `Cloud Starter` Iscrizioni](../getting-started/cloud-activation.md).

1. Crea [!DNL MBI] Account.

   - Vai al tuo [Accesso all’account Adobe Commerce](https://account.magento.com/customer/account/login)

   - Vai a **[!UICONTROL My Account** > **My [!DNL MBI] Instances]**.

   - Clic **[!UICONTROL Create Instance]**. Se non trovi questo pulsante, contatta il team dell’account di Adobe o il consulente tecnico del cliente.

   - Immetti le informazioni per creare l&#39;account.

   ![](../assets/create-account-2.png)

   - Vai alla tua casella in entrata e verifica il tuo indirizzo e-mail. Se non hai ricevuto un’e-mail, [contatta l’assistenza](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

   - Crea la password.

   ![](../assets/create-account-4.png)

   - Dopo aver creato l’account, puoi aggiungere utenti al nuovo account. È ora possibile aggiungere gli amministratori tecnici per eseguire i seguenti passaggi.

   ![](../assets/create-account-5.png)

1. Immetti le informazioni relative al tuo Negozio per impostare le preferenze.

   ![](../assets/create-account-6.png)

1. Connetti [!DNL MBI] al database di Commerce utilizzando una connessione crittografata.

   Commerce consiglia vivamente di connettersi utilizzando un [`SSH tunnel`](../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md). Tuttavia, se questa non è un’opzione, puoi comunque collegare [!DNL MBI] al database utilizzando una [`direct connection`](../data-analyst/importing-data/integrations/mysql-via-a-direct-connection.md).

1. Dopo aver effettuato correttamente la connessione [!DNL MBI] nel database Commerce, contatta il team dell’account Adobe per coordinare i passaggi successivi, ad esempio la configurazione delle integrazioni e altri passaggi di configurazione.

1. Al termine della configurazione, puoi [accedi](../getting-started/sign-in.md) al tuo [!DNL MBI] account.
