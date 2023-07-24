---
title: Tracciamento UTM nelle Google Analytics
description: Scopri le best practice per il tracciamento UTM (assegnazione tag) nelle Google Analytics.
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# Tracciamento UTM

`UTM` il tracciamento è una convenzione di assegnazione tag per gli URL che consente di analizzare la provenienza degli utenti. Se osservi gli URL su cui fai clic nella maggior parte delle e-mail di marketing o dei banner pubblicitari, visualizzi l’assegnazione tag UTM. Sono quei lunghi collegamenti che terminano con cose come `utm\_source` e `utm\_medium`.

[!DNL Google Analytics] utilizza `UTM` assegnare tag per sapere da dove proviene il traffico. Alcune di queste informazioni provengono da [referrer HTTP](https://en.wikipedia.org/wiki/HTTP_referer) ma il resto devi fornirti... `UTM` parametri. Quando vedi `google adwords` o `email marketing`, significa che `UTM` i parametri registrati dal clic del collegamento originale vengono quindi memorizzati nei cookie degli utenti. Da lì, [!DNL Google Analytics] utilizza tali dati per [attribuire comportamenti interessanti](../data-analyst/analysis/google-track-user-acq.md) sul tuo sito. Comprendere a cosa servono questi parametri consente di comprendere il modo migliore per impostare e utilizzare l’assegnazione tag UTM.

## Best practice per l’assegnazione tag UTM

Di seguito sono elencati i cinque elementi più importanti da ricordare durante la configurazione degli URL con `UTM` assegnazione tag.

### 1. Imposta i tag per ogni URL controllabile che arriva sul tuo sito

Ogni volta che chiedi a qualcuno di fare clic su un collegamento, devi impostare `UTM` assegnazione tag. Questo include tutti i tuoi collegamenti e-mail (il provider di servizi e-mail probabilmente ha un modo per assegnare automaticamente tag ai tuoi URL), collegamenti agli annunci, articoli di stampa, post di blog.

### 2. Utilizzare uno strumento per creare l’URL

`UTM`Gli URL con tag possono essere complicati. Invece di digitarli a lungo, utilizza uno strumento [piace questo](https://support.google.com/analytics/answer/1033867?hl=en) per aiutarti. In questo modo puoi aggiungere all’URL tutti i parametri pertinenti e ottenere l’URL da copiare e incollare immediatamente. Per gestire i collegamenti social, puoi utilizzare strumenti come [!DNL Hootsuite] includi l’opzione per aggiungere parametri URL personalizzati a tutti i collegamenti.

### 3. Assicurati di fare distinzione tra maiuscole e minuscole nei valori dei parametri

È importante ricordare che il tag `utm\_source=adwords` è un tag diverso da `utm\_source=Adwords`. Valuta di usare solo minuscole.

### 4. Memorizza i valori dei parametri UTM nel database

Ogni volta che si verifica una transazione o un evento, desideri valutare le prestazioni delle attività di marketing. A tale scopo, leggere i valori dei parametri UTM dall&#39; [[!DNL Google Analytics] cookie nel database](../data-analyst/analysis/google-track-user-acq.md).

### 5. Pensa al nome delle campagne

Per monitorare il miglioramento delle attività di marketing nel tempo, è necessario conoscere in modo intelligente le convenzioni di denominazione. Semplificalo e riduci al minimo il più possibile. I sistemi di denominazione complicati sono più difficili da mantenere.

Una volta acquisiti questi dati nel database, puoi valutare le prestazioni del marketing e della pubblicità tramite analisi più sofisticate, tra cui [Valore ciclo di vita cliente](../data-analyst/analysis/ess-expected-ltv.md), [Tassi di acquisto ripetuti](../data-analyst/analysis/repurchase-behavior.md), e [Valore medio ordine](../data-analyst/analysis/basic-analytics.md).
