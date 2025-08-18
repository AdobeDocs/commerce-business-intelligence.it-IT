---
title: Ordini degli ospiti
description: Scopri l'impatto degli ordini degli ospiti sui tuoi dati e quali opzioni hai per tenere in debito conto gli ordini degli ospiti nel tuo [!DNL Commerce Intelligence] Data Warehouse.
exl-id: cd5120ca-454c-4cf4-acb4-3aebe06cdc9a
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---

# Ordini Ospite

Durante l&#39;esame degli ordini, se si nota che molti valori di `customer\_id` sono nulli o non hanno un valore per tornare alla tabella di `customers`, ciò indica che lo store consente gli ordini degli ospiti. Ciò significa che la tabella `customers` probabilmente non include tutti i clienti.

In questo argomento viene illustrato l&#39;impatto degli ordini degli ospiti sui dati e le opzioni disponibili per tenere in debito conto gli ordini degli ospiti nel Data Warehouse [!DNL Commerce Intelligence].

## Impatto degli ordini dei clienti sui dati

Nel tipico database di commerce è presente una tabella `orders` che viene unita a una tabella `customers`. Ogni riga della tabella `orders` ha una colonna `customer\_id` univoca per una riga della tabella `customers`.

* **Se tutti i clienti sono registrati** e gli ordini dei guest non sono consentiti, significa che ogni record della tabella `orders` ha un valore nella colonna `customer\_id`. Di conseguenza, ogni ordine torna alla tabella `customers`.

  ![](../../assets/guest-orders-4.png)

* **Se sono consentiti ordini guest**, significa che alcuni ordini non hanno un valore nella colonna `customer\_id`. Solo ai clienti registrati viene assegnato un valore per la colonna `customer\_id` nella tabella `orders`. I clienti non registrati ricevono un valore `NULL` (o vuoto) per questa colonna. Di conseguenza, non tutti i record degli ordini hanno record corrispondenti nella tabella `customers`.

  >[!NOTE]
  >
  >Per identificare l&#39;utente univoco che ha effettuato l&#39;ordine, accanto a `customer\_id` deve essere presente un altro attributo utente univoco associato a un ordine. In genere, viene utilizzato l’indirizzo e-mail del cliente.

## Come registrare gli ordini degli ospiti nella configurazione di Data Warehouse

In genere, il Sales Engineer che implementa l&#39;account prende in considerazione gli ordini degli ospiti durante la creazione delle basi del Data Warehouse.

Il modo migliore per tenere conto degli ordini dei clienti è basare tutte le metriche a livello di cliente sulla tabella `orders`. Questa configurazione utilizza un ID cliente univoco di tutti i clienti, inclusi gli ospiti (di solito viene utilizzata l’e-mail del cliente). I dati di registrazione della tabella `customers` verranno ignorati. Con questa opzione, solo i clienti che hanno effettuato almeno un acquisto vengono inclusi nei rapporti a livello di cliente. Gli utenti registrati che non hanno ancora effettuato un acquisto non sono inclusi. Con questa opzione, la metrica `New customer` si basa sulla data del primo ordine del cliente nella tabella `orders`.

È possibile che il filtro `Customers we count` impostato in questo tipo di installazione abbia un filtro per `Customer's order number = 1`.

![](../../assets/guest-orders-filter-set.png)

In una situazione senza ordini, ogni cliente esiste come riga univoca nella tabella dei clienti (vedere Immagine 1). Una metrica come `New customers` può semplicemente contare l&#39;ID di questa tabella in base alla data `created\_at` per comprendere i nuovi clienti in base alla data di registrazione.

In una configurazione di ordini guest in cui tutte le metriche del cliente sono basate sulla tabella `orders` per tenere conto degli ordini dei clienti, è necessario assicurarsi di essere `not counting customers twice`. Se si conta l&#39;ID della tabella ordini, si conta ogni ordine. Se invece conteggi l&#39;ID nella tabella `orders` e utilizzi un filtro, `Customer's order number = 1`, verrà conteggiato ogni cliente univoco `only one time`. Applicabile a tutte le metriche a livello di cliente, ad esempio `Customer's lifetime revenue` o `Customer's lifetime number of orders`.

Nella tabella `customer\_ids` sono presenti `orders` null. Se utilizzi `customer\_email` per identificare clienti univoci, puoi notare che `erin@test.com` ha effettuato tre (3) ordini. È quindi possibile generare una metrica `New customers` nella tabella `orders` in base alle seguenti condizioni:

* `Operation table = orders`
* `Operation column = id`
* `Operation = count`
* `Timestamp = Customer's first order date`
* `Filter = Customer's we count (where Customer's order number = 1)`
