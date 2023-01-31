---
title: Tempo medio nel report del primo acquisto
description: Scopri come utilizzare il rapporto Tempo medio per il primo acquisto.
exl-id: c18734ce-0ae0-4e84-b9d0-eb2c21a5c3a5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Tempo medio nel report del primo acquisto

Molti dei nostri clienti hanno una metrica e un grafico denominati `Average time to first purchase`, che mostra il tempo medio tra la data di registrazione di un gruppo di utenti e la data di primo acquisto. I dati scendono quasi invariabilmente verso il basso man mano che il tempo si avvicina al presente.

![tempo medio al primo ordine](../../assets/average-time-to-first-order.png)

Questo perché questi nuovi clienti non hanno ancora avuto la possibilità di generare qualsiasi acquisto effettuato più di un mese dalla data di adesione. Poiché gli utenti che non hanno mai effettuato un acquisto non sono inclusi affatto (fino a quando non effettuano un acquisto), questo determina un calo della media per i gruppi di clienti più recenti.

Ci sono altri modi possibili per osservare questa metrica che introducono meno pregiudizi. Esploriamo un esempio.

## Esempio: Eseguire un `cohort` analisi dei primi ordinativi

Puoi avere un grafico sul tuo `Users` dashboard `Time to first order cohort`. Questo rapporto utilizza `Distinct buyers` metrica, raggruppa gli utenti per `cohort` settimane o mesi di registrazione e mostra il rapporto (tra `0` e `1`) degli utenti che hanno effettuato un primo acquisto nelle settimane o nei mesi successivi alla registrazione.

Il grafico può mostrarlo per gli utenti registrati a dicembre 2014, `0.56` o `56%`) ha effettuato un primo ordine per il mese 2 (ad esempio, gennaio 2015).

Questa analisi per coorte è un buon indicatore del tasso di attivazione dell’utente nel tempo. Se questo grafico inizia a appiattire o a appiattire e non sei ancora vicino alla conversione del 100% agli acquirenti, potrebbe essere il momento di attivare gli utenti rimanenti tramite le campagne e-mail.
