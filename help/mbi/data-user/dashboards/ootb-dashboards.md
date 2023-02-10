---
title: Dashboard inclusi
description: Scopri come verificare lo stato di salute di metriche essenziali come i ricavi per la vita dell’utente, il numero di acquisti ripetuti e altro ancora, creando in tal modo una solida base per l’esplorazione futura.
exl-id: f50fc417-e5d4-401c-9baa-cda1468196a2
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 0%

---

# Dashboard inclusi

Come parte dei nostri servizi, offriamo e-commerce e `SaaS` Pacchetti iniziali. Questi pacchetti, creati dai nostri analisti, contengono un set personalizzato di dashboard e rapporti per il tuo set di dati. Le analisi contenute in questi pacchetti ti consentono di verificare lo stato di salute di metriche essenziali come i ricavi per la vita dell’utente, il numero di acquisti ripetuti e altro ancora, creando in tal modo una solida base per le future esplorazioni.

>[!NOTE]
>
>La disponibilità di alcune dashboard dipende dal set di dati.

In caso di domande o se sei interessato ad aggiungere un pacchetto al tuo account, invia un [biglietto di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) per aiuto.

## Panoramica dell&#39;esecutivo

La `executive overview` il dashboard è generato da grafici esistenti su altre dashboard. Questo dashboard è una panoramica di alto livello dei dati e contiene grafici che verranno rivisti quotidianamente, mentre altri dashboard contengono informazioni più dettagliate. Inizialmente, viene impostato come dashboard predefinito in ogni account.

È disponibile un set generale di grafici, ma è consigliabile adattare il dashboard alle proprie esigenze aggiungendo altri grafici utilizzati più di frequente.

## Analisi per coorte

La `cohort analysis` il dashboard include un set di grafici che mostrano la crescita media dei ricavi per l’utente e la crescita incrementale dei ricavi, raggruppati per coorti di registrazione. Questo indica se il valore del ciclo di vita del cliente (LTV), il valore di un cliente per un&#39;azienda, aumenta nel tempo e identifica anche le tendenze intorno alla crescita di LTV. Tieni presente che, per impostazione predefinita, *stiamo tenendo conto di tutti gli utenti registrati (acquirenti e non acquirenti)* nel calcolo LTV medio - vedi la [argomento di analisi per coorte](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Questo dashboard può anche includere grafici a coorte che analizzano i ricavi per gli utenti di una specifica origine di acquisizione, canale o dati demografici (ad esempio, New York o California). Questo per dimostrare come è possibile analizzare LTV per segmenti molto specifici della base di utenti e vedere se un gruppo o un altro produce LTV più alto nel tempo.

