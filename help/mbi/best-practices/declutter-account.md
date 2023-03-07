---
title: Decluttering [!DNL MBI] Account
description: Scopri come pulire [!DNL MBI] account.
exl-id: 5fcdac2d-41ca-4011-b646-a699d9ecc6e4
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 0%

---

# Pulisci [!DNL MBI] Account

Se sei stato con [!DNL MBI] per sei mesi o sei anni, mantenere un account ordinato è fondamentale per ottenere il massimo dalla piattaforma. Nel tempo, è naturale che ci siano utenti, dashboard, rapporti, metriche e colonne che non sono più necessari. Forse hai creato un rapporto per un utilizzo una tantum e te ne sei dimenticato, oppure un utente che ha lasciato la tua azienda non ha mai avuto il suo account disattivato.

Con [denominazione standard e chiara per tutti gli elementi](../best-practices/naming-elements.md)) del tuo [!DNL MBI] account, i passaggi di controllo dell’account riportati di seguito consentono di ridurre l’ingombro e le analisi non necessarie per gli utenti. Un ulteriore vantaggio include [cicli di aggiornamento potenzialmente più rapidi](../best-practices/reduce-update-cycle-time.md).

## Passaggio 1: identificare gli utenti non attivi

Il primo passaggio per la pulizia dell’account consiste nel disattivare gli account degli utenti non attivi, ad esempio le persone che hanno lasciato l’azienda o che non utilizzano più [!DNL MBI] nei ruoli correnti.

Per farlo, fai clic sul nome della tua azienda nell’angolo in alto a destra della barra di navigazione superiore, quindi seleziona **[!UICONTROL Manage Users]**. Quindi, seleziona l’utente da disattivare e fai clic su **[!UICONTROL Deactivate User]**.

>[!NOTE]
>
>Hai bisogno di [Autorizzazioni amministratore](../administrator/user-management/user-management.md) per eseguire questa operazione.

>[!WARNING]
>
>La disattivazione di un utente comporta la rimozione di grafici, dashboard e altre risorse create dall’utente. Se desideri conservare queste risorse, contatta il [!DNL MBI] [supporto](../guide-overview.md) prima di disattivare l&#39;utente. Il supporto può essere utile per trasferire queste risorse a un altro utente.

### Riattivare un utente

Per riattivare un utente, è necessario ricreare l&#39;account con lo stesso indirizzo e-mail disattivato e ripristinare l&#39;accesso e i dati di proprietà all&#39;accesso.

## Passaggio 2: eliminare dashboard e rapporti non utilizzati

Il passaggio successivo per il controllo dell’account consiste nell’eliminare eventuali dashboard e rapporti non utilizzati.

>[!NOTE]
>
>Hai bisogno di `Admin` o `Standard` [autorizzazioni utente](../administrator/user-management/user-management.md) per eseguire questa operazione.

Ogni utente con `Admin` o `Standard` In Access è possibile creare report e dashboard. Per questo motivo, tutti coloro che dispongono di queste autorizzazioni devono seguire i passaggi seguenti per identificare e rimuovere i rapporti non utilizzati.

### Rivedere dashboard e rapporti

Prima di eliminare qualcosa, è necessario rivedere i rapporti e le dashboard per valutare ciò che è in uso. Mentre è possibile utilizzare il **[!UICONTROL find unused reports]** di seguito, qualsiasi revisione iniziale rende le attività di pulizia molto più produttive.

### Eliminazione di dashboard e report

Dopo aver effettuato l’accesso alle dashboard e ai rapporti, puoi iniziare a pulire l’account.

**Per rimuovere un report da un dashboard**

1. Individuare il report che si desidera rimuovere nel dashboard.
1. Seleziona **[!UICONTROL Options]** nell’angolo in alto a destra del rapporto.
1. Clic **[!UICONTROL Remove From Dashboard]**.

**Per eliminare un intero dashboard**

1. Seleziona **[!UICONTROL Manage Data]**, quindi **[!UICONTROL Dashboards**].
1. Fai clic sul dashboard da eliminare.
1. Clic **[!UICONTROL Delete Dashboard]**.

Puoi anche selezionare **[!UICONTROL Dashboard Options]**, quindi **[!UICONTROL Delete]** dalla dashboard stessa.

