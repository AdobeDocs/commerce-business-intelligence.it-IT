---
title: Gestione Date Warehouse
description: Scopri come gestire le impostazioni di sincronizzazione di tabelle e colonne, analizzare in profondità lo schema di una tabella e creare colonne calcolate da utilizzare nei rapporti.
exl-id: b9577919-0db0-47f1-a426-1abe48443ac0
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 0%

---

# Gestione Date Warehouse

>[!NOTE]
>
>Richiede [autorizzazioni amministratore](../../administrator/user-management/user-management.md)

La gestione Date Warehouse, a cui si accede facendo clic su **[!UICONTROL Manage Data > Data Warehouse]**, è il portale della Data Warehouse [!DNL Adobe Commerce Intelligence]. Tramite Gestione Date Warehouse è possibile gestire le impostazioni di sincronizzazione di tabelle e colonne, analizzare in profondità lo schema di una tabella e creare colonne calcolate da utilizzare nei report.

Questo argomento riguarda:

* [Imparare a spostarti](#learning)
* [Sincronizzazione di tabelle e colonne](#syncing)
* [Creazione di colonne calcolate](#calculated)
* [Eliminazione di tabelle e rimozione di colonne](#delete)
* [Sincronizzazione di nuove tabelle in background](#syncnew)
* [Quando è possibile utilizzare le nuove colonne?](#when)

## Imparare a spostarti {#learning}

Il lato sinistro della pagina `Data Warehouse Manager` contiene l&#39;elenco delle tabelle, che consente di passare facilmente da una tabella all&#39;altra. Quando si seleziona una tabella dall&#39;elenco, l&#39;area di gestione tabella viene compilata con lo schema della tabella in cui è possibile modificare la tabella selezionata.

All&#39;interno dell&#39;elenco delle tabelle, le tabelle sono raggruppate in base all&#39;origine di connessione. Queste origini vengono aggiunte in [!UICONTROL Manage Data > Integrations] e possono essere un database, un [API](https://developer.adobe.com/commerce/services/reporting/) o un connettore di terze parti. Nella parte superiore dell&#39;elenco delle tabelle è presente una casella di ricerca che consente di trovare facilmente le tabelle desiderate.

Sotto la casella di ricerca sono disponibili due opzioni: `All Tables` e `Synced Tables`. L&#39;opzione `All Tables` elenca tutte le tabelle rese disponibili per la Data Warehouse, incluse quelle sincronizzate e non.

L&#39;opzione `Synced Tables` mostra tutte le tabelle che sono già state aggiunte alla Data Warehouse e che contengono dati replicati dalle colonne selezionate.

La tabella cercata nell&#39;elenco `All Tables` non è visualizzata? Questo può essere dovuto ad alcuni motivi:

* L’origine dati non è stata ancora aggiunta
* L&#39;origine dati è un database e l&#39;utente [!DNL Commerce Intelligence] creato non dispone dell&#39;accesso. In questo caso, l&#39;utente o l&#39;amministratore del database deve concedere l&#39;accesso.
* L’origine dati o la tabella è stata aggiunta di recente e non è ancora stata sincronizzata

## Sincronizzazione di tabelle e colonne {#syncing}

### Sincronizzazione di nuove tabelle e colonne native

Gestione Date Warehouse consente non solo di visualizzare e gestire facilmente le origini dati, ma anche di selezionare le singole tabelle e colonne da sincronizzare.

1. Fare clic sull&#39;opzione `All Tables` e individuare la tabella da sincronizzare.
1. Fai clic sul nome della tabella per visualizzare in anteprima lo schema. Se la tabella è nuova, tutte le colonne vengono visualizzate come `Unsynced`.
1. Selezionare le colonne da sincronizzare.

   >[!NOTE]
   >
   >Le colonne native di una tabella hanno From Your Database nella colonna `Location`.

1. Controllare le colonne `Primary Key`. Queste colonne sono contrassegnate da un simbolo di chiave accanto al nome della colonna. È necessario un `Primary Key` per sincronizzare correttamente i dati nella Data Warehouse.

   Se si sta sincronizzando una tabella proveniente direttamente dal database, è possibile che `Primary Keys` non venga identificato. In questo caso, contattare l&#39;amministratore del database per richiedere l&#39;aggiunta di una o più chiavi primarie alla tabella.
1. Al termine, fare clic sul pulsante ![pulsante](../../assets/button.png).

*Operazione completata.Viene visualizzato il messaggio* e lo stato cambia in `Pending` per le colonne selezionate. Al termine del prossimo aggiornamento completo, le tabelle e le colonne appena sincronizzate saranno disponibili per l’utilizzo nei rapporti. È inoltre possibile impostare nuovi [metodi di replica](./cfg-replication-methods.md) dopo la sincronizzazione iniziale.

Ecco una breve panoramica dell&#39;intero processo:

![Aggiunta di colonne al data warehouse](../../assets/DW_sync.gif)

### Sincronizzazione di nuove tabelle in background {#syncnew}

Quando sincronizzi una tabella di grandi dimensioni per la prima volta, la Data Warehouse deve acquisire retroattivamente tutti i punti dati della tabella prima di acquisire nuovi dati su base continuativa. Se la tabella è grande, è possibile che non si desideri eseguire la sincronizzazione iniziale in sequenza con il **ciclo di aggiornamento**. In questa situazione, si desidera che la sincronizzazione iniziale venga eseguita in background, in *parallelo* con qualsiasi aggiornamento attualmente in esecuzione.

Per assicurarsi che ciò si verifichi, è necessario selezionare l&#39;opzione `Save and Sync Data Immediately` che sincronizza la tabella per la prima volta.

### Ricerca di nuove tabelle e colonne {#forceupdate}

La Data Warehouse non rileva automaticamente nuove origini, tabelle o colonne nel momento in cui vengono aggiunte. Un processo di sincronizzazione viene eseguito nel corso della settimana per trovare nuove aggiunte e renderle disponibili, ma è possibile forzare una sincronizzazione della struttura se si desidera accedere alle nuove tabelle e colonne aggiunte prima dell&#39;esecuzione del processo.

Sotto la barra di ricerca nell&#39;elenco delle tabelle è presente un collegamento `Check for new tables and columns`. Facendo clic su questo collegamento viene forzato l&#39;avvio del processo di sincronizzazione della struttura; le nuove aggiunte sono generalmente disponibili dopo 10 minuti. Aggiorna la pagina per visualizzare la nuova origine, tabella o colonna.

## Creazione di colonne calcolate {#calculated}

La semplice possibilità di visualizzare e gestire i dati provenienti da tutte le origini semplifica notevolmente la raccolta di informazioni sul business. In Gestione Date Warehouse, tuttavia, è possibile fare un ulteriore passo avanti creando colonne calcolate all&#39;interno delle tabelle. `Calculated` colonne derivano nuove informazioni dai dati esistenti.

Si supponga di voler aggiungere `user's lifetime revenue` alla tabella `users` per trovare utenti di valore elevato. Oppure, se desideri segmentare i ricavi per sesso, puoi aggiungere `customer's gender` alla tua tabella `orders`.

Per ulteriori informazioni, vedi questa [esercitazione](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md).

## Eliminazione di tabelle e rimozione di colonne {#delete}

È inoltre possibile eliminare o rimuovere tabelle e colonne da sincronizzare con la Data Warehouse.

>[!NOTE]
>
>Se si rilascia una tabella o si rimuovono colonne, dopo aver confermato l’eliminazione verranno eliminati tutti i rapporti, le metriche, i set di filtri e le colonne dipendenti. Assicurarsi di eseguire questa operazione - **questa azione non può essere annullata.**

Non preoccuparti se fai clic su **[!UICONTROL Delete]** per errore. Un controllo delle dipendenze viene eseguito prima dell’eliminazione di qualsiasi elemento, quindi hai la possibilità di rivedere tutto prima di confermare.

Per rimuovere le colonne, fare clic sulla tabella a cui appartiene la colonna. Selezionare le colonne da rimuovere e fare clic sul pulsante ![button\_1.png](../../assets/button_1.png).

Per rimuovere una tabella sincronizzata, selezionare tutte le colonne della tabella e fare di nuovo clic sul pulsante ![pulsante](../../assets/button_1.png). Verranno rimosse dalla Data Warehouse tutte le colonne native e calcolate che utilizzano questa tabella.

### Conferma delle modifiche

Se si elimina una tabella o si rimuovono colonne, viene eseguito un controllo di dipendenza prima del completamento del processo di eliminazione. Le dipendenze sono colonne calcolate, metriche, set di filtri e rapporti che utilizzano la tabella o le colonne da rimuovere. Tutte le dipendenze individuate vengono visualizzate. A questo punto, è possibile annullare il processo o fare clic su **[!UICONTROL Confirm Changes]** per eliminare la tabella o rimuovere le colonne.

Anche se le dipendenze eliminate non possono essere ripristinate, le tabelle e le colonne rimarranno disponibili se in futuro sarà necessario risincronizzare le colonne native.

Di seguito è riportato un rapido esempio di rimozione di una colonna:

![Rimozione di una colonna dal data warehouse](../../assets/DW_delete.gif)

## Quando è possibile utilizzare le nuove colonne? {#when}

Le nuove colonne sincronizzate e le colonne calcolate nuove/aggiornate saranno pronte per l’uso al termine del prossimo aggiornamento completo. Se un aggiornamento non è già in corso, è possibile forzarlo facendo clic su **[!UICONTROL Force update]** visualizzato nella parte superiore della pagina `Data Warehouse` o `Integrations`. È inoltre possibile pianificare una notifica e-mail al completamento dell&#39;aggiornamento facendo clic su **[!UICONTROL Email me when complete]**.

Quando sei pronto a utilizzare le nuove colonne nei rapporti, [devi prima aggiungerle alle metriche](../data-warehouse-mgr/manage-data-dimensions-metrics.md). Anche se i dati non sono disponibili fino al completamento di un aggiornamento, è comunque possibile utilizzare nuove colonne nei rapporti. I dati all’interno del rapporto vengono visualizzati al termine dell’aggiornamento.

## Ritorno a capo

Questo articolo copriva molto materiale. A questo punto è necessario avere una solida conoscenza di cosa è un database, come sono organizzati i dati, come le tabelle si relazionano tra loro e cosa è possibile fare con Data Warehouse Manager.

Verifica le tue conoscenze [creando una colonna calcolata](../data-warehouse-mgr/creating-calculated-columns.md) o [creando rapporti interessanti](../../tutorials/using-visual-report-builder.md).
