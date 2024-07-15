---
title: Tempo medio per il primo rapporto acquisti
description: Scopri come utilizzare il rapporto Tempo medio per il primo acquisto.
exl-id: c18734ce-0ae0-4e84-b9d0-eb2c21a5c3a5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 330832e2668024b00edb2b7c49b92bb042bd004a
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Tempo medio per il primo rapporto acquisti

Molti Adobi di clienti hanno una metrica e un grafico denominati `Average time to first purchase`, che mostra il tempo medio tra la data di registrazione di un gruppo di utenti e la data del primo acquisto. I dati tendono quasi invariabilmente a scendere man mano che il tempo si avvicina al presente.

![tempo medio per il primo ordine](../../assets/average-time-to-first-order.png)

Questo perché questi nuovi clienti non hanno ancora avuto l’opportunità di generare acquisti effettuati oltre un mese dalla data di adesione. Poiché gli utenti che non hanno mai effettuato un acquisto non sono inclusi per nulla (fino a quando non effettuano un acquisto), questo distorce la media verso il basso per i gruppi più recenti di clienti.

Esistono altri modi potenziali per esaminare questa metrica che introducono minore distorsione. Esplora un esempio.

## Esempio: eseguire un&#39;analisi `cohort` dei primi ordini

È possibile che nel dashboard di `Users` sia presente un grafico denominato `Time to first order cohort`. Questo report utilizza la metrica `Distinct buyers`, raggruppa gli utenti di `cohort` settimane o mesi di registrazione e mostra il rapporto (tra `0` e `1`) tra gli utenti che hanno effettuato un primo acquisto nelle settimane o nei mesi successivi alla registrazione.

Il grafico potrebbe mostrare che per gli utenti registrati a dicembre 2014, `0.56` (o `56%`) ha effettuato un primo ordine entro il mese 2 (ad esempio, gennaio 2015).

Questa analisi per coorte è un buon indicatore del tasso di attivazione dell’utente nel tempo. Se questo grafico inizia ad appiattirsi o a raggiungere un plateau e la conversione verso gli acquirenti non si avvicina ancora al 100%, potrebbe essere il momento di attivare gli utenti rimanenti tramite campagne e-mail.
