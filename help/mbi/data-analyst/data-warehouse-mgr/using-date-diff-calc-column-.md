---
title: Utilizzo della colonna calcolata differenza di data
description: Scopri lo scopo e gli usi della colonna calcolata Differenza di data .
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 2%

---

# Colonna calcolata Differenza data

In questo argomento vengono illustrati lo scopo e gli usi `Date Difference` colonna calcolata disponibile nella colonna **[!DNL Manage Data > Data Warehouse]** pagina. Di seguito è riportata una spiegazione di ciò che fa, seguita da un esempio, e la meccanica della sua creazione.

**Spiegazione**

La `Date Difference` tipo di colonna: trova il tempo tra due eventi appartenenti a un singolo record, in base alle marche temporali dell’evento. Il valore non elaborato calcolato in questa colonna è espresso in secondi, ma verrà convertito automaticamente in minuti, ore, giorni e così via per la visualizzazione nei rapporti. Tuttavia, se utilizzato come filtro/gruppo da, è necessario utilizzare il valore in secondi.

A `date difference` la colonna calcolata può essere utilizzata per creare una metrica che calcola il tempo medio o mediano tra due eventi, ad esempio il tempo medio tra la registrazione al cliente e i primi ordini.

**Esempio**

| **`id`** | **`timestamp_1`** | **`timestamp_2`** | **`Seconds between timestamp_2 and timestamp_1`** |
|--- |--- |--- |--- |
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style=&quot;table-layout:auto&quot;}


Nell’esempio precedente, la `Date Difference` è `Seconds between timestamp_2 and timestamp_1` colonna. Esegue il calcolo `timestamp_2 minus timestamp_1`.

**Meccanica**

I passaggi seguenti descrivono come creare un `Date Difference` colonna.

1. Passa a **[!DNL Manage Data > Data Warehouse]** pagina.
1. Passa alla tabella in cui desideri creare la colonna.
1. Fai clic su **[!UICONTROL Create a Column]** e configura la colonna come segue:
   * Seleziona `Column Definition Type` > `Same Table`
   * Seleziona `Column Definition Equation` > `DATE_DIFF = (Ending DATETIME - Starting DATETIME)`
   * Seleziona `Ending DATETIME` column > Choose the ending datetime field, che in genere è l’evento che si verifica più tardi
   * Seleziona `Starting DATETIME` colonna** > Scegli il campo datetime iniziale, che in genere è l’evento che si verifica prima

1. Immetti un nome alla colonna e fai clic su **[!UICONTROL Save]**.
1. La colonna sarà disponibile per l’utilizzo *immediatamente*.

Ad esempio, l’esempio seguente è configurato per calcolare il `Seconds between order date and customer's creation date`:

![](../../assets/date_diff.png)
