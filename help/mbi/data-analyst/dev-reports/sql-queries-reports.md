---
title: Traduzione di query SQL in report di Commerce Intelligence
description: Scopri come le query SQL vengono convertite nelle colonne calcolate e nelle metriche utilizzate in Commerce Intelligence.
exl-id: b3e3905f-6952-4f15-a582-bf892a971fae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# Traduzione di query SQL in Commerce Intelligence

Ti sei mai chiesto come le query SQL vengano tradotte in [colonne calcolate](../data-warehouse-mgr/creating-calculated-columns.md), [metriche](../../data-user/reports/ess-manage-data-metrics.md), e [rapporti](../../tutorials/using-visual-report-builder.md) utilizzi in [!DNL Commerce Intelligence]? Se l&#39;utente è un utente SQL con un numero elevato di richieste, informazioni su come SQL viene tradotto [!DNL Commerce Intelligence] consente di lavorare in modo più intelligente in [Gestione Date Warehouse](../data-warehouse-mgr/tour-dwm.md) e ottenere il massimo dal [!DNL Commerce Intelligence] piattaforma.

Alla fine di questo argomento, troverai **matrice di traduzione** per le clausole di query SQL e [!DNL Commerce Intelligence] elementi.

Inizia guardando una query generale:

| | |
|--- |--- |
| `SELECT` |  |
| `a,` | Report `group by` |
| `SUM(b)` | `Aggregate function` (colonna) |
| `FROM c` | `Source` tabella |
| `WHERE` |  |
| `d IS NOT NULL` | `Filter` |
| `AND time < X`<br><br> `AND time >= Y` | Report `time frame` |
| `GROUP BY a` | Report `group by` |

Questo esempio copre la maggior parte dei casi di traduzione, ma con alcune eccezioni. Immergiti, a partire da come `aggregate` la funzione viene tradotta.

## Aggregare funzioni

Funzioni di aggregazione (ad esempio, `count`, `sum`, `average`, `max`, `min`) nelle query assumono la forma di **aggregazioni di metriche** o **aggregazioni di colonne** in [!DNL Commerce Intelligence]. Il fattore di differenziazione è se è necessario un join per eseguire l&#39;aggregazione.

Osserva un esempio per ciascuno dei precedenti.

## Aggregazioni di metriche {#aggregate}

È necessaria una metrica durante l’aggregazione `within a single table`. Ad esempio, il `SUM(b)` la funzione di aggregazione dalla query precedente verrebbe probabilmente rappresentata da una metrica che somma la colonna `B`. 

Osserva un esempio specifico di come un `Total Revenue` la metrica potrebbe essere definita in [!DNL Commerce Intelligence]. Osserva la query seguente che tenti di tradurre:

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | `Metric operation` (colonna) |
| `FROM orders` | `Metric source` tabella |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Metrica `filter` |
| `AND created_at < X`<br><br>`AND created_at >= Y` | Metrica `timestamp` (e reporting `time range`) |

Passa al generatore di metriche facendo clic su **[!UICONTROL Manage Data** > ** Metriche **> **Crea nuova metrica]**, devi innanzitutto selezionare il `source` tabella, che in questo caso è il `orders` tabella. La metrica viene quindi impostata come mostrato di seguito:

![Aggregazione delle metriche](../../assets/Metric_aggregation.png)

## Aggregazioni di colonne

Una colonna calcolata è obbligatoria quando si aggrega una colonna unita in join da un&#39;altra tabella. Ad esempio, puoi avere una colonna creata nel tuo `customer` tabella denominata `Customer LTV`, che somma il valore totale di tutti gli ordini associati a quel cliente nel `orders` tabella.

La query per questa aggregazione potrebbe essere simile alla seguente:

|  |  |
|--- |--- |
| `Select` | |
| `c.customer_id` | Proprietario aggregato |
| `SUM(o.order_total) as "Customer LTV"` | Operazione di aggregazione (colonna) |
| `FROM customers c` | Tabella del proprietario aggregato |
| `JOIN orders o` | Tabella origine aggregazione |
| `ON c.customer_id = o.customer_id` | Percorso |
| `WHERE o.status = 'success'` | Aggregate filter |

Configurazione in [!DNL Commerce Intelligence] richiede l&#39;utilizzo del gestore della Data Warehouse, in cui si crea un percorso tra `orders` e `customers` quindi creare una colonna denominata `Customer LTV` nel tavolo del cliente.

Scopri come stabilire un nuovo percorso tra `customers` e `orders`. L’obiettivo finale è quello di creare una nuova colonna aggregata nel `customers` nella tabella, quindi passare alla `customers` nella Data Warehouse, quindi fai clic su **[!UICONTROL Create a Column** > ** Seleziona una definizione **> **SOMMA]**.

Successivamente, è necessario selezionare la tabella di origine. Se è presente un percorso per `orders` selezionala semplicemente dal menu a discesa. Tuttavia, se si sta creando un nuovo percorso, fare clic su **[!UICONTROL Create new path]** e viene visualizzata la schermata seguente:

![Crea nuovo percorso](../../assets/Create_new_path.png)

In questo caso è necessario considerare attentamente la relazione tra le due tabelle che si sta tentando di unire. In questo caso, è possibile che `Many` ordini associati a `One` cliente, quindi il `orders` la tabella è elencata nella `Many` , mentre il `customers` tabella selezionata nel `One` lato.

