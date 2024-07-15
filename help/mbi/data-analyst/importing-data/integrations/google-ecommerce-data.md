---
title: Previsti[!DNL Google ECommerce]dati
description: Scopri quali tipi di dati vengono condivisi con Google eCommerce.
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 3f16484f189f6b4a8b072d2e3514d2f170993d60
workflow-type: tm+mt
source-wordcount: '158'
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
