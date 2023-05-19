---
title: Differenze tra SQL e Data Warehouse Manager
description: Scopri le differenze tra SQL e Data Warehouse Manager.
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Differenze tra [!DNL SQL] e [!DNL Data Warehouse Manager]

Esistono due differenze chiave tra le colonne create in [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) e quelli creati utilizzando [[!DNL Data Warehouse Manager]](../data-warehouse-mgr/creating-calculated-columns.md). Uno è la dipendenza dai cicli di aggiornamento, l&#39;altro è il modo in cui le colonne vengono salvate nel tuo account.

## Colonne in [!DNL SQL Report Builder]

Le colonne non dipendono dai cicli di aggiornamento, pertanto non è più necessario attenderne il completamento prima di poter eseguire l’iterazione sulla colonna. Se si commette un errore, sono necessarie solo poche pressioni per correggerlo, senza attendere che vengano completati due aggiornamenti prima di poter tornare al lavoro.

>[!IMPORTANT]
>
>Le colonne create utilizzando [!DNL SQL] non vengono salvati nella Data Warehouse. È sempre possibile accedere alla query contenente la colonna, ma se si desidera utilizzare la colonna in più report, è necessario ricrearla nella query per ogni report. Ciò significa che le colonne create utilizzando [!DNL SQL] L&#39;editor non può essere utilizzato nel [!DNL Report Builder].

## Colonne in Gestione Date Warehouse

Le colonne dipendono dai cicli di aggiornamento, pertanto è necessario completare un ciclo completo prima di modificarle. Queste colonne vengono salvate in Gestione Date Warehouse e possono essere utilizzate nelle [!DNL Report Builder] o [!DNL SQL Report Builder].
