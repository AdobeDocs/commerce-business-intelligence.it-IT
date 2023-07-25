---
title: Utilizzare un rapporto
description: Scopri come utilizzare i dati del rapporto.
exl-id: 94d4db27-0e06-4066-9c03-036b109d2d9b
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 0%

---

# Utilizzare un rapporto

Utilizzare i rapporti in [!DNL Adobe Commerce Intelligence] per aiutarti a rispondere alle domande di business: vuoi semplicemente visualizzare i ricavi di questo mese rispetto all&#39;anno precedente o capire i costi di acquisizione per il tuo ultimo [!DNL Google AdWords] campagna.

Come si presenta esattamente il percorso da domanda a risposta?

Per aiutarti a visualizzare questo processo, la route è mappata di seguito. Questo argomento chiarisce sia il modo in cui affronti una domanda analitica sia la logistica back-end necessaria per ottenere i dati necessari.

## Iniziare con la domanda

Sapete che ponete costantemente domande per migliorare la vostra attività, dall&#39;aumento della soddisfazione dei clienti alla riduzione dei costi di fornitura. Ti concentri su come tradurre le tue domande in analisi che ti aiutino a guidare le decisioni.

Per questo esempio, si supponga di voler rispondere alla seguente domanda:

* Quanto velocemente si convertono i nuovi iscritti?

## Identificazione di una misurazione

È ora di identificare un elenco di possibili analisi e misurazioni per aiutare a rispondere alla domanda. Per questo esempio, considera la metrica seguente:

* Tempo medio dalla registrazione alla data del primo acquisto per uso.

Questo rivela il tempo medio che intercorre tra la data di registrazione e la data del primo acquisto dell’utente e dà un’idea del comportamento dell’utente in questo passaggio finale nel funnel di conversione.

## Ricerca dei dati

Capire cosa misurare solo ci porta ad una parte della strada. Per valutare il tempo medio dalla registrazione alla data del primo acquisto per utente, è necessario identificare tutti i punti di dati di cui è composta la misura.

Suddividi la misura nei suoi componenti core. Devi conoscere il numero di persone che si sono registrate, il numero di persone che hanno effettuato un acquisto e il tempo trascorso tra questi due eventi.

A un livello più alto, è necessario sapere dove trovare questi dati nel database, in particolare:

* Tabella che registra una riga di dati ogni volta che un utente si registra
* Tabella che registra una riga di dati ogni volta che qualcuno effettua un acquisto
* La colonna che può essere utilizzata per unire o fare riferimento al `purchase` tabella al `customer` tabella: consente di sapere chi ha effettuato un acquisto

A un livello più granulare, è necessario identificare i campi dati esatti utilizzati per questa analisi:

* La tabella e la colonna di dati che contengono la data di registrazione di un cliente: ad esempio `user.created\_at`
* La tabella e la colonna di dati che contengono una data di acquisto: ad esempio `order.created\_at`

## Creazione di colonne di dati per l’analisi

Oltre alle colonne di dati native descritte in precedenza, è necessario anche un set di campi di dati calcolati per abilitare questa analisi, tra cui:

* `Customer's first purchase date` che restituisce il `MIN(order.created_at`)

Viene quindi utilizzato per creare:

* `Time between a customer's registration date and first purchase date`, che restituisce il tempo trascorso da un utente specifico tra la registrazione e la data del primo acquisto. Questa è la base per la metrica in un secondo momento.

Entrambi questi campi devono essere creati a livello di utente (ad esempio, sul `user` tabella). Ciò consente all’analisi media di essere normalizzata dagli utenti (in altre parole, il denominatore in questo calcolo medio è il numero di utenti).

Qui è dove [!DNL Commerce Intelligence] entra! Puoi utilizzare il tuo [!DNL Commerce Intelligence] Data Warehouse per creare le colonne precedenti. Contatta il team di analisti Adobe e fornisci la definizione specifica delle nuove colonne da creare. È inoltre possibile utilizzare [Editor colonne](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md).

