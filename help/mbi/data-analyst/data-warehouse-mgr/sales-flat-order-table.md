---
title: tabella sales_order
description: Scopri come utilizzare la tabella sales_order .
exl-id: 19a8ab88-de51-48f8-af39-ae4897834afe
source-git-commit: 73373924b7adaffabf643b65bd290ce2d9408574
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 0%

---

# `sales_order` Tabella

La `sales_order` tabella (`sales_flat_order` su M1) è il luogo in cui viene acquisito ogni ordine. Nella maggior parte dei casi, ogni riga rappresenta un ordine univoco, anche se esistono implementazioni personalizzate di Commerce che consentono di suddividere un ordine in righe separate.

Questa tabella include tutti gli ordini dei clienti, indipendentemente dal fatto che l&#39;ordine sia stato elaborato tramite il pagamento degli ordini degli ospiti. Se il tuo negozio accetta il pagamento degli ospiti, puoi trovare ulteriori informazioni su questo [caso d&#39;uso](../data-warehouse-mgr/guest-orders.md).

## Colonne comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `base_currency_code` | Valuta per tutti i valori acquisiti in `base_*` campi `base_grand_total`, `base_subtotal`e così via). In genere questo riflette la valuta predefinita dell’archivio Commerce |
| `base_discount_amount` | Valore sconto applicato all&#39;ordine |
| `base_grand_total` | Prezzo finale pagato dal cliente sull&#39;ordine, dopo l&#39;applicazione di tutte le tasse, la spedizione e gli sconti. Sebbene il calcolo preciso sia personalizzabile, in generale il `base_grand_total` è calcolato come segue `base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount` |
| `base_subtotal` | Valore lordo delle merci di tutti gli elementi inclusi nell&#39;ordine. Tasse, spedizioni, sconti e così via non sono inclusi |
| `base_shipping_amount` | Valore di spedizione applicato all&#39;ordine |
| `base_tax_amount` | Valore fiscale applicato all&#39;ordine |
| `billing_address_id` | `Foreign key` associato a `sales_order_address` tabella. Iscriviti a `sales_order_address.entity_id` per determinare i dettagli dell&#39;indirizzo di fatturazione associati all&#39;ordine |
| `coupon_code` | Coupon applicato su ordine. Se non viene applicato alcun coupon, questo campo viene `NULL` |
| `created_at` | Timestamp di creazione dell&#39;ordine, in genere memorizzato localmente in UTC. A seconda della configurazione in [!DNL MBI], questa marca temporale può essere convertita in un fuso orario per la generazione di rapporti in [!DNL MBI] diverso dal fuso orario del database |
| `customer_email` | Indirizzo e-mail del cliente che effettua l’ordine. Questo verrà popolato in tutte le situazioni, inclusi gli ordini elaborati tramite il pagamento degli ospiti |
| `customer_group_id` | Chiave esterna associata al `customer_group` tabella. Iscriviti a `customer_group.customer_group_id` per determinare il gruppo di clienti associato all&#39;ordine |
| `customer_id` | `Foreign key` associato a `customer_entity` se il cliente è registrato. Iscriviti a `customer_entity.entity_id` per determinare gli attributi del cliente associati all’ordine. Se l&#39;ordine è stato effettuato tramite il pagamento per gli ospiti, questo campo sarà `NULL` |
| `entity_id` (PK) | Identificatore univoco per la tabella e comunemente utilizzato nei join ad altre tabelle all’interno dell’istanza Commerce |
| `increment_id` | Identificatore univoco per un ordine, comunemente denominato `order_id` nel Magento. La `increment_id` viene utilizzato più spesso per gli join a sorgenti esterne, come [!DNL Google Ecommerce] |
| `shipping_address_id` | Chiave esterna associata al `sales_order_address` tabella. Iscriviti a `sales_order_address.entity_id` per determinare i dettagli dell&#39;indirizzo di spedizione associati all&#39;ordine |
| `status` | Stato dell&#39;ordine. Può restituire valori come &quot;complete&quot;, &quot;elaborazioni&quot;, &quot;annullate&quot;, &quot;rimborsate&quot; ed eventuali stati personalizzati implementati nell’istanza Commerce. Soggetto a modifiche durante l&#39;elaborazione dell&#39;ordine |
| `store_id` | `Foreign key` associato a `store` tabella. Iscriviti a `store`.`store_id` per determinare quale visualizzazione dell&#39;archivio Commerce è associata all&#39;ordine |

