---
title: Decluttering dell'account  [!DNL Commerce Intelligence]
description: Scopri come pulire il tuo account  [!DNL Commerce Intelligence] .
exl-id: 5fcdac2d-41ca-4011-b646-a699d9ecc6e4
role: Admin, User
feature: Accounts
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 0%

---

# Pulisci account [!DNL Adobe Commerce Intelligence]

Che tu sia stato con [!DNL Commerce Intelligence] per sei mesi o sei anni, mantenere un account ordinato è fondamentale per ottenere il massimo dalla piattaforma. Nel tempo, è naturale che ci siano utenti, dashboard, rapporti, metriche e colonne che non sono più necessari. Forse hai creato un rapporto per un utilizzo una tantum e te ne sei dimenticato, oppure un utente che ha lasciato la tua azienda non ha mai avuto il suo account disattivato.

Con [nomi standardizzati e chiari per tutti gli elementi](../best-practices/naming-elements.md)) dell&#39;account [!DNL Commerce Intelligence], i passaggi di controllo dell&#39;account riportati di seguito consentono di ridurre il disordine e le analisi non necessarie per gli utenti. Un ulteriore vantaggio include [cicli di aggiornamento potenzialmente più veloci](../best-practices/reduce-update-cycle-time.md).

## Passaggio 1: identificare gli utenti non attivi

Il primo passaggio per la pulizia dell&#39;account consiste nel disattivare gli account degli utenti non attivi, ad esempio le persone che hanno lasciato l&#39;azienda o che non utilizzano più [!DNL Commerce Intelligence] nei loro ruoli correnti.

A questo scopo, fai clic sul nome della tua società nella barra di navigazione in alto a destra, quindi seleziona **[!UICONTROL Manage Users]**. Selezionare quindi l&#39;utente che si desidera disattivare e fare clic su **[!UICONTROL Deactivate User]**.

>[!NOTE]
>
>Per eseguire questa operazione sono necessarie [autorizzazioni amministratore](../administrator/user-management/user-management.md).