>[!NOTE]
>
>In entrata [!DNL Commerce Intelligence], a `path` equivale a un `Join` in SQL.

Una volta salvato il percorso, puoi creare `Customer LTV` colonna! Vedi di seguito:

![](../../assets/Customer_LTV.gif)

Ora che hai creato il nuovo `Customer LTV` colonna nel tuo `customers` tabella, è possibile creare una [aggregazione metrica](#aggregate) utilizzando questa colonna (ad esempio, per trovare l’LTV medio per cliente). È inoltre possibile `group by` o `filter` dalla colonna calcolata in un rapporto utilizzando metriche esistenti basate su `customers` tabella.

>[!NOTE]
>
>Per quest’ultimo, ogni volta che crei una nuova colonna calcolata, devi [aggiungere la dimensione alle metriche esistenti;](../data-warehouse-mgr/manage-data-dimensions-metrics.md) prima che sia disponibile come `filter` o `group by`.

Consulta [creazione di colonne calcolate](../data-warehouse-mgr/creating-calculated-columns.md) con il tuo responsabile Data Warehouse.

## `Group By` clausole

`Group By` le funzioni nelle query sono spesso rappresentate in [!DNL Commerce Intelligence] come colonna utilizzata per segmentare o filtrare un rapporto visivo. Ad esempio, ripercorriamo il `Total Revenue` che hai esplorato in precedenza, ma questa volta segmenta i ricavi in base al `coupon\_code` per capire meglio quali coupon generano maggior fatturato.

Inizia con la query seguente:

| | |
|--- |--- |
| `SELECT coupon_code,` | Report `group by` |
| `SUM(order_total) as "Total Revenue"` | `Metric operation`(colonna) |
| `FROM orders` | `Metric source` tabella |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Metrica `filter` |
| `AND created_at < '2016-12-01'` <br><br>`AND created_at >= '2016-09-01'` | Metrica `timestamp` (e reporting `time range`) |
| `GROUP BY coupon_code` | Report `group by` |

>[!NOTE]
>
>L’unica differenza rispetto alla query avviata in precedenza è l’aggiunta del &quot;coupon\_code&quot; come raggruppamento._

Utilizzando lo stesso `Total Revenue` metrica creata in precedenza, ora puoi creare il tuo report dei ricavi segmentato per codice coupon! Osserva il file gif qui sotto che mostra come impostare questo rapporto visivo con dati di settembre a novembre:

![Ricavi per codice coupon](../../assets/Revenue_by_coupon_code.gif)

## Formule

A volte, una query può richiedere più aggregazioni per calcolare la relazione tra colonne separate. Ad esempio, è possibile calcolare il valore medio dell&#39;ordine in una query in uno dei due modi seguenti:

* `AVG('order\_total')` OPPURE
* `SUM('order\_total')/COUNT('order\_id')`

Il primo metodo implicherebbe la creazione di una nuova metrica che esegue una media sul `order\_total` colonna. Tuttavia, quest’ultimo metodo potrebbe essere creato direttamente nel generatore di report, supponendo che tu disponga già di metriche configurate per calcolare `Total Revenue` e `Number of orders`.

Fai un passo indietro e osserva la query complessiva per `Average order value`:

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | Metrica `operation` (colonna) |
| `COUNT(order_id) as "Number of orders"` | Metrica `operation` (colonna) |
| `SUM(order_total)/COUNT(order_id) as "Average order value"` | Metrica `operation` (colonna) / Operazione della metrica (colonna) |
| `FROM orders` | Metrica `source` tabella |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Metrica `filter` |
| `AND created_at < '2016-12-01'`<br><br>`AND created_at >= '2016-09-01'` | Timestamp della metrica (e intervallo di tempo di reporting) |

Ora supponiamo che tu disponga già di metriche configurate per calcolare `Total Revenue` e `Number of orders`. Poiché queste metriche esistono, puoi semplicemente aprire la `Report Builder` e creare un calcolo on-demand utilizzando `Formula` funzionalità:

![Forumola AOV](../../assets/AOV_forumula.gif)

## Ritorno a capo

Se sei un utente SQL esperto, pensare a come le query si traducono in [!DNL Commerce Intelligence] consente di creare colonne calcolate, metriche e rapporti.

Per un riferimento rapido, consulta la matrice seguente. Mostra l&#39;equivalente di una clausola SQL [!DNL Commerce Intelligence] e come può essere mappato a più elementi, a seconda di come viene utilizzato nella query.

## Elementi di Commerce Intelligence

| **`SQL Clause`** | **`Metric`** | **`Filter`** | **`Report group by`** | **`Report time frame`** | **`Path`** | **`Calculated column inputs`** | **`Source table`** |
|---|---|---|---|---|---|---|---|
| `SELECT` | X | - | X | - | - | X | - |
| `FROM` | - | - | - | - | - | - | X |
| `WHERE` | - | X | - | - | - | - | - |
| `WHERE` (con elementi temporali) | - | - | - | X | - | - | - |
| `JOIN...ON` | - | X | - | - | X | X | - |
| `GROUP BY` | - | - | X | - | - | - | - |
