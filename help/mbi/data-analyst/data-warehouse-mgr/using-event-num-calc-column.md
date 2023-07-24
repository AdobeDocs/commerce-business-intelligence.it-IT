---
title: Colonna calcolata numero evento
description: Scopri lo scopo e gli utilizzi della colonna calcolata Numero evento.
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 3%

---

# Colonna calcolata numero evento

Questo argomento illustra lo scopo e gli utilizzi del `Event Number` colonna calcolata disponibile nella **[!DNL Manage Data > Data Warehouse]** pagina. Di seguito è riportata una spiegazione di ciò che fa, seguito da un esempio, e la meccanica della sua creazione.

**Spiegazione**

Il `Event Number` tipo di colonna identifica la sequenza in cui si sono verificati gli eventi per un particolare **proprietario evento**, come un `customer` o `user`. Se si ha familiarità con SQL, questo tipo di colonna è identico al `RANK` funzione. Può essere utilizzato per osservare le differenze di comportamento tra eventi nuovi, eventi ripetuti o eventi ennesimi nei dati.

In caso di parità, questa colonna contiene lo stesso **rango** per gli eventi associati e ignora i numeri successivi. Ad esempio, se si classificasse i numeri 5,8,10,10,12, i ranghi sarebbero 1,2,3,3,5.

Il caso d’uso più comune di questa colonna è quello di analizzare i nuovi acquirenti e gli acquirenti ripetuti. Gli acquirenti vengono identificati per la prima volta aggiungendo un filtro (a una metrica o a un rapporto) il `Customer's order number` = 1. `Customer's order number` è una colonna del tipo `Event Number`.

**Esempio**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 2015-01-01 00:00:00 | 1 |
| **2 | B | 2015-01-01 00:30:00 | 1 |
| **3 | A | 2015-01-01 02:00:00 | 2 |
| **4 | A | 2015-01-02 13:00:00 | 3 |
| **5 | B | 2015-01-03 13:00:00 | 2 |

Nell’esempio precedente, la colonna `Owner's event number` è un `Event Number` colonna. Classifica gli eventi del proprietario nell&#39;ordine in cui si sono verificati (in base al `timestamp` colonna).

Ad esempio, considera tutte le righe in cui `owner_id = A`. La prima riga della tabella è la prima marca temporale per questo proprietario, seguita dalla terza riga della tabella, seguita dalla quarta riga della tabella.

**Meccanica**

Di seguito sono riportate alcune istruzioni sulla creazione di un’ `Event Number` colonna:

1. Accedi a **[!UICONTROL Manage Data > Data Warehouse]** pagina.

1. Passare alla tabella in cui si desidera creare la colonna.

1. Clic **[!UICONTROL Create a Column]** e scegli la `EVENT_NUMBER (…)` tipo di colonna: sotto `Same Table` sezione.

1. Il primo elenco a discesa `Event Owner` specifica l&#39;entità per la quale deve essere determinata la classificazione. Se un `Customer's order number`, un identificativo del cliente come `customer_id` o `customer_email` sarebbe il `Event Owner`.

1. Secondo elenco a discesa `Event Rank` specifica la colonna che applica la sequenza che determina la classificazione della riga. Se un `Customer's order number`, il `created_at` timestamp sarebbe il `Event Rank`.

1. Sotto `Options` a discesa, puoi aggiungere filtri per escludere le righe dalla considerazione. Le righe escluse presentano `NULL` per questa colonna.

1. Assegna un nome alla colonna e fai clic su **[!UICONTROL Save]**.

1. È possibile utilizzare la colonna _immediatamente._
