---
title: Creare grafici Google Analytics
description: Scopri come creare grafici dai dati di Google Analytics.
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/xfh0BjVasnSNP9mic7ps4jckaGpjF7INFNi2lSaKi-o
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 160
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
