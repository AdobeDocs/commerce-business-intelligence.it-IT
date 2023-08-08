---
title: 'Google Analytics: panoramica di Tracciamento dei dati di origine dell’acquisizione da parte degli utenti'
description: Scopri come segmentare i dati per origine di acquisizione utente.
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: 3098909fdccb726108c24f2424e4ba4c1db9d1c2
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 1%

---

# Segmentazione per origine di acquisizione dell&#39;utente

>[!NOTE]
>
>Il processo seguente non supporta [!DNL Google Universal Analytics].

La capacità di segmentare i dati per origine di acquisizione utente è fondamentale per gestire efficacemente il piano di marketing. Conoscere la fonte di acquisizione dei nuovi utenti mostra quali canali producono i maggiori rendimenti e consente al team di allocare fondi di marketing in modo sicuro.

Se non tieni traccia delle origini di acquisizione utente nel database, [!DNL Adobe Commerce Intelligence] può aiutarti a iniziare:

## Tracciamento dell&#39;origine di acquisizione dell&#39;utente

[!DNL Adobe] consiglia due metodi per tenere traccia dei dati di origine dei riferimenti in base alla configurazione:

### (Opzione 1) Tracciare i dati di origine dei riferimenti dell&#39;ordine tramite [!DNL Google Analytics E-Commerce]

Se usa [!DNL Google Analytics E-Commerce] per tenere traccia dei dati relativi a ordini e vendite, è possibile utilizzare [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) per sincronizzare i dati di origine di riferimento di ogni ordine. Questo consente di segmentare i ricavi e gli ordini per origine di riferimento (ad esempio, `utm_source` o `utm_medium`). Inoltre, è possibile ottenere un&#39;idea delle origini di acquisizione del cliente tramite [!DNL Commerce Intelligence] dimensioni personalizzate come `User's first order source`.

### (Opzione 2) Salvataggio [!DNL Google Analytics]&#39; dati di origine di acquisizione nel database

Questo argomento spiega come salvare [!DNL Google Analytics] acquisire le informazioni sul canale nel proprio database, ovvero `source`, `medium`, `term`, `content`, `campaign`, e `gclid` parametri presenti durante la prima visita di un utente al sito web. Per una spiegazione di questi parametri, consulta [[!DNL Google Analytics] documentazione](https://support.google.com/analytics/answer/1191184?hl=en#zippy=%2Cin-this-article). Poi, esplori alcune delle potenti analisi di marketing che possono essere eseguite con queste informazioni in [!DNL Commerce Intelligence].

#### Perché?

Se stai solo osservando il valore predefinito [!DNL Google Analytics] metriche di conversione e acquisizione, non si ottiene il quadro completo. Mentre è interessante vedere il numero di conversioni dalla ricerca organica rispetto alla ricerca a pagamento, cosa si può fare con quelle informazioni? Dovresti spendere più soldi per la ricerca a pagamento? Questo dipende dal valore dei clienti provenienti da quel canale, che non è qualcosa che la Google Analytics fornisce.

>[!NOTE]
>
>[[!DNL Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) attenua il problema memorizzando i dati delle transazioni in [!DNL Google Analytics], ma questa soluzione non funziona per i siti non di eCommerce. Inoltre, alcuni strumenti come l’analisi per coorte non sono facili da usare nel [!DNL Google Analytics] di rete.

Cosa succede se vuoi inviare un&#39;e-mail di follow-up a tutti i clienti acquisiti da una determinata campagna e-mail? Oppure integrare i dati di acquisizione con il sistema CRM? Questo è impossibile in [!DNL Google Analytics] - infatti, è contrario alle Condizioni di utilizzo per [!DNL Google Analytics] per memorizzare i dati che identificano un individuo. Tuttavia, puoi archiviare questi dati da solo.

#### Il metodo

[!DNL Google Analytics] memorizza le informazioni di riferimento del visitatore in un cookie denominato `__utmz`. Dopo aver impostato questo cookie (da [!DNL Google Analytics] codice di tracciamento), il suo contenuto verrà inviato con ogni richiesta successiva al dominio da parte di tale utente. Quindi in PHP, per esempio, si può controllare il contenuto di `$_COOKIE['__utmz']` e vedreste una stringa che ha un aspetto simile a questo:

`100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

È chiaro che alcuni dati di origine di acquisizione sono codificati nella stringa. Viene testato per confermare che si tratta dell’origine di acquisizione più recente del visitatore e dei dati della campagna associati. Ora devi sapere come estrarre i dati.

Questo codice è stato tradotto in [Libreria PHP ospitata su github](https://github.com/RJMetrics/referral-grabber-php). Per utilizzare la libreria: `include` un riferimento a `ReferralGrabber.php` e quindi chiama

`$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

Il restituito `$data` array è una mappa delle chiavi `source`, `medium`, `term`, `content`, `campaign`, `gclid`e i rispettivi valori.

L’Adobe consiglia di aggiungere al database una tabella denominata, ad esempio: `user_referral`, con colonne del tipo: `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`. Ogni volta che un utente si iscrive, prendi le informazioni di riferimento e memorizzale in questa tabella.

#### Come utilizzare questi dati

Ora che stai salvando l&#39;origine di acquisizione dell&#39;utente, come puoi utilizzarla?

Si supponga di utilizzare un database SQL e di disporre di `users` tabella con la seguente struttura:

| ID | EMAIL | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 2012-01-24 | google | organico |
| 2 | jim@abc.com | 2012-01-24 | google | cpc |
| 3 | joe@def.com | 2012-01-25 | diretto | - |
| 4 | jess@ghi.com | 2012-01-26 | referral | techcrunch.com |
| 5 | jen@ghi.net | 2012-01-30 | altro | organico |
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
* A [analisi per coorte](https://en.wikipedia.org/wiki/Cohort_analysis) di utenti provenienti da ogni origine
* La probabilità che un utente proveniente da uno di questi canali ritorni come cliente in futuro

Le query necessarie per eseguire queste analisi sono complesse. Sulla base di queste informazioni, potrai determinare i canali di acquisizione più redditizi e concentrare di conseguenza i tempi e i soldi del marketing.

### Correlato

* **[Scopri le fonti e i canali di acquisizione più importanti](../analysis/most-value-source-channel.md)**
* **[Connetti [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)**
* **[Aumentare il ROI nelle campagne pubblicitarie](../analysis/roi-ad-camp.md)**
* **[In che modo [!DNL Google Analytics] Lavoro di attribuzione UTM?](../analysis/utm-attributes.md)**
