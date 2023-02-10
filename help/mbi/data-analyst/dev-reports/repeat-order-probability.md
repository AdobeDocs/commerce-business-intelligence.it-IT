---
title: Rapporto sulla probabilità dell'ordine di ripetizione
description: Scopri e comprendi il Rapporto sulla probabilità dell’ordine di ripetizione.
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# Rapporto sulla probabilità dell&#39;ordine di ripetizione

## Quando è il `Incremental Event Probability` prospettiva disponibile?

La `incremental event probability` la prospettiva è disponibile solo quando i filtri utilizzano dimensioni uguali per tutti gli ordini (ad esempio, `gender`, dell&#39;utente `age` o dell&#39;utente `source`)

Questo perché questa prospettiva si basa su una dimensione denominata `User's order number` per la segmentazione, che indica il numero di acquisti di un utente (ad esempio, 1°, 2° e 3° ordine di John).

Se dovessimo aggiungere un filtro che utilizza una dimensione che non è uguale per tutti gli ordini (ad esempio, `Order's Region`), `User's order number` La dimensione non sarà più precisa in quanto non tiene conto di aree specifiche quando si numerano gli ordini di un utente (ad esempio, 1°, 2°, 3° ordine di John sono ancora gli stessi, indipendentemente dalla loro regione).

## Trasformazione di una dimensione specifica per l’ordine in una dimensione specifica per l’utente

In alcuni casi, potremmo essere in grado di trasformare un `order-specific` in una dimensione `user-specific` dimensione da aggiungere come filtro nel `Repeat Order Probability` grafico. In questi casi, restituiremo l’attributo order del primo ordine o dell’ordine più recente di un utente (ad esempio, il nome dell’area del primo ordine dell’utente).

Se desideri creare una nuova dimensione, [contattare il supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

## Confronto della probabilità di ripetizione degli ordini con attributi diversi

Per confrontare il numero di acquisti ripetuti per attributi di ordine diversi (ad esempio, `region`), è consigliabile creare un grafico simile a quello di `Users by lifetime number of orders` che mostra il numero di utenti che hanno effettuato 1, 2, 3,... numero di ordini nel ciclo di vita e aggiunge il filtro del livello dell&#39;ordine. (in altre parole, questo può mostrare se gli utenti effettuano più o meno acquisti ripetuti in un’area o in un’altra).

I numeri che compongono un grafico di questo tipo possono quindi essere esportati in Excel per calcolare il rapporto di probabilità dell&#39;ordine di ripetizione. Per visualizzare la probabilità che i clienti abbiano effettuato `(x)` gli ordini `(x+1)` ordini, semplicemente` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)` acquisti.

### Esempio:

|  |  |
|---|---|
| Numero di clienti che hanno effettuato 1 acquisto nel corso della loro vita | `90` |
| Numero di clienti che hanno effettuato 2 acquisti nel corso della loro vita | `30` |
| Numero di clienti che hanno effettuato 3 acquisti nel corso della loro vita | `10` |
| Probabilità di ordine ripetuto dei clienti che hanno effettuato un acquisto nel corso della loro vita per effettuare un secondo acquisto | `(30 + 10) / (30+10+90) = 30.77%` |
