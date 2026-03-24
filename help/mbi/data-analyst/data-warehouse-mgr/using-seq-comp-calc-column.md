---
title: Colonna calcolata confronto sequenziale
description: Scopri lo scopo e gli utilizzi della colonna calcolata Confronto sequenziale.
exl-id: 625062b4-f05d-42aa-94c3-729b39c7d728
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/7fCAFSOningY5B-aM8A1w9icX47qjUBsIO47KoRDTDk
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 413
ht-degree: 0%

---

# Colonna calcolata confronto sequenziale

Questo argomento descrive lo scopo e gli utilizzi della colonna calcolata `Sequential Comparison` disponibile nella pagina **[!DNL Manage Data > Data Warehouse]**. Di seguito è riportata una spiegazione di ciò che fa, seguito da un esempio e dalla meccanica della sua creazione.

**Spiegazione**

Tipo di colonna `Sequential Comparison`: trova la differenza tra eventi consecutivi. Il tipo più comune di colonna `Sequential Comparison` è la colonna `Seconds since previous order`. Per questa colonna sono necessari tre input:

1. `Event Owner`: questo input determina l&#39;entità per cui le righe sono raggruppate. Ad esempio, nella colonna `Seconds since previous order` il proprietario dell&#39;evento è il cliente, perché si desidera trovare il numero di secondi dall&#39;ordine precedente dello stesso cliente.
1. `Event Date`: questo input applica la sequenza di eventi. Nei casi di `Seconds since previous order`, la colonna contenente la marca temporale dell&#39;ordine deve essere `Event Date`. Questo input è sempre una marca temporale.
1. `Value to Compare`: questo input è il valore effettivo da confrontare. Sottrae il valore della riga precedente dal valore della riga corrente. Pertanto, una colonna che rileva la differenza di tempo tra gli ordini successivi di un cliente è denominata `Seconds since previous order`. Questo input non deve essere una marca temporale. Un esempio di mancata marca temporale consiste nel trovare la differenza nel valore dell’ordine tra ordini successivi di un cliente.

**Esempio**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|--- |--- |--- |--- |
| **`1`** | A | 00:00:00 01/01/2015 | NULL |
| **`2`** | B | 00:30:00 01/01/2015 | NULL |
| **`3`** | A | 01/01/02/00:00: | 7200 |
| **`4`** | A | 02/01/2015 13/00:00: | 126000 |
| **`5`** | B | 03/01/2015 13/0}:00: | 217800 |

Nell&#39;esempio precedente, `Seconds since owner's previous event` è la colonna calcolata `Sequential Comparison`. Per `owner_id = A`, identifica innanzitutto una sequenza basata sulla colonna `timestamp`, quindi sottrae il `timestamp` dell&#39;evento precedente dalla marca temporale dell&#39;evento corrente. Nella terza riga della tabella, la seconda riga per `owner_id A`, il valore di `Seconds since owner's previous event` è il numero di secondi tra &#39;2015-01-01 02:00&#39; e &#39;2015-01-01 00:00:00&#39;. Questa differenza è uguale a due ore = 7200 secondi.

Per questo tipo di colonna calcolato, la riga corrispondente al primo evento del proprietario ha un valore `NULL`.

**Meccanica**

Per creare una colonna **Numero evento**:

1. Passare alla pagina **[!DNL Manage Data > Data Warehouse]**.

1. Passare alla tabella in cui si desidera creare la colonna.

1. Fare clic su **[!UICONTROL Create New Column]** nell&#39;angolo superiore destro.

1. Selezionare `Same Table` come `Definition Type` (se le colonne che si desidera confrontare non si trovano nella stessa tabella, potrebbe essere necessario riposizionarle).

1. Seleziona `SEQUENTIAL_COMPARISON` come `Column Definition Equation`.

1. Scegli gli input, come spiegato in precedenza:
   - `Event Owner`
   - `Event Date`
   - `Value to Compare`

1. È inoltre possibile aggiungere filtri per escludere le righe dalla considerazione. Le righe escluse hanno un valore `NULL` per questa colonna.

1. Specificare un nome per la colonna nella parte superiore della pagina e fare clic su **[!UICONTROL Save]**.

1. La colonna è disponibile per l&#39;utilizzo *immediato*.

![SEC](../../assets/SEC_new.png)
