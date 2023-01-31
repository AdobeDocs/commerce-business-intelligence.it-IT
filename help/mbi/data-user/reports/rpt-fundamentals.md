---
title: Utilizzare un rapporto
description: Scopri come utilizzare i dati del rapporto.
exl-id: 94d4db27-0e06-4066-9c03-036b109d2d9b
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 0%

---

# Utilizzare un rapporto

Utilizzare i rapporti in [!DNL MBI] per aiutarti a rispondere alle domande aziendali, sia che tu voglia semplicemente vedere le entrate di questo mese rispetto all&#39;anno precedente o capire i costi di acquisizione per i tuoi ultimi [!DNL Google AdWords] campagna.

Che aspetto ha esattamente quel percorso dalla domanda alla risposta?

Per aiutarti a visualizzare questo processo, abbiamo mappato quella rotta qui sotto. Questo argomento farà luce sia su come affrontiamo una domanda analitica, sia sulla logistica di back-end necessaria per ottenere i dati necessari.

## Inizia con la domanda

Sappiamo che stai facendo costantemente domande per migliorare il tuo business, dall&#39;aumento della soddisfazione dei clienti al taglio dei costi di fornitura. Ci concentreremo su come tradurre le tue domande in analisi che ti aiuteranno a guidare le decisioni.

Per il nostro esempio, supponiamo di voler rispondere alla seguente domanda:

* Quanto velocemente si convertono i miei nuovi registranti?

## Identificazione di una misurazione

Con la nostra domanda in mano, è giunto il momento di individuare un elenco di analisi e misurazioni possibili per contribuire a rispondere alla domanda. Per questo esempio, considera la metrica seguente:

* Tempo medio dalla registrazione alla prima data di acquisto per uso.

Questo mostrerà il tempo medio che intercorre tra la data di registrazione e la data di primo acquisto degli utenti e fornirà un&#39;idea su come questi si comportano in questo passaggio finale nel funnel di conversione.

## Ricerca dei dati

Capire cosa misurare ci rende solo parte del modo in cui siamo. Per valutare il tempo medio dalla registrazione alla prima data di acquisto per utente, dobbiamo identificare tutti i punti di dati di cui la nostra misura è composta.

Suddividi la nostra misura nei suoi componenti principali: dobbiamo conoscere il numero o il numero di persone che si sono registrate; il numero di persone che hanno effettuato un acquisto; e il tempo trascorso tra questi due eventi.

A un livello più alto, dobbiamo sapere dove trovare questi dati nel database, in particolare:

* Tabella che registra una riga di dati ogni volta che qualcuno si registra
* Tabella che registra una riga dati ogni volta che un utente effettua un acquisto
* La colonna che può essere utilizzata per unire o fare riferimento al `purchase` della tabella `customer` tabella - questo ci permetterà di sapere chi ha fatto un acquisto

A un livello più granulare, dobbiamo identificare i campi dati esatti che verranno utilizzati per questa analisi:

* Tabella di dati e colonna contenente la data di registrazione di un cliente: per esempio `user.created\_at`
* Tabella di dati e colonna contenente una data di acquisto: per esempio `order.created\_at`

## Creazione di colonne di dati per l’analisi

Oltre alle colonne di dati nativi sopra descritte, per abilitare questa analisi sarà necessario un set di campi di dati calcolati, tra cui:

* `Customer's first purchase date` che restituisce un `MIN(order.created_at`)

Verrà quindi utilizzato per creare:

* `Time between a customer's registration date and first purchase date`, che restituisce un intervallo di tempo tra la registrazione e la data di primo acquisto di un utente specifico. Questa sarà la base della nostra metrica in un secondo momento.

Entrambi questi campi devono essere creati a livello di utente (ad esempio, nel `user` tabella), in modo che l’analisi media possa essere normalizzata dagli utenti (in altre parole, il denominatore in questo calcolo medio sarà il numero di utenti).

Qui è dove [!DNL MBI] entra! Puoi sfruttare [!DNL MBI] data warehouse per creare le colonne di cui sopra. Contatta il nostro team di analisti e fornisci la definizione specifica delle tue nuove colonne e le creeremo. Puoi anche sfruttare il nostro [Editor colonne](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md).