>[!WARNING]
>
>La disattivazione di un utente comporta la rimozione di grafici, dashboard e altre risorse create dall’utente. Se desideri mantenere queste risorse, contatta il team di [!DNL Commerce Intelligence] [supporto](../guide-overview.md#Submitting-a-Support-Ticket) prima di disattivare l&#39;utente. Il supporto può essere utile per trasferire queste risorse a un altro utente.

### Riattivare un utente

Per riattivare un utente, è necessario ricreare l&#39;account con lo stesso indirizzo e-mail disattivato e ripristinare l&#39;accesso e i dati di proprietà all&#39;accesso.

## Passaggio 2: eliminare dashboard e rapporti non utilizzati

Il passaggio successivo per il controllo dell’account consiste nell’eliminare eventuali dashboard e rapporti non utilizzati.

>[!NOTE]
>
>Per eseguire questa operazione sono necessarie `Admin` o `Standard` [autorizzazioni utente](../administrator/user-management/user-management.md).

Ogni utente con accesso `Admin` o `Standard` può creare report e dashboard. Per questo motivo, tutti coloro che dispongono di queste autorizzazioni devono seguire i passaggi seguenti per identificare e rimuovere i rapporti non utilizzati.

### Rivedere dashboard e rapporti

Prima di eliminare qualcosa, è necessario rivedere i rapporti e le dashboard per valutare cosa è in uso. Anche se è possibile utilizzare la funzionalità **[!UICONTROL find unused reports]** descritta di seguito, qualsiasi revisione iniziale rende le operazioni di pulizia molto più produttive.

### Eliminazione di dashboard e report

Dopo aver effettuato l’accesso alle dashboard e ai rapporti, puoi iniziare a pulire l’account.

**Per rimuovere un report da un dashboard**

1. Individuare il report che si desidera rimuovere nel dashboard.
1. Seleziona **[!UICONTROL Options]** nell&#39;angolo in alto a destra del report.
1. Fare clic su **[!UICONTROL Remove From Dashboard]**.

**Per eliminare un intero dashboard**

1. Selezionare **[!UICONTROL Manage Data]**, quindi **[!UICONTROL Dashboards**].
1. Fai clic sul dashboard da eliminare.
1. Fare clic su **[!UICONTROL Delete Dashboard]**.

È inoltre possibile selezionare **[!UICONTROL Dashboard Options]**, quindi **[!UICONTROL Delete]** dal dashboard stesso.

![](../../mbi/assets/Delete_from_dashboard.png)

>[!NOTE]
>
>L’eliminazione di una dashboard non comporta l’eliminazione dei rapporti al suo interno, pertanto è necessario compiere un ulteriore passaggio per eliminare i rapporti.

**Per Eliminare I Report Non Utilizzati**

1. Selezionare **[!UICONTROL Manage Data]**, quindi **[!UICONTROL Reports]**.
1. Selezionare la casella **Mostra solo report inutilizzati** sotto l&#39;elenco delle metriche. In questo modo viene creato un elenco di rapporti che non vengono utilizzati in un dashboard o in un riepilogo e-mail.
1. Seleziona i rapporti da eliminare. Puoi selezionare tutto facendo clic sulla casella di controllo sopra l’elenco dei rapporti.
1. Fare clic su **[!UICONTROL Delete Selected]**.

Ecco un’occhiata al processo di eliminazione del rapporto non utilizzato:

![](../../mbi/assets/unused_reports.png)

## Passaggio 3: eliminare le metriche non utilizzate

Dopo aver ripulito l’elenco degli utenti, le dashboard e i rapporti, puoi passare al controllo dell’elenco delle metriche. Questo consente di identificare tutto ciò che potrebbe essere obsoleto - ad esempio, una nuova metrica creata con una definizione diversa - o non in uso.

1. Per generare un elenco di rapporti dipendenti per una metrica, passare a **[!DNL Manage Data]**, quindi selezionare Fare clic su **[!UICONTROL Metrics]**.
1. Fare clic su **[!UICONTROL Edit]** accanto a una metrica.
1. Nella parte inferiore della pagina è presente una sezione denominata **[!UICONTROL Dependent Charts]**. Fai clic sul collegamento per generare un elenco di rapporti dipendenti per questa metrica.
1. Dopo che il sistema ha completato il controllo, [!DNL Commerce Intelligence] visualizza un elenco di dashboard, report e utenti che utilizzano questa metrica.

![](../../mbi/assets/report_dependecies.png)

Se decidi che la metrica non è più necessaria, torna alla pagina **[!UICONTROL Metrics]** facendo clic su **[!UICONTROL Back to Metric List]** per trovare la metrica da eliminare. Fare clic su **[!UICONTROL Delete]**.

## Passaggio 4: valutare le colonne sincronizzate

L’ultimo passaggio consiste nel valutare le colonne attualmente sincronizzate nella Data Warehouse. L’annullamento della sincronizzazione delle colonne può danneggiare l’account e ridurre potenzialmente il tempo di aggiornamento.

Se desideri proseguire, contatta l&#39;assistenza [!DNL Commerce Intelligence] [Support](../guide-overview.md#Submitting-a-Support-Ticket). Il team di supporto può creare un report che include tutte le colonne che non vengono utilizzate in alcun dashboard per alcun utente e che non vengono utilizzate nei riepiloghi e-mail, esclusi i report SQL. Puoi quindi utilizzare questo rapporto come guida per selezionare le colonne da desincronizzare tramite Gestione Date Warehouse.

>[!NOTE]
>
>Puoi sempre iniziare di nuovo a sincronizzare queste colonne in futuro. Se si annulla la sincronizzazione di una colonna, verranno rimossi tutti i dati dalla Data Warehouse. Ciò significa solo che durante il ciclo di aggiornamento questa colonna non viene controllata per la presenza di valori nuovi o aggiornati.

**Per annullare la sincronizzazione di una o più colonne**

1. Vai a **[!DNL Manage Data]**, quindi a **[!UICONTROL Data Warehouse]**.
1. Nell&#39;elenco **[!UICONTROL Synced Tables]** passare alla tabella che contiene la colonna.
1. Selezionare una o più caselle accanto a una o più colonne da desincronizzare.
   >[!NOTE]
   >
   >Impossibile annullare la sincronizzazione di una colonna Chiave primaria senza eliminare l&#39;intera tabella.

1. Fare clic su **[!UICONTROL Remove]** per annullare la sincronizzazione di una o più colonne.

Di seguito viene illustrato l&#39;intero processo:

![](../../mbi/assets/drop_column.png)

## Ritorno a capo

L&#39;account [!DNL Commerce Intelligence] dovrebbe essere più semplice da esplorare per te e il tuo team.