Per ulteriori informazioni sulle coorti, consulta [Esecuzione di un’analisi per coorte](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Se al momento non stai tracciando l&#39;origine di acquisizione degli utenti, consulta la sezione [Panoramica dei dati sorgente di acquisizione degli utenti](../../data-analyst/analysis/google-track-user-acq.md).

## Riepilogo e-mail

La `Email Summary` il dashboard include un set di grafici di esempio che possono essere utilizzati in un riepilogo e-mail giornaliero automatico. Fai riferimento a [creazione di riepiloghi e-mail automatizzati](../../data-user/export-data/email-summaries.md) per ulteriori informazioni sulla configurazione dei riepiloghi delle e-mail.  

## Stato di conservazione

La `Retention health` dashboard mostra il comportamento di acquisto ripetuto della base utenti.

La `Time between orders` il grafico mostra il tempo medio e/o mediano trascorso tra il primo e il secondo ordine, il secondo e il terzo ordine degli utenti e così via. È possibile [considera l’utilizzo di questi dati per configurare le campagne di e-mail marketing](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/).

La `Users by lifetime number of orders` grafico elenca il numero totale di utenti per ogni ciclo di vita di ordini, in modo da fornire una panoramica generale del comportamento di acquisto ripetuto.  

La `Repeat order probability` grafico mostra la probabilità che un utente con un determinato numero di ordine effettui un acquisto ripetuto. Per visualizzare la probabilità che i clienti abbiano effettuato `x` gli ordini `(x+1)` ordini, basta dividere il numero di persone che hanno fatto almeno `(x+1)` acquisti effettuati da almeno un numero di persone `x` acquisti.

### Esempio

Numero di clienti che hanno effettuato 1 acquisto nel corso della loro vita: `90`

Numero di clienti che hanno effettuato 2 acquisti nel corso della loro vita: `30`

Numero di clienti che hanno effettuato 3 acquisti nel corso della loro vita: `10`

In questo esempio, la probabilità che un cliente abbia effettuato un acquisto nel corso della sua vita per effettuare un secondo acquisto è la seguente: `(30 + 10) / (30+10+90) = 30.77%`.

## Crescita dell&#39;LTV

La `Customer LTV growth` il dashboard include un set di grafici che individua il ricavo medio per utente. I grafici sono segmentati in base ai ricavi medi generati nei primi 30, 60, 90 o 365 giorni dalla registrazione.  

La riga inferiore dei grafici mostra queste medie segmentate per origini di acquisizione o dati demografici per rivelare quali gruppi di utenti generano il maggior fatturato nel tempo.

## Prestazioni del prodotto

La `Product Performance` il dashboard include grafici che mostrano le prestazioni generali del prodotto visualizzando il numero di articoli venduti e ricavi per articolo, nonché identificando i prodotti dalle prestazioni migliori.

## Attività recente

La `Recent Activity` dashboard mostra i dati sulle prestazioni per gli ultimi 30 giorni.

## Salute transazionale

La `Transaction Health` il dashboard include grafici di panoramica relativi a ricavi, ordini e valore medio dell&#39;ordine. Questi grafici possono essere segmentati per canali di marketing, dati demografici o codici speciali di coupon.

## Utenti da indirizzare

La `Users to target` nel dashboard sono inclusi grafici in stile tabella in cui sono elencati gli utenti con comportamenti di acquisto specifici in comune. Alcuni esempi:

* Elenco degli acquirenti unici che acquistano `X` mesi fa (chi riattivare)

* Elenco dei migliori spenditori (che si può voler mantenere felice)

* Elenco dei principali spenditori attivi in passato `X` giorni (chi si desidera ricompensare)

Utilizzando i nostri strumenti di esportazione dei dati, è facile [creare elenchi di e-mail di utenti con comportamento di acquisto simile per target marketing](http://blog.rjmetrics.com/creating-contact-lists-for-top-customers/).

## Attività utente

La `User activity` dashboard include grafici che segmentano gli utenti in base a una varietà di dati, tra cui origine acquisizione, dati demografici e tempo medio di esecuzione dell&#39;ordine. Include inoltre l’analisi per coorte degli utenti, inclusa la media complessiva dei ricavi per ciclo di vita per mese di registrazione degli utenti.

La `% of cohort members who have purchased` Il grafico è particolarmente utile, in quanto mostra il rapporto di conversione (tra 0 e 1) degli utenti in base al momento della registrazione (ogni riga rappresenta una coorte di utenti) e al momento del loro primo acquisto (ad esempio, nel mese 1, 2, 3... dopo la registrazione). Questo può mostrare che il 10% degli utenti attivati nel mese 1, mentre questo numero cresce nel mese 2, 3, 4... e può piovere più tardi.

In genere, le linee di questo grafico diventano orizzontali dopo un certo periodo di tempo, indicando che pochi membri della coorte aggiuntivi si stanno convertendo organicamente dopo quel punto - i, la maggior parte degli utenti che stanno per effettuare un acquisto lo hanno già fatto. A questo punto, è altamente improbabile che questi membri si convertano in acquirenti senza intervento. [Raggiungere il pubblico con promozioni personalizzate o e-mail mirate è un modo estremamente conveniente per avviare la conversione di questa popolazione.](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/)
