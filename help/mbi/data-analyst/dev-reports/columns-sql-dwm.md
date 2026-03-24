---
title: Differenze tra SQL e Data Warehouse Manager
description: Scopri le differenze tra SQL e Data Warehouse Manager.
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
TQID: https://experienceleague.adobe.com/aWLLAi9e-A6Di7AGujRNd79W7GqSRo5yIgmQRZAHOEQ
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 210
ht-degree: 0%

---

# Differenze tra [!DNL SQL] e [!DNL Data Warehouse Manager]

Esistono due differenze chiave tra le colonne create in [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) e quelle create utilizzando [[!DNL Data Warehouse Manager]](../data-warehouse-mgr/creating-calculated-columns.md). Uno è la dipendenza dai cicli di aggiornamento, l&#39;altro è il modo in cui le colonne vengono salvate nel tuo account.

## Colonne in [!DNL SQL Report Builder]

Le colonne non dipendono dai cicli di aggiornamento, pertanto non è più necessario attenderne il completamento prima di poter eseguire l’iterazione sulla colonna. Se si commette un errore, sono necessarie solo poche pressioni per correggerlo, senza attendere che vengano completati due aggiornamenti prima di poter tornare al lavoro.

>[!IMPORTANT]
>
>Le colonne create con l&#39;editor [!DNL SQL] non vengono salvate nel Data Warehouse. È sempre possibile accedere alla query contenente la colonna, ma se si desidera utilizzare la colonna in più report, è necessario ricrearla nella query per ogni report. Ciò significa che le colonne create con l&#39;editor [!DNL SQL] non possono essere utilizzate nel [!DNL Report Builder] tradizionale.

## Colonne in Data Warehouse Manager

Le colonne dipendono dai cicli di aggiornamento, pertanto è necessario completare un ciclo completo prima di modificarle. Queste colonne vengono salvate in Data Warehouse Manager e possono essere utilizzate nelle [!DNL Report Builder] o [!DNL SQL Report Builder] tradizionali.
