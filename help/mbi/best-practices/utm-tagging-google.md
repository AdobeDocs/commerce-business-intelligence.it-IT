---
title: Tracciamento UTM nelle Google Analytics
description: Scopri le best practice per il tracciamento UTM (assegnazione tag) nelle Google Analytics.
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# Tracciamento UTM

`UTM` il tracciamento è una convenzione di assegnazione tag per gli URL che consente di analizzare da dove provengono gli utenti. Se osservi gli URL su cui fai clic nella maggior parte delle e-mail di marketing o degli annunci banner, vedrai l’assegnazione di tag UTM. Sono quei collegamenti lunghi che terminano con cose come `utm\_source` e `utm\_medium`.

[!DNL Google Analytics] utilizza `UTM` assegnazione tag per sapere da dove viene il traffico. Alcune di queste informazioni provengono dal [referente HTTP](https://en.wikipedia.org/wiki/HTTP_referer) ma il resto deve fornire a se stessi `UTM` Parametri. Quando vedi `google adwords` o `email marketing` significa `UTM` i parametri da registrare dal collegamento originale clicca e poi memorizzati nei cookie degli utenti. Da lì, [!DNL Google Analytics] utilizza tali dati in [attribuire comportamenti interessanti](../data-analyst/analysis/google-track-user-acq.md) sul tuo sito. Scopri i vantaggi di questi parametri per comprendere come impostare e utilizzare al meglio i tag UTM.

## Tecniche consigliate per l’assegnazione di tag UTM

Di seguito sono elencate le cinque cose più importanti da ricordare durante la configurazione degli URL con `UTM` assegnazione tag.

### 1. Scopri come assegnare tag a ogni URL che puoi controllare arrivando al tuo sito

Ogni volta che chiedi alle persone di fare clic su un collegamento, devi configurare `UTM` assegnazione tag. Questo include tutti i tuoi collegamenti e-mail (il tuo provider di servizi e-mail probabilmente ha un modo per assegnare automaticamente tag ai tuoi URL), collegamenti ad, articoli per la stampa, post di blog.

### 2. Utilizza uno strumento per creare l’URL

`UTM`Gli URL con tag possono essere piuttosto ingombranti. Invece di cercare di digitarli a lungo, utilizza uno strumento [come questo](https://support.google.com/analytics/answer/1033867?hl=en) per aiutarti. Questo ti assicura di pensare aggiungendo tutti i parametri ragionevoli all’URL e di ottenere l’URL per copiarlo e incollarlo immediatamente. Per gestire i collegamenti social, strumenti come [!DNL Hootsuite] includi l’opzione per aggiungere parametri URL personalizzati a tutti i tuoi collegamenti.

### 3. Assicurati di fare distinzione tra maiuscole e minuscole nei valori dei parametri

È importante ricordare che il tag `utm\_source=adwords` è un tag diverso da `utm\_source=Adwords`. Considera di rendere tutto minuscolo.

### 4. Memorizza i valori dei parametri UTM nel database

Ogni volta che si verifica una transazione o un evento, è necessario valutare le prestazioni delle attività di marketing. Per farlo, leggi i valori dei valori dei parametri UTM dal [[!DNL Google Analytics] cookie nel database](../data-analyst/analysis/google-track-user-acq.md).

### 5. Pensa a come denominare le campagne

Per tenere traccia del miglioramento delle attività di marketing nel tempo, è necessario essere intelligenti nelle convenzioni di denominazione. Semplificalo e riduci il più possibile. I sistemi di denominazione complicati sono più difficili da mantenere.

Una volta acquisiti questi dati nel database, puoi valutare le prestazioni di marketing e pubblicità mediante analisi più sofisticate, tra cui [Valore del ciclo di vita del cliente](../data-analyst/analysis/ess-expected-ltv.md), [Tassi di acquisto ripetuti](../data-analyst/analysis/repurchase-behavior.md)e [Valore medio dell&#39;ordine](../data-analyst/analysis/basic-analytics.md).
