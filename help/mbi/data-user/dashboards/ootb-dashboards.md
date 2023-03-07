---
title: Dashboard inclusi
description: Scopri come verificare lo stato di metriche essenziali come i ricavi dal ciclo di vita dell’utente, il numero di acquisti ripetuti e altro ancora, creando in tal modo una solida base per le esplorazioni future.
exl-id: f50fc417-e5d4-401c-9baa-cda1468196a2
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 0%

---

# Dashboard inclusi

Adobe offre e-commerce e `SaaS` Pacchetti iniziali. Questi pacchetti, creati da analisti Adobe, contengono un set personalizzato di dashboard e rapporti per il set di dati. Le analisi contenute in questi pacchetti consentono di verificare lo stato di metriche essenziali quali i ricavi derivanti dal ciclo di vita dell’utente, il numero di acquisti ripetuti e altro ancora, creando in tal modo una solida base per le esplorazioni future.

>[!NOTE]
>
>La disponibilità di alcune dashboard dipende dal set di dati.

In caso di domande o se sei interessato ad aggiungere un pacchetto al tuo account, invia una [ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) per assistenza.

## Panoramica esecutiva

Il `executive overview` il dashboard è creato a partire dai grafici presenti in altri dashboard. Questa dashboard offre una panoramica di alto livello dei dati e contiene grafici che verrebbero rivisti quotidianamente, mentre altre dashboard contenevano informazioni più dettagliate. Inizialmente, viene impostato come dashboard predefinito in ogni account.

È incluso un set generale di grafici. L&#39;Adobe consiglia di adattare il dashboard alle proprie esigenze aggiungendo altri grafici utilizzati più di frequente.

## Analisi per coorte

Il `cohort analysis` la dashboard include un set di grafici che mostrano la crescita media dei ricavi nel ciclo di vita dell’utente e la crescita incrementale dei ricavi, raggruppati per coorti di registrazione. Questo mostra se il valore del ciclo di vita del cliente (Customer Lifetime Value, LTV), il valore del cliente per un&#39;azienda, aumenta nel tempo e identifica anche le tendenze di crescita dell&#39;LTV. Per impostazione predefinita, *tutti gli utenti registrati (acquirenti e non acquirenti) sono contabilizzati* nel calcolo del valore LTV medio - vedere [argomento di analisi per coorte](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Questo dashboard può includere anche grafici a coorte che analizzano i ricavi nel corso del ciclo di vita degli utenti da una fonte di acquisizione, un canale o un dato demografico specifico (ad esempio, New York o California). In questo modo è possibile dimostrare come analizzare l’LTV per segmenti specifici della base di utenti e se un gruppo o un altro produce un LTV più elevato nel tempo.

