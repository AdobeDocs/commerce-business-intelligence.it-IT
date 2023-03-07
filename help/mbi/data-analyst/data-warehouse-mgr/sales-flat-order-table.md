---
title: tabella sales_order
description: Scopri come utilizzare la tabella sales_order.
exl-id: 19a8ab88-de51-48f8-af39-ae4897834afe
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# `sales_order` Tabella

Il `sales_order` tabella (`sales_flat_order` su M1) è il punto in cui viene acquisito ogni ordine. In genere, ogni riga rappresenta un ordine univoco, anche se alcune implementazioni personalizzate di Commerce determinano la suddivisione di un ordine in righe separate.

Questa tabella include tutti gli ordini dei clienti, indipendentemente dal fatto che l&#39;ordine sia stato elaborato tramite pagamento guest. Se il tuo negozio accetta il pagamento, puoi trovare ulteriori informazioni su questo [caso d’uso](../data-warehouse-mgr/guest-orders.md).

## Colonne comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `base_currency_code` | Valuta per tutti i valori acquisiti in `base_*` campi (ovvero `base_grand_total`, `base_subtotal`e così via). Questo in genere riflette la valuta predefinita dell’archivio Commerce |
| `base_discount_amount` | Valore sconto applicato all&#39;ordine |
| `base_grand_total` | Prezzo finale pagato dal cliente sull’ordine, dopo l’applicazione di tutte le imposte, spedizione e sconti. Anche se il calcolo preciso è personalizzabile, in generale il `base_grand_total` viene calcolato come `base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount` |
| `base_subtotal` | Valore lordo della merce di tutti gli articoli inclusi nell&#39;ordine. Non sono inclusi imposte, spedizione, sconti e così via |
| `base_shipping_amount` | Valore di spedizione applicato all&#39;ordine |
| `base_tax_amount` | Valore imposta applicato all&#39;ordine |
| `billing_address_id` | `Foreign key` associato al `sales_order_address` tabella. Partecipa a `sales_order_address.entity_id` per determinare i dettagli dell&#39;indirizzo di fatturazione associati all&#39;ordine |
| `coupon_code` | Coupon applicato all&#39;ordine. Se non viene applicato alcun coupon, questo campo è `NULL` |
| `created_at` | Timestamp di creazione dell’ordine, memorizzato localmente in UTC. A seconda della configurazione in [!DNL MBI], questa marca temporale può essere convertita in un fuso orario di reporting in [!DNL MBI] diverso dal fuso orario del database |
| `customer_email` | Indirizzo e-mail del cliente che effettua l’ordine. Viene compilata in tutte le situazioni, inclusi gli ordini elaborati tramite il pagamento dei clienti |
| `customer_group_id` | Chiave esterna associata al `customer_group` tabella. Partecipa a `customer_group.customer_group_id` per determinare il gruppo di clienti associato all&#39;ordine |
| `customer_id` | `Foreign key` associato al `customer_entity` tabella, se il cliente è registrato. Partecipa a `customer_entity.entity_id` per determinare gli attributi del cliente associati all&#39;ordine. Se l’ordine è stato effettuato tramite pagamento guest, questo campo è `NULL` |
| `entity_id` PK | Identificatore univoco della tabella, di solito utilizzato nei join ad altre tabelle all’interno dell’istanza Commerce |
| `increment_id` | Identificatore univoco di un ordine, comunemente denominato `order_id` in Adobe Commerce. Il `increment_id` viene utilizzato più spesso per i join a sorgenti esterne, ad esempio [!DNL Google Ecommerce] |
| `shipping_address_id` | Chiave esterna associata al `sales_order_address` tabella. Partecipa a `sales_order_address.entity_id` per determinare i dettagli dell&#39;indirizzo di spedizione associati all&#39;ordine |
| `status` | Stato dell’ordine. Può restituire valori come &quot;complete&quot;, &quot;processing&quot;, &quot;canceled&quot;, &quot;repaid&quot; ed eventuali stati personalizzati implementati nell’istanza Commerce. Soggetto a modifiche man mano che l’ordine viene elaborato |
| `store_id` | `Foreign key` associato al `store` tabella. Partecipa a `store`.`store_id` per determinare quale visualizzazione archivio Commerce è associata all’ordine |

