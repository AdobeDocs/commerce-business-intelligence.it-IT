---
title: tabella sales_order
description: Scopri come utilizzare la tabella sales_order.
exl-id: 19a8ab88-de51-48f8-af39-ae4897834afe
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 0%

---

# Tabella `sales_order`

Nella tabella `sales_order` (`sales_flat_order` in M1) viene acquisito ogni ordine. Di solito, ogni riga rappresenta un ordine univoco, anche se ci sono alcune implementazioni personalizzate di Commerce che si traducono nella suddivisione di un ordine in righe separate.

Questa tabella include tutti gli ordini dei clienti, indipendentemente dal fatto che l&#39;ordine sia stato elaborato tramite pagamento guest. Se l&#39;archivio accetta l&#39;estrazione come ospite, puoi trovare ulteriori informazioni su questo [caso d&#39;uso](../data-warehouse-mgr/guest-orders.md).

## Colonne comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `base_currency_code` | Valuta per tutti i valori acquisiti nei campi `base_*` (ovvero `base_grand_total`, `base_subtotal` e così via). Questo in genere riflette la valuta predefinita del Commerce Store |
| `base_discount_amount` | Valore sconto applicato all&#39;ordine |
| `base_grand_total` | Prezzo finale pagato dal cliente sull’ordine, dopo l’applicazione di tutte le imposte, spedizione e sconti. Anche se il calcolo preciso è personalizzabile, in generale `base_grand_total` è calcolato come `base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount` |
| `base_subtotal` | Valore lordo della merce di tutti gli articoli inclusi nell&#39;ordine. Non sono inclusi imposte, spedizione, sconti e così via |
| `base_shipping_amount` | Valore di spedizione applicato all&#39;ordine |
| `base_tax_amount` | Valore imposta applicato all&#39;ordine |
| `billing_address_id` | `Foreign key` associato alla tabella `sales_order_address`. Partecipa a `sales_order_address.entity_id` per determinare i dettagli dell&#39;indirizzo di fatturazione associati all&#39;ordine |
| `coupon_code` | Coupon applicato all&#39;ordine. Se non viene applicato alcun coupon, questo campo è `NULL` |
| `created_at` | Timestamp di creazione dell’ordine, memorizzato localmente in UTC. A seconda della configurazione in [!DNL Commerce Intelligence], questa marca temporale può essere convertita in un fuso orario di reporting in [!DNL Commerce Intelligence] diverso dal fuso orario del database |
| `customer_email` | Indirizzo e-mail del cliente che effettua l’ordine. Viene compilata in tutte le situazioni, inclusi gli ordini elaborati tramite il pagamento dei clienti |
| `customer_group_id` | Chiave esterna associata alla tabella `customer_group`. Partecipa a `customer_group.customer_group_id` per determinare il gruppo di clienti associato all&#39;ordine |
| `customer_id` | `Foreign key` associato alla tabella `customer_entity`, se il cliente è registrato. Partecipa a `customer_entity.entity_id` per determinare gli attributi del cliente associati all&#39;ordine. Se l&#39;ordine è stato effettuato tramite il pagamento guest, questo campo è `NULL` |
| `entity_id` (PC) | Identificatore univoco della tabella, di solito utilizzato nei join ad altre tabelle nell’istanza di Commerce |
| `increment_id` | Identificatore univoco di un ordine, comunemente denominato `order_id` in Adobe Commerce. `increment_id` viene utilizzato più spesso per i join a origini esterne, ad esempio [!DNL Google Ecommerce] |
| `shipping_address_id` | Chiave esterna associata alla tabella `sales_order_address`. Iscriviti a `sales_order_address.entity_id` per determinare i dettagli dell&#39;indirizzo di spedizione associati all&#39;ordine |
| `status` | Stato dell’ordine. Può restituire valori quali &quot;complete&quot;, &quot;processing&quot;, &quot;canceled&quot;, &quot;rereturned&quot; e qualsiasi stato personalizzato implementato nell’istanza di Commerce. Soggetto a modifiche man mano che l’ordine viene elaborato |
| `store_id` | `Foreign key` associato alla tabella `store`. Partecipa a `store`.`store_id` per determinare quale visualizzazione store di Commerce è associata all&#39;ordine |

