---
title: Previsti[!DNL Google ECommerce]dati
description: Scopri quali tipi di dati vengono condivisi con Google eCommerce.
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/tGcSyz6DHcusK-RomMkRZoyY7acXb0dmXlHcc5pW7cg
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 158
ht-degree: 0%

---

# Previsti [!DNL Google ECommerce] dati

Una volta stabilita la connessione dell&#39;account [!DNL Google ECommerce] a [!DNL Commerce Intelligence], il sistema inizierà l&#39;importazione dei dati in una tabella denominata `ecommerce`. Questa tabella registra una riga di dati per ogni transazione. Sono incluse le seguenti colonne di dati a livello di ordine:

| Nome colonna | Descrizione |
|-----|-----|
| `\_id` | Questa colonna è la chiave primaria. |
| `accountId` | Questa colonna contiene l&#39;ID account associato all&#39;account eCommerce [!DNL Google Analytics]. |
| `profileName` | Questa colonna contiene il nome del profilo [!DNL Google Analytics]. |
| `profileId` | Questa colonna contiene l&#39;ID profilo [!DNL Google Analytics]. |
| `socialNetwork` | Questa colonna contiene il nome del social network, ad esempio [!DNL Facebook] o [!DNL YouTube] |
| `campaign` | Questa colonna contiene il nome della campagna, ad esempio [`utm\_campaign`](https://support.google.com/analytics/answer/1033867?hl=en). |
| `medium` | Questa colonna contiene il nome del supporto (ad esempio, [`utm\_medium`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `source` | Questa colonna contiene il nome dell’origine. (ad esempio, [`utm\_source`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `keyword` | Questa colonna contiene la descrizione della parola chiave, ad esempio [`utm\_term`](https://support.google.com/analytics/answer/1033867?hl=en) |
| `transactionId` | Questa colonna contiene l’ID ordine. Viene utilizzato per unire i dati di riferimento ai dati degli ordini. |
| `updated\_at` | Questa colonna contiene l’ultimo aggiornamento della riga di dati. |

{style="table-layout:auto"}
