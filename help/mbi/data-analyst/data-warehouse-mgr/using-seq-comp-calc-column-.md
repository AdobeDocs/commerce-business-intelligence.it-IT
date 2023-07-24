---
title: Colonna calcolata confronto sequenziale
description: Scopri lo scopo e gli utilizzi della colonna calcolata Confronto sequenziale.
exl-id: 625062b4-f05d-42aa-94c3-729b39c7d728
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 2%

---

# Colonna calcolata confronto sequenziale

Questo argomento illustra lo scopo e gli utilizzi del `Sequential Comparison` colonna calcolata disponibile nella **[!DNL Manage Data > Data Warehouse]** pagina. Di seguito è riportata una spiegazione di ciò che fa, seguito da un esempio e dalla meccanica della sua creazione.

**Spiegazione**

Il `Sequential Comparison` tipo di colonna: trova la differenza tra eventi consecutivi. Il tipo di `Sequential Comparison` colonna è il valore `Seconds since previous order` colonna. Per questa colonna sono necessari tre input:

1. `Event Owner`: questo input determina l’entità per la quale sono raggruppate le righe. Ad esempio, nel `Seconds since previous order` , il proprietario dell&#39;evento è il cliente, perché si desidera trovare il numero di secondi dall&#39;ordine precedente dello stesso cliente.
1. `Event Date`: questo input applica la sequenza di eventi. Nel caso di `Seconds since previous order`, la colonna contenente la marca temporale dell’ordine deve essere la `Event Date`. Questo input è sempre una marca temporale.
1. `Value to Compare`: questo input è il valore effettivo da confrontare. Sottrae il valore della riga precedente dal valore della riga corrente. Pertanto, viene chiamata una colonna che rileva la differenza di tempo tra gli ordini successivi di un cliente `Seconds since previous order`. Questo input non deve essere una marca temporale. Un esempio di mancata marca temporale consiste nel trovare la differenza nel valore dell’ordine tra ordini successivi di un cliente.

**Esempio**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|--- |--- |--- |--- |
| **`1`** | A | 2015-01-01 00:00:00 | NULL |
| **`2`** | B | 2015-01-01 00:30:00 | NULL |
| **`3`** | A | 2015-01-01 02:00:00 | 7200 |
| **`4`** | A | 2015-01-02 13:00:00 | 126000 |
| **`5`** | B | 2015-01-03 13:00:00 | 217800 |

Nell’esempio precedente, `Seconds since owner's previous event` è il `Sequential Comparison` colonna calcolata. Per `owner_id = A`, per prima cosa identifica una sequenza basata su `timestamp` e quindi sottrae il valore dell&#39;evento precedente `timestamp` dalla marca temporale dell’evento corrente. Nella terza riga della tabella: la seconda riga per `owner_id A` - il valore di `Seconds since owner's previous event` è il numero di secondi tra &quot;2015-01-01 02:00&quot; e &quot;2015-01-01 00&quot;:00:00&#39;. Questa differenza è uguale a due ore = 7200 secondi.

Per questo tipo di colonna calcolata, la riga corrispondente al primo evento del proprietario ha un `NULL` valore.

**Meccanica**

Per creare un **Numero evento** colonna:

1. Accedi a **[!DNL Manage Data > Data Warehouse]** pagina.

1. Passare alla tabella in cui si desidera creare la colonna.

1. Clic **[!UICONTROL Create New Column]** nell’angolo superiore destro.

1. Seleziona `Same Table` come `Definition Type` (se le colonne che desideri confrontare non si trovano nella stessa tabella, potrebbe essere necessario riposizionarle).

1. Seleziona `SEQUENTIAL_COMPARISON` come `Column Definition Equation`.

1. Scegli gli input, come spiegato in precedenza:
   - `Event Owner`
   - `Event Date`
   - `Value to Compare`

1. È inoltre possibile aggiungere filtri per escludere le righe dalla considerazione. Le righe escluse presentano `NULL` per questa colonna.

1. Immetti un nome per la colonna nella parte superiore della pagina e fai clic su **[!UICONTROL Save]**.

1. È possibile utilizzare la colonna *immediatamente*.

![SEC](../../assets/SEC_new.png)
