---
title: Declutamento del [!DNL MBI] Account
description: Scopri come ripulire il tuo [!DNL MBI] conto.
exl-id: 5fcdac2d-41ca-4011-b646-a699d9ecc6e4
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 0%

---

# Pulisci il tuo [!DNL MBI] Account

Se sei stato con [!DNL MBI] per 6 mesi o 6 anni, mantenere un account ordinato è fondamentale per ottenere il massimo dalla piattaforma. Nel tempo, è naturale che non siano più necessari utenti, dashboard, rapporti, metriche e colonne. Forse hai creato un rapporto per un utilizzo una tantum e se ne sei dimenticato, oppure un utente che ha lasciato la tua azienda non ha mai avuto il suo account disattivato.

In combinazione con [denominazione standardizzata e chiara di tutti gli elementi](../best-practices/naming-elements.md)) della [!DNL MBI] account, i passaggi di controllo dell&#39;account seguenti ti aiuteranno a ridurre il disordine e le analisi inutili per i tuoi utenti. Un vantaggio aggiuntivo include [cicli di aggiornamento potenzialmente più rapidi](../best-practices/reduce-update-cycle-time.md).

## Passaggio 1: Identificare gli utenti non attivi

Il primo passo per ripulire l’account è disattivare gli account degli utenti non attivi, ad esempio quelli che hanno lasciato l’azienda o che non utilizzano più [!DNL MBI] nei loro ruoli correnti.

Per farlo, fai clic sul nome della tua azienda nell’angolo in alto a destra della barra di navigazione superiore, quindi seleziona **[!UICONTROL Manage Users]**. Quindi, seleziona l’utente da disattivare e fai clic su **[!UICONTROL Deactivate User]**.

>[!NOTE]
>
>Hai bisogno di [Autorizzazioni amministratore](../administrator/user-management/user-management.md) per fare questo.

>[!WARNING]
>
>La disattivazione di un utente comporta anche la rimozione dei grafici, delle dashboard e di altre risorse create da tale utente. Per conservare queste risorse, contatta l’ [!DNL MBI] [supporto](../guide-overview.md) prima di disattivare l’utente. Il supporto consente di trasferire queste risorse a un altro utente.

### Riattivare un utente

Per riattivare un utente, invitare nuovamente l&#39;utente ricreando il suo account con lo stesso indirizzo e-mail disattivato e il loro accesso e i dati di proprietà verranno ripristinati al momento dell&#39;accesso.

## Passaggio 2: Eliminare dashboard e rapporti non utilizzati

Il passaggio successivo nel controllo dell’account consiste nell’eliminare tutte le dashboard e i rapporti non utilizzati.

>[!NOTE]
>
>Hai bisogno di `Admin` o `Standard` [autorizzazioni utente](../administrator/user-management/user-management.md) per fare questo.

Ogni utente con `Admin` o `Standard` l’accesso può creare rapporti e dashboard. Per questo motivo, tutti coloro che dispongono di queste autorizzazioni devono seguire i passaggi seguenti per identificare e rimuovere i rapporti non utilizzati.

### Rivedere dashboard e rapporti

Prima di eliminare qualsiasi cosa, è necessario esaminare i rapporti e le dashboard per valutare cosa è attualmente in uso. Quando è possibile utilizzare **[!UICONTROL find unused reports]** funzionalità descritta di seguito, qualsiasi revisione iniziale renderà i vostri sforzi di pulizia molto più produttivi.

### Eliminazione di dashboard e report

Dopo aver effettuato l’accesso alle dashboard e ai rapporti, puoi iniziare a pulire il tuo account.

**Rimozione di un rapporto da un dashboard**

1. Individua il rapporto da rimuovere nel dashboard.
1. Seleziona **[!UICONTROL Options]** nell’angolo in alto a destra del rapporto.
1. Fai clic su **[!UICONTROL Remove From Dashboard]**.

**Per eliminare un intero dashboard**

1. Seleziona **[!UICONTROL Manage Data]**, quindi **[!UICONTROL Dashboards**].
1. Fai clic sul dashboard da eliminare.
1. Fai clic su **[!UICONTROL Delete Dashboard]**.

Puoi anche selezionare **[!UICONTROL Dashboard Options]**, quindi **[!UICONTROL Delete]** dal dashboard stesso.

