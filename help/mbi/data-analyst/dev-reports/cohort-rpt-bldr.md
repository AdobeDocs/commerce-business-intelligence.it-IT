---
title: Report Builder coorte
description: Scopri l’analisi dei gruppi di utenti che condividono caratteristiche simili nel corso dei loro cicli di vita.
exl-id: d80c5389-7256-40e0-86e0-49903113f93d
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 0%

---

# Report Builder coorte

Hai mai desiderato studiare il comportamento nel tempo di diversi sottoinsiemi di utenti? Ad esempio, ti sei mai chiesto se gli utenti che si registrano durante un periodo promozionale hanno un ricavo medio sulla vita più alto rispetto a quelli che non lo fanno? Se la risposta è `Yes`, allora `Cohort Report Builder` è lo strumento perfetto per te. [!DNL Adobe Commerce Intelligence] è ottimizzato per eseguire questa analisi e renderla rilevante per la tua azienda.

## L’analisi per coorte {#what}

L&#39;analisi di `Cohort` può essere definita in modo generico come l&#39;analisi di gruppi di utenti che condividono caratteristiche simili nel corso dei loro cicli di vita. Consente di identificare le tendenze comportamentali tra diversi gruppi di utenti.

Per un&#39;introduzione approfondita all&#39;analisi `cohort`, esaminare [questa pagina](https://www.cohortanalysis.com/).

Nel dashboard di [!DNL Commerce Intelligence], è facile creare l&#39;utente `cohorts` in base a una data di `cohort` e a una metrica nel tuo account.

## Perché è importante l&#39;analisi per coorte? {#important}

Come accennato in precedenza, l&#39;analisi `cohort` consente di identificare le tendenze comportamentali tra i diversi gruppi di utenti. Grazie alla solida conoscenza del comportamento di alcuni gruppi, puoi adattare le tue decisioni di acquisto per massimizzare le vendite. Ad esempio, si prenda un&#39;analisi dei ricavi `cohort` per tutta la vita: anche se questo tipo di analisi è utile per molti motivi, quella immediata è quella che migliora le decisioni di acquisizione dei clienti.

## Come si crea un&#39;analisi `cohort` personalizzata?

### Nuova architettura

Queste sono le istruzioni per utilizzare `Cohort Report Builder` nella [Nuova architettura](../../administrator/account-management/new-architecture.md).

1. Fai clic su **[!UICONTROL Report Builder]** nella scheda a sinistra o su **[!UICONTROL Add Report** > **Create Report]** in qualsiasi dashboard.

1. Nella schermata di selezione `Report Builder`, fare clic su **[!UICONTROL Create Report]** accanto all&#39;opzione `Visual Report Builder`.

**Aggiunta di una metrica**

Ora che ti trovi in `Report Builder`, aggiungi la metrica su cui desideri eseguire l&#39;analisi (ad esempio: `Revenue` o `Orders`).

>[!NOTE]
>
>Le metriche native di [!DNL Google Analytics] non sono compatibili con `Cohort Report Builder`.

**Attiva/disattiva visualizzazione metrica su`Cohort`**

