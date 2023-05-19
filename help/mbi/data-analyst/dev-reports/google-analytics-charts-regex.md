---
title: Creare grafici Google Analytics
description: Scopri come creare grafici dai dati Google Analytics.
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
source-git-commit: 3bf4829543579d939d959753eb3017364c6465bd
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Crea [!DNL Google Analytics] grafici

(con aiuto per la sintassi regex)

Dopo aver connesso [[!DNL Google Analytics] account](../../data-analyst/importing-data/integrations/google-analytics.md), è possibile creare grafici con [!DNL Google Analytics] dati.

## Crea [!DNL Google Analytics] Grafici

1. Clic **[!UICONTROL Add Chart** > **Create New Chart]**.

1. Quando si seleziona una metrica in `Chart Builder`, scorri fino alla parte inferiore dell’elenco per trovare una sezione che includa [!DNL Google Analytics] Profili. Viene visualizzato un secondo elenco a discesa delle metriche. Qui puoi scegliere la metrica da analizzare.

1. Dopo aver scelto la metrica, puoi procedere con questo grafico come se fosse un qualsiasi altro grafico selezionando la `time period`, `interval`, e dati `perspectives` che vorresti vedere.

1. L&#39;unica grande differenza è che `√` utilizza espressioni regolari per i filtri. Un’espressione regolare (regex o short) è una stringa di testo speciale che descrive un pattern di ricerca. Vedi esempi di sintassi regex in [[!DNL Google] guida alle espressioni regolari di Analytics](https://support.google.com/analytics/answer/1034324?hl=en).

>[!NOTE]
>
>Gli unici caratteri speciali che devono essere preceduti dal carattere \ sono i metacaratteri seguenti:

|  |  |  |  |  |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style="table-layout:auto"}
