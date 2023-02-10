---
title: Incremento del ROI nelle campagne pubblicitarie
description: Scopri alcuni metodi diversi per valutare le prestazioni della campagna.
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '1294'
ht-degree: 0%

---

# Campagne pubblicitarie e ROI

MBI consente di [dati sul costo della pubblicità e sui ricavi](../../data-analyst/importing-data/integrations/google-adwords.md) dal database. Questo ti aiuterà a identificare quali campagne hanno il ROI più alto. In questo articolo, esaminiamo alcuni metodi diversi per valutare le prestazioni della campagna.

## Prerequisiti

* Importa i dati dei costi pubblicitari:
   * [Collega il tuo [!DNL Google AdWords] a [!DNL MBI]](../importing-data/integrations/google-adwords.md): Questo consente di sincronizzare automaticamente il [!DNL Adwords] spendere [!DNL MBI]
   * [Caricare altri dati sui costi pubblicitari](../importing-data/connecting-data/import-offline-ad-data.md): Questa opzione è consigliata per i canali senza connettore diretto a [!DNL MBI]
   * Se importi i dati dei costi da più origini, possiamo [consolidare](../../best-practices/consolidating-your-tables.md) i dati [!DNL MBI]. Semplicemente [inviare un ticket di supporto](../../guide-overview.md).
* [Tracciare i dati del canale di acquisizione utente](../analysis/google-track-user-acq.md)

## Campagne di acquisizione utente

Le campagne mirate all’acquisizione di utenti possono essere misurate da diverse prospettive, tra cui:

1. Il numero di nuovi utenti acquisiti delle campagne
1. Tasso di conversione dalla registrazione all’acquisto di campagne
1. Il ROI delle campagne in base al valore medio del ciclo di vita dell’utente (LTV)

Le analisi (1) e (2) di cui sopra sono esaminate in un&#39;esercitazione separata su [identificazione dei canali di marketing principali](../analysis/most-value-source-channel.md). In questo caso, esploriamo l’analisi (3) per misurare il ROI delle campagne nel tempo. In questo modo verrà verificato se gli utenti acquisiti da una particolare campagna hanno generato un fatturato a vita sufficiente a coprire i costi di acquisizione.

>[!NOTE]
>
>Ipotizziamo che tutti i costi della campagna siano stati utilizzati esclusivamente per acquisire nuovi utenti. In realtà, anche il costo della campagna viene condiviso con l’acquisizione di visite non convertite, con l’acquisto ripetuto e così via. Tuttavia, partendo dal presupposto che tutti i costi siano utilizzati per acquisire nuovi utenti registrati, il ROI risultante sarà lo scenario peggiore (il più alto costo per acquisizione), in modo da poter essere certi che il ROI effettivo sia più alto del nostro calcolo.
>
>Esempio: Presupponendo di aver speso $ 20 per una campagna che ha generato 10 nuovi utenti e 10 acquirenti ripetuti, il costo effettivo per nuovo utente è di $ 1, ma partendo dal presupposto che tutti i costi siano andati all&#39;acquisizione di nuovi utenti, il costo per acquisizione è di $ 2.)

**1. Inizia creando un grafico che segmenta il costo dell&#39;annuncio per campagne:**

