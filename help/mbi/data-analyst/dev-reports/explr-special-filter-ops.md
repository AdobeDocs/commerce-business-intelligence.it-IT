---
title: Operatori di filtro speciali
description: Scopri alcuni operatori speciali utilizzati nei filtri per creare un rapporto o una metrica.
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# Opzioni filtro

In questo articolo esploreremo alcuni particolari `operators` utilizzato in `filters` quando [creazione di un report](../../tutorials/using-visual-report-builder.md){: target=&quot;_blank&quot;} o [creazione di una metrica](../../data-user/reports/ess-manage-data-metrics.md){: target=&quot;_blank&quot;}.

## `Filter Operators`

* `LIKE` per la corrispondenza dei pattern. Deve essere utilizzato insieme ai caratteri jolly % (per un carattere jolly con un numero variabile di lettere) o _ (per un carattere jolly di una singola lettera).  Ad esempio, la restrizione `LIKE \_ake%` restituirebbe true per `Jake Stein`, `Jake Smith`oppure `Fake Smith`.  Restituisce false per `Drake Smith`.

* `NOT LIKE` è simile alla corrispondenza del pattern riportata sopra, ma verifica i pattern non corrispondenti.

* `IS` controlla se la colonna è `NULL`o vuoto.

* `IS NOT` è simile al `IS` , ma verifica la presenza di colonne non NULL.

* `IN` verifica la presenza di un valore in un elenco separato da virgole. (ad esempio, &quot;Colore `IN` rosso, arancione&quot; è l&#39;equivalente del colore `equal to` rosso o colore `equal to` arancione).

* `NOT IN` è simile a `IN` ma controlla l&#39;assenza di un valore.