È consigliabile evitare la creazione diretta di questi campi dati calcolati nel database in quanto comporta un onere inutile per i server di produzione.

## Creazione della metrica

Ora che disponiamo dei campi dati richiesti per la nostra analisi, è il momento di trovare o creare la metrica pertinente per costruire la nostra analisi.

Qui sappiamo che, matematicamente, vogliamo eseguire i seguenti calcoli:


_[SOMMA `Time between a customer's registration date and first purchase date`] / [Numero totale di clienti registrati e acquistati]_

E vogliamo vedere questo calcolo tracciato nel tempo, o trend, in base alla data di registrazione di un cliente. Ed ecco come [creare questa metrica](../../data-user/reports/ess-manage-data-metrics.md) in [!DNL MBI]:

1. Vai a **[!UICONTROL Data]** e seleziona la `Metrics` scheda .
1. Fai clic su **[!UICONTROL Add New Metric]** e seleziona la `user` tabella (in cui abbiamo creato le dimensioni sopra).
1. Dal menu a discesa, seleziona `Average` sulla`Time between a customer's registration date and first purchase date` nella colonna `user` tabella ordinata dal `Customer's registration date`  colonna.
1. Aggiungi eventuali filtri o set di filtri pertinenti.

Questa metrica è ora pronta.

## Creazione del rapporto

Con la nuova metrica impostata, possiamo utilizzarla per segnalare l’ora media tra la registrazione e la data del primo acquisto in base alla data di registrazione.

Basta accedere a qualsiasi dashboard e [creare un nuovo rapporto](../../data-user/reports/ess-manage-data-metrics.md) utilizzando la metrica creata in precedenza.

### `Visual Report Builder` {#visualrb}

[La `Visual Report Builder`](../../data-user/reports/ess-rpt-build-visual.md) è il modo più semplice per visualizzare i dati. Se non hai familiarità con SQL o desideri creare rapidamente un report, il Report Builder visivo è la soluzione migliore. Con pochi clic, puoi aggiungere metriche, segmentare i dati e creare rapporti per l’intera organizzazione. Questa opzione è perfetta per principianti ed esperti, in quanto non richiede alcuna competenza tecnica.

|  |  |
|--- |--- |
| **Questo è perfetto per...** | **Questo non è così grande per...** |
| - Tutti i livelli di esperienza di analisi/tecnologia<br>- Creazione rapida di report<br>- Creazione di analisi da condividere con altri utenti | - Analisi che richiedono funzioni specifiche di SQL<br>- Verifica di nuove colonne - le colonne calcolate dipendono dai cicli di aggiornamento per la popolazione iniziale dei dati, mentre quelle create con SQL non sono |

{style=&quot;table-layout:auto&quot;}

### Descrizioni e immagini dei rapporti

#### Aggiunta di descrizioni ai rapporti

Quando crei rapporti che verranno condivisi con altri membri del team, ti consigliamo di aggiungere descrizioni che consentano ad altri utenti di comprendere meglio la tua analisi.

1. Fai clic su **[!UICONTROL i]** nella parte superiore di qualsiasi report.
1. Immettere una descrizione nella casella della parola.
1. Fai clic su **[!UICONTROL Save Description]**.

Diamo un&#39;occhiata:

![Descrizione grafico](../../assets/Chart_Description.gif)

#### Esportazione di rapporti come immagini

È necessario includere un rapporto in una presentazione o in un documento? Qualsiasi rapporto può essere salvato come immagine (in formato PNG, PDF o SVG) utilizzando `Report Options` , nell’angolo in alto a destra di ogni rapporto.

1. Fai clic sull’icona a forma di ingranaggio nell’angolo in alto a destra di qualsiasi rapporto.
1. Dal menu a discesa, seleziona `Enlarge`.
1. Quando il rapporto si espande, fai clic su **[!UICONTROL Download]** nell’angolo in alto a destra del rapporto.
1. Seleziona il formato immagine preferito dal menu a discesa. Il download inizierà immediatamente.

Dai un&#39;occhiata:

![](../../assets/exp-rep-as-image.gif)
