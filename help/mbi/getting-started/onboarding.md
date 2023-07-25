---
title: Onboarding di Adobe Commerce Intelligence
description: Scopri come effettuare l’onboarding di Adobe Commerce Intelligence.
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# Onboarding [!DNL Adobe Commerce Intelligence]

Domande sull’onboarding relative a `store` e `database` Le impostazioni consentono di configurare correttamente la generazione rapporti. Con queste risposte, Adobe distribuisce i report personalizzati in base alla configurazione del negozio.

## Impostazioni store

- *Il tuo negozio accetta il pagamento degli ospiti?* - Seleziona **sì** se consenti ai clienti di effettuare un acquisto dal tuo negozio senza registrarti a un account.

- `Timezone` - Selezionare la `timezone` che desideri visualizzare nei rapporti.

- `Currency` - Selezionare la `currency` che il tuo negozio funzioni in.

- `Your week starts on...` - Selezionare il giorno della settimana per il quale si desidera impostare l&#39;inizio della settimana nei report.

- *Quale versione di Commerce utilizzi?* - Selezionare la `currency` che il tuo negozio funzioni in.

- *Il tuo punto vendita è nell&#39;Unione Europea?* - Se risponde `Yes` per rispondere a questa domanda, Adobe ospita la tua Data Warehouse e tutti i tuoi dati nell’Unione Europea, in conformità con il RGPD.

## Impostazioni del database

- `Database name` - Che cos&#39;è *nome del [!DNL MySQL] database* dove risiedono i dati transazionali di Commerce?

- `Table prefix (optional)` : le tabelle contenute nel database Commerce sono precedute da un elemento (ad esempio, `store_`)? Questo non avviene normalmente, ma si tratta di una personalizzazione che può essere effettuata.
