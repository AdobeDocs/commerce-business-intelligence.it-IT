---
title: Limitare l’accesso alle metriche
description: Scopri come utilizzare l’accesso alle metriche e le relative restrizioni.
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Gestire gli utenti delle metriche

Oltre a impostare i livelli di autorizzazione utente, puoi anche limitare l’accesso alle metriche utente per utente. Ad esempio, se desideri che il tuo reparto contabile abbia accesso alle metriche relative ai ricavi ma non a quelle di acquisizione degli utenti, puoi limitare l’accesso a tali metriche.

In casi come questi, l’Adobe consiglia di impostare l’account dell’utente su **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**. **[!UICONTROL Standard]** Le autorizzazioni devono essere concesse agli utenti che non hanno bisogno di creare o modificare metriche, colonne calcolate, integrazioni o utenti, ma che hanno bisogno dell’accesso ai dati nella Data Warehouse. Se desideri limitare completamente l’accesso ai dati, utilizza **[!UICONTROL Read Only]** autorizzazioni.

Dopo aver impostato il livello di autorizzazione, puoi selezionare le metriche a **[!UICONTROL Standard]** L’utente può accedere a eseguendo le seguenti operazioni:

1. Vai a **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**.
1. Seleziona l’account utente desiderato.
1. Il **[!UICONTROL Metrics]** Questa scheda mostra un elenco delle metriche disponibili. Controlla le metriche a cui desideri che l’utente abbia accesso e deseleziona quelle a cui l’utente non deve avere accesso.
1. [!DNL MBI] salva le modifiche automaticamente. Se la modifica ha esito positivo, [!DNL MBI] display **[!UICONTROL Saved!]** nella parte superiore della pagina.

>[!NOTE]
>
>Tutti gli utenti con **[!UICONTROL Standard]** Le autorizzazioni di possono accedere a tutti i dati nella Data Warehouse tramite Esportazione dati, oltre a tutte le metriche di [!DNL Google Analytics].

Puoi anche limitare l’accesso a una metrica modificando la metrica e **[!UICONTROL Standard]** selezione degli utenti in **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)** sezione.

>[!NOTE]
>
>Se duplichi una metrica, [!DNL MBI] copia le autorizzazioni utente impostate nella metrica originale.
