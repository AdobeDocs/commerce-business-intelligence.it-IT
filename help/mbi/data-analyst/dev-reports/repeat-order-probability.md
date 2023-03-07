---
title: Rapporto Probabilità di ripetizione ordine
description: Scopri e comprendi il rapporto Probabilità di ordine di ripetizione.
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# Rapporto Probabilità di ripetizione ordine

## Quando è `Incremental Event Probability` prospettiva disponibile?

Il `incremental event probability` la prospettiva è disponibile solo quando i filtri utilizzano dimensioni uguali per tutti gli ordini (ad esempio, `gender`, dell&#39;utente `age` o dell&#39;utente `source`)

Questo perché questa prospettiva si basa su una dimensione denominata `User's order number` per la segmentazione, che indica la quantità di acquisti di un utente (ad esempio, primo, secondo e terzo ordine di John).

Se hai aggiunto un filtro che utilizza una dimensione non uguale per tutti gli ordini (ad esempio, `Order's Region`), il `User's order number` non sarebbe più accurata. Questo perché non tiene conto di aree specifiche durante la numerazione degli ordini di un utente (ad esempio, il primo, il secondo e il terzo ordine di John sono ancora gli stessi, indipendentemente dalla loro area geografica).

## Trasformazione di una dimensione specifica dell&#39;ordine in una dimensione specifica dell&#39;utente

In alcuni casi, può essere possibile trasformare un `order-specific` dimensione in un `user-specific` dimensione da aggiungere come filtro nel `Repeat Order Probability` grafico. In questi casi, viene restituito l&#39;attributo order del primo ordine o dell&#39;ultimo ordine di un utente, ad esempio il nome dell&#39;area di primo ordine dell&#39;utente.

Se desiderate creare una nuova quota, [contatta l’assistenza](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

## Confronto della probabilità di ripetizione degli ordini con attributi diversi

Per confrontare il numero di acquisti ripetuti per diversi attributi dell&#39;ordine (ad esempio, `region`), Adobe consiglia di creare un grafico simile a `Users by lifetime number of orders`. Questo mostra il numero di utenti che hanno effettuato 1, 2, 3,... numero di ordini a vita e aggiungi il filtro a livello di ordine. (in altre parole, questo può mostrare se gli utenti effettuano più o meno acquisti ripetuti in una regione o in un&#39;altra.)

I numeri che compongono tale grafico possono quindi essere esportati in Excel per calcolare il rapporto di probabilità dell&#39;ordine di ripetizione. Per visualizzare la probabilità di clienti che hanno effettuato `(x)` ordini da effettuare `(x+1)` ordini, semplicemente` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)` acquisti.

### Esempio:

|  |  |
|---|---|
| Numero di clienti che hanno effettuato 1 acquisto nel corso della loro vita | `90` |
| Numero di clienti che hanno effettuato 2 acquisti nel corso della loro vita | `30` |
| Numero di clienti che hanno effettuato 3 acquisti nel corso della loro vita | `10` |
| La probabilità di ordine ripetuto dei clienti che hanno effettuato un acquisto nel corso della loro vita per effettuare un secondo acquisto | `(30 + 10) / (30+10+90) = 30.77%` |
