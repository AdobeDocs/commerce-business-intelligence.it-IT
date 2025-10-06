---
title: Utilizzo della colonna Differenza data calcolata
description: Scopri lo scopo e gli utilizzi della colonna calcolata Differenza data.
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Colonna Calcolata Differenza Data

Questo argomento descrive lo scopo e gli utilizzi della colonna calcolata `Date Difference` disponibile nella pagina **[!DNL Manage Data > Data Warehouse]**. Di seguito è riportata una spiegazione di ciò che fa, seguito da un esempio, e la meccanica della sua creazione.

**Spiegazione**

Il tipo di colonna `Date Difference` calcola il tempo tra due eventi appartenenti a un singolo record, in base ai timestamp dell&#39;evento. Il valore non elaborato calcolato in questa colonna è in secondi, ma viene convertito automaticamente in minuti, ore, giorni e così via, per la visualizzazione nei rapporti. Tuttavia, se utilizzato come filtro/gruppo da, desideri utilizzare il valore in secondi.

Una colonna calcolata `date difference` può essere utilizzata per creare una metrica che calcola il tempo medio o mediano tra due eventi, ad esempio il tempo medio tra la registrazione del cliente e i suoi primi ordini.

**Esempio**

| **`id`** | **`timestamp_1`** | **`timestamp_2`** | **`Seconds between timestamp_2 and timestamp_1`** |
|--- |--- |--- |--- |
| `A` | 00:00:00 01/01/2015 | 01/01/2015 12/00:30: | 45000 |
| `B` | 08:00:00 01/01/2015 | 01/01/2015 10/00:00: | 7200 |

{style="table-layout:auto"}


Nell&#39;esempio precedente, la colonna `Date Difference` è la colonna `Seconds between timestamp_2 and timestamp_1`. Esegue il calcolo `timestamp_2 minus timestamp_1`.

**Meccanica**

Nei passaggi seguenti viene descritto come creare una colonna `Date Difference`.

1. Passare alla pagina **[!DNL Manage Data > Data Warehouse]**.
1. Passare alla tabella in cui si desidera creare la colonna.
1. Fai clic su **[!UICONTROL Create a Column]** e configura la colonna come segue:
   * Seleziona `Column Definition Type` > `Same Table`
   * Seleziona `Column Definition Equation` > `DATE_DIFF = (Ending DATETIME - Starting DATETIME)`
   * Seleziona `Ending DATETIME` colonna > Scegli il campo data/ora finale, che in genere è l’evento che si verifica più tardi
   * Seleziona `Starting DATETIME` colonna** > Scegli il campo datetime iniziale, che in genere corrisponde all&#39;evento che si verifica prima

1. Specificare un nome per la colonna e fare clic su **[!UICONTROL Save]**.
1. La colonna è disponibile per l&#39;utilizzo *immediato*.

Ad esempio, l&#39;esempio seguente è configurato per calcolare `Seconds between order date and customer's creation date`:

![Configurazione del calcolo della differenza di data che mostra le selezioni della colonna datetime](../../assets/date_diff.png)