![](../../mbi/assets/Delete_from_dashboard.png)

>[!NOTE]
>
>L’eliminazione di una dashboard non comporta l’eliminazione dei rapporti al suo interno, pertanto è necessario compiere un ulteriore passaggio per eliminare i rapporti.

**Per eliminare i report inutilizzati**

1. Seleziona **[!UICONTROL Manage Data]**, quindi **[!UICONTROL Reports]**.
1. Controlla la **Mostra solo rapporti non utilizzati** si trova sotto l’elenco delle metriche. In questo modo viene creato un elenco di rapporti che non vengono utilizzati in un dashboard o in un riepilogo e-mail.
1. Seleziona i rapporti da eliminare. Puoi selezionare tutto facendo clic sulla casella di controllo sopra l’elenco dei rapporti.
1. Clic **[!UICONTROL Delete Selected]**.

Ecco un’occhiata al processo di eliminazione del rapporto non utilizzato:

![](../../mbi/assets/unused_reports.png)

## Passaggio 3: eliminare le metriche non utilizzate

Dopo aver ripulito l’elenco degli utenti, le dashboard e i rapporti, puoi passare al controllo dell’elenco delle metriche. Questo consente di identificare tutto ciò che potrebbe essere obsoleto - ad esempio, una nuova metrica creata con una definizione diversa - o non in uso.

1. Per generare un elenco di rapporti dipendenti per una metrica, vai a **[!DNL Manage Data]**, quindi seleziona Fai clic su **[!UICONTROL Metrics]**.
1. Clic **[!UICONTROL Edit]** accanto a una metrica.
1. Nella parte inferiore della pagina è disponibile una sezione denominata **[!UICONTROL Dependent Charts]**. Fai clic sul collegamento per generare un elenco di rapporti dipendenti per questa metrica.
1. Dopo che il sistema ha completato il controllo, [!DNL MBI] visualizza un elenco di dashboard, report e utenti che utilizzano questa metrica.

![](../../mbi/assets/report_dependecies.png)

Se decidi che la metrica non è più necessaria, torna alla **[!UICONTROL Metrics]** pagina facendo clic su **[!UICONTROL Back to Metric List]** per trovare la metrica da eliminare. Clic **[!UICONTROL Delete]**.

## Passaggio 4: valutare le colonne sincronizzate

L’ultimo passaggio consiste nel valutare le colonne attualmente sincronizzate nella Data Warehouse. L’annullamento della sincronizzazione delle colonne può danneggiare l’account e ridurre potenzialmente il tempo di aggiornamento.

Se desideri continuare, contatta il [!DNL MBI] [Supporto](../guide-overview.md). Il team di supporto può creare un report che include tutte le colonne che non vengono utilizzate in alcun dashboard per alcun utente e che non vengono utilizzate nei riepiloghi e-mail, esclusi i report SQL. Puoi quindi utilizzare questo rapporto come guida per selezionare le colonne da desincronizzare tramite Gestione Date Warehouse.

>[!NOTE]
>
>Puoi sempre iniziare di nuovo a sincronizzare queste colonne in futuro. Se si annulla la sincronizzazione di una colonna, verranno rimossi tutti i dati dalla Data Warehouse. Ciò significa solo che durante il ciclo di aggiornamento questa colonna non viene controllata per la presenza di valori nuovi o aggiornati.

**Per annullare la sincronizzazione di una o più colonne**

1. Vai a **[!DNL Manage Data]**, quindi **[!UICONTROL Data Warehouse]**.
1. In **[!UICONTROL Synced Tables]** , passare alla tabella che contiene la colonna.
1. Selezionare una o più caselle accanto a una o più colonne da desincronizzare.
   >[!NOTE]
   >
   >Impossibile annullare la sincronizzazione di una colonna Chiave primaria senza eliminare l&#39;intera tabella.

1. Clic **[!UICONTROL Remove]** per annullare la sincronizzazione di una o più colonne.

Di seguito viene illustrato l&#39;intero processo:

![](../../mbi/assets/drop_column.png)

## Ritorno a capo

Tutto qui! Il tuo [!DNL MBI] L’account dovrebbe essere più graduale e facile da navigare per te e il tuo team.
