---
title: Creare grafici Google Analytics
description: Scopri come creare grafici dai dati di Google Analytics.
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---

# Crea [!DNL Google Analytics] grafici

(con aiuto per la sintassi regex)

Dopo aver connesso il tuo [[!DNL Google Analytics] account](../../data-analyst/importing-data/integrations/google-analytics.md), puoi creare grafici con i tuoi dati di [!DNL Google Analytics].

## Crea [!DNL Google Analytics] grafici

1. Fare clic su **[!UICONTROL Add Chart** > **Create New Chart]**.

1. Quando selezioni una metrica in `Chart Builder`, scorri fino alla fine dell&#39;elenco per trovare una sezione che includa i tuoi profili [!DNL Google Analytics]. Viene visualizzato un secondo elenco a discesa delle metriche. Qui puoi scegliere la metrica da analizzare.

1. Dopo aver scelto la metrica, è possibile procedere con il grafico come se si trattasse di un qualsiasi altro grafico selezionando `time period`, `interval` e i dati `perspectives` che si desidera visualizzare.

1. L&#39;unica differenza importante è che `√` utilizza espressioni regolari per i filtri. Un’espressione regolare (regex o short) è una stringa di testo speciale che descrive un pattern di ricerca. Vedi esempi di sintassi regex nella [[!DNL Google] guida sulle espressioni regolari di Analytics](https://support.google.com/analytics/answer/1034324?hl=en).

>[!NOTE]
>
>Gli unici caratteri speciali che devono essere preceduti dal carattere \ sono i metacaratteri seguenti:

| | | | | |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style="table-layout:auto"}
