---
title: Onboarding di Adobe Commerce Intelligence
description: Scopri come effettuare l’onboarding di Adobe Commerce Intelligence.
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
TQID: https://experienceleague.adobe.com/36wmj-7QyDdemBWFwHTf1NJkd4H06tED9FZPqhFz8eg
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
subfeature_v2:
  - id: bcbf87e7-9b75-4596-bffe-0f376b4c73a7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 194
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
