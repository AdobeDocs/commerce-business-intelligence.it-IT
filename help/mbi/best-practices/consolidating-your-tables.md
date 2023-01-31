---
title: Consolidare le tabelle
description: Scopri come consolidare le tabelle e i database.
exl-id: 6065bed3-fb84-4147-a223-92dc3e1b15a5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# Consolidare le tabelle

Se si utilizzano più punti vendita o in più mercati, è possibile che i database simili siano archiviati separatamente. In [!DNL MBI], è facile consolidare insieme tabelle simili provenienti da diversi database.

Ad esempio, potresti avere un `orders` tabella per `Market A`e simili `orders` tabella per `Market B`. [!DNL MBI] consente di consolidare entrambe le tabelle e di esaminare i dati dell’ordine aggregato da entrambi `Market A` e `B`, oltre a segmentarla per un mercato specifico.

Per il consolidamento delle tabelle, le tabelle di input devono essere **con struttura simile**. In altre parole, tutte le tabelle di input devono contenere le colonne di dati richieste nella tabella consolidata.

Questo argomento illustra alcuni dei casi d’uso più comuni per le tabelle consolidate e i passaggi successivi necessari per crearne di nuovi.

## Recommendations per quando utilizzare le tabelle consolidate

Di seguito viene illustrato quando potrebbe essere opportuno utilizzare tabelle consolidate nel sistema.

### Integrazione di dati da più siti web

Se vendi i tuoi prodotti con marchi e siti web diversi, è probabile che le tabelle per ogni marchio o sito web siano strutturate in modo simile.

Ad esempio, potresti avere un `orders` tabella per il sito web `A` e un separato, ma simile, `orders` tabella per il sito web `B`. In questa situazione, può essere utile consolidare `orders` tabelle dal sito web `A` e `B` in modo da poter esaminare i ricavi consolidati e il numero di ordini provenienti dal sito web `A` e `B`, oltre a poter segmentare le metriche per questi due siti web.

### Integrazione di dati legacy

Molte aziende hanno reintegrato i loro database in un&#39;unica volta e i dati del vecchio database non sempre vengono convertiti nel nuovo sistema. È possibile utilizzare tabelle consolidate per unire le colonne chiave delle tabelle precedenti a quelle del sistema attivo. Questo consente di eseguire un’analisi unificata dei dati durante l’intera cronologia.

### Combinazione di eventi per l’analisi attiva degli utenti

Immagina un sito web dove gli utenti possono fare diverse cose: fai un sondaggio, fai un gioco, fai un acquisto, fai riferimento a un amico e così via. In genere, ciascuno di questi eventi viene memorizzato nella propria tabella. Ciò rende difficile condurre un&#39;analisi del numero di utenti distinti che in un dato periodo di tempo hanno intrapreso almeno una azione di qualsiasi tipo.

È possibile utilizzare tabelle consolidate per creare un elenco unificato di tutti gli utenti e quando si è verificato uno di questi eventi. È quindi possibile eseguire query sulla tabella consolidata per eseguire facilmente tale analisi.

Come per tutte le altre tabelle del data warehouse, è possibile aggiungere ulteriori colonne per fornire grafici e analisi di tipo diverso.

## Creazione, visualizzazione o aggiornamento di una tabella consolidata

Se ti interessa aggiungere una tabella consolidata al data warehouse, contatta [!DNL MBI] [supporto](../guide-overview.md).

>[!NOTE]
>
>Poiché le tabelle consolidate non sono visualizzabili in `Data Warehouse Manager`, la visualizzazione e l’aggiornamento di queste tabelle possono essere eseguiti solo da [!DNL MBI] supporto.
