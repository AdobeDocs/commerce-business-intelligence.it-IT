---
title: Dashboard inclusi
description: Scopri come verificare lo stato di metriche essenziali come i ricavi dal ciclo di vita dell’utente, il numero di acquisti ripetuti e altro ancora, creando in tal modo una solida base per le esplorazioni future.
exl-id: f50fc417-e5d4-401c-9baa-cda1468196a2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 0%

---

# Dashboard inclusi

[!DNL Adobe] offre `eCommerce` e `SaaS` pacchetti iniziali. Questi pacchetti, creati dagli analisti di Adobe, contengono un set personalizzato di dashboard e rapporti per il set di dati. Le analisi contenute in questi pacchetti consentono di verificare lo stato di metriche essenziali quali i ricavi derivanti dal ciclo di vita dell’utente, il numero di acquisti ripetuti e altro ancora, creando in tal modo una solida base per le esplorazioni future.

>[!NOTE]
>
>La disponibilità di alcune dashboard dipende dal set di dati.

In caso di domande o se sei interessato ad aggiungere un pacchetto al tuo account, invia un [ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=it) per assistenza.

## Panoramica esecutiva

Il dashboard `executive overview` è creato da grafici presenti in altri dashboard. Questa dashboard offre una panoramica di alto livello dei dati e contiene grafici che verrebbero rivisti quotidianamente, mentre altre dashboard contenevano informazioni più dettagliate. Inizialmente, viene impostato come dashboard predefinito in ogni account.

È incluso un set generale di grafici. Adobe consiglia di adattare il dashboard alle esigenze specifiche aggiungendo altri grafici utilizzati più di frequente.

## Analisi per coorte

Il dashboard `cohort analysis` include un set di grafici che mostrano la crescita dei ricavi medi nel ciclo di vita dell&#39;utente e la crescita dei ricavi incrementali raggruppati per coorti di registrazione. Questo mostra se il valore del ciclo di vita del cliente (Customer Lifetime Value, LTV), il valore del cliente per un&#39;azienda, aumenta nel tempo e identifica anche le tendenze di crescita dell&#39;LTV. Per impostazione predefinita, *tutti gli utenti registrati (acquirenti e non acquirenti) sono conteggiati per* nel calcolo LTV medio. Vedere l&#39;[argomento di analisi per coorte](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Questo dashboard può includere anche grafici a coorte che analizzano i ricavi nel corso del ciclo di vita degli utenti da una fonte di acquisizione, un canale o un dato demografico specifico (ad esempio, New York o California). In questo modo è possibile dimostrare come analizzare l’LTV per segmenti specifici della base di utenti e se un gruppo o un altro produce un LTV più elevato nel tempo.

