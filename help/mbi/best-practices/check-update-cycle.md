---
title: Controllo dello stato del ciclo di aggiornamento
description: Scopri come controllare lo stato del ciclo di aggiornamento.
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# Stato del ciclo di aggiornamento

Quando si accede al [!DNL MBI] dashboard, esistono diversi modi per controllare lo stato dell&#39;ultimo ciclo di aggiornamento. Dipende tutto dal tipo di [autorizzazioni utente](../administrator/user-management/user-management.md) lo hai fatto.

## Perché dovrei controllare lo stato del ciclo di aggiornamento?

Il controllo del ciclo di aggiornamento dello stato è utile quando si controllano i dati nel [!DNL MBI] conto. Se vedi [risultati che non soddisfano le tue aspettative](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md)ad esempio le vendite giornaliere in [!DNL MBI] non corrispondono a ciò che visualizzi nella tua piattaforma di e-commerce o nel tuo [[!DNL Google] Entrate e-commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=en) puoi controllare l’ultimo punto dati per vedere se il problema verrà risolto al termine di un aggiornamento.

## [!UICONTROL Read-Only] e [!UICONTROL Standard]** Utenti

`Read-only` gli utenti possono accedere al proprio dashboard e vedere quanto di recente i dati sono stati aggiornati passando il cursore sull’icona in alto a destra della pagina. Viene visualizzato quando è stato estratto l’ultimo punto dati.

![](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin] Utenti

`Admin` gli utenti possono accedere al dashboard e visualizzare l’ultimo punto dati di cui sopra, insieme a una breve icona di stato delle loro integrazioni account.

Per maggiori dettagli, gli utenti amministratori possono fare clic su **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**.

![](../../mbi/assets/detail-manage-data-integrations.png)

In questa pagina vengono visualizzati lo stato corrente dell’aggiornamento e l’ora dell’ultimo aggiornamento completato.

Se è in corso un aggiornamento, al termine dell’aggiornamento verrà visualizzato un collegamento per richiedere una notifica e-mail.

Se un aggiornamento non è in corso, viene visualizzato un collegamento per avviare un aggiornamento.

>[!NOTE]
>
>Se si dispone di ore di sospensione attività (tempo in cui non si desidera [!DNL MBI] per aggiornare i dati) impostati, forzare un aggiornamento avvierà un ciclo di aggiornamento che non rispetta le limitazioni di tali ore di blackout.
