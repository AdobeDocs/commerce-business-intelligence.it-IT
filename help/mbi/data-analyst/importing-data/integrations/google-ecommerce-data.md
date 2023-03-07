---
title: Previsto[!DNL Google ECommerce]dati
description: Scopri quali tipi di dati vengono condivisi con Google eCommerce.
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# Previsto[!DNL Google ECommerce] dati

Dopo il [!DNL Google ECommerce] l&#39;account è connesso correttamente a [!DNL MBI], il sistema inizierà a importare i dati in una tabella con titolo `ecommerce`. Questa tabella registra una riga di dati per ogni transazione. Sono incluse le seguenti colonne di dati a livello di ordine:

| Nome colonna | Descrizione |
|-----|-----|
| `\_id` | Questa colonna è la chiave primaria. |
| `accountId` | Questa colonna contiene l’ID account associato al tuo [!DNL Google Analytics] Account eCommerce. |
| `profileName` | Questa colonna contiene [!DNL Google Analytics] nome profilo. |
| `profileId` | Questa colonna contiene [!DNL Google Analytics] ID profilo. |
| `socialNetwork` | Questa colonna contiene il nome del social network (ad esempio, [!DNL Facebook], o [!DNL YouTube]) |
| `campaign` | Questa colonna contiene il nome della campagna (ad esempio, [`utm\_campaign`](https://support.google.com/analytics/answer/1033867?hl=en)). |
| `medium` | Questa colonna contiene il nome del supporto (ad esempio, [`utm\_medium`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `source` | Questa colonna contiene il nome dell’origine. (ad esempio, [`utm\_source`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `keyword` | Questa colonna contiene la descrizione della parola chiave (ad esempio, [`utm\_term`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `transactionId` | Questa colonna contiene l’ID ordine. Viene utilizzato per unire i dati di riferimento ai dati degli ordini. |
| `updated\_at` | Questa colonna contiene l’ultimo aggiornamento della riga di dati. |

{style="table-layout:auto"}