È consigliabile evitare di creare direttamente questi campi di dati calcolati nel database, in quanto ciò rappresenta un onere inutile per i server di produzione.

## Creazione della metrica

Ora che disponi dei campi di dati richiesti per l’analisi, è necessario trovare o creare la metrica pertinente per creare l’analisi.

A questo punto si desidera eseguire il seguente calcolo:


_[SOMMA di `Time between a customer's registration date and first purchase date`] / [Numero totale di clienti che hanno effettuato la registrazione e l&#39;acquisto]_

E vuoi vedere questo calcolo tracciato nel tempo, o tendenza, in base alla data di registrazione di un cliente. Ed ecco come [crea questa metrica](../../data-user/reports/ess-manage-data-metrics.md) in [!DNL Commerce Intelligence]:

1. Vai a **[!UICONTROL Data]** e seleziona la `Metrics` scheda.
1. Clic **[!UICONTROL Add New Metric]** e seleziona la `user` tabella (dove sono state create le quote precedenti).
1. Dal menu a discesa, seleziona `Average` il`Time between a customer's registration date and first purchase date` colonna nella `user` tabella ordinata da `Customer's registration date`  colonna.
1. Aggiungi eventuali filtri o set di filtri pertinenti.

Questa metrica è ora pronta.

## Creazione del rapporto

Con la nuova metrica impostata, puoi utilizzarla per generare rapporti sul tempo medio tra la registrazione e la data del primo acquisto per data di registrazione.

Basta andare a qualsiasi dashboard e [creare un rapporto](../../data-user/reports/ess-manage-data-metrics.md) utilizzando la metrica creata in precedenza.

### `Visual Report Builder` {#visualrb}

[Il `Visual Report Builder`](../../data-user/reports/ess-rpt-build-visual.md) è il modo più semplice per visualizzare i dati. Se non si ha familiarità con SQL o si desidera creare rapidamente un report, il Report Builder visivo rappresenta la soluzione migliore. Con pochi clic, puoi aggiungere metriche, segmentare i dati e creare rapporti in tutta l’organizzazione. Questa opzione è perfetta sia per i principianti che per gli esperti, in quanto non richiede alcuna competenza tecnica.

|  |  |
|--- |--- |
| **Questo è perfetto per...** | **Questo non è grandioso per...** |
| - Tutti i livelli di analisi/esperienza tecnica<br>- Creazione rapida di rapporti<br>- Creazione di analisi da condividere con altri utenti | - Analisi che richiedono funzioni specifiche di SQL<br>- Verifica di nuove colonne: le colonne calcolate dipendono dai cicli di aggiornamento per la popolazione di dati iniziale, mentre quelle create utilizzando SQL no. |

{style="table-layout:auto"}

### Descrizioni e immagini dei rapporti

#### Aggiunta di descrizioni ai rapporti

Durante la creazione di rapporti condivisi con altri membri del team, l’Adobe consiglia di aggiungere descrizioni che consentano ad altri utenti di comprendere meglio l’analisi.

1. Clic **[!UICONTROL i]** nella parte superiore di qualsiasi rapporto.
1. Immettere una descrizione nella casella di testo.
1. Clic **[!UICONTROL Save Description]**.

Vedi di seguito:

![Descrizione grafico](../../assets/Chart_Description.gif)

#### Esportazione di report come immagini

È necessario includere un report in una presentazione o in un documento? Qualsiasi rapporto può essere salvato come immagine (in formato PNG, PDF o SVG) utilizzando `Report Options` nell’angolo in alto a destra di ogni rapporto.

1. Fai clic sull’icona a forma di ingranaggio nell’angolo in alto a destra di qualsiasi rapporto.
1. Dal menu a discesa, seleziona `Enlarge`.
1. Quando il report viene ingrandito, fai clic su **[!UICONTROL Download]** nell’angolo in alto a destra del rapporto.
1. Seleziona il formato immagine preferito dal menu a discesa. Il download inizia immediatamente.

Vedi di seguito:

![](../../assets/exp-rep-as-image.gif)
