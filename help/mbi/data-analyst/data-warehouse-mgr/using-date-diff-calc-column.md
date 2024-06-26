---
title: Utilizzo della colonna Differenza data calcolata
description: Scopri lo scopo e gli utilizzi della colonna calcolata Differenza data.
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 2433a614e9858684842804a0ae29fb67f0d41ead
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# Colonna Calcolata Differenza Data

Questo argomento illustra lo scopo e gli utilizzi del `Date Difference` colonna calcolata disponibile nella **[!DNL Manage Data > Data Warehouse]** pagina. Di seguito è riportata una spiegazione di ciò che fa, seguito da un esempio, e la meccanica della sua creazione.

**Spiegazione**

Il `Date Difference` tipo di colonna calcola il tempo tra due eventi appartenenti a un singolo record, in base ai timestamp dell’evento. Il valore non elaborato calcolato in questa colonna è in secondi, ma viene convertito automaticamente in minuti, ore, giorni e così via, per la visualizzazione nei rapporti. Tuttavia, se utilizzato come filtro/gruppo da, desideri utilizzare il valore in secondi.

A `date difference` la colonna calcolata può essere utilizzata per creare una metrica che calcola il tempo medio o mediano tra due eventi, ad esempio il tempo medio tra la registrazione del cliente e i suoi primi ordini.

**Esempio**

| **`id`** | **`timestamp_1`** | **`timestamp_2`** | **`Seconds between timestamp_2 and timestamp_1`** |
|--- |--- |--- |--- |
| `A` | 01/01/2015:00:00 | 01/01/2015 12:30:00 | 45000 |
| `B` | 08/01/2015:00:00 | 01/01/2015 10:00:00 | 7200 |

{style="table-layout:auto"}


Nell’esempio precedente, il `Date Difference` colonna è il valore `Seconds between timestamp_2 and timestamp_1` colonna. Esegue il calcolo `timestamp_2 minus timestamp_1`.

**Meccanica**

I passaggi seguenti descrivono come creare un `Date Difference` colonna.

1. Accedi a **[!DNL Manage Data > Data Warehouse]** pagina.
1. Passare alla tabella in cui si desidera creare la colonna.
1. Clic **[!UICONTROL Create a Column]** e configura la colonna come segue:
   * Seleziona `Column Definition Type` > `Same Table`
   * Seleziona `Column Definition Equation` > `DATE_DIFF = (Ending DATETIME - Starting DATETIME)`
   * Seleziona `Ending DATETIME` column > Scegli il campo data/ora finale, che in genere è l’evento che si verifica più tardi
   * Seleziona `Starting DATETIME` column** > Scegli il campo datetime iniziale, che in genere corrisponde all&#39;evento che si verifica prima

1. Assegna un nome alla colonna e fai clic su **[!UICONTROL Save]**.
1. È possibile utilizzare la colonna *immediatamente*.

Ad esempio, l’esempio seguente è configurato per calcolare il `Seconds between order date and customer's creation date`:

![](../../assets/date_diff.png)