![Visual Report Builder mostra l&#39;opzione di attivazione/disattivazione analisi per coorte](../../assets/visual-report-builder-cohort-toggle.png)

Verrà aperta una nuova finestra per configurare i dettagli del report `Cohort`.

### Per creare un report `Cohort` sono necessarie cinque specifiche:

1. Come raggruppare `cohorts`
1. Il periodo di tempo `cohort`
1. Numero di `cohorts` da visualizzare
1. La quantità minima di dati che ogni `cohort` deve contenere
1. Intervallo di tempo dopo `cohort` occorrenza

#### &#x200B;1. Raggruppamento di `cohorts`

`Cohorts` sono raggruppati per marca temporale, ad esempio **data di registrazione** o **data primo ordine**.

>[!NOTE]
>
>Non è possibile utilizzare la stessa marca temporale su cui è basata la metrica per la data `cohort`. Per un&#39;analisi che richiede questo, puoi utilizzare invece `Standard report builder`.

#### &#x200B;2. Periodo di tempo `Cohort`

Scegliere il periodo di tempo in base al quale raggruppare `cohorts`. In altre parole, quale parte del timestamp selezionato in precedenza è più importante: `week`, `month`, `quarter` o `year`? Il rapporto visualizza i dati in qualsiasi intervallo selezionato qui

#### &#x200B;3. e 4. Imposta il numero di `cohorts` da visualizzare e la quantità di dati che ogni `cohort` deve avere

Questi parametri consentono di visualizzare solo i `cohorts` che ti interessano e la pratica casella `Preview` nella parte inferiore della finestra mostra esattamente le coorti visualizzate nel report.

Per impostazione predefinita, `cohort` corrente non è incluso a meno che non si modifichi la quantità minima di dati richiesti per ogni `cohort` in `0`. In questo caso, `cohort` per il periodo di tempo corrente include solo dati parziali.

#### &#x200B;5. Intervallo di tempo dopo `Cohort` occorrenza

Questa funzionalità consente di impostare l&#39;intervallo di tempo dei dati visualizzati per `cohorts` selezionato. Ad esempio, se si desidera visualizzare 24 `cohorts` mensili in base a `customer's first order date`, ma si è interessati solo ai primi 3 mesi di dati per ogni `cohort`, è possibile impostare `number of cohorts to view` su `24` e `time range after cohort occurrence` su `3`.

L&#39;intervallo per questo valore cambia con quello selezionato in `cohort time period` e il valore è impostato su `12` per impostazione predefinita; il valore non cambia a meno che non si faccia clic sull&#39;icona del calendario per modificarlo.

![Selettore intervallo di tempo coorte con opzioni data](../../assets/cohort-time-range.png)

#### Altre note

* [!UICONTROL Filters]: applicato alle metriche, rimane intatto quando si passa da `Standard` a `Cohort` visualizzazioni.

* Vedere [`Perspectives`](#perspectives).

#### Esempio

Ecco un esempio per mettere tutto insieme. In questo esempio, desidero controllare il comportamento degli ordini dopo il primo acquisto di `cohort` per verificare se la coorte torna a effettuare acquisti ripetuti nei prossimi sei mesi.

![Coorte ordini](../../assets/crb_example.gif)

### Architettura legacy

#### Architettura legacy {#personalinfo}

Di seguito sono riportate le istruzioni specifiche della versione legacy di `Cohort Report Builder`. Se sei interessato a utilizzare la nuova versione, consulta [Nuova architettura](../../administrator/account-management/new-architecture.md) per ulteriori informazioni sulla migrazione a un account [!DNL Commerce Intelligence] Nuova architettura.

#### Come si crea un&#39;analisi `cohort` personalizzata? {#create}

![Finestra di dialogo per l&#39;analisi per coorte con opzioni di configurazione](../../assets/create-cohort-analysis.png)

`Cohort` analisi in azione. In questo caso, puoi vedere i ricavi crescere nel tempo sia cumulativamente che per utente.

Questa sezione illustra come creare la propria analisi di `cohort`. Per esempi (e file GIF animati che illustrano il processo), consulta la [sezione Esempi](#examples) di questo argomento.

1. Fai clic su **[!UICONTROL Report Builder]** nella scheda a sinistra o su **[!UICONTROL Add Report** > **Create Report]** in qualsiasi dashboard.

1. Nella schermata `Report Builder Selection`, fare clic su **[!UICONTROL Create Report]** accanto all&#39;opzione `Cohort Analysis`.

#### Aggiunta di una metrica

Ora che ti trovi in `Cohort Report Builder`, aggiungi la metrica (ad esempio: `Revenue` o `Number of orders`) sulla quale desideri eseguire l&#39;analisi.

>[!NOTE]
>
>Le metriche native di [!DNL Google Analytics] non sono compatibili con `Cohort Report Builder`.

#### Selezione della data della coorte {#date}

Il passaggio successivo consiste nel specificare `cohort date`. Questa è la data entro la quale gli utenti sono raggruppati. Potrebbe essere `User's first order date` o `User's registration date`.

>[!NOTE]
>
>Non è possibile utilizzare la stessa data in cui la metrica è stata generata (ad esempio: `created at`) come `cohort date`.

#### Impostazione dell&#39;intervallo e del periodo di tempo

Quindi, impostare `Interval` e `Time Period`.

`Interval`
L&#39;opzione `Interval` consente di impostare `length` di `cohorts`. Ad esempio, se è impostato su `Month`, il report viene misurato in mesi.

Puoi modificare la modalità di visualizzazione di questi intervalli sull&#39;asse x utilizzando il menu **Durata**.

`Time Period`
Utilizzare il menu `Time Period` per scegliere l&#39;utente specifico `cohorts` da analizzare. È possibile visualizzare ogni `cohort`, scegliere da un elenco, specificare un intervallo di tempo o definire un intervallo di tempo continuo di `cohorts` da includere. Ad esempio, se è stata utilizzata l&#39;opzione `Specific Cohorts`, è possibile selezionare mesi specifici da includere nell&#39;analisi:

![Utilizzo del menu `Time Period` per aggiungere `Cohorts`](../../assets/Cohort_Time_Period.gif) specifici

Se si effettua il raggruppamento di `cohorts` per data di registrazione e quindi si seleziona Aprile, Maggio e Giugno nell&#39;elenco `Specific Cohorts`, verranno inclusi tutti gli utenti registrati in quei mesi.

#### Definizione dell’asse X

In `duration` è possibile definire le impostazioni dell&#39;asse X del grafico. In altre parole, quanti periodi di tempo ogni punto dati rappresenta e quanti punti dati includere nell’analisi.

#### Selezione della tabella `counting members`

Se si è scelto di raggruppare gli utenti in base a un `cohort date` che è stato aggiunto da un&#39;altra tabella, è possibile che venga visualizzata l&#39;opzione `counting members in the … table`.

![Opzione membri conteggio coorte con modalità indipendente e cumulativa](../../assets/Cohort_Counting_Members_option.png)

Guarda un esempio per comprendere questa impostazione. Supponiamo che tu abbia creato un rapporto che classifica una metrica `Revenue` per `Customer's registration date`. Si desidera inoltre utilizzare la prospettiva `Average value per cohort member` per visualizzare i ricavi per acquirente nel tempo. Per trovare il valore medio per acquirente, devi decidere il numero di acquirenti da dividere. È il numero di clienti registrati nella tabella `customers` o è il numero di acquirenti distinti in `orders table` per lo stesso periodo?

Questa impostazione risponde a tale domanda. Il conteggio dei membri nella tabella `customers` include in media tutti i clienti (sia che abbiano effettuato un acquisto). Il conteggio dei membri nella tabella `orders` include solo i clienti che hanno effettuato un acquisto.

#### Selezione di una prospettiva {#perspective}

Dopo aver definito la metrica e come analizzarla, è possibile selezionare `perspective` da utilizzare.

Appena sopra la visualizzazione del rapporto c&#39;è un elenco a discesa di `perspective` impostazioni.

Vedi [Prospettive](#perspectives).

![Menu Prospettiva coorte con diverse opzioni di visualizzazione](../../assets/Cohort_Perspective_Menu.png)

## Esempi di analisi per coorte {#examples}

Dopo aver descritto come creare un&#39;analisi `cohort`, vedere alcuni esempi.

### Desidero sapere in che modo il mio utente `cohorts` sta crescendo nel tempo.

![Utente `cohorts` in crescita nel tempo](../../assets/cohort1.gif)

In questo esempio, hai analizzato la metrica `Revenue`, hai raggruppato le coorti per `customer's first order date` e hai selezionato gli 8 `cohorts` più recenti (definiti nel menu `Time Period`) da includere nell&#39;analisi. Per vedere come le coorti sono cresciute nel tempo, hai utilizzato `Cumulative Average Value per Cohort Member` `perspective`.

### Voglio sapere, in media, quanti ordini un utente fa in momenti diversi della sua vita.

(../../assets/cohort2.gif

In questo esempio è stata analizzata la metrica `Number of orders`, le coorti sono state raggruppate in base a `customer's first order date` e nell&#39;analisi sono state incluse le otto coorti più recenti (definite nel menu `Time Period`). Per visualizzare il numero medio di ordini per ogni coorte, è stato modificato `perspective` in `Average Value per Cohort Member`.

### Voglio capire come si confronta l&#39;attività di acquisto futura di un utente con l&#39;attività del primo mese con l&#39;azienda.

![Confronto tra le attività di acquisto future di un utente e il primo mese di attività](../../assets/cohort3.gif)

## `Perspectives` {#perspectives}

`Standard`
Mostra il contributo incrementale di un dato gruppo di coorti in un dato momento del loro ciclo di vita. Ad esempio, il punto &quot;Settimana 6&quot; mostra tutte le coordinate effettuate dagli utenti nella sesta settimana.

`Average Value per Cohort Member`
L&#39;analisi `Standard cohort` in (1) viene divisa per il numero di utenti in ogni gruppo `cohort`. Ciò può essere utile per confrontare le prestazioni delle coorti in base al confronto tra mele, in quanto non tutti i gruppi di coorte possono includere lo stesso numero di utenti. Ad esempio, il ricavo medio settimanale 6 per utente da un determinato `cohort`.

`Cumulative`
`perspective` mostra l&#39;analisi `cohort` tradizionale su base `cumulative`. In altre parole, mostra il contributo totale di una determinata coorte fino ad oggi in un dato momento del loro ciclo di vita. Ad esempio, i ricavi cumulativi dopo sei settimane di utilizzo da una determinata coorte.

`Cumulative Average Value per Cohort Member`
L&#39;analisi `Cumulative` in (3) viene divisa per il numero di utenti in ogni gruppo `cohort`. Mostra il contributo medio per l&#39;intero ciclo di vita (spesso reddito medio per l&#39;intero ciclo di vita) per `cohort` membro in ogni periodo della durata di `cohort's`. Ad esempio, i ricavi medi del ciclo di vita dopo sei mesi di utenti che hanno aderito a giugno.

`Percent of First Value (show first value)`
Questo analizza il contributo aggregato `cohort` in un momento specifico in un ciclo di vita `cohort's` come percentuale del contributo nel primo periodo. Ad esempio, i ricavi del mese 6 divisi per i ricavi del mese 1 degli utenti che hanno aderito a giugno.

`Percent of First Value (hide first value)`
È lo stesso di `perspective` sopra, tranne per il fatto che il valore del primo periodo di tempo del 100% è nascosto.

## Ritorno a capo {#finish}

`Cohort Report Builder` è ottimizzato per il raggruppamento degli utenti in base a un `cohort date` comune. Potrebbe essere utile raggruppare gli utenti per un&#39;attività o un attributo simile. Adobe consiglia di consultare [questo tutorial sulle coorti qualitative](../dev-reports/create-qual-cohort-analysis.md) per iniziare.