{style="table-layout:auto"}

## Colonne calcolate comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `Billing address city` | Città di fatturazione dell&#39;ordine. Calcolato unendo `sales_order`.Da `billing_address_id` a `sales_order_address`.`entity_id` e restituzione del campo `city` |
| `Billing address country` | Codice paese di fatturazione per l’ordine. Calcolato unendo `sales_order`.Da `billing_address_id` a `sales_order_address`.`entity_id` e restituzione di `country_id` |
| `Billing address region` | Area di fatturazione (spesso stato o provincia) per l’ordine. Calcolato unendo `sales_order`.Da `billing_address_id` a `sales_order_address`.`entity_id` e restituzione del campo `region` |
| `Customer's first order date` | Timestamp del primo ordine effettuato da questo cliente. Spesso viene considerata come la &quot;data di acquisizione&quot; per un cliente. Calcolato restituendo il minimo `sales_order`.Valore `created_at` per ogni cliente univoco |
| `Customer's first order's billing region` | Area di fatturazione dell’acquisizione per il cliente che ha effettuato l’ordine. Calcolato restituendo il `Billing address region` associato al primo ordine del cliente |
| `Customer's first order's coupon_code` | Codice coupon di acquisizione per il cliente che ha effettuato l&#39;ordine. Calcolato restituendo il `coupon_code` associato al primo ordine del cliente |
| `Customer's group code` | Nome del gruppo del cliente che ha effettuato l&#39;ordine. Calcolato unendo `sales_order`.Da `customer_group_id` a `customer_group`.`customer_group_id` e restituzione del campo `customer_group_code` |
| `Customer's lifetime number of coupons` | Quantità totale di cedole applicate a tutti gli ordini effettuati dal cliente. Calcolato contando il numero di ordini in cui `coupon_code` non è `NULL` per ciascun cliente univoco |
| `Customer's lifetime number of orders` | Numero totale di ordini effettuati dal cliente. Calcolato contando il numero di righe nella tabella `sales_order` per ogni cliente univoco |
| `Customer's lifetime revenue` | Somma il totale dei ricavi per tutti gli ordini effettuati dal cliente. Calcolato sommando il campo `base_grand_total` per tutti gli ordini di ciascun cliente univoco |
| `Customer's order number` | Classificazione ordine sequenziale per l&#39;ordine del cliente. Calcolato identificando tutti gli ordini effettuati da un cliente, ordinandoli in ordine crescente in base alla marca temporale `created_at` e assegnando un valore intero incrementale a ciascun ordine. Ad esempio, il primo ordine del cliente restituisce `Customer's order number` di 1, il secondo ordine del cliente restituisce `Customer's order number` di 2 e così via. |
| `Customer's order number (previous-current)` | Classificazione dell&#39;ordine precedente del cliente concatenato con la classificazione di questo ordine, separati da un carattere `-`. Calcolato concatenando (&quot;`Customer's order number` - 1&quot;) con &quot;`-`&quot; seguito da &quot;`Customer's order number`&quot;. Ad esempio, per l&#39;ordine associato al secondo acquisto del cliente, questa colonna restituisce il valore `1-2`. Più spesso utilizzato quando si rappresenta il tempo tra due eventi di ordine (ovvero, nel grafico &quot;Tempo tra gli ordini&quot;) |
| `Is customer's last order?` | Determina se l&#39;ordine corrisponde all&#39;ultimo ordine del cliente o all&#39;ordine più recente. Calcolato confrontando il valore `Customer's order number` con `Customer's lifetime number of orders`. Quando questi due campi sono uguali per l&#39;ordine specificato, questa colonna restituisce `Yes`; in caso contrario restituisce `No` |
| `Number of items in order` | Quantità totale di articoli inclusi nell&#39;ordine. Calcolato unendo `sales_order`.Da `entity_id` a `sales_order_item`.`order_id` e somma di `sales_order_item`.Campo `qty_ordered` |
| `Seconds between customer's first order date and this order` | Tempo trascorso tra questo ordine e il primo ordine del cliente. Calcolato sottraendo `Customer's first order date` da `created_at` per ogni ordine, restituito come numero intero di secondi |
| `Seconds since previous order` | Tempo trascorso tra questo ordine e l&#39;ordine immediatamente precedente del cliente. Calcolato sottraendo `created_at` per l&#39;ordine precedente dal `created_at` di questo ordine, restituito come numero intero di secondi. Ad esempio, per il record dell’ordine corrispondente al terzo ordine di un cliente, questa colonna restituisce il numero di secondi tra il secondo e il terzo ordine del cliente. Per il primo ordine del cliente, questo campo restituisce `NULL` |
| `Shipping address city` | Città di spedizione per l&#39;ordine. Calcolato unendo `sales_order`.Da `shipping_address_id` a `sales_order_address`.`entity_id` e restituzione del campo `city` |
| `Shipping address country` | Codice paese di spedizione per l&#39;ordine. Calcolato unendo `sales_order`.Da `Shipping_address_id` a `sales_order_address`.`entity_id` e restituzione di `country_id` |
| `Shipping address region` | Area di spedizione (spesso stato o provincia) per l&#39;ordine. Calcolato unendo `sales_order`.Da `shipping_address_id` a `sales_order_address`.`entity_id` e restituzione del campo `region` |
| `Store name` | Nome dell&#39;archivio Commerce associato a questo ordine. Calcolato unendo `sales_order`.Da `store_id` a `store`.`store_id` e restituzione del campo `name` |

