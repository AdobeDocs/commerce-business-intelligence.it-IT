---
title: Attribuzione Google Analytics e UTM
description: Scopri il processo di attribuzione dell’origine Google Analytics.
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# [!DNL Google Analytics] e UTM Attribution

È fondamentale per [tracciare l’origine dell’acquisizione utente](../../data-analyst/analysis/google-track-user-acq.md) a [identificare le campagne pubblicitarie con le prestazioni migliori](../../data-analyst/analysis/most-value-source-channel.md). Questo argomento esplora [!DNL Google Analytics] processo di attribuzione della sorgente. In altre parole, quale informazione viene registrata quando.

## Cos’è l’attribuzione?

`Attribution` riguarda la specifica di un’origine di riferimento per una particolare attività. Queste attività sono tipicamente macro-conversioni o micro-conversioni, le macro sono cose come **acquisti**, micro sono cose come **registrazione, iscrizione e-mail, commento sul blog,** e così via.

Idealmente, ogni volta che si verifica un evento di conversione, viene registrata una sorgente di riferimento. Ma come viene determinata la sorgente?

La realtà è che gli utenti spesso provengono da diverse origini prima di raggiungere o eseguire una micro o macro conversione. Ad esempio, possono arrivare al sito tramite Organic, poi uscire, poi venire tramite ricerca a pagamento, poi uscire, quindi venire direttamente al sito stesso. Queste informazioni di tracciamento delle sorgenti vengono spesso fornite al sito tramite i parametri UTM, ma esistono anche sistemi più sofisticati. Per le tue finalità, concentrati su [UTM](https://support.google.com/analytics/answer/1033867?hl=en&amp;ref_topic=1032998).

## In che modo [!DNL Google Analytics] attribuire le origini di riferimento tramite i parametri UTM?

Quando i parametri UTM vengono specificati nell’URL, vengono analizzati e inseriti in un [!DNL Google Analytics] [cookie](https://en.wikipedia.org/wiki/HTTP_cookie). Se un sito web non dispone di [!DNL Google Analytics], non ha senso avere UTM. [!DNL Google Analytics] dispone di regole per il modo in cui si relaziona con un utente che hit per più URL con UTM durante il suo ciclo di vita (ulteriori informazioni in seguito). Supponendo che il sito web sia configurato per acquisire i parametri UTM in un database esterno, quando si verifica una micro o macro conversione, indipendentemente dalla [!DNL Google Analytics] Il cookie al momento della conversione viene replicato nel database.

## Primo clic e ultimo clic

### Attribuzione ultimo clic

L’attribuzione ultimo clic è il modello di attribuzione più comune utilizzato da [!DNL Google Analytics]. In questo caso, il [!DNL Google Analytics] cookie rappresenta i parametri UTM per l’origine più recente prima dell’evento di conversione, ovvero [registrati nel database](../../data-analyst/analysis/google-track-user-acq.md). Il [!DNL Google Analytics] Il cookie sovrascrive i parametri UTM precedenti solo se l’utente fa clic su un nuovo URL che contiene un nuovo set di parametri UTM.

Ad esempio, considera un utente che visita per la prima volta un sito web tramite [!DNL Google Analytics] *ricerca a pagamento*, quindi restituisce tramite *ricerca organica* e infine torna al *direttamente sul sito web* o tramite un *collegamento e-mail* **senza parametri UTM** prima dell’evento di conversione. In questo esempio, la proprietà [!DNL Google Analytics] cookie indica che l’origine dell’utente è organica, poiché rappresenta l’ultima origine prima della conversione. Il *percorso* dell’utente prima che l’evento di conversione finale venga ignorato. Se invece l’utente ha visitato il sito web da un collegamento e-mail con UTM, allora il [!DNL Google Analytics] Il cookie potrebbe indicare che l’origine è &quot;e-mail&quot;. Pertanto, se nel cookie sono presenti parametri UTM esistenti e l’utente arriva direttamente tramite, il [!DNL Google Analytics] Il cookie mostra i parametri UTM anziché &quot;direct&quot;.

>[!NOTE]
>
>Di un utente specifico [!DNL Google Analytics] i parametri dei cookie vengono cancellati quando il cookie [scade](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage)o quando un utente cancella i suoi cookie nel browser.*

### Attribuzione con primo clic

Alcuni strumenti di attribuzione a pagamento consentono di acquisire &quot;lo stack pancake&quot; di origini nel percorso di un utente. In tale situazione, nell’esempio precedente, l’attribuzione tramite primo clic ci direbbe ricerca a pagamento. In alternativa, alcuni siti web implementano i propri cookie che acquisiscono uno stack di pancake e memorizzano la prima sorgente nel proprio database.

## Come si analizza l’attribuzione?

[!DNL Google Analytics] dispone di alcune solide funzionalità nell’interfaccia web che consentono di eseguire quattro diversi modelli di attribuzione:

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

* [Tracciare l’origine di riferimento dell’ordine tramite [!DNL Google Analytics] E-commerce](../importing-data/integrations/google-ecommerce.md)
* [Tracciare l&#39;origine di riferimento dell&#39;utente nel database](../analysis/google-track-user-acq.md)
* [Tenere traccia dei dati relativi a dispositivi utente, browser e sistema operativo nel database](../analysis/google-track-user-acq.md)
* [Scopri le fonti e i canali di acquisizione più importanti](../analysis/most-value-source-channel.md)
* [Connetti [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [Aumentare il ROI nelle campagne pubblicitarie](../analysis/roi-ad-camp.md)
* [Cinque best practice per l’assegnazione di tag UTM in [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
