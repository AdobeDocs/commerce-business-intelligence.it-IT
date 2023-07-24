---
title: Consolidare le tabelle
description: Scopri come consolidare le tabelle e i database.
exl-id: 6065bed3-fb84-4147-a223-92dc3e1b15a5
role: Admin, User
feature: Commerce Tables, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Consolidare le tabelle

Se si gestiscono più punti vendita o mercati, è possibile che database simili siano archiviati separatamente. In entrata [!DNL Adobe Commerce Intelligence], è facile consolidare tabelle simili provenienti da database diversi.

Ad esempio, è possibile che `orders` tabella per `Market A`, e una simile `orders` tabella per `Market B`. [!DNL Commerce Intelligence] può consolidare entrambe le tabelle e consentire di esaminare i dati aggregati dell&#39;ordine da entrambe `Market A` e `B`, oltre a segmentarla per mercato specifico.

Affinché il consolidamento delle tabelle funzioni, le tabelle di input devono essere **con struttura simile**. In altre parole, tutte le tabelle di input devono contenere le colonne di dati richieste nella tabella consolidata.

In questo argomento vengono descritti alcuni dei casi d&#39;uso più comuni per le tabelle consolidate e i passaggi successivi necessari per la creazione di tabelle personalizzate.

## Recommendations per quando utilizzare le tabelle consolidate

Di seguito viene descritto quando potrebbe essere appropriato utilizzare tabelle consolidate nel sistema.

### Integrazione di dati da più siti Web

Se vendi i tuoi prodotti con marchi e siti web diversi, è probabile che le tabelle per ogni marchio o sito web siano strutturate in modo simile.

Ad esempio, è possibile che `orders` tabella per il sito web `A` e una distinta, ma simile, `orders` tabella per il sito web `B`. In questa situazione, può essere utile consolidare `orders` tabelle dal sito web `A` e `B`. Questo consente di esaminare i ricavi consolidati e il numero di ordini dal sito Web `A` e `B`, oltre a poter segmentare le metriche in base a questi due siti web.

### Integrazione dei dati legacy

Molte aziende hanno effettuato il refactoring dei propri database in un momento o in un altro e i dati del vecchio database non sempre vengono convertiti nel nuovo sistema. È possibile utilizzare le tabelle consolidate per unire le colonne chiave delle tabelle legacy a quelle del sistema attivo. Questo consente di condurre un’analisi unificata dei dati nel corso della storia.

### Combinazione di eventi per l&#39;analisi attiva degli utenti

Immagina un sito web in cui gli utenti possano fare diverse cose: rispondere a un sondaggio, giocare, acquistare, contattare un amico e così via. In genere, ciascuno di questi eventi viene memorizzato nella propria tabella. Questo rende difficile condurre un’analisi del numero di utenti distinti che hanno intrapreso almeno un’azione di qualsiasi tipo in un determinato periodo di tempo.

È possibile utilizzare le tabelle consolidate per creare un elenco unificato di tutti gli utenti e specificare quando si è verificato uno di questi eventi. Puoi quindi eseguire query sulla tabella consolidata per eseguire facilmente un’analisi di questo tipo.

Come per tutte le altre tabelle della Data Warehouse, è possibile aggiungere colonne aggiuntive per alimentare diversi tipi di grafici e analisi.

## Creazione, visualizzazione o aggiornamento di una tabella consolidata

Per aggiungere una tabella consolidata alla Data Warehouse, contattare [!DNL Commerce Intelligence] [supporto](../guide-overview.md#Submitting-a-Support-Ticket).

>[!NOTE]
>
>Perché le tabelle consolidate non sono visualizzabili in `Data Warehouse Manager`, la visualizzazione e l&#39;aggiornamento di queste tabelle possono essere eseguiti solo da [!DNL Commerce Intelligence] supporto.
