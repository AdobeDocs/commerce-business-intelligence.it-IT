---
title: Colonna calcolata numero evento
description: Scopri lo scopo e gli usi della colonna calcolata Numero evento .
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# Colonna calcolata numero evento

In questo argomento vengono illustrati lo scopo e gli usi `Event Number` colonna calcolata disponibile nella colonna **[!DNL Manage Data > Data Warehouse]** pagina. Di seguito è riportata una spiegazione di ciò che fa, seguita da un esempio, e la meccanica della sua creazione.

**Spiegazione**

La `Event Number` tipo di colonna: identifica la sequenza in cui si sono verificati gli eventi per una particolare **proprietario dell&#39;evento**, come `customer` o `user`. Se si ha familiarità con SQL, questo tipo di colonna è identico al `RANK` funzione . Può essere utilizzato per osservare le differenze di comportamento tra gli eventi della prima volta, gli eventi di ripetizione o i nth eventi nei dati.

In caso di legami, questa colonna contiene lo stesso **rango** per gli eventi associati e ignora i numeri successivi. Ad esempio, se classificasse i numeri 5,8,10,10,12, i numeri sarebbero 1,2,3,3,5.

Il caso d’uso più comune di questa colonna è quello di analizzare i nuovi acquirenti e gli acquirenti ripetuti. La prima volta che gli acquirenti vengono identificati aggiungendo un filtro (a una metrica o a un report) in `Customer's order number` 1. `Customer's order number` è una colonna del tipo `Event Number`.

**Esempio**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 01/01/2015:00:00 | 1 |
| **2 | B | 01/01/2015:30:00 | 1 |
| **3 | A | 01/01/2015:00:00 | 2 |
| **4 | A | 01/01/2015:00:00 | 3 |
| **5 | B | 01/03/2015:00:00 | 2 |

Nell’esempio precedente, la colonna `Owner's event number` è un `Event Number` colonna. Classifica gli eventi del proprietario nell’ordine in cui si sono verificati (in base al `timestamp` ).

Ad esempio, considera tutte le righe in cui `owner_id = A`. La prima riga della tabella è la marca temporale più recente per questo proprietario, seguita dalla terza riga della tabella, seguita dalla quarta riga della tabella.

**Meccanica**

Di seguito sono riportate alcune istruzioni sulla creazione di un `Event Number` colonna:

1. Passa a **[!UICONTROL Manage Data > Data Warehouse]** pagina.
1. Passa alla tabella in cui desideri creare la colonna.
1. Fai clic su **[!UICONTROL Create a Column]** e scegli la `EVENT_NUMBER (…)` tipo di colonna: in `Same Table` sezione .
1. Il primo menu a discesa `Event Owner` specifica l’entità per la quale deve essere determinata la classificazione. Nel caso di `Customer's order number`, un identificatore del cliente come `customer_id` o `customer_email` sarebbe `Event Owner`.
1. Il secondo menu a discesa `Event Rank` specifica la colonna che applica la sequenza che determina il rango della riga. Nel caso di `Customer's order number`, `created_at` la marca temporale è `Event Rank`.
1. Sotto la `Options` a discesa, puoi aggiungere filtri per escludere le righe dalla considerazione. Le righe escluse avranno un `NULL` per questa colonna.
1. Immetti un nome alla colonna e fai clic su **[!UICONTROL Save]**.
1. La colonna sarà disponibile per l’utilizzo _immediatamente._