Per ulteriori informazioni sulle coorti, vedere [Esecuzione dell&#39;analisi per coorte](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Se al momento non tieni traccia dell&#39;origine di acquisizione dell&#39;utente, consulta la [Panoramica dei dati di Source per il tracciamento dell&#39;acquisizione dell&#39;utente](../../data-analyst/analysis/google-track-user-acq.md).

## Riepilogo e-mail

Il dashboard `Email Summary` include un set di grafici di esempio che è possibile utilizzare in un riepilogo e-mail giornaliero automatico. Per ulteriori informazioni sulla configurazione dei riepiloghi e-mail, consulta [creazione di riepiloghi e-mail automatizzati](../../data-user/export-data/email-summaries.md).  

## Integrità di conservazione

La dashboard di `Retention health` mostra il comportamento di acquisto ripetuto della base utenti.

Il grafico `Time between orders` mostra il tempo medio e/o mediano trascorso tra il primo e il secondo ordine di un utente, il secondo e il terzo ordine e così via. Puoi [considerare l&#39;utilizzo di questi dati per configurare le campagne di e-mail marketing](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/).

Il grafico `Users by lifetime number of orders` elenca il numero totale di utenti per ogni numero di ordini del ciclo di vita per fornire una panoramica generale del comportamento di acquisto ripetuto.  

Il grafico `Repeat order probability` mostra la probabilità che un utente con un determinato numero di ordine effettui un acquisto ripetuto. Per visualizzare la probabilità che i clienti che hanno effettuato `x` ordini effettuino `(x+1)` ordini, è sufficiente dividere il numero di persone che hanno effettuato almeno `(x+1)` acquisti per il numero di persone che hanno effettuato almeno `x` acquisti.

### Esempio

Numero di clienti che hanno effettuato un acquisto nel corso della loro durata: `90`

Numero di clienti che hanno effettuato due acquisti nel corso della loro durata: `30`

Numero di clienti che hanno effettuato tre acquisti nel corso della loro durata: `10`

In questo esempio, la probabilità di ripetere l&#39;ordine dei clienti che hanno effettuato un acquisto nel corso della loro vita per effettuare un secondo acquisto è: `(30 + 10) / (30+10+90) = 30.77%`.

## Crescita del Customer LTV

Il dashboard `Customer LTV growth` include un set di grafici che individua il reddito medio per utente. I grafici sono segmentati in base al reddito medio generato entro i primi 30, 60, 90 o 365 giorni dalla registrazione.  

La riga inferiore dei grafici mostra che queste medie sono segmentate da fonti di acquisizione o dati demografici per rivelare quali gruppi di utenti generano più ricavi nel tempo.

## Prestazioni del prodotto

Il dashboard di `Product Performance` include grafici che mostrano le prestazioni generali del prodotto visualizzando il numero di articoli venduti e ricavi per articolo e identificando i prodotti con le prestazioni migliori.

## Attività recente

Il dashboard `Recent Activity` mostra i dati sulle prestazioni per gli ultimi 30 giorni.

## Integrità transazionale

Il dashboard `Transaction Health` include grafici generali di ricavi, ordini e valore medio dell&#39;ordine. Questi grafici possono essere segmentati in base ai canali di marketing, ai dati demografici o a codici coupon speciali.

## Utenti di destinazione

Il dashboard `Users to target` include grafici in stile tabella che elencano gli utenti con comportamenti di acquisto specifici in comune. Alcuni esempi includono:

* Elenco di acquirenti occasionali che hanno acquistato `X` mesi fa (che potresti voler riattivare)

* Elenco dei principali spenditori (che si può desiderare di mantenere felice)

* Elenco dei principali spenditori attivi negli ultimi `X` giorni (che puoi premiare)

Utilizzando gli strumenti di esportazione dei dati, è facile [creare elenchi e-mail di utenti con comportamenti di acquisto simili per il marketing di destinazione](http://blog.rjmetrics.com/creating-contact-lists-for-top-customers/).

## Attività utente

Il dashboard `User activity` include grafici che segmentano gli utenti in base a vari dati, tra cui origine acquisizione, dati demografici e media del primo ordine. Include inoltre l’analisi per coorte di utenti, incluso il ricavo medio complessivo nel ciclo di vita per mese di registrazione degli utenti.

Il grafico `% of cohort members who have purchased` è utile perché mostra il rapporto di conversione (da 0 a 1) degli utenti in base al momento della registrazione (ogni riga rappresenta una coorte di utenti). Mostra anche quando effettuano il primo acquisto (ad esempio, nel mese 1, 2, 3... dopo la registrazione). Questo potrebbe mostrare che il 10% degli utenti si è attivato nel mese 1, mentre questo numero aumenta nei mesi 2, 3, 4... e potrebbe stabilizzarsi in un secondo momento.

In genere, le linee di questo grafico diventano orizzontali dopo un certo periodo di tempo. Ciò indica che pochi membri della coorte aggiuntivi effettueranno la conversione organicamente dopo tale momento; la maggior parte degli utenti che effettueranno un acquisto lo hanno già fatto. A questo punto, è altamente improbabile che questi membri si convertano ad acquirenti senza intervento. [Per avviare la conversione di questa popolazione, è consigliabile contattare i destinatari tramite promozioni personalizzate o e-mail mirate.](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/)
