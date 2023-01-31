---
title: Comprendere il tuo [!DNL MBI] Ambiente
description: Scopri come lavorare con e migliorare il tuo [!DNL MBI] ambiente.
exl-id: 601b5fba-da02-4cc8-96ed-147c24f326f9
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---

# Le [!DNL MBI] Ambiente

Quando analizzi i dati di e-commerce, tieni presente questi fattori e i concetti errati comuni. Se hai bisogno di assistenza per assicurarti di utilizzare correttamente lo schema Commerce, non esitare a [contattare il supporto](../guide-overview.md).

## [!DNL entity\_id]

Molte tabelle contengono una colonna denominata `entity\_id`. In ogni tabella che contiene un `entity\_id`, questa colonna viene utilizzata per identificare righe univoche.

Ad esempio, ogni riga nel `sales\_order` tabella è un ordine univoco. La chiave primaria in questa tabella è denominata `entity\_id`. Questa colonna può essere pensata come `order\_id`. In una tabella separata, `customer\_entity`, ogni riga rappresenta un cliente univoco. Anche la chiave primaria in questa tabella è denominata `entity\_id`, che può essere considerato come `customer\_id`.

In queste tabelle, `sales\_order.entity\_id` è diverso da `customer\_entity.entity\_id`. Questo vale per tutti i set di tabelle contenenti `entity\_id`: `table\_A.entity\_id` è diverso da `table\_B.entity\_id`.

## [!DNL Guest orders]

Se consenti ai clienti di ordinare dal tuo sito senza avere un account (ordini dei clienti), questi clienti non verranno compilati come riga nel tuo `customer\_entity` tabella. Inoltre, ogni ordine effettuato da un ospite avrà un valore null `customer\_id` sul valore `sales\_order` tabella.

Pertanto, se desideri tenere traccia dei comportamenti degli ospiti nel tempo, tutte le colonne a livello di cliente devono essere calcolate in `sales\_order` utilizzando un identificatore del cliente, ad esempio `customer\_email`.

Se utilizzi `sales\_order` come tabella cliente, devi quindi prestare attenzione durante la creazione di metriche a livello di cliente. Ad esempio, considera una metrica di ricavo medio del ciclo di vita. Questa metrica viene utilizzata per identificare il ricavo medio del ciclo di vita nella base cliente. Questa prima colonna richiede una nuova colonna che, per ogni cliente, restituisca i ricavi del ciclo di vita. A quel punto, devi calcolare la media di questa colonna per ottenere il ricavo medio del ciclo di vita dei tuoi clienti.

Se sei in grado di utilizzare il `customer\_entity` tabella, ogni riga è un singolo cliente e ogni cliente esiste in tale tabella una sola volta. Pertanto, quando hai la colonna del ricavo del ciclo di vita, tutto ciò che ti serve è creare una metrica media. Tuttavia, se utilizzi il `sales\_order` come tabella del cliente, un cliente può potenzialmente esistere in numerose righe. Dopo aver impostato la colonna dei ricavi per tutta la durata, ogni ordine (riga) effettuato da un determinato cliente mostrerà i ricavi per tutta la vita del cliente; ma desideri includere quel cliente solo una volta nella metrica media complessiva.

In questo caso, devi aggiungere un filtro alla metrica in modo da includere ogni cliente una sola volta. Ti consigliamo di creare e utilizzare un set di filtri denominato **Clienti contati** che filtrerà **Numero dell&#39;ordine del cliente = 1** (tra gli altri filtri potrebbe essere necessario escludere i clienti indesiderati). L’aggiunta di questo filtro assicura che ogni cliente venga incluso solo una volta in una metrica a livello di cliente.

## Prodotti e categorie

I prodotti possono avere più categorie e le categorie possono essere utilizzate per più di un prodotto. Pertanto, quando si impostano le analisi a livello di categoria, occorre fare attenzione a utilizzare le definizioni corrette. Vuoi la categoria di livello superiore? Categoria di secondo livello? Cosa succede se il prodotto può rientrare in più categorie di primo livello?

Immagina un paio di jeans che rientrano in tre diversi livelli di categoria, come definito da un&#39;implementazione Commerce: &quot;Abbigliamento&quot; (livello superiore), &quot;outerwear&quot; (secondo livello) e &quot;Pants&quot; (terzo livello). Potrebbe essere utile analizzare le prestazioni delle categorie in base al numero di unità vendute. La metrica necessaria per questa analisi è _Articoli venduti_, che si basa sul `sales\_order\_item` tabella. Pertanto, è necessario spostare le informazioni a livello di categoria nella tabella degli elementi. Ogni riga del `sales\_order\_item` a una tabella associata `product\_id`quindi, se conosci le categorie associate a un prodotto, puoi portare tali informazioni nella tabella desiderata.

Prima di spostare qualsiasi dato, devi prima conoscere i join e i filtri appropriati per assicurarti di acquisire la categoria corretta. Per alcune analisi, potrebbe essere necessario conoscere &#39;Pantaloni&#39;, ma in altre analisi, &#39;Abbigliamento&#39; potrebbe essere più appropriato. Si tratta di categorie distinte identificate separatamente. Sapere come è definito ogni livello di categoria garantirà di attribuire le vendite per unità alla categoria appropriata per la tua analisi specifica.

Ora, immagina anche di avere una categoria di livello superiore &quot;I nostri preferiti&quot; nella home page del tuo sito web. Forse hai implementato il tuo negozio Commerce per includere questi jeans sia nella categoria &quot;Abbigliamento&quot; sia nella categoria &quot;I nostri preferiti&quot;. In tal caso, questo paio di jeans avrà più di una categoria di livello superiore. In tal caso, sposta una singola categoria di primo livello verso il `sales\_order\_item` tabella non ha senso, in quanto ci sono più opzioni. Per tenere conto di ciò, si consiglia di creare colonne sì/no che verifichino categorie specifiche. Ad esempio: `Is product in Clothing category?` e `Is product in Our Favorites category?` Le colonne ti consentono di verificare se un prodotto rientra in queste categorie specifiche.
