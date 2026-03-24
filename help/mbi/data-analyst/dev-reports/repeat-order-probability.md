---
title: Rapporto Probabilità di ripetizione ordine
description: Scopri e comprendi il rapporto Probabilità di ordine di ripetizione.
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/MW9jxiwitZyjc6-woelN-FOAmvEFPCWDt01wyTOX16k
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 343
ht-degree: 0%

---

# Rapporto Probabilità di ripetizione ordine

## Quando è disponibile la prospettiva `Incremental Event Probability`?

La prospettiva `incremental event probability` è disponibile solo quando i filtri utilizzano dimensioni uguali per tutti gli ordini (ad esempio, `gender` dell&#39;utente, `age` dell&#39;utente o `source` dell&#39;utente).

Questo perché questa prospettiva si basa su una dimensione denominata `User's order number` per la segmentazione, che indica il numero di acquisti di un utente (ad esempio, 1o, 2o e 3o ordine di John).

Se si aggiunge un filtro che utilizza una dimensione non uguale per tutti gli ordini (ad esempio, `Order's Region`), la dimensione `User's order number` non sarà più precisa. Questo perché non tiene conto di aree specifiche durante la numerazione degli ordini di un utente (ad esempio, il primo, il secondo e il terzo ordine di John sono ancora gli stessi, indipendentemente dalla loro area geografica).

## Trasformazione di una dimensione specifica dell&#39;ordine in una dimensione specifica dell&#39;utente

In alcuni casi, è possibile trasformare una dimensione `order-specific` in una dimensione `user-specific` da aggiungere come filtro nel grafico `Repeat Order Probability`. In questi casi, viene restituito l&#39;attributo order del primo ordine o dell&#39;ultimo ordine di un utente, ad esempio il nome dell&#39;area di primo ordine dell&#39;utente.

Se desideri creare una nuova dimensione, [contatta il supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## Confronto della probabilità di ripetizione degli ordini con attributi diversi

Per confrontare il numero di acquisti ripetuti per diversi attributi dell&#39;ordine (ad esempio, l&#39;ordine `region`), Adobe consiglia di creare un grafico simile a `Users by lifetime number of orders`. Questo mostra il numero di utenti che hanno effettuato 1, 2, 3,... numero di ordini a vita e aggiungi il filtro a livello di ordine. (in altre parole, questo può mostrare se gli utenti effettuano più o meno acquisti ripetuti in una regione o in un&#39;altra.)

I numeri che compongono tale grafico possono quindi essere esportati in Excel per calcolare il rapporto di probabilità dell&#39;ordine di ripetizione. Per vedere la probabilità dei clienti che hanno effettuato `(x)` ordini di effettuare `(x+1)` ordini, è sufficiente` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)` acquisti.

### Esempio:

| Categoria | Valore |
|---|---|
| Numero di clienti che hanno effettuato 1 acquisto nel corso della loro vita | `90` |
| Numero di clienti che hanno effettuato 2 acquisti nel corso della loro vita | `30` |
| Numero di clienti che hanno effettuato 3 acquisti nel corso della loro vita | `10` |
| La probabilità di ordine ripetuto dei clienti che hanno effettuato un acquisto nel corso della loro vita per effettuare un secondo acquisto | `(30 + 10) / (30+10+90) = 30.77%` |
