---
title: Comprendere l'ambiente  [!DNL Commerce Intelligence]
description: Scopri come utilizzare e migliorare l'ambiente  [!DNL Commerce Intelligence] .
exl-id: 601b5fba-da02-4cc8-96ed-147c24f326f9
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 0%

---

# L&#39;ambiente [!DNL Adobe Commerce Intelligence]

Mentre analizzi i dati di e-commerce, presta attenzione a questi fattori e ai pregiudizi più comuni. Se hai bisogno di assistenza per assicurarti di utilizzare correttamente lo schema di Commerce, non esitare a [contattare il supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## [!DNL entity\_id]

Molte tabelle contengono una colonna denominata `entity\_id`. In ogni tabella che contiene `entity\_id`, tale colonna viene utilizzata per identificare righe univoche.

Ad esempio, ogni riga nella tabella `sales\_order` è un ordine univoco. La chiave primaria in questa tabella è denominata `entity\_id`. Questa colonna può essere considerata come `order\_id`. In una tabella separata, `customer\_entity`, ogni riga rappresenta un cliente univoco. La chiave primaria in questa tabella è denominata anche `entity\_id`, che può essere considerata come `customer\_id`.

In queste tabelle, `sales\_order.entity\_id` non è uguale a `customer\_entity.entity\_id`. Ciò vale per tutti i set di tabelle che contengono `entity\_id`: `table\_A.entity\_id` non è uguale a `table\_B.entity\_id`.

## [!DNL Guest orders]

Se si consente ai clienti di ordinare dal sito senza disporre di un account (ordini guest), tali clienti non verranno inseriti come riga nella tabella `customer\_entity`. Inoltre, ogni ordine effettuato da un ospite ha un valore `customer\_id` nullo nella tabella `sales\_order`.

Pertanto, se desideri tenere traccia dei comportamenti degli ospiti nel tempo, tutte le colonne a livello di cliente devono essere calcolate sulla tabella `sales\_order`, utilizzando un identificatore cliente come `customer\_email`.

Se utilizzi la tabella `sales\_order` come tabella del cliente, devi prestare attenzione quando crei le metriche a livello del cliente. Ad esempio, considera una metrica dei ricavi medi per tutta la vita. Questa metrica viene utilizzata per identificare i ricavi medi nel ciclo di vita in tutta la base di clienti. In primo luogo, è necessaria una nuova colonna che restituisca i ricavi relativi al ciclo di vita di ogni cliente. Quindi devi calcolare la media di questa colonna per ottenere i ricavi medi del ciclo di vita dei tuoi clienti.

Se si è in grado di utilizzare la tabella `customer\_entity`, ogni riga rappresenta un singolo cliente e ogni cliente esiste in tale tabella una sola volta. Pertanto, quando si dispone della colonna dei ricavi relativi al ciclo di vita, tutto ciò di cui si ha bisogno è creare una metrica media. Tuttavia, se utilizzi la tabella `sales\_order` come tabella del cliente, un cliente può potenzialmente esistere in numerose righe. Dopo aver impostato la colonna dei ricavi relativi al ciclo di vita, ogni ordine (riga) effettuato da un determinato cliente mostrerà i ricavi relativi al ciclo di vita del cliente; tuttavia, si desidera includere il cliente solo una volta nella metrica media complessiva.

Il trucco è quello di aggiungere alla metrica un filtro che assicuri di includere ogni cliente una sola volta. L&#39;Adobe ti incoraggia a creare e utilizzare un set di filtri denominato **Clienti conteggiati** che filtra per **Numero ordine cliente = 1** (tra gli altri filtri potrebbe essere necessario escludere i clienti indesiderati). L’aggiunta di questo filtro assicura che ogni cliente sia incluso una sola volta in una metrica a livello di cliente.

## Prodotti e categorie

I prodotti possono avere più categorie e le categorie possono essere utilizzate per più prodotti. Pertanto, quando si impostano analisi a livello di categoria, è necessario prestare attenzione a utilizzare le definizioni corrette. Desideri la categoria principale? Categoria di secondo livello? Cosa succede se il prodotto può rientrare in più categorie principali?

Immaginate un paio di jeans che rientrano in tre diversi livelli di categoria, definiti da un&#39;implementazione di Commerce: &quot;Abbigliamento&quot; (livello superiore), &quot;Outerwear&quot; (secondo livello) e &quot;Pantaloni&quot; (terzo livello). È possibile analizzare le prestazioni delle categorie in base al numero di unità vendute. La metrica necessaria per l&#39;analisi è _Elementi venduti_, generata nella tabella `sales\_order\_item`. Pertanto, è necessario spostare le informazioni a livello di categoria nella tabella degli elementi. A ogni riga della tabella `sales\_order\_item` è associato `product\_id`, quindi se si conoscono le categorie associate a un prodotto, è possibile trasferire tali informazioni nella tabella desiderata.

Prima di spostare qualsiasi dato, è necessario conoscere i join e i filtri corretti per assicurarsi di acquisire la categoria corretta. Per alcune analisi, potrebbe essere necessario conoscere &#39;Pantaloni&#39;, ma in altre, &#39;Abbigliamento&#39; potrebbe essere più appropriato. Si tratta di categorie distinte identificate separatamente. La conoscenza della definizione di ogni livello di categoria consente di attribuire le vendite unitarie alla categoria appropriata per l&#39;analisi specifica.

Ora, immagina di avere anche una categoria di livello superiore `Our Favorites` nella home page del sito Web. Forse hai implementato il tuo Commerce store per includere questi jeans sia nella categoria `Clothing` che nella categoria `Our Favorites`. In tal caso, questa coppia di jeans ha più di una categoria di primo livello. In tal caso, lo spostamento di una singola categoria di primo livello alla tabella `sales\_order\_item` non ha molto senso, in quanto sono disponibili più opzioni. Per tenere conto di questo, l’Adobe suggerisce di creare colonne sì/no che controllano categorie specifiche. Ad esempio, le colonne `Is product in Clothing category?` e `Is product in Our Favorites category?` ti consentono di verificare se un prodotto rientra in tali categorie specifiche.