{style=&quot;table-layout:auto&quot;}

## Colonne calcolate comuni

| **Nome colonna** | **Descrizione** |
|---|---|
| `Billing address city` | Città di fatturazione per l&#39;ordine. Calcolato mediante unione `sales_order`.`billing_address_id` a `sales_order_address`.`entity_id` e restituendo `city` field |
| `Billing address country` | Codice del paese di fatturazione per l&#39;ordine. Calcolato mediante unione `sales_order`.`billing_address_id` a `sales_order_address`.`entity_id` e restituendo `country_id` |
| `Billing address region` | Area di fatturazione (più spesso stato o provincia) per l&#39;ordine. Calcolato mediante unione `sales_order`.`billing_address_id` a `sales_order_address`.`entity_id` e restituendo `region` field |
| `Customer's first order date` | Timestamp del primo ordine inserito dal cliente. Spesso considerato come la &quot;data di acquisizione&quot; per un cliente. Calcolato restituendo il minimo `sales_order`.`created_at` valore per ogni cliente univoco |
| `Customer's first order's billing region` | Area di fatturazione dell’acquisizione per il cliente che ha effettuato l’ordine. Calcolato restituendo la variabile `Billing address region` associato al primo ordine del cliente |
| `Customer's first order's coupon_code` | Codice coupon di acquisizione per il cliente che ha effettuato questo ordine. Calcolato restituendo la variabile `coupon_code` associato al primo ordine del cliente |
| `Customer's group code` | Nome del gruppo del cliente che ha effettuato l&#39;ordine. Calcolato mediante unione `sales_order`.`customer_group_id` a `customer_group`.`customer_group_id` e restituendo `customer_group_code` field |
| `Customer's lifetime number of coupons` | Quantità totale di coupon applicati a tutti gli ordini immessi dal cliente. Calcolato contando il numero di ordini in cui il `coupon_code` non `NULL` per ogni cliente unico |
| `Customer's lifetime number of orders` | Totale degli ordini effettuati dal cliente. Calcolato contando il numero di righe nel `sales_order` tabella per ogni cliente univoco |
| `Customer's lifetime revenue` | Somma totale dei ricavi per tutti gli ordini effettuati dal cliente. Calcolato sommando il `base_grand_total` campo per tutti gli ordini per ogni cliente unico |
| `Customer's order number` | Classificazione ordine sequenziale per l&#39;ordine del cliente. Calcolato identificando tutti gli ordini immessi da un cliente, ordinandoli in ordine crescente in base al `created_at` marca temporale e assegnazione di un valore intero incrementale a ciascun ordine. Ad esempio, il primo ordine del cliente restituisce un `Customer's order number` 1; il secondo ordine restituisce un `Customer's order number` 2; e così via |
| `Customer's order number (previous-current)` | Classificazione dell&#39;ordine precedente del cliente concatenato con il rango di questo ordine, separato da un `-` carattere. Calcolato concatenando (&quot;`Customer's order number` - 1&quot;) con &quot;`-`&quot; seguito da &quot;`Customer's order number`&quot;. Ad esempio, per l’ordine associato al secondo acquisto del cliente, questa colonna restituirà un valore di `1-2`. Utilizzato più spesso per rappresentare il tempo tra due eventi dell&#39;ordine (cioè nel grafico &quot;Intervallo di tempo tra gli ordini&quot;) |
| `Is customer's last order?` | Determina se l&#39;ordine corrisponde o meno all&#39;ultimo ordine del cliente o all&#39;ultimo ordine più recente. Calcolato confrontando il `Customer's order number` con `Customer's lifetime number of orders`. Quando questi due campi sono uguali all’ordine specificato, questa colonna restituisce &quot;Sì&quot;; altrimenti restituisce &quot;No&quot; |
| `Number of items in order` | Quantità totale di articoli inclusi nell&#39;ordine. Calcolato mediante unione `sales_order`.`entity_id` a `sales_order_item`.`order_id` e sommare `sales_order_item`.`qty_ordered` field |
| `Seconds between customer's first order date and this order` | Tempo trascorso tra questo ordine e il primo ordine del cliente. Calcolato mediante sottrazione `Customer's first order date` dal `created_at` per ogni ordine, restituito come numero intero di secondi |
| `Seconds since previous order` | Tempo trascorso tra questo ordine e l&#39;ordine immediatamente precedente del cliente. Calcolato sottraendo il `created_at` per l&#39;ordine precedente dal `created_at` di questo ordine, restituito come numero intero di secondi. Ad esempio, per il record dell&#39;ordine corrispondente al terzo ordine del cliente, questa colonna restituisce il numero di secondi tra il secondo ordine del cliente e il terzo ordine. Per il primo ordine del cliente, questo campo restituirà `NULL` |
| `Shipping address city` | Città di spedizione per l&#39;ordine. Calcolato mediante unione `sales_order`.`shipping_address_id` a `sales_order_address`.`entity_id` e restituendo `city` field |
| `Shipping address country` | Codice del paese di spedizione per l&#39;ordine. Calcolato mediante unione `sales_order`.`Shipping_address_id` a `sales_order_address`.`entity_id` e restituendo `country_id` |
| `Shipping address region` | Regione di spedizione (più spesso stato o provincia) per l&#39;ordine. Calcolato mediante unione `sales_order`.`shipping_address_id` a `sales_order_address`.`entity_id` e restituendo `region` field |
| `Store name` | Nome dell&#39;archivio Commerce associato a questo ordine. Calcolato mediante unione `sales_order`.`store_id` a `store`.`store_id` e restituendo `name` field |

