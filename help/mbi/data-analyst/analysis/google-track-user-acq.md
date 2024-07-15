---
title: Google Analytics - Panoramica sul tracciamento dei dati Source di acquisizione degli utenti
description: Scopri come segmentare i dati per origine di acquisizione utente.
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: 3098909fdccb726108c24f2424e4ba4c1db9d1c2
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 1%

---

# Segmentazione per origine di acquisizione dell&#39;utente

>[!NOTE]
>
>Il processo seguente non supporta [!DNL Google Universal Analytics].

La capacità di segmentare i dati per origine di acquisizione utente è fondamentale per gestire efficacemente il piano di marketing. Conoscere la fonte di acquisizione dei nuovi utenti mostra quali canali producono i maggiori rendimenti e consente al team di allocare fondi di marketing in modo sicuro.

Se non si tiene traccia delle origini di acquisizione utente nel database, [!DNL Adobe Commerce Intelligence] può essere utile per iniziare:

## Tracciamento dell&#39;origine di acquisizione dell&#39;utente

[!DNL Adobe] consiglia due metodi per tenere traccia dei dati di origine dei riferimenti in base alla configurazione:

### (Opzione 1) Tenere traccia dei dati di origine dei riferimenti dell&#39;ordine tramite [!DNL Google Analytics E-Commerce]

Se si utilizza [!DNL Google Analytics E-Commerce] per tenere traccia dei dati relativi a ordini e vendite, è possibile utilizzare [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) per sincronizzare i dati di origine di riferimento di ogni ordine. Questo consente di segmentare i ricavi e gli ordini per origine di riferimento (ad esempio, `utm_source` o `utm_medium`). È inoltre possibile ottenere un&#39;idea delle origini di acquisizione del cliente tramite [!DNL Commerce Intelligence] dimensioni personalizzate, ad esempio `User's first order source`.

### (Opzione 2) Salvataggio dei dati di origine di acquisizione di [!DNL Google Analytics] nel database

In questo argomento viene illustrato come salvare le informazioni sul canale di acquisizione di [!DNL Google Analytics] nel proprio database, ovvero i parametri `source`, `medium`, `term`, `content`, `campaign` e `gclid` presenti durante la prima visita di un utente al sito Web. Per una spiegazione di questi parametri, consulta la [[!DNL Google Analytics] documentazione](https://support.google.com/analytics/answer/1191184?hl=en#zippy=%2Cin-this-article). Vengono quindi esaminate alcune delle potenti analisi di marketing che è possibile eseguire con queste informazioni in [!DNL Commerce Intelligence].

#### Perché?

Se si considerano solo le metriche di conversione e acquisizione predefinite di [!DNL Google Analytics], non si ottiene l&#39;intera immagine. Mentre è interessante vedere il numero di conversioni dalla ricerca organica rispetto alla ricerca a pagamento, cosa si può fare con quelle informazioni? Dovresti spendere più soldi per la ricerca a pagamento? Questo dipende dal valore dei clienti provenienti da quel canale, che non è qualcosa che la Google Analytics fornisce.

>[!NOTE]
>
>[[!DNL Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) attenua il problema memorizzando i dati della transazione in [!DNL Google Analytics], ma questa soluzione non funziona per i siti non di eCommerce. Inoltre, alcuni strumenti come l&#39;analisi per coorte non sono facili da usare nell&#39;interfaccia [!DNL Google Analytics].

Cosa succede se vuoi inviare un&#39;e-mail di follow-up a tutti i clienti acquisiti da una determinata campagna e-mail? Oppure integrare i dati di acquisizione con il sistema CRM? Impossibile in [!DNL Google Analytics]. In effetti, è contrario ai termini di servizio per [!DNL Google Analytics] memorizzare i dati che identificano un individuo. Tuttavia, puoi archiviare questi dati da solo.

#### Il metodo

[!DNL Google Analytics] memorizza le informazioni di riferimento del visitatore in un cookie denominato `__utmz`. Una volta impostato il cookie (dal codice di tracciamento [!DNL Google Analytics]), il suo contenuto verrà inviato insieme a ogni richiesta successiva dell&#39;utente al dominio. In PHP, ad esempio, è possibile estrarre il contenuto di `$_COOKIE['__utmz']` e visualizzare una stringa simile alla seguente:

`100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

È chiaro che alcuni dati di origine di acquisizione sono codificati nella stringa. Viene testato per confermare che si tratta dell’origine di acquisizione più recente del visitatore e dei dati della campagna associati. Ora devi sapere come estrarre i dati.

Questo codice è stato tradotto in una libreria [PHP ospitata su github](https://github.com/RJMetrics/referral-grabber-php). Per utilizzare la libreria, `include` un riferimento a `ReferralGrabber.php` e quindi chiamare

`$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

L&#39;array `$data` restituito è una mappa delle chiavi `source`, `medium`, `term`, `content`, `campaign`, `gclid` e dei rispettivi valori.

L&#39;Adobe consiglia di aggiungere al database una tabella denominata, ad esempio, `user_referral`, con colonne del tipo: `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`. Ogni volta che un utente si iscrive, prendi le informazioni di riferimento e memorizzale in questa tabella.

#### Come utilizzare questi dati

Ora che stai salvando l&#39;origine di acquisizione dell&#39;utente, come puoi utilizzarla?

Si supponga di utilizzare un database SQL e di disporre di una tabella `users` con la seguente struttura:

| ID | EMAIL | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 24/01/2012 | google | organico |
| 2 | jim@abc.com | 24/01/2012 | google | cpc |
| 3 | joe@def.com | 25/01/2012 | diretto | - |
| 4 | jess@ghi.com | 26/01/2012 | referral | techcrunch.com |
| 5 | jen@ghi.net | 30/01/2012 | altro | organico |
| ... | ... | ... | ... | ... |

Per iniziare, puoi contare il numero di utenti provenienti da ciascun canale di riferimento eseguendo la seguente query sul database:

`SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

Il risultato è simile al seguente:

| ACQ_SOURCE | CONTEGGIO_UTENTI |
|--- |--- |
| google | 294 |
| diretto | 156 |
| referral | 55 |
| altro | 16 |

Questo è interessante, ma di uso limitato. Quello che vorresti sapere è:

* Tasso di crescita di questi numeri nel tempo
* La quantità di ricavi generati da ogni origine di acquisizione
* [analisi per coorte](https://en.wikipedia.org/wiki/Cohort_analysis) di utenti provenienti da ogni origine
* La probabilità che un utente proveniente da uno di questi canali ritorni come cliente in futuro

Le query necessarie per eseguire queste analisi sono complesse. Sulla base di queste informazioni, potrai determinare i canali di acquisizione più redditizi e concentrare di conseguenza i tempi e i soldi del marketing.

### Correlato

* **[Scopri le fonti e i canali di acquisizione più importanti](../analysis/most-value-source-channel.md)**
* **[Connetti il tuo [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)**
* **[Aumentare il ROI nelle campagne pubblicitarie](../analysis/roi-ad-camp.md)**
* **[Come funziona l&#39;attribuzione  [!DNL Google Analytics] UTM?](../analysis/utm-attributes.md)**
