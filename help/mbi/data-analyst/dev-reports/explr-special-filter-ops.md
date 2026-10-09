---
title: Operatori filtro speciali
description: Scopri alcuni operatori speciali utilizzati nei filtri durante la creazione di un rapporto o di una metrica.
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: 'https://experienceleague.adobe.com/xUfPCWqheQFIG9faVsA5PEWiyn6hLO-Rrm8jPzmaWiw'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: f842eedf-96a8-52c7-891d-4e56f7441a7e
    internal-label: Reports
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%
---
# Opzioni filtro

In questo argomento vengono illustrati alcuni `operators` speciali utilizzati in `filters` durante la [creazione di un report](../../tutorials/using-visual-report-builder.md){: target="_blank"} o la [creazione di una metrica](../../data-user/reports/ess-manage-data-metrics.md){: target="_blank"}.

## `Filter Operators`

* `LIKE` per corrispondenza pattern. Deve essere utilizzato con i caratteri jolly % (per un carattere jolly con un numero variabile di lettere) o _ (per un carattere jolly a lettera singola).  Ad esempio, la restrizione `LIKE \_ake%` restituirebbe true per `Jake Stein`, `Jake Smith` o `Fake Smith`.  Restituisce false per `Drake Smith`.

* `NOT LIKE` è simile alla corrispondenza del pattern di cui sopra, ma verifica quali pattern non corrispondono.

* `IS` verifica se la colonna è `NULL` o vuota.

* `IS NOT` è simile all&#39;operatore `IS` sopra, ma verifica la presenza di colonne non NULL.

* `IN` verifica la presenza di un valore in un elenco separato da virgole. (ad esempio, &quot;Colore `IN` rosso,arancione&quot; è l&#39;equivalente del colore `equal to` rosso OR `equal to` arancione).

* `NOT IN` è simile a `IN`, ma verifica l&#39;assenza di un valore.
