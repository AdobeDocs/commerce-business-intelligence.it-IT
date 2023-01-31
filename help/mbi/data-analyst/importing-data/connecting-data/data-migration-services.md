---
title: Servizi di migrazione dei dati
description: Scopri tutto il necessario per inviare una richiesta e iniziare la migrazione.
exl-id: 105cd003-98ef-4358-80b9-b3190c2c57b7
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---

# Migrazione dei dati

La migrazione a un nuovo schema di database, server o database di reporting non deve essere stressante. Nostro **[!DNL Magento Services - Analytics]** team offre assistenza in materia di migrazione - facciamo tutto il sollevamento pesante in modo che non sia necessario.

Per garantire che la transizione avvenga nel modo più semplice possibile, quando invii la richiesta di migrazione ti chiediamo di essere il più dettagliato possibile. In questo articolo troverai tutto il necessario per inviare una richiesta e iniziare la migrazione. Fornire un quadro completo delle vostre esigenze garantirà che il vostro progetto sia delimitato correttamente e che la stima sia accurata.

## Introduzione {#started}

Prima di immergerci, dovresti conoscere le risposte a queste domande:

* **Il nuovo database è su un nuovo server?** Prima di inviare una richiesta, aggiorna le impostazioni della connessione dati in **[!UICONTROL Manage Data** > **Connections]**. Se hai bisogno di un aggiornamento su come farlo, vai alla [`Integrations`](../integrations/integrations.md) e trovare le istruzioni per il tipo di database in uso.
* **Tutti i dati storici esistono nel nuovo database o è necessario eseguire la migrazione?** Possiamo consolidare i dati storici e quelli nuovi durante il processo di migrazione. Anche se non hai bisogno di un consolidamento, ti chiediamo di comunicarcelo nella tua richiesta.

Dopo aver ricevuto le risposte, dovremo conoscere il tipo di migrazione: il nuovo database avrà [`same`](#sameschema) schema o avrà una [`different`](#newschema) schema? Nelle sezioni seguenti trovi istruzioni dettagliate per ogni tipo di migrazione.

## Migrazione a un nuovo database con lo stesso schema {#sameschema}

Quando invii la richiesta, informa che lo schema del database non sta cambiando e che la connessione è già impostata in [!DNL MBI].

Se il database ha un nuovo nome, includilo nella richiesta in modo che le dashboard possano essere migrate correttamente.

Se il nome del database non viene modificato, la migrazione è completa. Dashboard e rapporti verranno aggiornati al termine del prossimo aggiornamento completo. Vi chiediamo di contattarci ancora in modo da poter superare tutti i problemi che potrebbero derivare dalla migrazione.

## Migrazione a un nuovo database con uno schema diverso {#newschema}

>[!IMPORTANT]
>
>Se alcune colonne di dati non hanno colonne equivalenti nel nuovo database, è possibile che alcune analisi vengano perse nel processo.

Per completare correttamente questo tipo di migrazione, le colonne di dati esistenti devono essere abbinate ai loro equivalenti nel nuovo database. Questo non è obbligatorio per te, ma eseguire la corrispondenza per noi aiuterà ad accelerare il tempo di consegna della tua richiesta e ridurre il prezzo della migrazione.

Se ti senti a tuo agio nel fare la corrispondenza, segui queste istruzioni e allega il foglio di calcolo finito alla tua richiesta:

1. Rivedi tutte le tabelle e le colonne attualmente sincronizzate con la tua Data Warehouse (**[!UICONTROL Manage Data** > **Data Warehouse]**).
1. In un foglio di calcolo, creare una scheda per la migrazione di ogni tabella nel nuovo database.
1. In ogni scheda, crea una colonna per tutte le colonne esistenti da migrare. Consigliamo di denominarlo con un nome simile a `Existing column name`.
1. È inoltre necessario creare un’altra colonna per gli equivalenti di colonna nel nuovo database in ogni scheda del foglio di calcolo. Consigliamo di assegnare alla colonna un nome simile a `New column name`.
1. Immettere le colonne esistenti e i relativi equivalenti. Se una colonna esistente non ha un nuovo equivalente, è sufficiente immettere `N/A`.

   Inoltre, se esiste un nuovo modo di calcolare le stesse informazioni nel nuovo database, inseriscilo nel [`New column name`] colonna.

Ecco un esempio:

![](../../../assets/Migration_Spreadsheet.png)

>[!NOTE]
>
>Se alcune colonne di dati non hanno colonne equivalenti nel nuovo database, è possibile che alcune analisi vengano perse nel processo.

## Come si invia una richiesta? {#submitreq}

Puoi contattarci tramite [invio di una richiesta di supporto](../../../guide-overview.md).

Se hai seguito i passaggi della sezione precedente per creare il foglio di calcolo corrispondente alle colonne, non dimenticare di allegarlo.

## Cosa succede dopo? {#wrapup}

Per determinare l’ambito del progetto sarà necessaria una certa collaborazione tra te e l’analista del team Commerce Services che esegue la migrazione. La complessità dei cambiamenti e la reattività di te e dell’analista influisce direttamente sul tempo necessario alla migrazione. Dopo aver azzerato i dettagli, verrà stabilita una cronologia e vi verrà inviata una dichiarazione di lavoro.
