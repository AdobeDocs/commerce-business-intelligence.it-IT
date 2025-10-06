---
title: Utilizzare un rapporto
description: Scopri come utilizzare i dati del rapporto.
exl-id: 94d4db27-0e06-4066-9c03-036b109d2d9b
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 0%

---

# Utilizzare un rapporto

Utilizza i report in [!DNL Adobe Commerce Intelligence] per rispondere alle domande aziendali, per vedere semplicemente i ricavi di questo mese rispetto all&#39;anno scorso o per capire i costi di acquisizione per l&#39;ultima campagna [!DNL Google AdWords].

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
* La colonna che può essere utilizzata per unire o fare riferimento alla tabella `purchase` nella tabella `customer`. Questo consente di sapere chi ha effettuato un acquisto

A un livello più granulare, è necessario identificare i campi dati esatti utilizzati per questa analisi:

* Tabella dati e colonna che contengono la data di registrazione di un cliente, ad esempio `user.created\_at`
* Tabella dati e colonna che contengono una data di acquisto, ad esempio `order.created\_at`

## Creazione di colonne di dati per l’analisi

Oltre alle colonne di dati native descritte in precedenza, è necessario anche un set di campi di dati calcolati per abilitare questa analisi, tra cui:

* `Customer's first purchase date` che restituisce il `MIN(order.created_at` di un utente specifico)

Viene quindi utilizzato per creare:

* `Time between a customer's registration date and first purchase date`, che restituisce il tempo trascorso da un utente specifico tra la registrazione e la data del primo acquisto. Questa è la base per la metrica in un secondo momento.

Entrambi questi campi devono essere creati a livello di utente (ad esempio, nella tabella `user`). Ciò consente all’analisi media di essere normalizzata dagli utenti (in altre parole, il denominatore in questo calcolo medio è il numero di utenti).

[!DNL Commerce Intelligence] interviene qui. Puoi utilizzare il Data Warehouse [!DNL Commerce Intelligence] per creare le colonne di cui sopra. Contatta il team di analisti di Adobe e forniscici la definizione specifica delle nuove colonne da creare. È inoltre possibile utilizzare l&#39;[Editor colonne](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md).

È consigliabile evitare di creare direttamente questi campi di dati calcolati nel database, in quanto ciò rappresenta un onere inutile per i server di produzione.

## Creazione della metrica

Ora che disponi dei campi di dati richiesti per l’analisi, è necessario trovare o creare la metrica pertinente per creare l’analisi.

A questo punto si desidera eseguire il seguente calcolo:


_[SOMMA di `Time between a customer's registration date and first purchase date`] / [Numero totale di clienti registrati e acquistati]_

E vuoi vedere questo calcolo tracciato nel tempo, o tendenza, in base alla data di registrazione di un cliente. Ecco come [creare questa metrica](../../data-user/reports/ess-manage-data-metrics.md) in [!DNL Commerce Intelligence]:

1. Vai a **[!UICONTROL Data]** e seleziona la scheda `Metrics`.
1. Fare clic su **[!UICONTROL Add New Metric]** e selezionare la tabella `user` (in cui sono state create le dimensioni sopra).
1. Dal menu a discesa, selezionare `Average` nella colonna `Time between a customer's registration date and first purchase date` della tabella `user` ordinata in base alla colonna `Customer's registration date`.
1. Aggiungi eventuali filtri o set di filtri pertinenti.

Questa metrica è ora pronta.

## Creazione del rapporto

Con la nuova metrica impostata, puoi utilizzarla per generare rapporti sul tempo medio tra la registrazione e la data del primo acquisto per data di registrazione.

Basta accedere a qualsiasi dashboard e [creare un report](../../data-user/reports/ess-manage-data-metrics.md) utilizzando la metrica creata in precedenza.

### `Visual Report Builder` {#visualrb}

[Il `Visual Report Builder`](../../data-user/reports/ess-rpt-build-visual.md) è il modo più semplice per visualizzare i dati. Se non si ha familiarità con SQL o si desidera creare rapidamente un report, Visual Report Builder rappresenta la soluzione ottimale. Con pochi clic, puoi aggiungere metriche, segmentare i dati e creare rapporti in tutta l’organizzazione. Questa opzione è perfetta sia per i principianti che per gli esperti, in quanto non richiede alcuna competenza tecnica.

|  |  |
|--- |--- |
| **Questo è perfetto per...** | **Non è un&#39;ottima soluzione per...** |
| - Tutti i livelli di esperienza di analisi/tecnica<br>- Creazione rapida di report<br>- Creazione di analisi da condividere con altri utenti | - Analisi che richiedono funzioni specifiche di SQL<br>- Verifica delle nuove colonne - le colonne calcolate dipendono dai cicli di aggiornamento per la popolazione iniziale dei dati, mentre le colonne create utilizzando SQL no. |

{style="table-layout:auto"}

### Descrizioni e immagini dei rapporti

#### Aggiunta di descrizioni ai rapporti

Durante la creazione di rapporti condivisi con altri membri del team, Adobe consiglia di aggiungere descrizioni che consentano ad altri utenti di comprendere meglio l’analisi.

1. Fai clic su **[!UICONTROL i]** nella parte superiore di qualsiasi rapporto.
1. Immettere una descrizione nella casella di testo.
1. Fare clic su **[!UICONTROL Save Description]**.

Vedi di seguito:

![Descrizione grafico](../../assets/Chart_Description.gif)

#### Esportazione di report come immagini

È necessario includere un report in una presentazione o in un documento? Qualsiasi report può essere salvato come immagine (in formato PNG, PDF o SVG) utilizzando il menu `Report Options`, che si trova nell&#39;angolo in alto a destra di ogni report.

1. Fai clic sull’icona a forma di ingranaggio nell’angolo in alto a destra di qualsiasi rapporto.
1. Dal menu a discesa, selezionare `Enlarge`.
1. Quando il report viene ingrandito, fare clic su **[!UICONTROL Download]** nell&#39;angolo superiore destro del report.
1. Seleziona il formato immagine preferito dal menu a discesa. Il download inizia immediatamente.

Vedi di seguito:

![Dimostrazione animata dell&#39;esportazione di un report come file di immagine](../../assets/exp-rep-as-image.gif)
