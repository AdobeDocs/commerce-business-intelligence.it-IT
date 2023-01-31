---
title: Creare grafici a Google Analytics
description: Scopri come creare grafici dai dati Google Analytics.
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# Crea [!DNL Google Analytics] grafici

(con la guida della sintassi regex)

Dopo aver connesso il [[!DNL Google Analytics] account](../../data-analyst/importing-data/integrations/google-analytics.md), puoi creare grafici dal tuo [!DNL Google Analytics] dati.

## Crea [!DNL Google Analytics] Grafici

1. Fai clic su **[!UICONTROL Add Chart** > **Create New Chart]**.

1. Quando selezioni una metrica in `Chart Builder`, scorri fino alla parte inferiore dell’elenco per trovare una sezione che include [!DNL Google Analytics] Profili. Viene visualizzato un secondo menu a discesa della metrica. Qui puoi scegliere la metrica da analizzare.

1. Dopo aver scelto la metrica, puoi procedere con questo grafico come se si trattasse di un altro grafico selezionando la `time period`, `interval`e dati `perspectives` che ti piacerebbe vedere.

1. L&#39;unica grande differenza qui è che `√` utilizza espressioni regolari per i filtri. Un&#39;espressione regolare (regex for short) è una stringa di testo speciale per la descrizione di un pattern di ricerca. Vedi esempi di sintassi regex nella [[!DNL Google] guida sulle espressioni regolari di Analytics](https://support.google.com/analytics/answer/1034324?hl=en).

>[!NOTE]
>
>Gli unici caratteri speciali che devono essere preceduti dal carattere \ sono i metacaratteri seguenti:

|  |  |  |  |  |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style=&quot;table-layout:auto&quot;}
