---
title: Tempo medio per il primo rapporto acquisti
description: Scopri come utilizzare il rapporto Tempo medio per il primo acquisto.
exl-id: c18734ce-0ae0-4e84-b9d0-eb2c21a5c3a5
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/LWbb4E4IMPQd-hUpsylSGt4lgrrvYI1VUhmovjvcfu4
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 258
ht-degree: 0%

---

# Tempo medio per il primo rapporto acquisti

Molti clienti Adobe dispongono di una metrica e di un grafico denominati `Average time to first purchase` che mostrano il tempo medio tra la data di registrazione di un gruppo di utenti e la data del primo acquisto. I dati tendono quasi invariabilmente a scendere man mano che il tempo si avvicina al presente.

![tempo medio per il primo ordine](../../assets/average-time-to-first-order.png)

Questo perché questi nuovi clienti non hanno ancora avuto l’opportunità di generare acquisti effettuati oltre un mese dalla data di adesione. Poiché gli utenti che non hanno mai effettuato un acquisto non sono inclusi per nulla (fino a quando non effettuano un acquisto), questo distorce la media verso il basso per i gruppi più recenti di clienti.

Esistono altri modi potenziali per esaminare questa metrica che introducono minore distorsione. Esplora un esempio.

## Esempio: eseguire un&#39;analisi `cohort` dei primi ordini

È possibile che nel dashboard di `Users` sia presente un grafico denominato `Time to first order cohort`. Questo report utilizza la metrica `Distinct buyers`, raggruppa gli utenti di `cohort` settimane o mesi di registrazione e mostra il rapporto (tra `0` e `1`) tra gli utenti che hanno effettuato un primo acquisto nelle settimane o nei mesi successivi alla registrazione.

Il grafico potrebbe mostrare che per gli utenti registrati a dicembre 2014, `0.56` (o `56%`) ha effettuato un primo ordine entro il mese 2 (ad esempio, gennaio 2015).

Questa analisi per coorte è un buon indicatore del tasso di attivazione dell’utente nel tempo. Se questo grafico inizia ad appiattirsi o a raggiungere un plateau e la conversione verso gli acquirenti non si avvicina ancora al 100%, potrebbe essere il momento di attivare gli utenti rimanenti tramite campagne e-mail.
