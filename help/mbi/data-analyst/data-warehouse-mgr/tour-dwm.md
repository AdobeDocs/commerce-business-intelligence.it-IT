---
title: Data Warehouse Manager
description: Scopri come gestire le impostazioni di sincronizzazione di tabelle e colonne, approfondire lo schema di una tabella e creare colonne calcolate da utilizzare nei rapporti.
exl-id: b9577919-0db0-47f1-a426-1abe48443ac0
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 0%

---

# Data Warehouse Manager

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../administrator/user-management/user-management.md)

Gestione Date Warehouse, a cui si accede facendo clic su **[!UICONTROL Manage Data > Data Warehouse]** nella barra laterale è il portale della [!DNL MBI] Data Warehouse. Utilizzando Data Warehouse Manager, puoi gestire le impostazioni di sincronizzazione di tabelle e colonne, approfondire lo schema di una tabella e creare colonne calcolate da utilizzare nei rapporti.

In questo articolo tratteremo:

* [Apprendimento del percorso](#learning)
* [Sincronizzazione di tabelle e colonne](#syncing)
* [Creazione di colonne calcolate](#calculated)
* [Eliminazione di tabelle e rimozione di colonne](#delete)
* [Sincronizzazione di nuove tabelle in background](#syncnew)
* [Quindi, quando posso usare le mie nuove colonne?](#when)

## Apprendimento del percorso {#learning}

Il lato sinistro del `Data Warehouse Manager` la pagina contiene l’elenco delle tabelle, che consente di passare facilmente da una tabella all’altra. Quando si seleziona una tabella dall’elenco, l’area di gestione delle tabelle viene compilata con lo schema della tabella in cui è possibile apportare modifiche alla tabella selezionata.

Nell’elenco delle tabelle, le tabelle sono raggruppate in base all’origine della connessione. Queste fonti vengono aggiunte in [!UICONTROL Manage Data > Integrations] e può essere una banca dati [API](https://developer.adobe.com/commerce/services/reporting/)o un connettore di terze parti. Nella parte superiore dell’elenco delle tabelle è presente una casella di ricerca che consente di trovare facilmente le tabelle desiderate.

Sotto la casella di ricerca sono visualizzate due opzioni: `All Tables` e `Synced Tables`. La `All Tables` elenca tutte le tabelle rese disponibili per la Data Warehouse, incluse le tabelle sincronizzate e non sincronizzate.

La `Synced Tables` mostra tutte le tabelle che sono già state aggiunte alla Data Warehouse e i cui dati vengono replicati dalle colonne selezionate.

Non visualizzare la tabella che stai cercando nel `All Tables` elenco? Ci sono alcuni possibili motivi per questo:

* L&#39;origine dati non è ancora stata aggiunta
* L&#39;origine dati è un database e [!DNL MBI] l&#39;utente creato non dispone dell&#39;accesso. In questo caso, l&#39;utente o l&#39;amministratore del database dovrà concedere l&#39;accesso.
* L’origine dati o la tabella è stata aggiunta di recente e non è ancora stata sincronizzata

## Sincronizzazione di tabelle e colonne {#syncing}

### Sincronizzazione di nuove tabelle e colonne native

Data Warehouse Manager consente non solo di visualizzare e gestire facilmente le origini dati, ma anche di selezionare le singole tabelle e colonne da sincronizzare.

1. Fai clic sul pulsante `All Tables` e individuare la tabella da sincronizzare.
1. Fare clic sul nome della tabella per visualizzare l&#39;anteprima dello schema. Se la tabella è nuova, tutte le colonne verranno visualizzate come `Unsynced`.
1. Seleziona le colonne da sincronizzare.

   >[!NOTE]
   >
   >Le colonne native di una tabella avranno dal database in `Location` colonna.

1. Controlla la `Primary Key` colonne : accanto al nome della colonna è presente un simbolo di chiave. A `Primary Key` è necessario per sincronizzare correttamente i dati nella Data Warehouse.

   Se si sincronizza una tabella proveniente direttamente dal database, è possibile che `Primary Keys` possono non essere identificate. In questo caso, contatta l’amministratore del database per richiedere l’aggiunta di una o più chiavi primarie alla tabella.
1. Al termine, fai clic sul pulsante ![pulsante](../../assets/button.png) pulsante .

A *Successo!* verrà visualizzato il messaggio e lo stato cambierà in `Pending` per le colonne selezionate. Al termine del prossimo aggiornamento completo, le nuove tabelle e colonne sincronizzate saranno disponibili per l’uso nei rapporti; è inoltre possibile impostare nuove [metodi di replica](./cfg-replication-methods.md) dopo la sincronizzazione iniziale.

Ecco un rapido sguardo sull&#39;intero processo:

![Aggiunta di colonne al data warehouse](../../assets/DW_sync.gif)

### Sincronizzazione di nuove tabelle in background {#syncnew}

Quando si sincronizza per la prima volta una nuova tabella di grandi dimensioni, il data warehouse deve acquisire retroattivamente tutti i punti dati della tabella prima di acquisire continuamente nuovi dati. Se la tabella è particolarmente grande, potrebbe non essere necessario eseguire la sincronizzazione iniziale in sequenza con il **ciclo di aggiornamento** — in una situazione, desideri che la sincronizzazione iniziale si verifichi in background, in *parallelo* con eventuali aggiornamenti in esecuzione.

Per assicurarti che ciò si verifichi, seleziona la `Save and Sync Data Immediately` sincronizzazione della tabella per la prima volta.

### Verifica di nuove tabelle e colonne {#forceupdate}

La Data Warehouse non rileva automaticamente nuove origini, tabelle o colonne nel momento in cui vengono aggiunte. Un processo di sincronizzazione viene eseguito durante la settimana per trovare nuove aggiunte e renderle disponibili, ma è possibile forzare una sincronizzazione della struttura se si desidera accedere a nuove tabelle e colonne aggiunte prima dell&#39;esecuzione del processo.

Sotto la barra di ricerca nell’elenco delle tabelle è `Check for new tables and columns` link. Facendo clic su questo collegamento si avvia il processo di sincronizzazione della struttura; le nuove aggiunte sono generalmente disponibili dopo 10 minuti. Aggiorna la pagina per visualizzare la nuova origine, tabella o colonna.

## Creazione di colonne calcolate {#calculated}

La semplice possibilità di visualizzare e gestire i dati provenienti da tutte le fonti semplifica notevolmente l&#39;acquisizione di informazioni sulla tua attività. Tuttavia, in Data Warehouse Manager è possibile fare un ulteriore passo avanti creando colonne calcolate all’interno delle tabelle. `Calculated` le colonne derivano nuove informazioni dai dati esistenti.

Diciamo che desideri aggiungere `user's lifetime revenue` al tuo `users` tabella per trovare utenti di alto valore. Oppure, se desideri segmentare le entrate per genere, puoi aggiungere `customer's gender` al tuo `orders` tabella.

Per padroneggiare la creazione di queste colonne, [abbiamo creato un tutorial](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md) per attraversarla.

## Eliminazione di tabelle e rimozione di colonne {#delete}

Così come puoi selezionare tabelle e colonne da sincronizzare con la tua Data Warehouse, puoi anche eliminarle o rimuoverle.

>[!NOTE]
>
>Se si rilascia una tabella o si rimuovono colonne, verranno eliminati tutti i rapporti, le metriche, i set di filtri e le colonne dipendenti una volta confermata l’eliminazione. Assicurati di volerlo fare - **questa azione non può essere annullata.**

Non preoccuparti se fai clic su **[!UICONTROL Delete]** per caso. Un controllo della dipendenza viene eseguito prima dell’eliminazione di qualsiasi elemento, pertanto potrai esaminare tutti gli elementi prima di confermare.

Per rimuovere le colonne, fare clic sulla tabella a cui appartiene la colonna. Seleziona le colonne da rimuovere e fai clic sul pulsante ![button\_1.png](../../assets/button_1.png) pulsante .

Per rimuovere una tabella sincronizzata, selezionare tutte le colonne della tabella e fare nuovamente clic sul pulsante ![pulsante](../../assets/button_1.png) pulsante . Verranno rimosse tutte le colonne native e calcolate che utilizzano questa tabella dal data warehouse.

### Conferma delle modifiche

Se si rilascia una tabella o si rimuovono le colonne, prima del completamento del processo di eliminazione verrà eseguito un controllo di dipendenza. Le dipendenze sono colonne calcolate, metriche, set di filtri e rapporti che utilizzano la tabella o le colonne da rimuovere. Verranno visualizzate tutte le dipendenze rilevate. A questo punto, è possibile annullare il processo o fare clic su **[!UICONTROL Confirm Changes]** per eliminare la tabella o rimuovere le colonne.

Sebbene non sia possibile ripristinare le dipendenze eliminate, le tabelle e le colonne saranno comunque disponibili se in futuro sarà necessario risincronizzare le colonne native.

Ecco un rapido sguardo sulla rimozione di una colonna:

![Rimozione di una colonna dal data warehouse](../../assets/DW_delete.gif)

## Quindi, quando posso usare le mie nuove colonne? {#when}

Le nuove colonne sincronizzate e le colonne calcolate nuove/aggiornate saranno pronte per l’uso al termine del prossimo aggiornamento completo. Se un aggiornamento non è già in corso, è possibile forzare un aggiornamento facendo clic su **[!UICONTROL Force update]** mostrato nella parte superiore della `Data Warehouse` o `Integrations` pagina. Puoi anche pianificare una notifica e-mail al termine dell’aggiornamento facendo clic su **[!UICONTROL Email me when complete]**.

Quando sei pronto a utilizzare le nuove colonne nei rapporti, [devi prima aggiungerli alle metriche](../data-warehouse-mgr/manage-data-dimensions-metrics.md). Anche se i dati non saranno disponibili fino al completamento di un aggiornamento, puoi comunque utilizzare nuove colonne nei rapporti. I dati all’interno del rapporto vengono visualizzati al termine dell’aggiornamento.

## Tutto qui - siamo alla fine!

Abbiamo trattato molto materiale in questo tutorial. A questo punto, è necessario avere una conoscenza approfondita di ciò che è un database, del modo in cui i dati vengono organizzati, del modo in cui le tabelle si relazionano tra loro e delle operazioni che è possibile eseguire con Gestione Date Warehouse.

Eccellente! Esegui il test della tua nuova conoscenza [creazione di una colonna calcolata](../data-warehouse-mgr/creating-calculated-columns.md) o [creazione di report interessanti](../../tutorials/using-visual-report-builder.md).