![](../../mbi/assets/Delete_from_dashboard.png)

>[!NOTE]
>
>L&#39;eliminazione di una dashboard non comporta l&#39;eliminazione dei report al suo interno, pertanto dovrai effettuare un ulteriore passaggio per eliminare i report.

**Per eliminare i rapporti non utilizzati**

1. Seleziona **[!UICONTROL Manage Data]**, quindi **[!UICONTROL Reports]**.
1. Controlla la **Mostra solo rapporti non utilizzati** sotto l’elenco delle metriche. Verrà creato un elenco di rapporti non utilizzati in un dashboard o in un riepilogo e-mail.
1. Selezionare i rapporti da eliminare. Per selezionare tutti gli elementi, fai clic sulla casella di controllo posta sopra l’elenco dei rapporti.
1. Fai clic su **[!UICONTROL Delete Selected]**.

Ecco un&#39;occhiata al processo di eliminazione dei report non utilizzati:

![](../../mbi/assets/unused_reports.png)

## Passaggio 3: Eliminare le metriche non utilizzate

Dopo aver ripulito l’elenco degli utenti, le dashboard e i rapporti, puoi passare al controllo dell’elenco delle metriche. Questo ti aiuterà a identificare qualsiasi elemento che potrebbe essere obsoleto, ad esempio, una nuova metrica è stata creata con una definizione diversa, o che non è in uso.

1. Per generare un elenco di rapporti dipendenti per una metrica, vai a **[!DNL Manage Data]**, quindi fai clic su **[!UICONTROL Metrics]**.
1. Fai clic su **[!UICONTROL Edit]** accanto a una metrica.
1. Nella parte inferiore della pagina viene visualizzata una sezione denominata **[!UICONTROL Dependent Charts]**. Fai clic sul collegamento per generare un elenco di rapporti dipendenti per questa metrica.
1. Dopo che il sistema ha completato il controllo, [!DNL MBI] visualizza un elenco di dashboard, report e utenti che utilizzano questa metrica.

![](../../mbi/assets/report_dependecies.png)

Se decidi che la metrica non è più necessaria, torna alla sezione **[!UICONTROL Metrics]** facendo clic su **[!UICONTROL Back to Metric List]** nella parte superiore della pagina e trova la metrica da eliminare. Fai clic su **[!UICONTROL Delete]**.

## Passaggio 4: Valutare le colonne sincronizzate

L&#39;ultimo passaggio consiste nel valutare le colonne attualmente sincronizzate nel data warehouse. Non solo è possibile annullare la sincronizzazione delle colonne riducendo il tuo account, ma può anche potenzialmente ridurre il tempo di aggiornamento.

Se desideri proseguire, contatta [!DNL MBI] [Supporto](../guide-overview.md). Il team di supporto può creare un rapporto che include tutte le colonne che non vengono utilizzate in alcun dashboard per alcun utente e che non vengono utilizzate nei riepiloghi e-mail, esclusi i report SQL. Puoi quindi utilizzare questo rapporto come guida per selezionare le colonne da rimuovere dalla sincronizzazione tramite Data Warehouse Manager.

>[!NOTE]
>
>Puoi sempre iniziare a sincronizzare di nuovo queste colonne in futuro. La rimozione della sincronizzazione di una colonna non comporta la rimozione di dati dal data warehouse; significa solo che questa colonna non verrà controllata per verificare la presenza di valori nuovi o aggiornati durante il ciclo di aggiornamento.

**Per annullare la sincronizzazione di una colonna (o colonne)**

1. Vai a **[!DNL Manage Data]**, quindi **[!UICONTROL Data Warehouse]**.
1. In **[!UICONTROL Synced Tables]** selezionare la tabella contenente la colonna.
1. Seleziona le caselle accanto alle colonne da desincronizzare.
   >[!NOTE]
   >
   >Non è possibile annullare la sincronizzazione di una colonna Chiave principale senza eliminare l’intera tabella.

1. Fai clic su **[!UICONTROL Remove]** per annullare la sincronizzazione delle colonne.

Ecco un&#39;occhiata all&#39;intero processo:

![](../../mbi/assets/drop_column.png)

## Ritorno a capo

Tutto qui! Le [!DNL MBI] ora l’account deve essere più ordinato e facile da navigare per te e il tuo team.
