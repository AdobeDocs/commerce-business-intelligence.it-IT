---
title: MBI Essentials vs Pro
description: Scopri in che modo MBI Essentials differisce da MBI Pro.
exl-id: 624a6285-8497-43d9-a56d-8ae503e0e2dd
source-git-commit: dcd02693b3ca060ecdc47cbee189428ce157dd58
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 4%

---

# [!DNL MBI Essentials] vs [!DNL MBI Pro]

>[!NOTE]
>
>Questa è la documentazione archiviata per [!DNL MBI].

La tabella seguente descrive cosa è incluso in Essentials e Pro.

|  | **`MBI Essentials`** | **`MBI Pro`** |
|-----|-----|-----|
| `Pre-Defined Reports` | Fino a 100 | Personalizzato |
| `Pre-Defined Dashboards` | 5-6 | Personalizzato |
| `New Custom Report Creation` | Sì | Sì |
| `Commerce Tables` | 4-6 | Senza limiti |
| `Log-ins/User Accounts` | 10 | 20 |
| `User Permissions` | Sì | Sì |
| `Data Warehouse Manager` | Non disponibile | Disponibile |
| `Email Reports` | Sì | Sì |
| `Cohort Report Builder` | Sì | Sì |
| `Google Analytics Live Integration` | Sì | Senza limiti |
| `3rd Party Integrations` | Non disponibile | Disponibile |
| `Full API Access` | No | Sì |
| `Access to CS, AM, or Analysts` | No | Sì |
| `Professional Services` | Disponibile | Disponibile |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Il numero di tabelle dipende dal pagamento degli ospiti.

**Tabelle incluse**

* `sales\_order`
* `sales\_order\_item`
* `sales\_order\_address`
* `customer\_entity`
* `customer\_group`
* `store`

## Colonne incluse nelle funzioni di base

Elementi in _corsivo_ sono campi calcolati.

* `sales_order` tabella
   * `entity_id`
   * `base_grand_total`
   * `customer_id`
   * `status`
   * `customer_email`
   * `store_id`
   * `base_currency_code`
   * `billing_address_id`
   * `shipping_address_id`
   * `base_shipping_amount`
   * `base_tax_amount`
   * `coupon_code`
   * `created_at`
   * `updated_at`
   * `base_subtotal`
   * `customer_group_id`
   * `base_discount_amount`
   * `base_discount_invoiced`
   * `increment_id`
   * `Customer's order number`
   * `Customer's first order date`
   * `Customer's lifetime number of orders`
   * `Is customer's last order?`
   * `Billing address region`
   * `Shipping address country`
   * `Customer's lifetime revenue`
   * `Seconds between customer's first order date and this order`
   * `Seconds since previous order`
   * `Store name`
   * `Customer's lifetime number of coupons`
   * `Customer's order number (previous-current)`
   * `Shipping address region`
   * `Number of items in order`
   * `Billing address city`
   * `Shipping address city`
   * `Customer's group code`
   * `Customer's first order's billing region`
   * `Customer's first order's coupon_code`
   * `Customer's creation date`
   * `Billing address country`

* `sales_order_item` tabella
   * `item_id`
   * `qty_ordered`
   * `base_price`
   * `name`
   * `order_id`
   * `sku`
   * `product_type`
   * `product_id`
   * `created_at`
   * `updated_at`
   * `parent_item_id`
   * `store_id`
   * `base_discount_amount`
   * `base_discount_invoiced`
   * `Order's coupon_code`
   * `Order item total value (quantity * price)`
   * `Order's increment_id`
   * `Customer's email`
   * `Customer's lifetime number of orders`
   * `Store name`
   * `Customer's order number`
   * `Order's status`
   * `Customer's lifetime revenue`

* `sales_order_address` tabella
   * `entity_id`
   * `city`
   * `region`
   * `country_id`

* `customer_entity` tabella
   * `entity_id`
   * `email`
   * `group_id`
   * `created_at`
   * `updated_at`
   * `store_id`
   * `Customer's lifetime revenue`
   * `Customer's lifetime number of coupons`
   * `Customer's first order date`
   * `Customer's lifetime number of orders`
   * `Seconds since customer's first order date`
   * `Customer's first 30 day revenue`
   * `Customer's first order's billing region`
   * `Customer's first order's coupon_code`
   * `Customer's group code`
   * `Store name`

* `customer_group` tabella
   * `customer_group_id`
   * `customer_group_code`

* `store` tabella
   * `store_id`
   * `name`