Per ulteriori informazioni sulle coorti, consulta [Esecuzione dell’analisi per coorte](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Se al momento non tieni traccia dell&#39;origine di acquisizione dell&#39;utente, consulta [Panoramica sul tracciamento dei dati sorgente di acquisizione dell’utente](../../data-analyst/analysis/google-track-user-acq.md).

## Riepilogo e-mail

Il `Email Summary` il dashboard include un set di grafici di esempio che possono essere utilizzati in un riepilogo e-mail giornaliero automatico. Fai riferimento a [creazione di riepiloghi e-mail automatizzati](../../data-user/export-data/email-summaries.md) per ulteriori informazioni sulla configurazione dei riepiloghi e-mail.  

## Integrità di conservazione

Il `Retention health` la dashboard mostra il comportamento di acquisto ripetuto della base utenti.

Il `Time between orders` il grafico mostra il tempo medio e/o mediano trascorso tra il primo e il secondo ordine, il secondo e il terzo ordine di un utente e così via. È possibile [prova a utilizzare questi dati per configurare le campagne di e-mail marketing](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/).

Il `Users by lifetime number of orders` il grafico elenca il numero totale di utenti per ciascun numero di ordini nell’arco della loro durata, in modo da fornire una panoramica generale del comportamento di acquisto ripetuto.  

Il `Repeat order probability` grafico mostra la probabilità che un utente con un certo numero di ordine effettui un acquisto ripetuto. Per visualizzare la probabilità di clienti che hanno effettuato `x` ordini da effettuare `(x+1)` ordini, semplicemente dividere il numero di persone che hanno fatto almeno `(x+1)` acquisti in base al numero di persone che hanno effettuato almeno `x` acquisti.

### Esempio

Numero di clienti che hanno effettuato un acquisto nel corso della loro vita: `90`

Numero di clienti che hanno effettuato due acquisti nel corso della loro vita: `30`

Numero di clienti che hanno effettuato tre acquisti nel corso della loro vita: `10`

In questo esempio, la probabilità di ordine ripetuto dei clienti che hanno effettuato un acquisto nel corso della loro vita per effettuare un secondo acquisto è: `(30 + 10) / (30+10+90) = 30.77%`.

## Crescita del Customer LTV

Il `Customer LTV growth` il dashboard include un set di grafici che individua il reddito medio per utente. I grafici sono segmentati in base al reddito medio generato entro i primi 30, 60, 90 o 365 giorni dalla registrazione.  

La riga inferiore dei grafici mostra che queste medie sono segmentate da fonti di acquisizione o dati demografici per rivelare quali gruppi di utenti generano più ricavi nel tempo.

## Prestazioni del prodotto

Il `Product Performance` la dashboard include grafici che rivelano le prestazioni generali del prodotto visualizzando il numero di articoli venduti e ricavi per articolo e identificando i prodotti con le prestazioni migliori.

## Attività recente

Il `Recent Activity` il dashboard mostra i dati sulle prestazioni per gli ultimi 30 giorni.

## Integrità transazionale

Il `Transaction Health` il dashboard include grafici generali di ricavi, ordini e valore medio dell’ordine. Questi grafici possono essere segmentati in base ai canali di marketing, ai dati demografici o a codici coupon speciali.

## Utenti di destinazione

Il `Users to target` la dashboard include grafici in stile tabella che elencano gli utenti con comportamenti di acquisto specifici in comune. Alcuni esempi includono:

* Elenco di acquirenti occasionali che acquistano `X` mesi fa (da riattivare)

* Elenco dei principali spenditori (che si può desiderare di mantenere felice)

* Elenco dei principali finanziatori attivi in passato `X` giorni (da premiare)

Utilizzando gli strumenti di esportazione dei dati, è facile [creare elenchi e-mail di utenti con comportamento di acquisto simile per il marketing target](http://blog.rjmetrics.com/creating-contact-lists-for-top-customers/).

## Attività utente

Il `User activity` il dashboard include grafici che segmentano gli utenti in base a vari dati, tra cui origine acquisizione, dati demografici e media del primo ordine. Include inoltre l’analisi per coorte di utenti, incluso il ricavo medio complessivo nel ciclo di vita per mese di registrazione degli utenti.

Il `% of cohort members who have purchased` il grafico è utile, perché mostra il rapporto di conversione (da 0 a 1) degli utenti in base a quando si registrano (ogni linea rappresenta una coorte di utenti). Mostra anche quando effettuano il primo acquisto (ad esempio, nel mese 1, 2, 3... dopo la registrazione). Questo potrebbe mostrare che il 10% degli utenti si è attivato nel mese 1, mentre questo numero aumenta nei mesi 2, 3, 4... e potrebbe stabilizzarsi in un secondo momento.

In genere, le linee di questo grafico diventano orizzontali dopo un certo periodo di tempo. Ciò indica che pochi membri della coorte aggiuntivi effettueranno la conversione organicamente dopo tale momento; la maggior parte degli utenti che effettueranno un acquisto lo hanno già fatto. A questo punto, è altamente improbabile che questi membri si convertano ad acquirenti senza intervento. [Raggiungerli con promozioni personalizzate o e-mail mirate è un modo a basso rischio per avviare rapidamente la conversione di questa popolazione.](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/)
