---
title: Controllo dello stato del ciclo di aggiornamento
description: Scopri come controllare lo stato del ciclo di aggiornamento.
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Avanzamento ciclo di aggiornamento

Quando accedi a [!DNL Adobe Commerce Intelligence] sono disponibili diversi modi per controllare lo stato dell’ultimo ciclo di aggiornamento. Dipende tutto dal tipo di [autorizzazioni utente](../administrator/user-management/user-management.md) che hai.

## Perché devo controllare lo stato del ciclo di aggiornamento?

La verifica del ciclo di aggiornamento dello stato è utile quando si controllano i dati nel [!DNL Commerce Intelligence] account. Se vedi [risultati che non soddisfano le tue aspettative](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md)ad esempio le vendite giornaliere in [!DNL Commerce Intelligence] non corrispondono a ciò che visualizzi nella tua piattaforma di e-commerce o nel tuo [[!DNL Google] ricavi da e-commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html) puoi controllare l’ultimo punto dati per vedere se il problema è risolto al termine di un aggiornamento.

## [!UICONTROL Read-Only] e [!UICONTROL Standard] Utenti

`Read-only` gli utenti possono accedere al proprio dashboard e vedere quanto recentemente i dati sono stati aggiornati passando con il mouse sull’icona in alto a destra della pagina. Questo mostra quando è stato estratto l’ultimo punto dati.

![](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin] Utenti

`Admin` gli utenti possono accedere al dashboard e visualizzare l’ultimo punto dati in alto, insieme a una breve icona di stato delle integrazioni dei propri account.

Per ulteriori dettagli, gli utenti amministratori possono fare clic su **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**.

![](../../mbi/assets/detail-manage-data-integrations.png)

Questa pagina mostra lo stato attuale dell’aggiornamento e l’ora dell’ultimo aggiornamento completato.

Se è in corso un aggiornamento, viene visualizzato un collegamento per richiedere una notifica e-mail al termine dell’aggiornamento.

Se un aggiornamento non è in corso, viene visualizzato un collegamento per forzarne l’avvio.

>[!NOTE]
>
>Se si dispone di ore di sospensione attività (orario non desiderato) [!DNL Commerce Intelligence] per aggiornare i dati) impostata, forzare un aggiornamento avvia un ciclo di aggiornamento che non rispetta le limitazioni di tali ore di sospensione attività.
