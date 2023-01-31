---
title: Ordini degli ospiti
description: Scopri l’impatto degli ordini degli ospiti sui tuoi dati e quali opzioni devi tenere in debito conto per gli ordini degli ospiti nel tuo [!DNL MBI] data warehouse.
exl-id: cd5120ca-454c-4cf4-acb4-3aebe06cdc9a
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# Ordini degli ospiti

Durante la revisione dei tuoi ordini, se noti che molti `customer\_id` i valori sono nulli o non hanno un valore da aggiungere di nuovo a `customers` tavolo, questo è solitamente indicativo che il vostro negozio permette gli ordini degli ospiti. Ciò significa che il tuo `customers` probabilmente la tabella non include tutti i clienti.

In questo argomento, discutiamo l&#39;impatto degli ordini degli ospiti sui vostri dati e quali opzioni è necessario tenere adeguatamente conto degli ordini degli ospiti nel vostro [!DNL MBI] data warehouse.

## Impatto degli ordini dei clienti sui dati

Nel database di e-commerce tipico è presente un `orders` tabella che si unisce a una `customers` tabella. Ogni riga `orders` la tabella ha `customer\_id` che è univoco per una riga nella colonna `customers` tabella.

* **Se tutti i clienti sono registrati** e gli ordini degli ospiti non sono consentiti, ciò significa che ogni record nel `orders` nella tabella è presente un valore `customer\_id` colonna. Di conseguenza, ogni ordine si unisce al `customers` tabella. Lo puoi vedere nell&#39;immagine seguente.

   ![](../../assets/guest-orders-4.png)

* **Se gli ordini degli ospiti sono consentiti**, ciò significa che alcuni ordini non hanno un valore nel `customer\_id` colonna. Solo ai clienti registrati viene assegnato un valore per `customer\_id` nella colonna `orders` tabella. I clienti non registrati riceveranno un `NULL` (o vuoto) per questa colonna. Di conseguenza, non tutti i record dell&#39;ordine avranno record corrispondenti nel `customers` tabella.

   >[!NOTE]
   >
   >Per identificare la persona univoca che ha effettuato l’ordine, accanto a deve essere presente un altro attributo utente univoco `customer\_id` collegato a un ordine. In genere, viene utilizzato l’indirizzo e-mail del cliente.

## Come contabilizzare gli ordini guest nella configurazione del data warehouse

In genere, l&#39;ingegnere vendite che implementa il tuo account terrà conto degli ordini dei clienti durante la creazione della base del tuo data warehouse.

Il modo più ottimale per tenere conto degli ordini dei clienti è quello di basare tutte le metriche a livello di cliente su `orders` tabella. Questa configurazione utilizza un ID cliente univoco di tutti i clienti, inclusi gli ospiti (normalmente viene utilizzata l’e-mail del cliente). I dati di registrazione vengono ignorati dal `customers` tabella. Con questa opzione, solo i clienti che hanno effettuato almeno un acquisto saranno inclusi nei rapporti a livello di cliente. Gli utenti registrati che non hanno ancora effettuato un acquisto non saranno inclusi. Con questa opzione, il tuo `New customer` sarà basato sulla data del primo ordine del cliente nel `orders` tabella.

Si può notare che `Customers we count` il filtro impostato in questo tipo di configurazione ha un filtro per `Customer's order number = 1`. Pensiamo al perché.

![](../../assets/guest-orders-filter-set.png)

In una situazione senza ordini guest, ogni cliente esiste come riga univoca nella tabella del cliente (vedi Immagine 1). Una metrica come `New customers` può semplicemente contare l’id di questa tabella in base a `created\_at` per comprendere i nuovi clienti in base alla data di registrazione.

In una configurazione di ordini guest in cui tutte le metriche del cliente si basano su `orders` per tenere conto degli ordini dei clienti, è necessario assicurarsi di essere `not counting customers twice`. Se conteggi l’id della tabella ordini, conterai ogni ordine. Se invece conteggi l&#39;id sul `orders` tabella e utilizzare un filtro, `Customer's order number = 1`, conterai ogni cliente unico `only one time`. Questa funzione è applicabile a tutte le metriche a livello di cliente quali `Customer's lifetime revenue` o `Customer's lifetime number of orders`.

Nell&#39;immagine 2 precedente, puoi vedere che ci sono null `customer\_ids` in `orders` tabella. Se utilizziamo `customer\_email` per identificare clienti unici, puoi vedere che `erin@test.com` ha effettuato tre (3) ordini. Pertanto, possiamo costruire un `New customers` metrica `orders` tabella basata sulle seguenti condizioni:

* `Operation table = orders`
* `Operation column = id`
* `Operation = count`
* `Timestamp = Customer's first order date`
* `Filter = Customer's we count (where Customer's order number = 1)`