## Metriche comuni

| **Nome della metrica** | **Descrizione** | **Costruzione** |
|---|---|---|
| `Avg order value` | Il ricavo medio per ordine, in cui il ricavo è definito come `base_grand_total` | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | Tempo medio tra l&#39;ordine (n-1) di un cliente e l&#39;ordine nth, per tutti i clienti e gli ordini | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | La somma del valore lordo delle merci per tutti gli ordini, in cui il GMV è definito come il subtotale, prima che siano applicate tutte le imposte e gli sconti | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | Il tempo medio tra l&#39;ordine (n-1) di un cliente e l&#39;ordine nth, per tutti i clienti e gli ordini | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | Totale degli ordini inseriti | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | La somma dei ricavi per tutti gli ordini, in cui i ricavi sono definiti come il prezzo finale pagato dal cliente, dopo l&#39;applicazione di tutte le imposte, gli sconti, la spedizione e così via | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | La somma dell&#39;importo della spedizione per tutti gli ordini | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | Somma delle imposte applicate a tutti gli ordini | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | Il numero di clienti univoci che ordinano un ordine nell&#39;intervallo di tempo di reporting specificato. Ad esempio, se l’intervallo del rapporto è settimanale, ogni cliente che inserisce almeno un ordine in una data settimana sarà conteggiato esattamente una volta, indipendentemente dal numero di ordini che ha effettuato in quella settimana | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key` Unione dei percorsi

`customer_entity`

* Iscriviti a `customer_entity` per creare nuove colonne a livello di cliente associate al cliente che ha effettuato l’ordine.
   * Percorso: `sales_order.customer_id` (molti) => `customer_entity.entity_id` 1)

`customer_group`

* Iscriviti a `customer_group` per creare nuove colonne che restituiscono il nome del gruppo di clienti del cliente che ha effettuato l’ordine.
   * Percorso: `sales_order.customer_group_id` (molti) => `customer_group.customer_group_id` 1)

`sales_order_address`

* Iscriviti a `sales_order_address` tabella per creare nuove colonne che restituiscono le posizioni di fatturazione e spedizione associate all&#39;ordine. Sono possibili due percorsi di unione, a seconda che siano richiesti i dettagli di fatturazione o spedizione.
   * Percorsi:
      * Spedizione: `sales_order.shipping_address_id`(molti) => `sales_order_address.entity_id` 1)
      * Fatturazione: `sales_order.billing_address_id`(molti) => `sales_order_address.entity_id` 1)

`store`

* Iscriviti a `store` per creare nuove colonne che restituiscono i dettagli relativi all&#39;archivio Commerce associato all&#39;ordine.
   * Percorso: `sales_order.store_id` (molti) => `store.store_id` 1)
