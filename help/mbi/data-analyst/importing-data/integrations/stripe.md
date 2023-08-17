---
title: Connetti Stripe
description: Scopri come gestire e tenere traccia dei dati di pagamento e delle fatture aziendali.
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 1%

---

# Connetti [!DNL Stripe]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![](../../../assets/stripe-logo.png)

[!DNL Stripe] consente di gestire e tenere traccia dei dati di pagamento e delle fatture aziendali. Collegamento [!DNL Stripe] account a [!DNL Commerce Intelligence] è un semplice processo in due fasi:

1. [Aggiungi [!DNL Stripe] come origine dati in [!DNL Commerce Intelligence]](#stepone)
1. [Consenti [!DNL Commerce Intelligence] accesso al tuo [!DNL Stripe] Dati](#steptwo)

## Aggiungi [!DNL Stripe] come origine dati {#stepone}

1. Vai a `Connections` pagina in **[!UICONTROL Admin** > **Connections]**.
1. Clic **[!UICONTROL Add a Data Source]**, situato sul lato destro dello schermo sopra la `Data Sources` tabella.
1. Fai clic su [!DNL Stripe] icona. Viene visualizzata la `[!DNL Stripe] authorization` pagina.
1. Clic **[!UICONTROL Connect with Stripe]**.

## Consenti [!DNL Commerce Intelligence] accesso al tuo [!DNL Stripe] dati {#steptwo}

Dopo aver fatto clic su **[!UICONTROL Connect with Stripe]**, viene visualizzata una pagina di richiesta di accesso.

1. Clic **[!UICONTROL Sign in with Stripe to Continue]**.

1. Immetti le credenziali e fai clic su **[!UICONTROL Sign in to your account]**.

1. Le tue credenziali verranno convalidate e verrai indirizzato di nuovo a [!DNL Commerce Intelligence].

1. Se la connessione ha esito positivo, viene visualizzata una *Connessione riuscita* nella parte superiore dello schermo.

## Correlato:

Il [[!DNL Stripe] Documentazione API](https://stripe.com/docs/api) può essere una risorsa utile per saperne di più su come [!DNL Stripe] è integrato con [!DNL Commerce Intelligence].

* [Previsto [!DNL Stripe] dati](../integrations/stripe-data.md)
* [Reautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
