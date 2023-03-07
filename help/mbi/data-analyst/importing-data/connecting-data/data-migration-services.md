---
title: Servizi di migrazione dati
description: Scopri tutto ciò che ti serve per inviare una richiesta e iniziare a eseguire la migrazione.
exl-id: 105cd003-98ef-4358-80b9-b3190c2c57b7
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---

# Migrazione dei dati

La migrazione a un nuovo schema di database, server o database di reporting non deve essere troppo complessa. Il **[!DNL Adobe Commerce Services - Analytics]** team offre assistenza per la migrazione.

Per garantire una transizione quanto più fluida possibile, è necessario essere il più dettagliati possibile durante l’invio della richiesta di migrazione. In questo articolo trovi tutto ciò che serve per inviare una richiesta e iniziare a eseguire la migrazione. Fornendoci un quadro completo delle tue esigenze, assicurati che il tuo progetto abbia un ambito appropriato e che la stima sia accurata.

## Introduzione {#started}

Prima di iniziare, è necessario conoscere le risposte alle seguenti domande:

* **Il nuovo database si trova su un nuovo server?** Prima di inviare una richiesta, aggiorna le impostazioni della connessione dati in **[!UICONTROL Manage Data** > **Connections]**. Se hai bisogno di un aggiornamento su come farlo, vai al [`Integrations`](../integrations/integrations.md) e trovare le istruzioni per il tipo di database in uso.
* **Il nuovo database contiene tutti i dati storici o è necessario eseguirne la migrazione?** Puoi consolidare i dati storici e quelli nuovi durante il processo di migrazione. Anche se non hai bisogno di un consolidamento, comunicaci nella tua richiesta.

Dopo aver risposto a quanto sopra, è necessario conoscere il tipo di migrazione: il nuovo database avrà [`same`](#sameschema) o avrà un [`different`](#newschema) schema? Nelle sezioni seguenti trovi istruzioni dettagliate per ciascun tipo di migrazione.

## Migrazione a un nuovo database con lo stesso schema {#sameschema}

Quando invii la richiesta, informa che lo schema del database non sta cambiando e che la connessione è già impostata in [!DNL MBI].

Se il database ha un nuovo nome, includilo nella richiesta in modo che sia possibile migrare correttamente le dashboard.

Se il nome del database non viene modificato, la migrazione è completa. Le dashboard e i rapporti verranno aggiornati al termine del prossimo aggiornamento completo. Contatta l’Adobe per essere sempre al corrente di eventuali problemi derivanti dalla migrazione.

## Migrazione a un nuovo database con uno schema diverso {#newschema}

>[!IMPORTANT]
>
>Se alcune colonne di dati non hanno colonne equivalenti nel nuovo database, è possibile che alcune analisi vadano perse nel processo.

Per completare correttamente questo tipo di migrazione, le colonne di dati esistenti devono corrispondere ai loro equivalenti nel nuovo database. Questo non è obbligatorio, ma l’esecuzione della corrispondenza per Dell consente di velocizzare il tempo di risposta della richiesta e ridurre il prezzo della migrazione.

Se ti senti a tuo agio a fare da solo la corrispondenza, segui queste istruzioni e allega alla tua richiesta il foglio di calcolo finito:

1. Esaminare tutte le tabelle e le colonne attualmente sincronizzate con la Data Warehouse (**[!UICONTROL Manage Data** > **Data Warehouse]**).
1. In un foglio di calcolo creare una scheda per ogni tabella da migrare al nuovo database.
1. In ogni scheda, crea una colonna per tutte le colonne esistenti da migrare. L’Adobe consiglia di denominarlo in un modo simile a `Existing column name`.
1. È inoltre necessario creare un&#39;altra colonna per gli equivalenti di colonna nel nuovo database in ogni scheda del foglio di calcolo. L’Adobe consiglia di denominare la colonna in un modo simile a `New column name`.
1. Inserire le colonne esistenti e le relative equivalenti. Se una colonna esistente non ha un nuovo equivalente, immettere: `N/A`.

   Inoltre, se esiste un nuovo metodo per calcolare le stesse informazioni nel nuovo database, immetterlo nel [`New column name`] colonna.

Ecco un esempio:

![](../../../assets/Migration_Spreadsheet.png)

>[!NOTE]
>
>Se alcune colonne di dati non hanno colonne equivalenti nel nuovo database, è possibile che alcune analisi vadano perse nel processo.

## Come si invia una richiesta? {#submitreq}

Puoi contattarci tramite [invio di una richiesta di assistenza](../../../guide-overview.md).

Se hai seguito i passaggi della sezione precedente per creare il foglio di calcolo corrispondente alle colonne, non dimenticare di allegarlo.

## Cosa succede dopo? {#wrapup}

La determinazione dell’ambito del progetto richiede una certa collaborazione tra l’utente e l’analista del team Commerce Services che esegue la migrazione. La complessità delle modifiche e la reattività dell’utente e dell’analista influiscono direttamente sul tempo necessario per la migrazione. Dopo aver individuato i dettagli, verrà stabilita una sequenza temporale e inviata all&#39;utente con una descrizione del lavoro.
