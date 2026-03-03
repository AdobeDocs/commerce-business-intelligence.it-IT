---
title: Onboarding di Adobe Commerce Intelligence
description: Scopri come effettuare l’onboarding di Adobe Commerce Intelligence.
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 5e80ff8f8ec76996b88a22b115be696b110581be
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# Onboarding di [!DNL Adobe Commerce Intelligence]

Le domande sull&#39;onboarding relative alle impostazioni `store` e `database` garantiscono la corretta configurazione dei rapporti. Con queste risposte, Adobe distribuisce report personalizzati in base alla configurazione del negozio.

## Impostazioni store

- *Il tuo store accetta l&#39;acquisto degli ospiti?* - Seleziona **sì** se consenti ai clienti di effettuare un acquisto dal tuo store senza registrarti a un account.

- `Timezone` - Seleziona `timezone` in cui visualizzare i tuoi report.

- `Currency` - Seleziona `currency` in cui opera il tuo archivio.

- `Your week starts on...` - Selezionare nei report il giorno della settimana di inizio settimana.

- *Quale versione di Commerce utilizzi?* - Seleziona `currency` in cui opera il tuo archivio.

- *Il tuo punto vendita si trova nell&#39;Unione Europea?* - Se rispondi a `Yes` a questa domanda, Adobe ospita il tuo Data Warehouse e tutti i tuoi dati nell&#39;Unione Europea, in conformità con il RGPD.

## Impostazioni del database

- `Database name` - Qual è il *nome del database [!DNL MySQL]* in cui risiedono i dati transazionali di Commerce?

- `Table prefix (optional)` - Le tabelle contenute nel database Commerce sono precedute da un elemento (ad esempio, `store_`)? Questo non avviene normalmente, ma si tratta di una personalizzazione che può essere effettuata.
