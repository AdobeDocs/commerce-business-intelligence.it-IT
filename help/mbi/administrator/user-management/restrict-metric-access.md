---
title: Limitare l’accesso alle metriche
description: Scopri come utilizzare l’accesso alle metriche e le restrizioni.
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Gestione degli utenti delle metriche

Oltre a impostare i livelli di autorizzazione utente, puoi anche limitare l’accesso alle metriche a seconda dell’utente. Ad esempio, se desideri che il reparto contabilità abbia accesso alle metriche relative ai ricavi ma non alle metriche di acquisizione degli utenti, puoi limitare l&#39;accesso a tali metriche.

In casi come questi, consigliamo di impostare l’account dell’utente su **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**. **[!UICONTROL Standard]** devono essere concesse autorizzazioni agli utenti che non hanno bisogno di creare o modificare metriche, colonne calcolate, integrazioni o utenti, ma che hanno bisogno di accedere ai dati nella Data Warehouse. Se desideri limitare completamente l’accesso ai dati, utilizza il **[!UICONTROL Read Only]** autorizzazioni.

Dopo aver impostato il livello di autorizzazione, puoi selezionare le metriche a **[!UICONTROL Standard]** l&#39;utente può accedere eseguendo le operazioni seguenti:

1. Vai a **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**.
1. Seleziona l’account utente desiderato.
1. La **[!UICONTROL Metrics]** visualizza un elenco delle metriche disponibili. Controlla le metriche a cui desideri che l’utente abbia accesso; deseleziona i dati a cui l’utente non deve avere accesso.
1. [!DNL MBI] salva automaticamente le modifiche. Se la modifica ha esito positivo, [!DNL MBI] display **[!UICONTROL Saved!]** nella parte superiore della pagina.

>[!NOTE]
>
>Tutti gli utenti con **[!UICONTROL Standard]** le autorizzazioni possono accedere a tutti i dati del data warehouse tramite Esportazione dati, oltre a tutte le metriche da [!DNL Google Analytics].

Puoi anche limitare l’accesso a una metrica modificando la metrica e **[!UICONTROL Standard]** selezione degli utenti nella **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)** sezione .

>[!NOTE]
>
>Se duplichi una metrica, [!DNL MBI] copia le autorizzazioni utente impostate nella metrica originale.
