---
title: Google Analytics e attribuzione UTM
description: Scopri il processo di attribuzione dell’origine Google Analytics.
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 0%

---

# Google Analytics e attribuzione UTM

È fondamentale [tracciamento dell&#39;origine di acquisizione utente](../../data-analyst/analysis/google-track-user-acq.md) a [identificare le campagne pubblicitarie con le prestazioni migliori](../../data-analyst/analysis/most-value-source-channel.md). In questa esercitazione viene esplorato il processo di attribuzione dell’origine Google Analytics. In altre parole, quale informazione viene registrata quando.

## Cos’è l’attribuzione?

`Attribution` riguarda la specifica di un&#39;origine di riferimento di una particolare attività. Queste attività sono tipicamente macro-conversioni o micro-conversioni, macro sono cose come **acquisti** Il micro essere cose come **registrazione, iscrizione e-mail, commento blog,** e così via.

Idealmente, ogni volta che si verifica un evento di conversione, viene registrata un&#39;origine di riferimento. Ma come viene determinata la fonte?

La realtà è che gli utenti spesso provengono da molte fonti prima di colpire/commettere una micro o macro conversione (per esempio, possono venire al sito tramite organico, poi andarsene, poi venire via ricerca a pagamento, poi andarsene, poi venire direttamente al sito stesso). Queste informazioni di tracciamento delle sorgenti vengono spesso fornite al sito tramite parametri UTM, ma esistono anche sistemi più sofisticati. Per i nostri scopi ci concentreremo su [UTM](https://support.google.com/analytics/answer/1033867?hl=en&amp;ref_topic=1032998).

## Come funziona [!DNL Google Analytics] origini di riferimento attributo tramite parametri UTM?

Quando i parametri UTM vengono specificati sull’URL, vengono analizzati e inseriti in un [!DNL Google Analytics] [cookie](https://en.wikipedia.org/wiki/HTTP_cookie). Se un sito web non ha [!DNL Google Analytics]Non ha senso avere gli UTM. [!DNL Google Analytics] dispone di regole per il modo in cui si relaziona con un utente che accede a più URL con UTM nel corso della sua vita (ulteriori informazioni in seguito). Supponendo che il sito web sia configurato per acquisire parametri UTM in un database esterno, ogni volta che si verifica una micro o una macro conversione, qualsiasi cosa si trovi in [!DNL Google Analytics] il cookie al momento della conversione viene replicato nel database.

## Primo clic rispetto all’ultimo clic

### Attribuzione ultimo clic

L’attribuzione dell’ultimo clic è il modello di attribuzione più comune utilizzato da [!DNL Google Analytics]. In questo caso, il [!DNL Google Analytics] il cookie rappresenta i parametri UTM per l’ultima origine, o la più recente, precedente all’evento di conversione, ed è questo l’elemento [registrati nel database](../../data-analyst/analysis/google-track-user-acq.md). Tieni presente che [!DNL Google Analytics] il cookie sovrascrive i parametri UTM precedenti solo se l’utente fa clic su un nuovo URL che contiene un nuovo set di parametri UTM.

Ad esempio, considera un utente che visita per la prima volta un sito web tramite [!DNL Google Analytics][!DNL Google Analytics][!DNL Google Analytics] *ricerca a pagamento*, quindi restituisce tramite *ricerca organica*, e infine ritorna al *sito web direttamente* o tramite *collegamento e-mail* **senza parametri UTM** prima dell’evento di conversione. In questo esempio, la [!DNL Google Analytics] cookie indica che la sorgente dell’utente è organica, poiché rappresenta l’ultima sorgente prima della conversione. La *path* dell’utente prima dell’evento di conversione finale viene ignorato. Se invece l&#39;utente ha visitato il sito web da un collegamento e-mail con UTM, allora il [!DNL Google Analytics] cookie direbbe che la fonte è &quot;email&quot;. Pertanto, se nel cookie sono presenti parametri UTM esistenti e l’utente accede tramite direct, l’ [!DNL Google Analytics] i cookie mostreranno sempre i parametri UTM anziché &quot;direct&quot;.

>[!NOTE]
>
>Un utente specifico [!DNL Google Analytics] i parametri dei cookie verranno cancellati quando il cookie [scadenza](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage)o quando un utente cancella i propri cookie nel browser.*)

### Attribuzione primo clic

Alcuni strumenti di attribuzione a pagamento consentono di acquisire &quot;lo stack di frittelle&quot; di sorgenti nel percorso di un utente. In questa situazione, nel nostro esempio precedente, l’attribuzione di primo clic ci direbbe la ricerca a pagamento. In alternativa, una minoranza di siti web implementa i propri cookie che catturano uno stack di pancake e memorizzano la prima fonte nel loro database.

## Come analizzare l’attribuzione?

[!DNL Google Analytics] dispone di alcune funzionalità più affidabili nella loro interfaccia web che consentono di eseguire quattro diversi modelli di attribuzione: primo clic, ultimo clic, lineare (dividi i ricavi equamente tra tutte le sorgenti nel percorso) e ponderato (attribuzione personalizzata).

Ora che capisci qual è il modello di attribuzione per ogni micro o macro-conversione, la domanda diventa cosa fare con la totalità delle conversioni di un utente?  Ad esempio, guarda gli UTM registrati in base alla logica dell’ultimo clic GA:

* Registratori di utenti in modalità organica
* Primo acquisto dell&#39;utente con ricerca a pagamento $5.00
* Secondo acquisto dell&#39;utente con e-mail $50.00
* Terzo acquisto dell&#39;utente con 10,00 $ biologici

Ecco dove si chiede: Quanti ricavi ho ottenuto dalla ricerca a pagamento?  Da e-mail?  Da organico?  Si potrebbe dire che le risposte sono 5, 50 e 10 (cioè, qualunque fosse l&#39;ultima fonte), o si potrebbe anche dire che si attribuiscono tutti i ricavi alla prima fonte (cioè, tutti i 65 vanno al biologico). Si potrebbe anche applicare un&#39;analisi ponderata o il modello lineare (cioè circa 22 ciascuno).

## Documentazione correlata

* [Tracciare l’origine di riferimento dell’ordine tramite [!DNL Google Analytics] E-commerce](../importing-data/integrations/google-ecommerce.md)
* [Tracciare l’origine del riferimento utente nel database](../analysis/google-track-user-acq.md)
* [Tieni traccia dei dati di dispositivi utente, browser e sistemi operativi nel database](../analysis/google-track-user-acq.md)
* [Scopri le fonti e i canali di acquisizione più importanti](../analysis/most-value-source-channel.md)
* [Collega il tuo [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [Aumenta il ROI delle campagne pubblicitarie](../analysis/roi-ad-camp.md)
* [5 best practice per l’assegnazione di tag UTM in [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