{style="table-layout:auto"}

## Colonne calcolate comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `Billing address city` | Città di fatturazione dell&#39;ordine. Calcolato tramite unione `sales_order`.`billing_address_id` a `sales_order_address`.`entity_id` e la restituzione del `city` campo |
| `Billing address country` | Codice paese di fatturazione per l’ordine. Calcolato tramite unione `sales_order`.`billing_address_id` a `sales_order_address`.`entity_id` e la restituzione del `country_id` |
| `Billing address region` | Area di fatturazione (spesso stato o provincia) per l’ordine. Calcolato tramite unione `sales_order`.`billing_address_id` a `sales_order_address`.`entity_id` e la restituzione del `region` campo |
| `Customer's first order date` | Timestamp del primo ordine effettuato da questo cliente. Spesso viene considerata come la &quot;data di acquisizione&quot; per un cliente. Calcolato restituendo il valore minimo `sales_order`.`created_at` valore per ogni cliente univoco |
| `Customer's first order's billing region` | Area di fatturazione dell’acquisizione per il cliente che ha effettuato l’ordine. Calcolato restituendo il valore `Billing address region` associato al primo ordine del cliente |
| `Customer's first order's coupon_code` | Codice coupon di acquisizione per il cliente che ha effettuato l&#39;ordine. Calcolato restituendo il valore `coupon_code` associato al primo ordine del cliente |
| `Customer's group code` | Nome del gruppo del cliente che ha effettuato l&#39;ordine. Calcolato tramite unione `sales_order`.`customer_group_id` a `customer_group`.`customer_group_id` e la restituzione del `customer_group_code` campo |
| `Customer's lifetime number of coupons` | Quantità totale di cedole applicate a tutti gli ordini effettuati dal cliente. Calcolato conteggiando il numero di ordini in cui `coupon_code` non è `NULL` per ogni cliente univoco |
| `Customer's lifetime number of orders` | Numero totale di ordini effettuati dal cliente. Calcolato contando il numero di righe nel `sales_order` tabella per ogni cliente univoco |
| `Customer's lifetime revenue` | Somma il totale dei ricavi per tutti gli ordini effettuati dal cliente. Calcolato sommando i `base_grand_total` campo per tutti gli ordini di ciascun cliente univoco |
| `Customer's order number` | Classificazione ordine sequenziale per l&#39;ordine del cliente. Calcolato identificando tutti gli ordini effettuati da un cliente, ordinandoli in ordine crescente in base al `created_at` timestamp e l’assegnazione di un valore intero incrementale a ciascun ordine. Ad esempio, il primo ordine del cliente restituisce un `Customer's order number` di 1, il secondo ordine del cliente restituisce un `Customer's order number` di 2 e così via. |
| `Customer's order number (previous-current)` | Classificazione dell&#39;ordine precedente del cliente concatenato con la classificazione di questo ordine, separati da un `-` carattere. Calcolato mediante concatenazione (&quot;`Customer's order number` - 1&quot;) con &quot;`-`&quot; seguito da &quot;`Customer's order number`&quot;. Ad esempio, per l’ordine associato al secondo acquisto del cliente, questa colonna restituisce il valore `1-2`. Più spesso utilizzato quando si rappresenta il tempo tra due eventi di ordine (ovvero, nel grafico &quot;Tempo tra gli ordini&quot;) |
| `Is customer's last order?` | Determina se l&#39;ordine corrisponde all&#39;ultimo ordine del cliente o all&#39;ordine più recente. Calcolato confrontando il `Customer's order number` valore con `Customer's lifetime number of orders`. Quando questi due campi sono uguali per l’ordine specificato, questa colonna restituisce &quot;Sì&quot;; altrimenti restituisce &quot;No&quot; |
| `Number of items in order` | Quantità totale di articoli inclusi nell&#39;ordine. Calcolato tramite unione `sales_order`.`entity_id` a `sales_order_item`.`order_id` e sommando i `sales_order_item`.`qty_ordered` campo |
| `Seconds between customer's first order date and this order` | Tempo trascorso tra questo ordine e il primo ordine del cliente. Calcolato sottraendo `Customer's first order date` dal `created_at` per ogni ordine, restituito come numero intero di secondi |
| `Seconds since previous order` | Tempo trascorso tra questo ordine e l&#39;ordine immediatamente precedente del cliente. Calcolato sottraendo il `created_at` per l&#39;ordine precedente dal `created_at` di questo ordine, restituito come numero intero di secondi. Ad esempio, per il record dell’ordine corrispondente al terzo ordine di un cliente, questa colonna restituisce il numero di secondi tra il secondo e il terzo ordine del cliente. Per il primo ordine del cliente, questo campo restituisce `NULL` |
| `Shipping address city` | Città di spedizione per l&#39;ordine. Calcolato tramite unione `sales_order`.`shipping_address_id` a `sales_order_address`.`entity_id` e la restituzione del `city` campo |
| `Shipping address country` | Codice paese di spedizione per l&#39;ordine. Calcolato tramite unione `sales_order`.`Shipping_address_id` a `sales_order_address`.`entity_id` e la restituzione del `country_id` |
| `Shipping address region` | Area di spedizione (spesso stato o provincia) per l&#39;ordine. Calcolato tramite unione `sales_order`.`shipping_address_id` a `sales_order_address`.`entity_id` e la restituzione del `region` campo |
| `Store name` | Nome dell’archivio Commerce associato a questo ordine. Calcolato tramite unione `sales_order`.`store_id` a `store`.`store_id` e la restituzione del `name` campo |

