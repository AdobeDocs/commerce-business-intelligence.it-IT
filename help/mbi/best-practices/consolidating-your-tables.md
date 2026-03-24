---
title: Consolidare le tabelle
description: Scopri come consolidare le tabelle e i database.
exl-id: 6065bed3-fb84-4147-a223-92dc3e1b15a5
role: Admin, User
feature: Commerce Tables, Data Integration
TQID: https://experienceleague.adobe.com/HC5REx483htdfFigZPxcrZeD5byyJKk-beQqnEARt1E
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 469
ht-degree: 0%

---

# Consolidare le tabelle

Se si gestiscono più punti vendita o mercati, è possibile che database simili siano archiviati separatamente. In [!DNL Adobe Commerce Intelligence] è facile consolidare tabelle simili da database diversi.

Ad esempio, è possibile avere una tabella `orders` per `Market A` e una tabella `orders` simile per `Market B`. [!DNL Commerce Intelligence] può consolidare entrambe le tabelle e consentire di esaminare i dati aggregati dell&#39;ordine di `Market A` e `B`, oltre a segmentarli per mercato specifico.

Affinché il consolidamento delle tabelle funzioni, le tabelle di input devono essere **strutturate in modo simile**. In altre parole, tutte le tabelle di input devono contenere le colonne di dati richieste nella tabella consolidata.

In questo argomento vengono descritti alcuni dei casi d&#39;uso più comuni per le tabelle consolidate e i passaggi successivi necessari per la creazione di tabelle personalizzate.

## Raccomandazioni su quando utilizzare le tabelle consolidate

Di seguito viene descritto quando potrebbe essere appropriato utilizzare tabelle consolidate nel sistema.

### Integrazione di dati da più siti Web

Se vendi i tuoi prodotti con marchi e siti web diversi, è probabile che le tabelle per ogni marchio o sito web siano strutturate in modo simile.

È possibile ad esempio disporre di una tabella `orders` per il sito Web `A` e di una tabella `orders` separata ma simile per il sito Web `B`. In questa situazione, potrebbe essere utile consolidare le tabelle `orders` dal sito Web `A` e `B`. Questo consente di esaminare i ricavi consolidati e il numero di ordini dal sito Web `A` e `B`, oltre a poter segmentare le metriche da questi due siti Web.

### Integrazione dei dati legacy

Molte aziende hanno effettuato il refactoring dei propri database in un momento o in un altro e i dati del vecchio database non sempre vengono convertiti nel nuovo sistema. È possibile utilizzare le tabelle consolidate per unire le colonne chiave delle tabelle legacy a quelle del sistema attivo. Questo consente di condurre un’analisi unificata dei dati nel corso della storia.

### Combinazione di eventi per l&#39;analisi attiva degli utenti

Immagina un sito web in cui gli utenti possano fare diverse cose: rispondere a un sondaggio, giocare, acquistare, contattare un amico e così via. In genere, ciascuno di questi eventi viene memorizzato nella propria tabella. Questo rende difficile condurre un’analisi del numero di utenti distinti che hanno intrapreso almeno un’azione di qualsiasi tipo in un determinato periodo di tempo.

È possibile utilizzare le tabelle consolidate per creare un elenco unificato di tutti gli utenti e specificare quando si è verificato uno di questi eventi. Puoi quindi eseguire query sulla tabella consolidata per eseguire facilmente un’analisi di questo tipo.

Come per tutte le altre tabelle del Data Warehouse, è possibile aggiungere colonne aggiuntive per alimentare diversi tipi di grafici e analisi.

## Creazione, visualizzazione o aggiornamento di una tabella consolidata

Per aggiungere una tabella consolidata al Data Warehouse, contattare [!DNL Commerce Intelligence] [supporto](../guide-overview.md#Submitting-a-Support-Ticket).

>[!NOTE]
>
>Poiché le tabelle consolidate non sono visualizzabili in `Data Warehouse Manager`, è possibile visualizzarle e aggiornarle solo con il supporto di [!DNL Commerce Intelligence].
