---
title: Connetti Stripe
description: Scopri come gestire e tenere traccia dei dati di pagamento e delle fatture aziendali.
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '151'
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
* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=it)
