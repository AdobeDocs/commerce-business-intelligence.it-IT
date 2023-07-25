---
title: Operatori filtro speciali
description: Scopri alcuni operatori speciali utilizzati nei filtri durante la creazione di un rapporto o di una metrica.
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Opzioni filtro

In questo argomento vengono illustrati alcuni aspetti speciali `operators` utilizzato in `filters` quando [creazione di un rapporto](../../tutorials/using-visual-report-builder.md){: target=&quot;_blank&quot;} o [creazione di una metrica](../../data-user/reports/ess-manage-data-metrics.md){: target=&quot;_blank&quot;}.

## `Filter Operators`

* `LIKE` per la corrispondenza dei pattern. Deve essere utilizzato con i caratteri jolly % (per un carattere jolly con un numero variabile di lettere) o _ (per un carattere jolly a lettera singola).  Ad esempio, la restrizione `LIKE \_ake%` restituirebbe true per `Jake Stein`, `Jake Smith`, o `Fake Smith`.  Restituisce false per `Drake Smith`.

* `NOT LIKE` è simile alla corrispondenza dei pattern di cui sopra, ma verifica quali pattern non corrispondono.

* `IS` controlla se la colonna è `NULL`, o vuoto.

* `IS NOT` è simile al `IS` sopra, ma verifica la presenza di colonne non NULL.

* `IN` verifica la presenza di un valore in un elenco separato da virgole. (ad esempio, &quot;Colore `IN` rosso,arancione&quot; è l’equivalente del colore `equal to` rosso OR `equal to` arancione).

* `NOT IN` è simile a `IN` ma verifica l&#39;assenza di un valore.