## Metriche comuni

| **Nome della metrica** | **Descrizione** | **Costruzione** |
|---|---|---|
| `Avg order value` | Il ricavo medio per ordine, dove il ricavo è definito come `base_grand_total` | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | Tempo medio tra l&#39;ordine di un cliente (n-1) e l&#39;ordine n, per tutti i clienti e gli ordini | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | Somma del valore lordo delle merci per tutti gli ordini, dove GMV è definito come subtotale, prima dell&#39;applicazione di tutte le imposte e gli sconti | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | Il tempo mediano tra l&#39;ordine di un cliente (n-1) e l&#39;ordine n°, per tutti i clienti e gli ordini | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | Numero totale di ordini effettuati | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | La somma dei ricavi per tutti gli ordini, in cui i ricavi sono definiti come il prezzo finale pagato dal cliente dopo l&#39;applicazione di tutte le imposte, gli sconti, la spedizione e così via | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | Somma dell&#39;importo di spedizione per tutti gli ordini | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | Somma delle imposte applicate a tutti gli ordini | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | Il numero di clienti univoci che effettuano un ordine nell’intervallo di tempo di reporting specificato. Ad esempio, se l’intervallo del rapporto era settimanale, ogni cliente che effettua almeno un ordine in una data settimana viene conteggiato esattamente una volta, indipendentemente dal numero di ordini che ha effettuato in quella settimana | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key` Percorsi di unione

`customer_entity`

* Partecipa a `customer_entity` tabella per creare nuove colonne a livello di cliente associate al cliente che ha effettuato l&#39;ordine.
   * Percorso: `sales_order.customer_id` (molti) => `customer_entity.entity_id` (uno)

`customer_group`

* Partecipa a `customer_group` tabella per creare colonne che restituiscono il nome del gruppo di clienti del cliente che ha effettuato l&#39;ordine.
   * Percorso: `sales_order.customer_group_id` (molti) => `customer_group.customer_group_id` (uno)

`sales_order_address`

* Partecipa a `sales_order_address` tabella per creare colonne che restituiscono le ubicazioni di fatturazione e di spedizione associate all&#39;ordine. Sono possibili due percorsi di unione, a seconda che siano necessari i dettagli di fatturazione o di spedizione.
   * Percorsi:
      * Spedizione: `sales_order.shipping_address_id`(molti) => `sales_order_address.entity_id` (uno)
      * Fatturazione: `sales_order.billing_address_id`(molti) => `sales_order_address.entity_id` (uno)

`store`

* Partecipa a `store` tabella per creare colonne che restituiscono i dettagli relativi all’archivio Commerce associato all’ordine.
   * Percorso: `sales_order.store_id` (molti) => `store.store_id` (uno)