1. Crea un [!UICONTROL Metric] che somma la vostra spesa nel tempo
1. Vai a [!UICONTROL Data > Metrics]
1. Seleziona `Add New Metric` e seleziona la [!DNL `Adwords...`] tabella che registra il tuo [!DNL AdWords] dati sui costi.
1. Nell’editor metriche, assegna un nome alla metrica (ad esempio, [!UICONTROL AdWord Cost])
1. Utilizzando i menu a discesa, esegui una **Somma** sulla `adCost` nella colonna [!DNL Adwords...] tabella (Modifica) ordinata dal `date` colonna.
   ![](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1. abbiamo finito. Fai clic su `Back to Metric List` in alto e vai su qualsiasi dashboard.

1. Creare un rapporto che i segmenti spendono per campagne
1. In qualsiasi dashboard, fai clic su [!UICONTROL Add Report > Create new report]
1. Seleziona la [!UICONTROL Adword Cost] metrica appena creata
1. Imposta la [!UICONTROL Time period] a `All-time`e [!UICONTROL Interval] a `None`
1. Sotto la `Group by` scheda aggiungi `campaign` come [!UICONTROL grouping field]e fai clic su `Add All` nella scatola.
1. Questo rapporto mostrerà il tuo tempo [!DNL AdWords] costo per campagne

**2. Verrà quindi creato un rapporto che conta i nuovi utenti per campagne:**

1. In qualsiasi dashboard, fai clic su **[!UICONTROL Add Report > Create new report]**
1. Seleziona la `New users` metrica che conta il numero di nuovi utenti registrati nel tempo
1. Imposta la [!UICONTROL Time period] a `All-time`e [!UICONTROL Interval] a `None`
1. Sotto la `Group by` scheda aggiungi `campaign` come `grouping field`e fai clic su **`Add All`** nella scatola
1. Questo rapporto mostrerà i tuoi utenti registrati per campagne

**3. Permettiamo inoltre di creare un rapporto che segmenta l’utente medio LTV per campagne:**

1. In qualsiasi dashboard, fai clic su **[!UICONTROL Add Report > Create new report]**
1. Seleziona la `Average lifetime revenue` metrica che calcola il ricavo medio della vita di un utente
1. Imposta la [!UICONTROL Time period] a `All-time`e [!UICONTROL Interval] a `None`
1. Sotto la `Group by` scheda aggiungi `campaign` o `utm\_campaign` come [!UICONTROL grouping field]e fai clic su `Add All` nella scatola
1. Questo rapporto mostra il fatturato medio dell’utente per campagna

**Infine, calcoleremo il ROI della campagna riunendo queste tre analisi in un rapporto:**

1. In qualsiasi dashboard, fai clic su **[!UICONTROL Add Report > Create new report]**
1. Aggiungi come input utilizzeremo le tre metriche precedentemente utilizzate. A ciascuno verrà assegnata una lettera (ad esempio,\[`A`\], \[`B`\] e \[`C`\]
1. [!UICONTROL Cost]: Aggiungi il costo di AdWords della metrica, che sarà variabile \[A\]. Questo restituirà semplicemente il costo per campagne.
1. [!UICONTROL Users]: Aggiungi la metrica Nuovi utenti - sarà variabile \[B\]. In questo modo verrà semplicemente restituito il numero di utenti per campagna.
1. [!UICONTROL LTV]: Aggiungi la metrica Ricavo medio della vita - sarà variabile \[`C`\]. Questo restituirà semplicemente LTV tramite campagne.

1. Fare clic sull&#39;icona nascondi accanto alla parola Grafico per attivare la tabella
1. Ora utilizzeremo `Add Formula` per combinare queste metriche, come segue:
1. [!UICONTROL ROI]: Immettere la formula `(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])`, se \[`A`\] rappresenta `Ad Cost by Campaigns`, \[`B`\] rappresenta `New users by campaigns`, e \[`C`\] `LTV by campaigns`. Ciò restituirà il rapporto (costo medio per acquisizione di LTV per utente - costo medio per acquisizione) / (costo medio per acquisizione)
1. [!UICONTROL Avg Return per User]: Immettere la formula **\[`C`\]-(\[`A`\]/\[`B`\]**. Ciò restituirà il margine medio di un utente calcolando (costo medio per acquisizione) (LTV per utente medio).
1. [!UICONTROL CPA]: Immettere la formula **`\[A\]/\[B\]`**. Questo restituirà il costo effettivo della campagna per acquisizione.
1. Altre metriche potenziali da includere [!DNL AdWords] i dati includono somme  `Impressions` e `adClicks` (da [!DNL AdWords] dati), insieme al totale `number of orders` realizzato tramite una campagna particolare.
1. Può anche essere interessante calcolare il ROI sulla base di LTV 30 giorni e 90 giorni dopo che un utente si registra o effettua un primo acquisto.

1. Puoi fare clic e trascinare le metriche e le formule per riordinare le colonne del rapporto
1. Assegna un nome al report e assicurati di salvarlo come tabella.

## Campagne di prodotto

Stai eseguendo annunci pubblicitari specifici per prodotto? In tal caso, è possibile misurare il ROI su tali campagne calcolando i ricavi/costi per prodotti specifici.

>[!NOTE]
>
>Ipotizziamo che tutti i costi della campagna siano stati utilizzati esclusivamente per generare acquisti di prodotti specifici. Supponendo che tutti i costi siano stati spesi per la generazione degli acquisti, il ROI risultante sarà il peggiore scenario (il più alto costo per acquisto), in modo da essere sicuri che il ROI effettivo sia superiore a questo calcolo. Esempio: Presupponendo di aver speso 20 dollari per una campagna che ha generato 10 nuovi utenti e 10 acquisti, il costo effettivo per acquisto è di 1 $, ma partendo dal presupposto che tutti i costi siano andati all&#39;acquisizione di nuovi utenti, il costo per acquisto è di 2 $.)*

Prima di iniziare, [inviare un ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) per aggiungere le dimensioni seguenti alla tabella degli elementi riga (`sales\_flat\_order\_item, order\_item`):

* Origine dell’ordine (se tieni traccia dell’origine del riferimento solo a livello di utente, unisciti all’origine dell’utente)
* Campagna dell’ordine (se tieni traccia dell’origine del riferimento solo a livello di utente, unisciti alla campagna dell’utente)
* Canale dell&#39;ordine (se tieni traccia dell&#39;origine del riferimento solo a livello di utente, unisciti al supporto dell&#39;utente)

**1. Ora inizia creando un grafico che restituisce i ricavi per campagna per prodotti specifici:**

1. In qualsiasi dashboard, fai clic su **[!UICONTROL Add Report > Create new report]**
1. Seleziona la `Revenue by items` metrica che calcola i ricavi a livello di voci
1. Imposta la [!UICONTROL Time period] a `All-time`e [!UICONTROL Interval] a `None`
1. Sotto la `Filter by` scheda aggiungi `product name 'IN'` Prodotto `A`, Prodotto `B`, Prodotto `C`, ...&quot; e includere tutti i nomi di prodotto interessati dalla campagna, separati da una virgola (ad esempio, `product name 'IN' yellow t-shirt`, `red t-shirt, blue t-shirt`)
1. Sotto la `Group by` scheda aggiungi `order's campaign` o `order's utm\_campaign` come `grouping` e fai clic su **[!UICONTROL Add All]** nella scatola
1. Questo rapporto ti mostrerà i ricavi per prodotti specifici per campagne

**2. Per calcolare il ROI, combineremo ancora una volta le metriche in un rapporto:**

1. In qualsiasi dashboard, fai clic su **[!UICONTROL Add Report > Create new report]**
1. Aggiungi il `Revenue by items` , seguendo il filtro e raggruppando per direzioni dal rapporto della campagna per prodotti specifici riportato sopra e fai clic su **[!UICONTROL Hide]** sotto il valore scalare della metrica
1. Aggiungi ora il [!DNL AdWords Cost] , seguendo il filtro e raggruppando per direzioni dalla `Ad cost by campaigns` rapporto esplorato nel `User acquisition campaigns` sezione precedente; quindi fai clic su **[!UICONTROL Hide]** sotto il valore scalare della metrica
1. Con queste metriche attive, verranno aggiunte delle formule:
1. [!UICONTROL ROI]: Immettere la formula `\[A\]/\[B\]`, se `\[A\]` rappresenta `Revenue per campaign for specific product(s)` e `\[B\]` rappresenta `Ad cost by campaigns`. Restituisce il rapporto tra (Ricavi per prodotti specifici) / (Costo campagna)
1. [!UICONTROL Return]: Immettere la formula `\[A\]-\[B\]`. Questo restituirà il margine medio di un utente calcolando (LTV media utente) - (costo medio per acquisizione)
1. (Facoltativo) [!UICONTROL Revenue]: Mostra gli `Revenue by items` per visualizzare i ricavi per prodotti specifici per campagne
1. (Facoltativo) [!UICONTROL Cost]: Mostra gli `AdWords Cost` per visualizzare il costo delle campagne

1. Assegna un nome al report e accertati di salvarlo come tabella

**3. Ripeti i passaggi 1 e 2 per ciascuno dei tuoi prodotti o gruppi di prodotti pubblicizzati.**

## Documentazione correlata

* [Tracciare l’origine di riferimento dell’ordine tramite [!DNL Google Analytics] E-commerce](../importing-data/integrations/google-ecommerce.md)
* [Tracciare l’origine del riferimento utente nel database](../analysis/google-track-user-acq.md)
* [Tieni traccia dei dati di dispositivi utente, browser e sistemi operativi nel database](../analysis/track-usr-dev-browser.md)
* [Scopri le fonti e i canali di acquisizione più importanti](../analysis/most-value-source-channel.md)
* [Collega il tuo [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [Come funziona [!DNL Google Analytics] L’attribuzione UTM funziona?](../analysis/utm-attributes.md)
* [5 best practice per l’assegnazione di tag UTM in [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
