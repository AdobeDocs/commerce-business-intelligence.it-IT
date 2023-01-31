---
title: Colonna calcolata del confronto sequenziale
description: Scopri lo scopo e gli utilizzi della colonna calcolata di Confronto sequenziale.
exl-id: 625062b4-f05d-42aa-94c3-729b39c7d728
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# Colonna calcolata del confronto sequenziale

In questo argomento vengono illustrati lo scopo e gli usi `Sequential Comparison` colonna calcolata disponibile nella colonna **[!DNL Manage Data > Data Warehouse]** pagina. Di seguito è riportata una spiegazione di ciò che fa, seguita da un esempio, e la meccanica della sua creazione.

**Spiegazione**

La `Sequential Comparison` tipo di colonna: trova la differenza tra eventi consecutivi. Il tipo più comune di `Sequential Comparison` è `Seconds since previous order` colonna. Sono necessari tre input per questa colonna:

1. `Event Owner`: Questo input determina l’entità per la quale le righe sono raggruppate. Ad esempio, nella `Seconds since previous order` Il proprietario dell’evento è il cliente, perché desideri trovare il numero di secondi dall’ordine precedente dello stesso cliente.
1. `Event Date`: Questo input applica la sequenza di eventi. Nel caso di `Seconds since previous order`, la colonna contenente la marca temporale dell’ordine deve essere `Event Date`. Questo input è sempre una marca temporale.
1. `Value to Compare`: Questo input è il valore effettivo da confrontare. Sottrae il valore della riga precedente dal valore della riga corrente. Viene quindi chiamata una colonna che rileva la differenza di tempo tra gli ordini successivi di un cliente `Seconds since previous order`. Questo input non deve necessariamente essere una marca temporale. Un esempio non di marca temporale è quello di trovare la differenza di valore dell&#39;ordine tra ordini successivi di un cliente.

**Esempio**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|--- |--- |--- |--- |
| **`1`** | A | 01/01/2015:00:00 | NULL |
| **`2`** | B | 01/01/2015:30:00 | NULL |
| **`3`** | A | 01/01/2015:00:00 | 7200 |
| **`4`** | A | 01/01/2015:00:00 | 126000 |
| **`5`** | B | 01/03/2015:00:00 | 217800 |

Nell’esempio precedente, `Seconds since owner's previous event` è `Sequential Comparison` colonna calcolata. Per `owner_id = A`, identifica prima una sequenza basata su `timestamp` e quindi sottrae l&#39;evento precedente `timestamp` dalla marca temporale dell’evento corrente. Nella terza riga della tabella - la seconda riga per `owner_id A` - il valore di `Seconds since owner's previous event` è il numero di secondi tra &#39;2015-01-01 02:00&#39; e &#39;2015-01-01 00:00:00&quot;. Questa differenza è uguale a 2 ore = 7200 secondi.

Per questo tipo di colonna calcolato, la riga corrispondente al primo evento del proprietario ha un `NULL` valore.

**Meccanica**

Per creare un **Numero evento** colonna:

1. Passa a **[!DNL Manage Data** > **Data Warehouse]** pagina.
1. Passa alla tabella in cui desideri creare la colonna.
1. Fai clic su **[!UICONTROL Create New Column]** in alto a destra dello schermo.
1. Seleziona `Same Table` come `Definition Type` (se le colonne che desideri confrontare non si trovano nella stessa tabella, potrebbe essere necessario spostarle).
1. Seleziona `SEQUENTIAL_COMPARISON` come `Column Definition Equation`.
1. Scegliete gli ingressi, come spiegato in precedenza:
   - `Event Owner`
   - `Event Date`
   - `Value to Compare`
1. È inoltre possibile aggiungere filtri per escludere le righe dall’esame. Le righe escluse avranno un valore NULL per questa colonna.
1. Specifica un nome per la colonna nella parte superiore della pagina e fai clic su **[!UICONTROL Save]**.
1. La colonna sarà disponibile per l’utilizzo *immediatamente*.

![SEC](../../assets/SEC_new.png)
