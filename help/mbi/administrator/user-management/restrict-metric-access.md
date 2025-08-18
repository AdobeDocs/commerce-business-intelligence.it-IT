---
title: Limitare l’accesso alle metriche
description: Scopri come utilizzare l’accesso alle metriche e le relative restrizioni.
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
role: Admin, User
feature: User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Gestire gli utenti delle metriche

Oltre a impostare i livelli di autorizzazione utente, puoi anche limitare l’accesso alle metriche utente per utente. Ad esempio, se desideri che il tuo reparto contabile abbia accesso alle metriche relative ai ricavi ma non a quelle di acquisizione degli utenti, puoi limitare l’accesso a tali metriche.

In casi simili, Adobe consiglia di impostare l&#39;account dell&#39;utente su **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**. Le autorizzazioni **[!UICONTROL Standard]** devono essere assegnate agli utenti che non hanno bisogno di creare o modificare metriche, colonne calcolate, integrazioni o utenti, ma che hanno bisogno dell&#39;accesso ai dati in Data Warehouse. Se si desidera limitare completamente l&#39;accesso ai dati, utilizzare le autorizzazioni **[!UICONTROL Read Only]**.

Dopo aver impostato il livello di autorizzazione, è possibile selezionare le metriche a cui un utente **[!UICONTROL Standard]** può accedere eseguendo le operazioni seguenti:

1. Vai a **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**.
1. Seleziona l’account utente desiderato.
1. Nella scheda **[!UICONTROL Metrics]** viene visualizzato un elenco delle metriche disponibili. Controlla le metriche a cui desideri che l’utente abbia accesso e deseleziona quelle a cui l’utente non deve avere accesso.
1. [!DNL Adobe Commerce Intelligence] salva le modifiche automaticamente. Se la modifica ha esito positivo, [!DNL Commerce Intelligence] visualizza **[!UICONTROL Saved!]** nella parte superiore della pagina.

>[!NOTE]
>
>Tutti gli utenti con autorizzazioni **[!UICONTROL Standard]** possono accedere a tutti i dati in Data Warehouse tramite Esportazione dati, oltre a tutte le metriche di [!DNL Google Analytics].

È inoltre possibile limitare l&#39;accesso a una metrica modificando la metrica e **[!UICONTROL Standard]** selezionando gli utenti nella sezione **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)**.

>[!NOTE]
>
>Se si duplica una metrica, [!DNL Commerce Intelligence] copia le autorizzazioni utente impostate nella metrica originale.
