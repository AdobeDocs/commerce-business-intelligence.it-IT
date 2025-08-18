---
title: Colonna calcolata numero evento
description: Scopri lo scopo e gli utilizzi della colonna calcolata Numero evento.
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 1%

---

# Colonna calcolata numero evento

Questo argomento descrive lo scopo e gli utilizzi della colonna calcolata `Event Number` disponibile nella pagina **[!DNL Manage Data > Data Warehouse]**. Di seguito è riportata una spiegazione di ciò che fa, seguito da un esempio, e la meccanica della sua creazione.

**Spiegazione**

Il tipo di colonna `Event Number` identifica la sequenza in cui si sono verificati gli eventi per un determinato **proprietario evento**, ad esempio `customer` o `user`. Se si ha familiarità con SQL, questo tipo di colonna è identico alla funzione `RANK`. Può essere utilizzato per osservare le differenze di comportamento tra eventi nuovi, eventi ripetuti o eventi ennesimi nei dati.

In caso di parità, questa colonna contiene lo stesso **rango** per gli eventi associati e ignora i numeri successivi. Ad esempio, se si classificasse i numeri 5,8,10,10,12, i ranghi sarebbero 1,2,3,3,5.

Il caso d’uso più comune di questa colonna è quello di analizzare i nuovi acquirenti e gli acquirenti ripetuti. Gli acquirenti vengono identificati per la prima volta aggiungendo un filtro (a una metrica o a un report) il `Customer's order number` = 1. `Customer's order number` è una colonna di tipo `Event Number`.

**Esempio**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 00:00:00 01/01/2015 | 1 |
| **2 | B | 00:30:00 01/01/2015 | 1 |
| **3 | A | 01/01/02/00:00: | 2 |
| **4 | A | 02/01/2015 13/00:00: | 3 |
| **5 | B | 03/01/2015 13/0&rbrace;:00: | 2 |

Nell&#39;esempio precedente, la colonna `Owner's event number` è una colonna `Event Number`. Gli eventi del proprietario vengono classificati nell&#39;ordine in cui si sono verificati (in base alla colonna `timestamp`).

Considerare ad esempio tutte le righe in cui `owner_id = A`. La prima riga della tabella è la prima marca temporale per questo proprietario, seguita dalla terza riga della tabella, seguita dalla quarta riga della tabella.

**Meccanica**

Di seguito sono riportate alcune istruzioni sulla creazione di una colonna `Event Number`:

1. Passare alla pagina **[!UICONTROL Manage Data > Data Warehouse]**.

1. Passare alla tabella in cui si desidera creare la colonna.

1. Fare clic su **[!UICONTROL Create a Column]** e scegliere il tipo di colonna `EVENT_NUMBER (…)`: nella sezione `Same Table`.

1. Il primo elenco a discesa `Event Owner` specifica l&#39;entità per la quale deve essere determinato il rango. Nel caso in cui un `Customer's order number`, un identificatore cliente come `customer_id` o `customer_email` sarebbe `Event Owner`.

1. Il secondo elenco a discesa `Event Rank` specifica la colonna che applica la sequenza che determina la classificazione della riga. Nel caso in cui un `Customer's order number`, la marca temporale `created_at` sarebbe `Event Rank`.

1. Nel menu a discesa `Options` puoi aggiungere filtri per escludere le righe dall&#39;essere considerate. Le righe escluse hanno un valore `NULL` per questa colonna.

1. Specificare un nome per la colonna e fare clic su **[!UICONTROL Save]**.

1. La colonna è disponibile per l&#39;utilizzo immediato di _._
