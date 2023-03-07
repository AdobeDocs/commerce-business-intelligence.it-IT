---
title: Ordini degli ospiti
description: Scopri l’impatto degli ordini degli ospiti sui tuoi dati e quali opzioni hai per tenere adeguatamente conto degli ordini degli ospiti nel tuo [!DNL MBI] Data Warehouse.
exl-id: cd5120ca-454c-4cf4-acb4-3aebe06cdc9a
source-git-commit: 8de036e2717aedef95a8bb908898fd9b9bc9c3fa
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---

# Ordini Ospite

Durante la revisione degli ordini, se noti che molti `customer\_id` i valori sono nulli o non hanno un valore per eseguire il join al `customers` tabella, questo è indicativo del fatto che il tuo negozio consente gli ordini degli ospiti. Ciò significa che `customers` La tabella non include probabilmente tutti i clienti.

In questo argomento viene illustrato l&#39;impatto degli ordini degli ospiti sui dati e le opzioni disponibili per tenere in debito conto gli ordini degli ospiti nel [!DNL MBI] Data Warehouse.

## Impatto degli ordini dei clienti sui dati

Nel database di Commerce tipico, è presente un `orders` tabella che si unisce a una `customers` tabella. Ogni riga del `orders` la tabella ha un `customer\_id` una colonna univoca di una riga `customers` tabella.

* **Se tutti i clienti sono registrati** e gli ordini degli ospiti non sono consentiti, il che significa che ogni record nel `orders` la tabella contiene un valore in `customer\_id` colonna. Di conseguenza, ogni ordine torna al `customers` tabella. È visibile nell’immagine seguente.

   ![](../../assets/guest-orders-4.png)

* **Se gli ordini degli ospiti sono consentiti**, ciò significa che alcuni ordini non hanno un valore in `customer\_id` colonna. Solo i clienti registrati ricevono un valore per `customer\_id` colonna sulla `orders` tabella. I clienti non registrati ricevono un `NULL` o vuoto per questa colonna. Di conseguenza, non tutti i record degli ordini hanno record corrispondenti nel `customers` tabella.

   >[!NOTE]
   >
   >Per identificare l’individuo univoco che ha effettuato l’ordine, accanto a deve essere presente un altro attributo utente univoco `customer\_id` allegato a un ordine. In genere, viene utilizzato l’indirizzo e-mail del cliente.

## Come contabilizzare gli ordini degli ospiti nella configurazione Data Warehouse

In genere, il Sales Engineer che implementa l&#39;account prende in considerazione gli ordini dei clienti al momento di creare le basi della Data Warehouse.

Il modo migliore per tenere conto degli ordini dei clienti è basare tutte le metriche a livello di cliente sul `orders` tabella. Questa configurazione utilizza un ID cliente univoco di tutti i clienti, inclusi gli ospiti (di solito viene utilizzata l’e-mail del cliente). I dati di registrazione provenienti dal `customers` tabella. Con questa opzione, solo i clienti che hanno effettuato almeno un acquisto vengono inclusi nei rapporti a livello di cliente. Gli utenti registrati che non hanno ancora effettuato un acquisto non sono inclusi. Con questa opzione, `New customer` metrica basata sulla data del primo ordine del cliente in `orders` tabella.

È possibile notare che il `Customers we count` il filtro impostato in questo tipo di impostazione ha un filtro per `Customer's order number = 1`. Pensate al perché.

![](../../assets/guest-orders-filter-set.png)

In una situazione senza ordini, ogni cliente esiste come riga univoca nella tabella dei clienti (vedere Immagine 1). Una metrica come `New customers` può semplicemente contare l’id di questa tabella in base a `created\_at` data per comprendere i nuovi clienti in base alla data di registrazione.

In una configurazione di ordini guest in cui tutte le metriche del cliente sono basate su `orders` tabella per gli ordini degli ospiti, è necessario assicurarsi di essere `not counting customers twice`. Se si conta l&#39;ID della tabella ordini, si conta ogni ordine. Se invece conti l’ID sul `orders` tabella e utilizzare un filtro, `Customer's order number = 1`, quindi conteggerai ogni cliente univoco `only one time`. Questo è applicabile a tutte le metriche a livello di cliente come `Customer's lifetime revenue` o `Customer's lifetime number of orders`.

Nell’immagine 2 precedente, puoi vedere che sono presenti valori nulli `customer\_ids` nel `orders` tabella. Se si utilizza `customer\_email` per identificare clienti univoci, puoi vedere che `erin@test.com` ha effettuato tre (3) ordini. Pertanto, puoi creare un’ `New customers` metrica sul tuo `orders` tabella basata sulle seguenti condizioni:

* `Operation table = orders`
* `Operation column = id`
* `Operation = count`
* `Timestamp = Customer's first order date`
* `Filter = Customer's we count (where Customer's order number = 1)`
