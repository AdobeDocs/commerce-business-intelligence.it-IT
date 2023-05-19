---
title: Utilizzare le opzioni di tempo nel Report Builder visivo
description: Scopri come analizzare i dati nel rapporto per un periodo di tempo specifico.
exl-id: a1bb4838-f882-44b1-a29f-84b985032ceb
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 0%

---

# Utilizzare [!DNL Time] Opzioni in [!DNL Visual Report Builder]

Una delle caratteristiche della [!DNL Visual Report Builder] è il valore globale `Time Range` e `Interval` impostazioni. Queste impostazioni consentono di analizzare i dati nel rapporto per un periodo di tempo specifico.

Tuttavia, per alcune analisi, potrebbe essere necessario considerare diversi intervalli di tempo o intervalli di tempo nello stesso rapporto. È qui che `Time` Le opzioni entrano. Per darti un&#39;idea migliore di come usare `Time` opzioni nei rapporti, questo tutorial descrive i seguenti casi d’uso:

* [Analisi delle metriche senza marca temporale](#notimestamp)
* [Assegnare a una metrica un intervallo di tempo indipendente](#independenttimeinterval)
* [Confronto della stessa metrica tra intervalli di tempo diversi](#difftimerange)

Se desideri seguire alcuni dei rapporti di esempio discussi in questo argomento, apri la sezione [[!DNL Visual Report Builder]](../data-user/reports/ess-rpt-build-visual.md) prima di continuare.

## Analisi delle metriche senza marca temporale {#notimestamp}

Alcune metriche semplicemente non possono avere una tendenza nel tempo perché i dati non vengono raccolti o memorizzati con una marca temporale associata. Ad esempio, una tabella di inventario spesso contiene una sola riga per ogni SKU. In tal caso, dovresti [creare la metrica](../data-user/reports/ess-manage-data-metrics.md) senza specificare una marca temporale.

Quando si utilizza tale metrica nei rapporti, si nota che l’aggiunta di tale metrica a un rapporto imposta automaticamente un’attività indipendente `Time Interval` di `None` e `Time Range` di `Global`:

![](../assets/Metrics_without_timestamps.gif)

## Assegnare a una metrica un intervallo di tempo indipendente {#independenttimeinterval}

`Time` Le opzioni consentono di creare grafici al 100% basati sul tempo per identificare il giorno, la settimana, il mese o l’anno che ha contribuito di più durante un intervallo di tempo specifico. In questa sezione viene creato un grafico che mostra la percentuale di ricavi generati in ogni mese di calendario di un anno.

Questo tipo di rapporto può essere utile se si desidera confrontare i ricavi generati anno su anno. Ad esempio, un grafico per il 2015 rivela che gennaio ha contribuito per il 18% alle entrate dell&#39;anno, mentre un grafico per il 2016 mostra solo l&#39;8%. Potresti iniziare a fare ricerche su quello che potrebbe essere successo.

1. Aggiungi il `Revenue` metrica al rapporto.
1. Clic **[!UICONTROL Duplicate]** per creare una copia della metrica.
1. Fai clic sul pulsante **[!UICONTROL Time Range]** , quindi **[!UICONTROL Moving Time Range]**. Imposta su `Last Year`.
1. Fai clic sul pulsante **[!UICONTROL Time Interval]** e impostarla su `Monthly`.
1. Report Builder aggiunge automaticamente un secondo asse Y per una seconda metrica. Deseleziona il `Multiple Y-Axes` casella.
1. Quindi, si applica un `Time Interval` alla prima metrica. Clic **[!UICONTROL Time Options]** (icona dell’orologio) a destra del `first Revenue metric`.
1. Clic **[!UICONTROL Time Options]** nella finestra espansa visualizzata sopra il rapporto.
1. Nel menu a discesa, imposta quanto segue:

   * `Time Interval`: imposta su `None`.

   * `Time Range`: imposta su `Last Year` facendo clic su **[!UICONTROL Custom]**, quindi **[!UICONTROL Moving Range]**, e infine la selezione del `Last Year` opzione.

   * Clic **[!UICONTROL Apply]** per salvare le impostazioni di intervallo e intervallo. Viene creata una metrica che calcola i ricavi totali per l’anno precedente. Quindi, utilizza questa metrica come denominatore in una formula.

   * Per visualizzare la percentuale di ricavi per ogni mese, è necessario aggiungere una formula al rapporto. Clic **[!UICONTROL Add Formula]**.

   * Invio `B/A` nel campo formula e selezionare `% Percent` dal menu a discesa accanto al campo di testo. Questa formula divide l’importo delle entrate provenienti da un mese specifico dello scorso anno per l’importo totale delle entrate dello scorso anno.

   * Clic **[!UICONTROL Apply Changes]**.

   * Nascondi entrambe le metriche di input e rinomina la formula.

Ora puoi vedere quanto ha avuto un impatto ogni mese lo scorso anno:

![](../assets/Independent_Time_Int.png)

## Confronto della stessa metrica tra intervalli di tempo diversi {#difftimerange}

In questo esempio viene utilizzata una dimensione personalizzata denominata `Day number of the month`. Se desideri creare questo rapporto e non hai già questa dimensione nella tua Data Warehouse, [contatta l’assistenza](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) per assistenza.

I due esempi più comuni in questa categoria sono (1) il confronto delle metriche di crescita (ricavi su base annua o mese sul mese) e (2) una migliore comprensione delle recenti tendenze delle scorte o delle vendite di articoli.

Per dimostrare questo caso d’uso, osserva le entrate giornaliere del mese precedente rispetto allo stesso mese dell’anno precedente. Se vuoi esaminare i ricavi per ogni giorno di gennaio 2016 e poi confrontarli con gennaio 2015, gennaio 2014 e così via, questo rapporto ce lo mostrerebbe.

1. Aggiungi il `Revenue` metrica al rapporto.
1. Clic **[!UICONTROL Duplicate]** per creare una copia della metrica.
1. Rinomina la prima metrica in `Items sold last 7 days` e la seconda metrica da `Items sold last 28 days`.
1. Clic **[!UICONTROL Time Range]**, quindi **[!UICONTROL Moving Time Range]**. Imposta su `Last Month`.
1. Clic **[!UICONTROL Time Interval]** e impostarlo su `None`.
1. Clic **[!UICONTROL Time Options]** (icona orologio) accanto al secondo `Revenue` metrica.
1. Clic **[!UICONTROL Time Options]** nella finestra espansa visualizzata sopra il rapporto.
1. Nel menu a discesa, imposta quanto segue:

   * `Time Interval`: imposta su `None`.

   * `Time Range`: imposta su `From 14 Months Ago To 13 Months Ago` facendo clic su **[!UICONTROL Custom]** allora **[!UICONTROL Moving Range]**. Utilizza i campi e i menu a discesa nella parte superiore del menu per impostare l’intervallo. Questa impostazione consente di visualizzare i ricavi del mese precedente, ma dell’anno precedente.
   Non preoccuparti se la metrica scompare dal rapporto: l’impostazione di un’opzione di tempo indipendente nasconde automaticamente la metrica dal rapporto. Per visualizzarlo di nuovo, fai clic su **[!UICONTROL Show]** accanto alla metrica.

   ![](../assets/Different_Time_Ranges.gif)

   * Clic **[!UICONTROL Apply]** per salvare le impostazioni di intervallo e intervallo.

   * Quindi, aggiungi il tuo `Day number of the month` dimensione facendo clic su **[!UICONTROL Group By]** e selezionando la quota. In questo modo verrà restituito il numero del giorno del mese di un ordine, ad esempio un ordine effettuato il 2 marzo verrà restituito `2`.

   * In `Group By` a discesa, seleziona `Show All` e fai clic su **[!UICONTROL Apply]**. In questo modo vengono creati i valori dell’asse X per il rapporto:

   ![](../assets/TO4.png)

   * Rinominare le metriche. Nell’esempio, la prima metrica è `Revenue - 2015` e la seconda è `Revenue - 2014`.



Un altro uso comune di `Time Options` è quello di determinare le settimane di fornitura. Soprattutto durante le feste o un periodo promozionale speciale, puoi prendere in considerazione gli articoli venduti nell&#39;ultima settimana, nell&#39;ultimo mese e nel periodo promozionale precedente per prendere decisioni di acquisto informate.

Ricordati di impostare gli intervalli di tempo in base alle tue esigenze durante la creazione di questo rapporto.

1. Aggiungi il `Items Sold` metrica al rapporto.
1. Clic **[!UICONTROL Duplicate]** per creare una copia della metrica.
1. Rinominare le metriche. Puoi usare gli stessi nomi o qualcosa di simile:
   1. Rinomina la prima metrica in `Items sold last 7 days`.
   1. Rinomina la seconda metrica in `Items sold last 28 days`.
1. Il giorno `Items sold last 7 days` metrica, fai clic sul collegamento globale **[!UICONTROL Time Range]** opzione then **[!UICONTROL Moving Time Range]**. Per questo esempio, impostalo su `Last 7 Days`.
1. Clic **[!UICONTROL Time Interval]** e impostarlo su `None`.
1. Quindi, puoi definire `Time Options` per `Items sold last 28 days` metrica. Clic **[!UICONTROL Time Options]** (icona dell’orologio) a destra del `second Items sold` metrica.
1. Clic **[!UICONTROL Time Options]** nella finestra espansa visualizzata sopra il rapporto.
1. Nel menu a discesa, imposta quanto segue:

   * `Time Interval`: imposta su `None`.
   * `Time Range`: imposta su `From 29 days to 1 day ago` facendo clic su **[!UICONTROL Custom]**, quindi **[!UICONTROL Moving Range]**. Utilizza i campi e i menu a discesa nella parte superiore del menu per impostare l’intervallo.
   * Clic **[!UICONTROL Apply]** per salvare le impostazioni di intervallo e intervallo.
   * Duplica il `Items sold last 28 days` e aprire la nuova metrica `Time Options`. Impostare le opzioni come segue:

      * `Time Interval`: lascia questo come `None`.
      * `Time Range`: imposta l’intervallo di date che corrisponde alla promozione che ti interessa facendo clic su **[!UICONTROL Specific Date Range]** e quindi immettere le date appropriate.
      * Rinominare la metrica `Items sold during last promotion` o qualcosa di simile.
      * Aggiungi il `Units on hand` metrica.
      * Successivamente, è necessario aggiungere i calcoli che mostrano le settimane disponibili, considerando l&#39;andamento delle vendite, per i periodi di tempo (`last 7 days`, `last 28 days`, e `last promo` punto) che si sta includendo nel report. Questa operazione deve essere eseguita una volta per ogni periodo di tempo.

Per creare le formule, fare clic su **[!UICONTROL Add Formula]**. Immetti le formule seguenti e fai clic su **[!UICONTROL Apply Changes]** al termine. Ripetere questa operazione per ciascuno dei tre periodi di tempo:

* Per `last 7 days time period`, immetti `D / A` nel `Formula` campo.
* Per `last 28 days time period`, immetti `D / (B/4)` nel `Formula` campo.

   >[!NOTE]
   >
   >È importante normalizzare qui gli intervalli di tempo selezionati. In questo esempio, suddividi 28 giorni in quattro settimane. Potrebbe essere necessario applicare una logica diversa alla formula.

* Per `last promo period`, immetti `D / C` nel `Formula` campo.

   ![](../assets/Different_Time_Ranges_2.png)

* Infine, personalizza il rapporto nascondendo le metriche e aggiungendo una `SKU` o una dimensione simile al rapporto come `Group By`.

Questo esempio dimostra che gli attuali livelli di scorte erano ben posizionati per una vendita di 14 giorni a livello di prodotto. Tuttavia, l&#39;aggiunta di un periodo promozionale comparabile suggerisce che l&#39;azienda deve apportare alcune modifiche - sia ordinando più scorte e promuovendo solo gli articoli con abbastanza unità in magazzino.

Poiché i tuoi clienti si comportano in modo diverso nel tempo, puoi aspettarti di vedere varianze nei dati durante l’esecuzione delle analisi. L’impostazione di opzioni di tempo personalizzate consente di creare rapidamente analisi complesse, consentendo decisioni basate sui dati che tengono conto delle tendenze storiche.

