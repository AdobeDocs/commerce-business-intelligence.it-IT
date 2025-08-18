---
title: Tracciamento UTM in Google Analytics
description: Scopri le best practice per il tracciamento UTM (assegnazione tag) in Google Analytics.
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Tracciamento UTM

Il monitoraggio di `UTM` è una convenzione di assegnazione tag per gli URL che consente di analizzare la provenienza degli utenti. Se osservi gli URL su cui fai clic nella maggior parte delle e-mail di marketing o dei banner pubblicitari, visualizzi l’assegnazione tag UTM. Questi collegamenti lunghi terminano con elementi come `utm\_source` e `utm\_medium`.

[!DNL Google Analytics] utilizza l&#39;assegnazione tag `UTM` per sapere da dove proviene il traffico. Alcune di queste informazioni provengono dal [referrer HTTP](https://en.wikipedia.org/wiki/HTTP_referer), ma per il resto devi fornire a te stesso `UTM` parametri. Quando visualizzi `google adwords` o `email marketing`, significa che questi `UTM` parametri vengono registrati dal clic del collegamento originale e quindi memorizzati nei cookie degli utenti. Da lì, [!DNL Google Analytics] utilizza questi dati per [attribuire comportamenti interessanti](../data-analyst/analysis/google-track-user-acq.md) sul tuo sito. Comprendere a cosa servono questi parametri consente di comprendere il modo migliore per impostare e utilizzare l’assegnazione tag UTM.

## Best practice per l’assegnazione tag UTM

Di seguito sono elencati i cinque elementi più importanti da ricordare durante la configurazione degli URL con tag `UTM`.

### &#x200B;1. Imposta i tag per ogni URL controllabile che arriva sul tuo sito

Ogni volta che si chiede alle persone di fare clic su un collegamento, è necessario impostare l&#39;assegnazione tag `UTM`. Questo include tutti i tuoi collegamenti e-mail (il provider di servizi e-mail probabilmente ha un modo per assegnare automaticamente tag ai tuoi URL), collegamenti agli annunci, articoli di stampa, post di blog.

### &#x200B;2. Utilizzare uno strumento per creare l’URL

Gli URL con tag di `UTM` possono essere complicati. Invece di digitarli a lungo, utilizza uno strumento [simile a questo](https://support.google.com/analytics/answer/1033867?hl=en) per aiutarti. In questo modo puoi aggiungere all’URL tutti i parametri pertinenti e ottenere l’URL da copiare e incollare immediatamente. Per gestire i collegamenti social, strumenti come [!DNL Hootsuite] includono l&#39;opzione di aggiungere parametri URL personalizzati a tutti i collegamenti.

### &#x200B;3. Assicurati di fare distinzione tra maiuscole e minuscole nei valori dei parametri

È importante ricordare che il tag `utm\_source=adwords` è diverso da `utm\_source=Adwords`. Valuta di usare solo minuscole.

### &#x200B;4. Memorizza i valori dei parametri UTM nel database

Ogni volta che si verifica una transazione o un evento, desideri valutare le prestazioni delle attività di marketing. A tale scopo, leggere i valori dei parametri UTM dal cookie [[!DNL Google Analytics] nel database](../data-analyst/analysis/google-track-user-acq.md).

### &#x200B;5. Pensa al nome delle campagne

Per monitorare il miglioramento delle attività di marketing nel tempo, è necessario conoscere in modo intelligente le convenzioni di denominazione. Semplificalo e riduci al minimo il più possibile. I sistemi di denominazione complicati sono più difficili da mantenere.

Una volta acquisiti questi dati nel database, puoi valutare le prestazioni del marketing e della pubblicità tramite analisi più sofisticate, tra cui [Valore durata cliente](../data-analyst/analysis/ess-expected-ltv.md), [Tassi di acquisto ripetuti](../data-analyst/analysis/repurchase-behavior.md) e [Valore medio ordine](../data-analyst/analysis/basic-analytics.md).
