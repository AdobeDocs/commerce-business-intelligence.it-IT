---
title: 'Google Analytics: tenere traccia dei dati del dispositivo utente e del browser nel database'
description: Scopri quanti utenti accedono effettivamente tramite dispositivi mobili e come questo influisce sul valore del ciclo di vita di tali utenti.
exl-id: 57b1bc45-b139-4370-86ea-2fbd021aa14d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# [!UICONTROL Google Analytics] Tracking

Con [!UICONTROL Google Analytics] è possibile [salvare le informazioni sull&#39;origine di riferimento](../analysis/google-track-user-acq.md) per capire da dove provengono i tuoi utenti più importanti. In questo argomento vengono fornite informazioni sulla piattaforma (ad esempio, il dispositivo o il browser) su cui stanno lavorando gli utenti. In questo modo, potrai capire quanti utenti accedono effettivamente tramite dispositivi mobili e in che modo ciò influisce sul valore del ciclo di vita di tali utenti.

## Salvataggio dei dati del dispositivo e del browser utente

Ogni volta che viene effettuata una richiesta al sito web, il browser dell’utente invia una stringa Utente-Agente con informazioni sulla piattaforma che effettua la richiesta. Di seguito sono riportati alcuni esempi della stringa Utente-Agente:

1. `Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_8\_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36`
1. `Mozilla/5.0 (Windows NT 6.1; WOW64; rv:17.0) Gecko/17.0 Firefox/17.0`
1. `Mozilla/5.0 (iPhone; U; CPU iPhone OS 4\_0 like Mac OS X; en-us) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8A293 Safari/6531.22.7`
1.
` Mozilla/5.0 (iPad; CPU OS 5\_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B176 Safari/7534.48.3`
1. `Mozilla/5.0 (Linux; U; Android 2.2; en-us; Nexus One Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1`

Se osservi attentamente, puoi vedere che la stringa contiene informazioni sul sistema operativo, sul browser e sul nome del dispositivo utilizzato dall&#39;utente (se ha un nome). Anche se le stringhe Utente-Agente variano notevolmente tra le piattaforme e anche tra le versioni della stessa piattaforma, è generalmente vero che il nome della piattaforma esiste da qualche parte all&#39;interno di. Ad esempio, #1 sopra è un Mac con il browser Chrome, #2 sopra è una macchina Windows con il browser Firefox, #3 è un iPhone, #4 è un iPad e #5 è un dispositivo Android.

Queste informazioni sono accessibili dal server ogni volta che viene effettuata una richiesta. In PHP, la stringa Utente-Agente è memorizzata in `$_SERVER['HTTP_USER_AGENT']`. In Ruby su Rails, viene memorizzato in `request.env['HTTP_USER_AGENT']`. Altri linguaggi e ambienti consentono di accedervi in modo simile.

### Quando registrare questi dati?

È consigliabile aggiungere un nuovo campo denominato `Platform` o `User-Agent` al tuo `Customers` e `Orders` tabelle di database per memorizzare queste informazioni ogni volta che un utente viene creato o viene inserito un ordine. Se si utilizza un database SQL, questo campo deve essere un `VARCHAR(255)`. 

>[!NOTE]
>
>La `User-Agent` La stringa può essere molto più lunga, ma in pratica raramente supera tale lunghezza.

### Come posso analizzare i segmenti utili?

Ci sono diverse librerie là fuori per aiutare ad analizzare il `User-Agent` in componenti quali sistema operativo, dispositivo e così via. Fai riferimento a [progetto ua-parser](https://github.com/tobie/ua-parser) per saperne di più.

Queste nuove informazioni consentono di comprendere meglio come gli utenti accedono al sito. Puoi quindi personalizzare la loro esperienza o creare campagne di marketing per determinati gruppi.

## Correlati

* [Tracciare l’origine di riferimento dell’ordine tramite [!DNL Google Anaytics] E-commerce](../importing-data/integrations/google-ecommerce.md)
* [Tracciare l’origine del riferimento utente nel database](../analysis/google-track-user-acq.md)
* [Scopri le fonti e i canali di acquisizione più importanti](../analysis/most-value-source-channel.md)
* [Collega il tuo [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [Aumenta il ROI delle campagne pubblicitarie](../analysis/roi-ad-camp.md)
* [Come funziona [!DNL Google Analytics] L’attribuzione UTM funziona?](../analysis/utm-attributes.md)
