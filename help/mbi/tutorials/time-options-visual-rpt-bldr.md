---
title: Utilizzare le opzioni di tempo in Visual Report Builder
description: Scopri come analizzare i dati nel rapporto per un periodo di tempo specifico.
exl-id: a1bb4838-f882-44b1-a29f-84b985032ceb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 0%

---

# Usa opzioni [!DNL Time] in [!DNL Visual Report Builder]

Una delle caratteristiche di [!DNL Visual Report Builder] è l&#39;impostazione globale di `Time Range` e `Interval`. Queste impostazioni consentono di analizzare i dati nel rapporto per un periodo di tempo specifico.

Tuttavia, per alcune analisi, potrebbe essere necessario considerare diversi intervalli di tempo o intervalli di tempo nello stesso rapporto. Qui entrano in gioco le opzioni `Time`. Per avere un&#39;idea migliore dell&#39;utilizzo delle opzioni `Time` nei report, questo tutorial illustra i seguenti casi d&#39;uso:

* [Analisi delle metriche senza marca temporale](#notimestamp)
* [Assegnare a una metrica un intervallo di tempo indipendente](#independenttimeinterval)
* [Confronto della stessa metrica tra intervalli di tempo diversi](#difftimerange)

Se desideri seguire alcuni dei report di esempio descritti in questo argomento, apri [[!DNL Visual Report Builder]](../data-user/reports/ess-rpt-build-visual.md) prima di continuare.

## Analisi delle metriche senza marca temporale {#notimestamp}

Alcune metriche semplicemente non possono avere una tendenza nel tempo perché i dati non vengono raccolti o memorizzati con una marca temporale associata. Ad esempio, una tabella di inventario spesso contiene una sola riga per ogni SKU. In tal caso, è necessario [creare la metrica](../data-user/reports/ess-manage-data-metrics.md) senza specificare una marca temporale.

Quando si utilizza tale metrica nel reporting, si nota che l&#39;aggiunta di questa metrica a un report imposta automaticamente un `Time Interval` indipendente di `None` e un `Time Range` di `Global`:

![](../assets/Metrics_without_timestamps.gif)

## Assegnare a una metrica un intervallo di tempo indipendente {#independenttimeinterval}

`Time` Le opzioni consentono di creare grafici al 100% basati sul tempo per identificare il giorno, la settimana, il mese o l&#39;anno che ha contribuito maggiormente durante un intervallo di tempo specifico. In questa sezione viene creato un grafico che mostra la percentuale di ricavi generati in ogni mese di calendario di un anno.

Questo tipo di rapporto può essere utile se si desidera confrontare i ricavi generati anno su anno. Ad esempio, un grafico per il 2015 rivela che gennaio ha contribuito per il 18% alle entrate dell&#39;anno, mentre un grafico per il 2016 mostra solo l&#39;8%. Potresti iniziare a fare ricerche su quello che potrebbe essere successo.

1. Aggiungi la metrica `Revenue` al rapporto.
1. Fare clic su **[!UICONTROL Duplicate]** per creare una copia della metrica.
1. Fare clic sull&#39;opzione globale **[!UICONTROL Time Range]**, quindi su **[!UICONTROL Moving Time Range]**. Imposta su `Last Year`.
1. Fare clic sull&#39;opzione globale **[!UICONTROL Time Interval]** e impostarla su `Monthly`.
1. Report Builder aggiunge automaticamente un secondo asse Y per una seconda metrica. Deselezionare la casella `Multiple Y-Axes`.
1. Successivamente, applichi un `Time Interval` indipendente alla prima metrica. Fai clic su **[!UICONTROL Time Options]** (icona orologio) a destra di `first Revenue metric`.
1. Fare clic su **[!UICONTROL Time Options]** nella finestra espansa visualizzata sopra il report.
1. Nel menu a discesa, imposta quanto segue:

   * `Time Interval`: impostare su `None`.

   * `Time Range`: impostare `Last Year` facendo clic su **[!UICONTROL Custom]**, quindi su **[!UICONTROL Moving Range]** e infine selezionando l&#39;opzione `Last Year`.

   * Fare clic su **[!UICONTROL Apply]** per salvare le impostazioni dell&#39;intervallo e dell&#39;intervallo. Viene creata una metrica che calcola i ricavi totali per l’anno precedente. Quindi, utilizza questa metrica come denominatore in una formula.

   * Per visualizzare la percentuale di ricavi per ogni mese, è necessario aggiungere una formula al rapporto. Fare clic su **[!UICONTROL Add Formula]**.

   * Immetti `B/A` nel campo formula e seleziona `% Percent` dal menu a discesa accanto al campo di testo. Questa formula divide l’importo delle entrate provenienti da un mese specifico dello scorso anno per l’importo totale delle entrate dello scorso anno.

   * Fare clic su **[!UICONTROL Apply Changes]**.

   * Nascondi entrambe le metriche di input e rinomina la formula.

Ora puoi vedere quanto ha avuto un impatto ogni mese lo scorso anno:

![](../assets/Independent_Time_Int.png)

## Confronto della stessa metrica tra intervalli di tempo diversi {#difftimerange}

In questo esempio viene utilizzata una dimensione personalizzata denominata `Day number of the month`. Se desideri creare questo report e non hai già questa dimensione nel tuo Data Warehouse, [contatta il supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) per assistenza.

I due esempi più comuni in questa categoria sono (1) il confronto delle metriche di crescita (ricavi su base annua o mese sul mese) e (2) una migliore comprensione delle recenti tendenze delle scorte o delle vendite di articoli.

Per dimostrare questo caso d’uso, osserva le entrate giornaliere del mese precedente rispetto allo stesso mese dell’anno precedente. Se vuoi esaminare i ricavi per ogni giorno di gennaio 2016 e poi confrontarli con gennaio 2015, gennaio 2014 e così via, questo rapporto ce lo mostrerebbe.

1. Aggiungi la metrica `Revenue` al rapporto.
1. Fare clic su **[!UICONTROL Duplicate]** per creare una copia della metrica.
1. Rinominare la prima metrica in `Items sold last 7 days` e la seconda in `Items sold last 28 days`.
1. Fare clic su **[!UICONTROL Time Range]**, quindi su **[!UICONTROL Moving Time Range]**. Imposta su `Last Month`.
1. Fare clic su **[!UICONTROL Time Interval]** e impostarlo su `None`.
1. Fai clic su **[!UICONTROL Time Options]** (icona orologio) accanto alla seconda metrica `Revenue`.
1. Fare clic su **[!UICONTROL Time Options]** nella finestra espansa visualizzata sopra il report.
1. Nel menu a discesa, imposta quanto segue:

   * `Time Interval`: impostare su `None`.

   * `Time Range`: impostare `From 14 Months Ago To 13 Months Ago` facendo clic su **[!UICONTROL Custom]** e quindi su **[!UICONTROL Moving Range]**. Utilizza i campi e i menu a discesa nella parte superiore del menu per impostare l’intervallo. Questa impostazione consente di visualizzare i ricavi del mese precedente, ma dell’anno precedente.

   Non preoccuparti se la metrica scompare dal rapporto: l’impostazione di un’opzione di tempo indipendente nasconde automaticamente la metrica dal rapporto. Per visualizzarlo nuovamente, fare clic su **[!UICONTROL Show]** accanto alla metrica.

   ![](../assets/Different_Time_Ranges.gif)

   * Fare clic su **[!UICONTROL Apply]** per salvare le impostazioni dell&#39;intervallo e dell&#39;intervallo.

   * Aggiungere quindi la dimensione `Day number of the month` personalizzata facendo clic su **[!UICONTROL Group By]** e selezionando la dimensione. In questo modo verrà restituito il numero del giorno del mese di un ordine. Ad esempio, un ordine effettuato il 2 marzo restituirà `2`.

   * Nel menu a discesa `Group By`, seleziona `Show All` e fai clic su **[!UICONTROL Apply]**. In questo modo vengono creati i valori dell’asse X per il rapporto:

   ![](../assets/TO4.png)

   * Rinominare le metriche. Nell&#39;esempio, la prima metrica è `Revenue - 2015` e la seconda è `Revenue - 2014`.

Un altro uso comune di `Time Options` personalizzati consiste nel determinare le settimane di fornitura. Soprattutto durante le feste o un periodo promozionale speciale, puoi prendere in considerazione gli articoli venduti nell&#39;ultima settimana, nell&#39;ultimo mese e nel periodo promozionale precedente per prendere decisioni di acquisto informate.

Ricordati di impostare gli intervalli di tempo in base alle tue esigenze durante la creazione di questo rapporto.

1. Aggiungi la metrica `Items Sold` al rapporto.
1. Fare clic su **[!UICONTROL Duplicate]** per creare una copia della metrica.
1. Rinominare le metriche. Puoi usare gli stessi nomi o qualcosa di simile:
   1. Rinomina la prima metrica in `Items sold last 7 days`.
   1. Rinominare la seconda metrica in `Items sold last 28 days`.
1. Nella metrica `Items sold last 7 days`, fare clic sull&#39;opzione globale **[!UICONTROL Time Range]** e quindi **[!UICONTROL Moving Time Range]**. In questo esempio è stato impostato su `Last 7 Days`.
1. Fare clic su **[!UICONTROL Time Interval]** e impostarlo su `None`.
1. Successivamente, si definisce `Time Options` per la metrica `Items sold last 28 days`. Fare clic su **[!UICONTROL Time Options]** (icona orologio) a destra della metrica `second Items sold`.
1. Fare clic su **[!UICONTROL Time Options]** nella finestra espansa visualizzata sopra il report.
1. Nel menu a discesa, imposta quanto segue:

   * `Time Interval`: impostare su `None`.
   * `Time Range`: impostare `From 29 days to 1 day ago` facendo prima clic su **[!UICONTROL Custom]**, quindi su **[!UICONTROL Moving Range]**. Utilizza i campi e i menu a discesa nella parte superiore del menu per impostare l’intervallo.
   * Fare clic su **[!UICONTROL Apply]** per salvare le impostazioni dell&#39;intervallo e dell&#39;intervallo.
   * Duplica la metrica `Items sold last 28 days` e apri la nuova metrica `Time Options`. Impostare le opzioni come segue:

      * `Time Interval`: lasciare `None`.
      * `Time Range`: modificare l&#39;intervallo di date per allinearlo alla promozione desiderata facendo clic su **[!UICONTROL Specific Date Range]** e immettendo le date appropriate.
      * Rinominare la metrica `Items sold during last promotion` o qualcosa di simile.
      * Aggiungi la metrica `Units on hand`.
      * È quindi necessario aggiungere i calcoli che mostrano le settimane disponibili, considerando l&#39;andamento delle vendite, per i periodi di tempo (`last 7 days`, `last 28 days` e `last promo`) che si stanno includendo nel report. Questa operazione deve essere eseguita una volta per ogni periodo di tempo.

Per creare le formule, scegliere **[!UICONTROL Add Formula]**. Immettere le formule seguenti e fare clic su **[!UICONTROL Apply Changes]** al termine. Ripetere questa operazione per ciascuno dei tre periodi di tempo:

* Per `last 7 days time period`, immettere `D / A` nel campo `Formula`.
* Per `last 28 days time period`, immettere `D / (B/4)` nel campo `Formula`.

  >[!NOTE]
  >
  >È importante normalizzare qui gli intervalli di tempo selezionati. In questo esempio, suddividi 28 giorni in quattro settimane. Potrebbe essere necessario applicare una logica diversa alla formula.

* Per `last promo period`, immettere `D / C` nel campo `Formula`.

  ![](../assets/Different_Time_Ranges_2.png)

* Infine, personalizzare il rapporto nascondendo le metriche e aggiungendo una dimensione `SKU` o simile al rapporto come `Group By`.

Questo esempio dimostra che gli attuali livelli di scorte erano ben posizionati per una vendita di 14 giorni a livello di prodotto. Tuttavia, l&#39;aggiunta di un periodo promozionale comparabile suggerisce che l&#39;azienda deve apportare alcune modifiche - sia ordinando più scorte e promuovendo solo gli articoli con abbastanza unità in magazzino.

Poiché i tuoi clienti si comportano in modo diverso nel tempo, puoi aspettarti di vedere varianze nei dati durante l’esecuzione delle analisi. L’impostazione di opzioni di tempo personalizzate consente di creare rapidamente analisi complesse, consentendo decisioni basate sui dati che tengono conto delle tendenze storiche.

