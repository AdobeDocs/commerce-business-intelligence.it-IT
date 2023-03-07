---
title: Ottimizzazione delle query SQL
description: Scopri come ottimizzare le query SQL.
exl-id: 2782c707-6a02-4e5d-bfbb-eff20659fbb2
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 0%

---

# Ottimizzare le query SQL

Il Report Builder SQL consente di eseguire query e iterazioni su tali query in qualsiasi momento. Questa opzione è utile quando è necessario modificare una query senza dover attendere il completamento di un ciclo di aggiornamento prima di realizzare che è necessario aggiornare una colonna o un report creato.

Prima dell’esecuzione di una query [[!DNL MBI] stima il costo](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/sql-queries-explain-cost-errors.html?lang=en). Il costo considera il tempo e il numero di risorse necessari per eseguire una query. Se il costo è ritenuto troppo elevato o se il numero di righe restituite supera i limiti MBI, la query non riesce. Per eseguire query sulla Data Warehouse, in modo da garantire la scrittura delle query più semplici possibile, l’Adobe consiglia quanto segue.

## Utilizzo di SELECT o selezione di tutte le colonne

La selezione di tutte le colonne non consente di eseguire una query tempestiva e semplice. Query che utilizzano `SELECT *` L&#39;esecuzione può richiedere un po&#39; di tempo, soprattutto se la tabella contiene molte colonne.

Per questo motivo, l’Adobe consiglia di evitare l’utilizzo di `SELECT *` se possibile e includi solo le colonne necessarie:

| **Invece...** | **Prova questo!** |
|-----|-----|
| ![](../../mbi/assets/Select_all_1.png) | ![](../../mbi/assets/Select_all_2.png) |

{style="table-layout:auto"}

## Utilizzo dei join esterni completi

I join esterni selezionano la totalità di entrambe le tabelle collegate in join, il che aumenta il costo di calcolo della query. Ciò significa che l’esecuzione della query richiede più tempo ed è più probabile che non riesca, in quanto la restituzione dei risultati potrebbe richiedere più tempo del limite di esecuzione.

Invece di utilizzare questo tipo di join, è consigliabile utilizzare un inner join o left join. I join interni restituiscono i risultati solo in presenza di una corrispondenza a livello di colonna tra le tabelle (ad esempio, `order_id` esiste sia in un tipico `customers` e `orders` tabella). I join a sinistra restituiscono tutti i risultati della tabella sinistra (prima) insieme ai risultati corrispondenti della tabella destra (seconda).

Osservare come è possibile riscrivere una query FULL OUTER JOIN:

| **Invece...** | **Prova questo!** |
|-----|-----|
| ![](../../mbi/assets/Full_Outer_Join_1.png) | ![](../../mbi/assets/Full_Outer_Join_2.png) |

{style="table-layout:auto"}

Queste query sono identiche in tutti i modi tranne che per il tipo di JOIN utilizzato.

## Utilizzo di più join

Sebbene sia possibile includere più join nella query, tenere presente che questo potrebbe determinare un aumento dei costi della query. Per evitare di raggiungere la soglia di costo, Adobe consiglia di evitare più join, ove possibile.

## Utilizzo dei filtri

Se possibile, utilizza i filtri. `WHERE` e `HAVING` Le clausole filtrano i risultati e forniscono solo i dati desiderati.

## Utilizzo dei filtri nelle clausole JOIN

Se si utilizza un filtro durante l&#39;esecuzione di un join, assicurarsi di applicarlo a entrambe le tabelle del join. Anche se è ridondante, questo riduce il costo di elaborazione della query e il tempo di esecuzione.

| **Invece...** | **Prova questo!** |
|-----|-----|
| ![](../../mbi/assets/Join_filters_1.png) | ![](../../mbi/assets/Join_filters_2.png) |

{style="table-layout:auto"}

## Utilizzo degli operatori

Quando scrivi le query, puoi utilizzare gli operatori &quot;meno costosi&quot; possibili. Ogni query ha un costo computazionale determinato dalle funzioni, dagli operatori e dai filtri che la compongono. Alcuni operatori richiedono un minore sforzo di calcolo, il che li rende meno costosi di altri.

Gli operatori di confronto (>, &lt;, = e così via) sono i meno costosi, seguiti da [TIPO. Operatori LIKE TO e POSIX](https://www.postgresql.org/docs/9.5/functions-matching.html) che sono gli operatori più costosi.

## Utilizzo di EXISTS e IN

Utilizzo di `EXISTS` rispetto a `IN` dipende dal tipo di risultati che stai tentando di restituire. Se sei interessato a un solo valore, utilizza `EXISTS` clausola invece di `IN`. `IN` viene utilizzato con elenchi di valori separati da virgole, che aumentano il costo di calcolo della query.

Quando `IN` vengono eseguite le query, il sistema deve prima elaborare la sottoquery (la `IN` ), quindi l&#39;intera query in base alla relazione specificata nella `IN` dichiarazione. `EXISTS` è molto più efficiente perché la query non deve essere eseguita più volte; viene restituito un valore true/false durante il controllo della relazione specificata nella query.

In parole povere: il sistema non deve elaborare tanto quando utilizza `EXISTS`.

| **Invece...** | **Prova questo!** |
|-----|-----|
| ![](../../mbi/assets/Exists_1.png) | ![](../../mbi/assets/Exists_2.png) |

{style="table-layout:auto"}

## Utilizzo di ORDER BY

`ORDER BY` è una funzione costosa in SQL e può aumentare in modo significativo il costo di una query. Se viene visualizzato un messaggio di errore che indica che il costo EXPLAIN della query è troppo elevato, provare a eliminare qualsiasi `ORDER BY`s dalla query, a meno che non sia necessario.

Questo non è per dire che `ORDER BY` non può essere utilizzato, solo che deve essere utilizzato solo quando necessario.

## Utilizzo di GROUP BY e ORDER BY

In alcune situazioni questo approccio non è conforme a quello che stai cercando di fare. La regola generale è che se utilizzi un’ `GROUP BY` e `ORDER BY`, è necessario disporre le colonne di entrambe le clausole nello stesso ordine. Ad esempio:

| **Invece...** | **Prova questo!** |
|-----|-----|
| ![](../../mbi/assets/Group_by_2.png) | ![](../../mbi/assets/Group_by_1.png) |

{style="table-layout:auto"}

## Ritorno a capo

Il modo migliore per imparare a scrivere SQL - e farlo in modo efficiente - è tramite tentativi ed errori. Per individuare le operazioni più appropriate, provare a ricreare alcuni report utilizzando solo l&#39;editor SQL.
