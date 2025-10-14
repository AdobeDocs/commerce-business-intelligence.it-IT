---
title: 'Google Analytics: tieni traccia dei dati del browser e del dispositivo utente nel database'
description: Scopri quanti utenti accedono effettivamente tramite dispositivi mobili e come questo influisce sul loro valore nel ciclo di vita.
exl-id: 57b1bc45-b139-4370-86ea-2fbd021aa14d
role: Admin, User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# Tracciamento di [!UICONTROL Google Analytics]

Con [!UICONTROL Google Analytics] puoi [salvare le informazioni sull&#39;origine del riferimento](../analysis/google-track-user-acq.md) per capire da dove provengono gli utenti più importanti. In questo argomento viene illustrata la piattaforma, ad esempio il dispositivo o il browser, su cui gli utenti stanno lavorando. In questo modo, potrai capire quanti utenti accedono effettivamente tramite dispositivi mobili e in che modo questo influisce sul valore del ciclo di vita di tali utenti.

## Salvataggio dei dati del dispositivo utente e del browser

Ogni volta che viene effettuata una richiesta al sito web, il browser dell’utente invia una stringa Agente utente con informazioni sulla piattaforma che effettua la richiesta. Di seguito sono riportati alcuni esempi della stringa dell’agente utente:

1. `Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_8\_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36`
1. `Mozilla/5.0 (Windows NT 6.1; WOW64; rv:17.0) Gecko/17.0 Firefox/17.0`
1. `Mozilla/5.0 (iPhone; U; CPU iPhone OS 4\_0 like Mac OS X; en-us) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8A293 Safari/6531.22.7`
1.` Mozilla/5.0 (iPad; CPU OS 5\_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B176 Safari/7534.48.3`
1. `Mozilla/5.0 (Linux; U; Android 2.2; en-us; Nexus One Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1`

Se osservi attentamente, vedrai che la stringa contiene informazioni sul sistema operativo dell’utente, sul browser e sul nome del dispositivo che sta utilizzando (se ha un nome). Anche se le stringhe dell’agente utente variano notevolmente tra le piattaforme e persino tra le versioni della stessa piattaforma, è generalmente vero che il nome della piattaforma esisterà da qualche parte all’interno di. Ad esempio, #1 sopra è un Mac con il browser Chrome, #2 sopra è un computer Windows con il browser Firefox, #3 è un iPhone, #4 è un iPad e #5 è un dispositivo Android.

È possibile accedere a queste informazioni dal server ogni volta che viene effettuata una richiesta. In PHP, la stringa dell&#39;agente utente è memorizzata in `$_SERVER['HTTP_USER_AGENT']`. In Ruby on Rails è memorizzato in `request.env['HTTP_USER_AGENT']`. Altri linguaggi e ambienti ti consentiranno di accedervi in modo simile.

### Quando registrare i dati?

[!DNL Adobe] consiglia di aggiungere un nuovo campo denominato `Platform` o `User-Agent` alle tabelle di database `Customers` e `Orders` per memorizzare queste informazioni ogni volta che viene creato un utente o effettuato un ordine. Se si utilizza un database SQL, questo campo deve essere un `VARCHAR(255)`. 

>[!NOTE]
>
>La stringa `User-Agent` può essere molto più lunga di questa, ma in pratica raramente supera questa lunghezza.

### Come posso analizzare i segmenti utili?

Sono disponibili diverse librerie che consentono di analizzare la stringa `User-Agent` in componenti quali sistema operativo, dispositivo e così via. Per ulteriori informazioni, consulta il [progetto ua-parser](https://github.com/tobie/ua-parser).

Con queste nuove informazioni, puoi comprendere meglio in che modo gli utenti accedono al tuo sito. Puoi quindi adattare la loro esperienza o creare campagne di marketing per determinati gruppi.

## Correlato

* [Tracciare l&#39;origine di riferimento dell&#39;ordine tramite  [!DNL Google Anaytics] E-Commerce](../importing-data/integrations/google-ecommerce.md)
* [Tracciare l&#39;origine di riferimento dell&#39;utente nel database](../analysis/google-track-user-acq.md)
* [Scopri le fonti e i canali di acquisizione più importanti](../analysis/most-value-source-channel.md)
* [Connetti il tuo account  [!DNL Google Adwords] &#x200B;](../importing-data/integrations/google-adwords.md)
* [Aumentare il ROI nelle campagne pubblicitarie](../analysis/roi-ad-camp.md)
* [Come funziona l&#39;attribuzione  [!DNL Google Analytics] UTM?](../analysis/utm-attributes.md)
