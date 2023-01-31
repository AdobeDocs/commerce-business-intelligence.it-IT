---
title: Differenze tra SQL e Data Warehouse Manager
description: Scopri le differenze tra SQL e Data Warehouse Manager.
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Differenze tra SQL e Data Warehouse Manager

Esistono due differenze chiave tra le colonne create nel [Report Builder SQL](../dev-reports/sql-rpt-bldr.md) e quelli creati utilizzando [Data Warehouse Manager](../data-warehouse-mgr/creating-calculated-columns.md): una è la dipendenza dai cicli di aggiornamento, l&#39;altra è la modalità di salvataggio delle colonne nel tuo account.

## Colonne in `SQL Report Builder`

Le colonne non dipendono dai cicli di aggiornamento, quindi non è più necessario attendere il completamento di uno prima di poter iterare sulla colonna. Se si fa un errore, ci vogliono solo pochi tasti per correggerlo - non più in attesa di due aggiornamenti per concludere prima di poter tornare al lavoro.

>[!IMPORTANT]
>
>Le colonne create con l&#39;editor SQL non vengono salvate nella Data Warehouse. Hai sempre accesso alla query contenente la colonna, ma se desideri utilizzare la colonna in più rapporti, devi ricrearla nella query per ogni rapporto. Ciò significa che le colonne create utilizzando l&#39;editor SQL non possono essere utilizzate nel tradizionale `Report Builder`.

## Colonne nel Gestore Date Warehouse

Le colonne dipendono dai cicli di aggiornamento, pertanto è necessario completare un ciclo completo prima di modificarli. Queste colonne vengono salvate in Data Warehouse Manager e possono essere utilizzate nelle `Report Builder` o `SQL Report Builder`.