## Metriche comuni

| **Nome metrica** | **Descrizione** | **Costruzione** |
|---|---|---|
| `Avg order value` | Ricavi medi per ordine, dove i ricavi sono definiti come `base_grand_total` | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | Tempo medio tra l&#39;ordine di un cliente (n-1) e l&#39;ordine n, per tutti i clienti e gli ordini | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | Somma del valore lordo delle merci per tutti gli ordini, dove GMV è definito come subtotale, prima dell&#39;applicazione di tutte le imposte e gli sconti | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | Il tempo mediano tra l&#39;ordine di un cliente (n-1) e l&#39;ordine n°, per tutti i clienti e gli ordini | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | Numero totale di ordini effettuati | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | La somma dei ricavi per tutti gli ordini, in cui i ricavi sono definiti come il prezzo finale pagato dal cliente dopo l&#39;applicazione di tutte le imposte, gli sconti, la spedizione e così via | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | Somma dell&#39;importo di spedizione per tutti gli ordini | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | Somma delle imposte applicate a tutti gli ordini | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | Il numero di clienti univoci che effettuano un ordine nell’intervallo di tempo di reporting specificato. Ad esempio, se l’intervallo del rapporto era settimanale, ogni cliente che effettua almeno un ordine in una data settimana viene conteggiato esattamente una volta, indipendentemente dal numero di ordini che ha effettuato in quella settimana | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key` percorsi di unione

`customer_entity`

* Partecipa alla tabella `customer_entity` per creare nuove colonne a livello di cliente associate al cliente che ha effettuato l&#39;ordine.
   * Percorso: `sales_order.customer_id` (molti) => `customer_entity.entity_id` (uno)

`customer_group`

* Partecipa alla tabella `customer_group` per creare colonne che restituiscono il nome del gruppo di clienti del cliente che ha effettuato l&#39;ordine.
   * Percorso: `sales_order.customer_group_id` (molti) => `customer_group.customer_group_id` (uno)

`sales_order_address`

* Unisciti alla tabella `sales_order_address` per creare colonne che restituiscono le ubicazioni di fatturazione e di spedizione associate all&#39;ordine. Sono possibili due percorsi di unione, a seconda che siano necessari i dettagli di fatturazione o di spedizione.
   * Percorsi:
      * Spedizione: `sales_order.shipping_address_id`(molti) => `sales_order_address.entity_id` (uno)
      * Fatturazione: `sales_order.billing_address_id`(molti) => `sales_order_address.entity_id` (uno)

`store`

* Partecipa alla tabella `store` per creare colonne che restituiscono i dettagli relativi all&#39;archivio Commerce associato all&#39;ordine.
   * Percorso: `sales_order.store_id` (molti) => `store.store_id` (uno)
