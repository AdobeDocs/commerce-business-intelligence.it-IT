---
title: Comprendere il [!DNL MBI] Ambiente
description: Scopri come utilizzare e migliorare i [!DNL MBI] ambiente.
exl-id: 601b5fba-da02-4cc8-96ed-147c24f326f9
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 0%

---

# Il tuo [!DNL MBI] Ambiente

Mentre analizzi i dati di e-commerce, presta attenzione a questi fattori e ai pregiudizi più comuni. Se hai bisogno di assistenza per assicurarti di utilizzare correttamente lo schema Commerce, non esitare a [contatta l’assistenza](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

## [!DNL entity\_id]

Molte tabelle contengono una colonna denominata `entity\_id`. In ogni tabella che contiene un `entity\_id`, la colonna viene utilizzata per identificare righe univoche.

Ad esempio, ogni riga nel `sales\_order` la tabella è un ordine univoco. La chiave primaria in questa tabella è denominata `entity\_id`. Questa colonna può essere considerata come `order\_id`. In una tabella separata, `customer\_entity`, ogni riga rappresenta un cliente univoco. La chiave primaria in questa tabella è denominata anche `entity\_id`, che può essere considerato come `customer\_id`.

In tali tabelle, `sales\_order.entity\_id` non è uguale a `customer\_entity.entity\_id`. Ciò vale per tutti i set di tabelle che contengono `entity\_id`: `table\_A.entity\_id` non è uguale a `table\_B.entity\_id`.

## [!DNL Guest orders]

Se consenti ai clienti di ordinare dal sito senza disporre di un account (ordini degli ospiti), questi non si presentano come una riga nel tuo `customer\_entity` tabella. Inoltre, ogni ordine effettuato da un ospite ha un valore nullo `customer\_id` valore sul `sales\_order` tabella.

Pertanto, se desideri tenere traccia dei comportamenti degli ospiti nel tempo, tutte le colonne a livello di cliente devono essere calcolate sulla base `sales\_order` tabella, utilizzando un identificatore cliente come `customer\_email`.

Se si utilizza `sales\_order` come tabella del cliente, devi quindi prestare attenzione quando crei metriche a livello di cliente. Ad esempio, considera una metrica dei ricavi medi per tutta la vita. Questa metrica viene utilizzata per identificare i ricavi medi nel ciclo di vita in tutta la base di clienti. In primo luogo, è necessaria una nuova colonna che restituisca i ricavi relativi al ciclo di vita di ogni cliente. Quindi devi calcolare la media di questa colonna per ottenere i ricavi medi del ciclo di vita dei tuoi clienti.

Se è in grado di utilizzare il `customer\_entity` tabella, ogni riga è un singolo cliente e ogni cliente esiste in tale tabella una sola volta. Pertanto, quando si dispone della colonna dei ricavi relativi al ciclo di vita, tutto ciò di cui si ha bisogno è creare una metrica media. Tuttavia, se utilizzi il `sales\_order` come tabella del cliente, un cliente può potenzialmente esistere in numerose righe. Dopo aver impostato la colonna dei ricavi relativi al ciclo di vita, ogni ordine (riga) effettuato da un determinato cliente mostrerà i ricavi relativi al ciclo di vita del cliente; tuttavia, si desidera includere il cliente solo una volta nella metrica media complessiva.

Il trucco è quello di aggiungere alla metrica un filtro che assicuri di includere ogni cliente una sola volta. L’Adobe ti incoraggia a creare e utilizzare un set di filtri denominato **Clienti che contiamo** che filtra per **Numero ordine cliente = 1** (ad esempio, potrebbe essere necessario escludere i clienti indesiderati). L’aggiunta di questo filtro assicura che ogni cliente sia incluso una sola volta in una metrica a livello di cliente.

## Prodotti e categorie

I prodotti possono avere più categorie e le categorie possono essere utilizzate per più prodotti. Pertanto, quando si impostano analisi a livello di categoria, è necessario prestare attenzione a utilizzare le definizioni corrette. Desideri la categoria principale? Categoria di secondo livello? Cosa succede se il prodotto può rientrare in più categorie principali?

Immagina un paio di jeans che rientrano in tre diversi livelli di categoria, definiti da un’implementazione Commerce: &quot;Abbigliamento&quot; (livello superiore), &quot;Outerwear&quot; (secondo livello) e &quot;Pantaloni&quot; (terzo livello). È possibile analizzare le prestazioni delle categorie in base al numero di unità vendute. La metrica necessaria per questa analisi è _Oggetti venduti_, che è basato su `sales\_order\_item` tabella. Pertanto, è necessario spostare le informazioni a livello di categoria nella tabella degli elementi. Ogni riga del `sales\_order\_item` alla tabella è associato un `product\_id`Pertanto, se conosci le categorie associate a un prodotto, puoi inserire tali informazioni nella tabella desiderata.

Prima di spostare qualsiasi dato, è necessario conoscere i join e i filtri corretti per assicurarsi di acquisire la categoria corretta. Per alcune analisi, potrebbe essere necessario conoscere &#39;Pantaloni&#39;, ma in altre, &#39;Abbigliamento&#39; potrebbe essere più appropriato. Si tratta di categorie distinte identificate separatamente. La conoscenza della definizione di ogni livello di categoria consente di attribuire le vendite unitarie alla categoria appropriata per l&#39;analisi specifica.

Immaginate di avere anche un `Our Favorites` categoria di primo livello nella home page del sito web. Forse hai implementato il tuo punto vendita Commerce per includere questi jeans sia nel `Clothing` categoria e `Our Favorites` categoria. In tal caso, questa coppia di jeans ha più di una categoria di primo livello. In tal caso, spostando una singola categoria di primo livello sul `sales\_order\_item` la tabella non ha molto senso, in quanto ci sono più opzioni. Per tenere conto di questo, l’Adobe suggerisce di creare colonne sì/no che controllano categorie specifiche. Ad esempio: `Is product in Clothing category?` e `Is product in Our Favorites category?` Le colonne ti consentono di verificare se un prodotto rientra in tali categorie specifiche.
