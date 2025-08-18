---
title: Attribuzione Google Analytics e UTM
description: Scopri il processo di attribuzione sorgente di Google Analytics.
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
role: Admin, Data Architect, Data Engineer, User
feature: Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# Attribuzione [!DNL Google Analytics] e UTM

È fondamentale [tenere traccia dell&#39;origine di acquisizione dell&#39;utente](../../data-analyst/analysis/google-track-user-acq.md) per [identificare le campagne pubblicitarie con le prestazioni migliori](../../data-analyst/analysis/most-value-source-channel.md). Questo argomento esplora il processo di attribuzione dell&#39;origine [!DNL Google Analytics]. In altre parole, quale informazione viene registrata quando.

## Cos’è l’attribuzione?

`Attribution` sta per specificare un&#39;origine di riferimento per una particolare attività. Tali attività sono in genere macro-conversioni o micro-conversioni, ad esempio **acquisti**, micro **registrazione, iscrizione e-mail, commento al blog** e così via.

Idealmente, ogni volta che si verifica un evento di conversione, viene registrata una sorgente di riferimento. Ma come viene determinata la sorgente?

La realtà è che gli utenti spesso provengono da diverse origini prima di raggiungere o eseguire una micro o macro conversione. Ad esempio, possono arrivare al sito tramite Organic, poi uscire, poi venire tramite ricerca a pagamento, poi uscire, quindi venire direttamente al sito stesso. Queste informazioni di tracciamento delle sorgenti vengono spesso fornite al sito tramite i parametri UTM, ma esistono anche sistemi più sofisticati. Per il tuo scopo, concentrati su [UTM](https://support.google.com/analytics/answer/1033867?hl=en&ref_topic=1032998).

## In che modo [!DNL Google Analytics] attribuisce origini di riferimento tramite parametri UTM?

Quando i parametri UTM vengono specificati nell&#39;URL, vengono analizzati e inseriti in un [!DNL Google Analytics] [cookie](https://en.wikipedia.org/wiki/HTTP_cookie). Se un sito Web non ha [!DNL Google Analytics], non ha senso avere UTM. [!DNL Google Analytics] ha delle regole su come gestire un utente che hit con più URL tramite UTM durante il suo ciclo di vita (ulteriori informazioni in seguito). Supponendo che il sito Web sia configurato per acquisire i parametri UTM in un database esterno, quando si verifica una conversione micro o macro, qualsiasi elemento del cookie [!DNL Google Analytics] al momento della conversione viene replicato nel database.

## Primo clic e ultimo clic

### Attribuzione ultimo clic

L&#39;attribuzione ultimo clic è il modello di attribuzione più comune utilizzato da [!DNL Google Analytics]. In questo caso, il cookie [!DNL Google Analytics] rappresenta i parametri UTM per l&#39;origine più recente prima dell&#39;evento di conversione, ed è [registrato nel database](../../data-analyst/analysis/google-track-user-acq.md). Il cookie [!DNL Google Analytics] sovrascrive i parametri UTM precedenti solo se l&#39;utente fa clic su un nuovo URL che contiene un nuovo set di parametri UTM.

Consideriamo ad esempio un utente che visita prima un sito Web tramite [!DNL Google Analytics] *ricerca a pagamento*, poi restituisce tramite *ricerca organica* e infine ritorna al *sito Web direttamente* o tramite un *collegamento e-mail* **senza parametri UTM** prima dell&#39;evento di conversione. In questo esempio, il cookie [!DNL Google Analytics] indica che l&#39;origine dell&#39;utente è organica, poiché rappresenta l&#39;ultima origine prima della conversione. Il *percorso* dell&#39;utente prima dell&#39;evento di conversione finale viene ignorato. Se invece l&#39;utente ha visitato il sito Web da un collegamento e-mail con UTM, il cookie [!DNL Google Analytics] indicherà che l&#39;origine è &quot;e-mail&quot;. Pertanto, se nel cookie sono presenti parametri UTM esistenti e l&#39;utente accede tramite direct, il cookie [!DNL Google Analytics] mostra i parametri UTM anziché &quot;direct&quot;.

>[!NOTE]
>
>I parametri cookie [!DNL Google Analytics] di un utente specifico vengono cancellati alla scadenza del cookie [o quando un utente cancella i suoi cookie nel browser.*](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage)

### Attribuzione con primo clic

Alcuni strumenti di attribuzione a pagamento consentono di acquisire &quot;lo stack pancake&quot; di origini nel percorso di un utente. In tale situazione, nell’esempio precedente, l’attribuzione tramite primo clic ci direbbe ricerca a pagamento. In alternativa, alcuni siti web implementano i propri cookie che acquisiscono uno stack di pancake e memorizzano la prima sorgente nel proprio database.

## Come si analizza l’attribuzione?

[!DNL Google Analytics] dispone di alcune solide funzionalità nell&#39;interfaccia Web che consentono di eseguire quattro diversi modelli di attribuzione:

1. primo clic
1. ultimo clic
1. lineare (dividi i ricavi equamente tra tutte le origini nel percorso)
1. ponderato (attribuzione personalizzata)

Ora che conosci il modello di attribuzione per ogni micro o macro-conversione, la domanda diventa: &quot;Cosa fai con la totalità delle conversioni di un utente?&quot;.  Ad esempio, osserva gli UTM registrati in base alla logica dell’ultimo clic GA:

* Registri utenti in organico
* Primo acquisto dell&#39;utente con ricerca a pagamento $5,00
* Secondo acquisto dell&#39;utente via e-mail $50,00
* Terzo acquisto dell&#39;utente sotto organico $10,00

Qui è dove si chiede, &quot;Quanto reddito ho ottenuto dalla ricerca a pagamento? Da e-mail?  Dal biologico?&quot;. Si può dire che le risposte sono 5, 50 e 10 (qualunque sia stata l&#39;ultima fonte), o si può anche dire che si attribuiscono tutti i ricavi alla prima fonte (tutti i 65 vanno a organico). Potete anche applicare un&#39;analisi ponderata o applicare il modello lineare (cioè circa 22 ciascuno).

## Documentazione correlata

* [Tracciare l&#39;origine di riferimento dell&#39;ordine tramite  [!DNL Google Analytics] E-Commerce](../importing-data/integrations/google-ecommerce.md)
* [Tracciare l&#39;origine di riferimento dell&#39;utente nel database](../analysis/google-track-user-acq.md)
* [Tenere traccia dei dati relativi a dispositivi utente, browser e sistema operativo nel database](../analysis/google-track-user-acq.md)
* [Scopri le fonti e i canali di acquisizione più importanti](../analysis/most-value-source-channel.md)
* [Connetti il tuo account  [!DNL Google Adwords] ](../importing-data/integrations/google-adwords.md)
* [Aumentare il ROI nelle campagne pubblicitarie](../analysis/roi-ad-camp.md)
* [Cinque best practice per l&#39;assegnazione di tag UTM in [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
