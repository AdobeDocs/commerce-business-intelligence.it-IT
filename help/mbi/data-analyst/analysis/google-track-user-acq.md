---
title: Google Analytics - Panoramica dei dati sorgente di acquisizione degli utenti
description: Scopri come segmentare i dati per origine di acquisizione utente.
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 1%

---

# Segmentazione per origine di acquisizione utente

>[!NOTE]
>
>Il processo seguente non supporta [!DNL GoogleUniversal Analytics].

La possibilità di segmentare i dati per origine di acquisizione utente è fondamentale per gestire in modo efficace il piano di marketing. Conoscere la fonte di acquisizione dei nuovi utenti mostra quali canali producono i maggiori rendimenti e consente al tuo team di allocare i dollari di marketing con fiducia.

Se non tieni traccia delle origini di acquisizione utente nel database, [!DNL MBI] guida introduttiva:

## Tracciamento dell&#39;origine di acquisizione utente

Consigliamo due metodi per tenere traccia dei dati di origine dei riferimenti in base alla configurazione:

### (Opzione 1) Tenere traccia dei dati di origine del riferimento all&#39;ordine tramite [!DNL Google Analytics E-Commerce] (Compresi [!DNL Shopify] Negozi)

Se sfrutti [!DNL Google Analytics E-Commerce] per tenere traccia dei dati relativi all&#39;ordine e alle vendite, puoi sfruttare [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) per sincronizzare i dati di origine del riferimento di ogni ordine. Questo ti consente di segmentare ricavi e ordini per origine di riferimento (ad esempio, `utm_source` o `utm_medium`) e ottenere anche un&#39;idea delle fonti di acquisizione dei clienti tramite [!DNL MBI] dimensioni personalizzate quali `User's first order source`.

>[!NOTE]
>
>Per gli utenti Shopify**: Attiva [!DNL [Google Analytics E-Commerce] tracking in Shopify](http://docs.shopify.com/manual/settings/general/google-analytics#ecommerce-tracking) prima di collegare il [!DNL Google Analytics E-Commerce] account a [!DNL MBI].

### (Opzione 2) Salvataggio [!DNL Google Analytics]&#39; acquisizione dei dati di origine nel database

In questo articolo spiegheremo come salvare [!DNL Google Analytics] le informazioni sul canale di acquisizione nel tuo database, ovvero `source`, `medium`, `term`, `content`, `campaign`e `gclid` che erano presenti alla prima visita di un utente al sito web. Per una spiegazione di questi parametri, controlla la [!DNL [Google Analytics] documentation](http://support.google.com/analytics/bin/answer.py?hl=en&amp;answer=1191184). Esploreremo quindi alcune delle potenti analisi di marketing che possono essere eseguite con queste informazioni in [!DNL MBI].

#### Perché?

Se stai solo visualizzando il valore predefinito [!DNL Google Analytics] metriche di conversione e acquisizione, non ottieni l&#39;immagine completa. Mentre vedere il numero di conversioni dalla ricerca organica rispetto alla ricerca a pagamento è interessante, cosa si può fare con quelle informazioni? Dovresti spendere più soldi per la ricerca a pagamento? Questo dipende dal valore dei clienti provenienti da quel canale, che non è qualcosa che Google Analytics fornisce.

>[!NOTE]
>
>[!DNL [Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) mitiga questo problema archiviando i dati delle transazioni in [!DNL Google Analytics], ma questa soluzione non funziona per i siti non e-commerce e alcuni strumenti come l’analisi per coorte non sono facili da eseguire nel [!DNL Google Analytics] interfaccia.

Cosa succede se desideri inviare un&#39;e-mail di follow-up a tutti i clienti acquisiti da una determinata campagna e-mail? Oppure puoi integrare i dati di acquisizione con il tuo sistema CRM? Questo è impossibile in [!DNL Google Analytics] - in realtà, è contrario ai Termini di Servizio per [!DNL Google Analytics] per memorizzare tutti i dati che identificano un individuo.  Ma questo non significa che non si possono archiviare questi dati da soli.

#### Metodo

[!DNL Google Analytics] memorizza le informazioni sul riferimento del visitatore in un cookie denominato `__utmz`. Dopo che questo cookie è stato impostato (dal [!DNL Google Analytics] codice di tracciamento), il suo contenuto verrà inviato con ogni successiva richiesta al tuo dominio da parte di tale utente. Quindi in PHP, per esempio, si può controllare il contenuto di `$_COOKIE['__utmz']` e vedreste una stringa simile a questa:

> `100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

Nella stringa sono chiaramente codificati alcuni dati dell&#39;origine di acquisizione e abbiamo verificato che si tratta dell&#39;origine di acquisizione più recente del visitatore e dei dati della campagna associati. Ora dobbiamo solo sapere come estrarre i dati. Fortunatamente, Justin Cutroni ha descritto in precedenza il funzionamento di questa codifica e ha condiviso del codice javascript per estrarre le informazioni chiave.

Abbiamo preso questo codice e lo abbiamo tradotto in un [Libreria PHP ospitata su github](https://github.com/RJMetrics/referral-grabber-php).   Per utilizzare la libreria, `include` un riferimento a `ReferralGrabber.php` e poi chiama

> `$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

Il restituito `$data` array sarà una mappa delle chiavi `source`, `medium`, `term`, `content`, `campaign`, `gclid` e i rispettivi valori.

È consigliabile aggiungere una nuova tabella al database denominata, ad esempio, `user_referral`, con colonne come: `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`. Ogni volta che un utente si registra, acquisisci le informazioni di riferimento e memorizzale in questa tabella.

#### Come utilizzare questi dati

Ora che stiamo salvando la fonte di acquisizione utente, come possiamo usarla?

Supponiamo di utilizzare un database SQL e di avere un `users` tabella con la seguente struttura:

| ID | E-MAIL | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 2012-01-24 | google | organico |
| 2 | jim@abc.com | 2012-01-24 | google | cpc |
| 3 | joe@def.com | 2012-01-25 | diretto | - |
| 4 | jess@ghi.com | 2012-01-26 | riferimento | techcrunch.com |
| 5 | jen@ghi.net | 2012-01-30 | altro | organico |
| ... | ... | ... | ... | ... |

Per iniziare, possiamo contare il numero di utenti provenienti da ciascun canale di riferimento eseguendo la seguente query sul database:

> `SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

Il risultato sarà simile al seguente:

| ACQ_SOURCE | USER_COUNT |
|--- |--- |
| google | 294 |
| diretto | 156 |
| riferimento | 55 |
| altro | 16 |

Questo è interessante, ma di uso limitato. Quello che vorremmo davvero sapere è il tasso di crescita di questi numeri nel tempo, la quantità di ricavi generati da ogni fonte di acquisizione, un [analisi per coorte](http://cohortanalysis.com/) degli utenti provenienti da ogni origine e della probabilità che un utente proveniente da uno di questi canali ritorni come cliente in futuro. Le query necessarie per eseguire queste analisi sono complesse - ecco perché abbiamo costruito [!DNL MBI]. Grazie a queste informazioni possiamo determinare i nostri canali di acquisizione più redditizi e concentrare di conseguenza i nostri tempi di marketing e i nostri soldi.

### Correlati

* **[Scopri le fonti e i canali di acquisizione più importanti](../analysis/most-value-source-channel.md)**
* **[Collega il tuo [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)**
* **[Aumenta il ROI delle campagne pubblicitarie](../analysis/roi-ad-camp.md)**
* **[Come funziona [!DNL Google Analytics] L’attribuzione UTM funziona?](../analysis/utm-attributes.md)**
