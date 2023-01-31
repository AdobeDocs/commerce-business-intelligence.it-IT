---
title: Dashboard
description: Scopri come creare e utilizzare un dashboard.
exl-id: a872344b-ac66-41eb-a471-5a69f8802527
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---

# Dashboard

[!DNL MBI] Le dashboard ti offrono una panoramica rapida delle prestazioni e delle attività di vendita del tuo negozio. Le singole dashboard possono essere condivise con altri utenti e organizzate in gruppi logici. Puoi anche impostare diversi livelli di autorizzazione per altri utenti.

È facile creare un nuovo rapporto, aggiungerlo a un dashboard ed esportare i dati in Excel. I grafici e i rapporti possono essere ridimensionati e trascinati in posizione sul dashboard.

![Dashboard](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## Creazione di dashboard {#createdash}

Le dashboard sono essenzialmente bucket a tema condivisibili per le analisi create nei Report Builder. Questo è il modo in cui puoi incoraggiare il tuo team a collaborare e mantenere un&#39;unica fonte di verità in tutta la tua organizzazione.

*Se sei un amministratore o un utente Standard*, puoi creare un dashboard facendo clic sul pulsante `Dashboard Options` menu a discesa e scelta `Create New dashboard`.

L’aspetto delle dashboard create dipende interamente dall’utente. Puoi disporre e ridimensionare gli elementi nel dashboard in base alle tue esigenze e al flusso di lavoro.

![disporre l&#39;elemento del dashboard di ridimensionamento](../../assets/arrange_resize_dashboard_element.gif)

### Crea un nuovo dashboard

1. Scegliere **[!UICONTROL Dashboards]**.

1. Il nome del dashboard predefinito viene visualizzato nell&#39;angolo superiore sinistro dell&#39;intestazione del dashboard. Fai clic sulla freccia giù (![](../../assets/magento-bi-btn-down.png)) per visualizzare le opzioni disponibili.

   ![Crea dashboard](../../assets/magento-bi-dashboard-create.png)

1. Fai clic su **[!UICONTROL Create Dashboard]**. Quindi, procedi come segue:

   * Inserisci un `Name` per il dashboard.

   * Per creare una nuova `Group` per il dashboard, immetti il nome del gruppo.

      Ad esempio, se l’installazione Commerce dispone di più viste Store, puoi creare un gruppo per ogni visualizzazione Store.

   * Fai clic su **[!UICONTROL Create]**.

   ![nome del dashboard](../../assets/magento-bi-dashboard-create-name.png)

   * Il nome del nuovo dashboard viene visualizzato nell&#39;angolo in alto a sinistra. Fai clic sulla freccia giù (![](../../assets/magento-bi-btn-down.png)) per visualizzare le opzioni. Se hai creato un gruppo, il nuovo dashboard viene visualizzato sotto il gruppo nell’elenco.


### Aggiungere un rapporto

1. Per aggiungere un rapporto, effettuare una delle seguenti operazioni:

   * Fai clic sul pulsante **[!UICONTROL Add a report]** nella pagina.

   * Nell’intestazione del dashboard, fai clic su **[!UICONTROL Add Report]**.

      ![Aggiungi rapporto](../../assets/magento-bi-dashboard-create-add-report.png)

1. Fai clic su **[!UICONTROL Create Report]** per mostrare **[!UICONTROL Report Builder Options]**.

   ![Opzioni Report Builder](../../assets/magento-bi-report-builder.png)

## Disporre gli elementi su un dashboard

* Per ridimensionare un grafico o un rapporto, trascinare l&#39;angolo inferiore destro sulla nuova dimensione.

* Per spostare un grafico o un rapporto, passa il cursore sul titolo o sull’intestazione fino a quando il cursore non assume la forma di una croce. Quindi, trascinalo in posizione.

## Gestione delle dashboard {#managedash}

In **[!DNL Manage Data** > **Dashboards]**, puoi gestire le autorizzazioni utente per le dashboard di tua proprietà, eliminare le dashboard di cui non hai più bisogno e impostare un dashboard predefinito.

### Condivisione delle dashboard {#sharingdash}

Scalabilità reale [!DNL MBI] in tutta l’organizzazione e per ottenere informazioni utili, ti invitiamo a condividere le dashboard create con altri membri del team. *Puoi condividere le dashboard di tua proprietà* facendo clic sul pulsante `Share Dashboard` nella parte superiore della pagina.

Quando condividi un dashboard, puoi assegnare autorizzazioni in tutta l’organizzazione OPPURE su base individuale, ovvero decidere chi può visualizzare e modificare i rapporti.

>[!NOTE]
>
>`Read-Only` gli utenti possono accedere solo alle dashboard che sono direttamente condivise con loro; non possono cercare e aggiungere dashboard da soli. Non dimenticate di tenerli in loop!

### Accesso alle dashboard condivise {#accessshared}

*Se sei un utente amministratore o Standard* e desideri aggiungere un dashboard condiviso al tuo account, fai clic su **[!UICONTROL Dashboard Options]** e quindi facendo clic su **[!UICONTROL Find]** nel menu a discesa .

![trova dashboard](../../assets/find_dashboard.png)<!--{: width="1000" height="535"}-->

### Gestione delle impostazioni del dashboard

1. Scegliere **[!DNL Manage Data** > **Dashboards]**.

1. Se applicabile, immetti un nuovo `Dashboard Name`.

1. Per assegnare il dashboard a uno specifico `Dashboard Group`, scegli dall’elenco dei gruppi.

   **`Permissions`**

   Per assegnare a tutti gli utenti lo stesso livello di accesso al dashboard, procedi come segue:

   1. Sotto **`Shared with`**, scegli una delle seguenti opzioni:

      * `View`
      * `Edit`
      * `None`
   1. Quando viene richiesto di confermare, fai clic su **[!UICONTROL OK]** per aggiornare il livello di autorizzazioni per ogni utente.

   1. Per modificare il livello di autorizzazione di un individuo, individua l’utente nell’elenco che modifica il livello di autorizzazione. La modifica viene salvata automaticamente.

   **`Default`**

   1. Per impostare questa dashboard come predefinita [!DNL MBI] account, fai clic su **[!UICONTROL Make Default]**.

   **`Remove`**

   1. Per rimuovere il dashboard, fai clic su **[!UICONTROL Delete Dashboard]**.
