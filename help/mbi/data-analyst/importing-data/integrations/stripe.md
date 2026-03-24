---
title: Connetti Stripe
description: Scopri come gestire e tenere traccia dei dati di pagamento e delle fatture aziendali.
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/S6-otAlCeS8aKQ6K-xZH2ZaqEjZ-ZZ6fMWXtFFafu6c
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 151
ht-degree: 0%

---

# Connetti [!DNL Stripe]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![Logo Stripe](../../../assets/stripe-logo.png)

[!DNL Stripe] ti consente di gestire e tenere traccia dei dati di pagamento e fattura della tua azienda. La connessione dell&#39;account [!DNL Stripe] a [!DNL Commerce Intelligence] è un semplice processo in due fasi:

1. [Aggiungi [!DNL Stripe] come origine dati in [!DNL Commerce Intelligence]](#stepone)
1. [Consenti [!DNL Commerce Intelligence] accesso ai tuoi [!DNL Stripe] dati](#steptwo)

## Aggiungi [!DNL Stripe] come origine dati {#stepone}

1. Passare alla pagina `Connections` in **[!UICONTROL Admin** > **Connections]**.
1. Fare clic su **[!UICONTROL Add a Data Source]**, che si trova sul lato destro della schermata sopra la tabella `Data Sources`.
1. Fare clic sull&#39;icona [!DNL Stripe]. Verrà visualizzata la pagina `[!DNL Stripe] authorization`.
1. Fare clic su **[!UICONTROL Connect with Stripe]**.

## Consenti a [!DNL Commerce Intelligence] l&#39;accesso ai tuoi dati di [!DNL Stripe] {#steptwo}

Dopo aver fatto clic su **[!UICONTROL Connect with Stripe]**, viene visualizzata una pagina di richiesta di accesso.

1. Fare clic su **[!UICONTROL Sign in with Stripe to Continue]**.

1. Immettere le credenziali e fare clic su **[!UICONTROL Sign in to your account]**.

1. Le credenziali verranno convalidate e verrà eseguito il reindirizzamento a [!DNL Commerce Intelligence].

1. Se la connessione ha esito positivo, *Connessione riuscita.Il messaggio* viene visualizzato nella parte superiore dello schermo.

## Correlato:

La [[!DNL Stripe] documentazione API](https://stripe.com/docs/api) può essere una risorsa utile per ulteriori informazioni sull&#39;integrazione di [!DNL Stripe] con [!DNL Commerce Intelligence].

* [Previsti [!DNL Stripe] dati](../integrations/stripe-data.md)
* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
