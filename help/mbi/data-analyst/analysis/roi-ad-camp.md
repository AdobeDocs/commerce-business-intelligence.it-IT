---
title: Aumento del ROI nelle campagne pubblicitarie
description: Scopri alcuni metodi diversi per valutare le prestazioni della campagna.
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
role: Admin, User
feature: Data Warehouse Manager, Reports, Campaigns
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1253'
ht-degree: 0%

---

# Campagne Advertising e ROI

[!DNL Adobe Commerce Intelligence] ti consente di [unire facilmente i dati dei costi pubblicitari e dei ricavi](../../data-analyst/importing-data/integrations/google-adwords.md) dal tuo database. Questo consente di identificare quali campagne hanno il maggiore ritorno sull’investimento (ROI). In questo argomento vengono illustrati alcuni metodi diversi per valutare le prestazioni della campagna.

## Prerequisiti

* Importa i dati sui costi pubblicitari:
   * [Connetti  [!DNL Google AdWords] a [!DNL Commerce Intelligence]](../importing-data/integrations/google-adwords.md): questa operazione sincronizza la spesa di [!DNL Adwords] in [!DNL Commerce Intelligence]
   * [Carica altri dati sui costi della pubblicità](../importing-data/connecting-data/import-offline-ad-data.md): consigliato per i canali senza un connettore diretto a [!DNL Commerce Intelligence]
   * Se importi dati sui costi da più origini, puoi [consolidare](../../best-practices/consolidating-your-tables.md) i dati in [!DNL Commerce Intelligence]. È sufficiente [inviare un ticket di supporto](../../guide-overview.md#Submitting-a-Support-Ticket).
* [Tracciare i dati del canale di acquisizione dell&#39;utente](../analysis/google-track-user-acq.md)

## Campagne di acquisizione utente

Le campagne mirate all’acquisizione di utenti possono essere misurate da molti punti di vista, tra cui:

1. Numero di nuovi utenti acquisiti delle campagne
1. Tasso di conversione dalla registrazione all’acquisto di campagne
1. Il ROI delle campagne in base al valore medio del ciclo di vita dell’utente (LTV)

Le analisi (1) e (2) di cui sopra vengono esaminate in un&#39;esercitazione separata su [identificazione dei tuoi canali di marketing principali](../analysis/most-value-source-channel.md). Qui puoi esplorare l’analisi (3) per misurare il ROI delle campagne nel tempo. Questo risponde al quesito se gli utenti acquisiti da una particolare campagna hanno generato ricavi sufficienti per coprire i costi di acquisizione.

>[!NOTE]
>
>Questo esempio presuppone che tutti i costi della campagna siano stati utilizzati esclusivamente per acquisire nuovi utenti. In realtà, il costo della campagna viene condiviso anche con l’acquisizione di visite non convertite, acquirenti ripetuti e così via. Supponendo che tutti i costi vengano utilizzati per acquisire nuovi utenti registrati, il ROI risultante rappresenta lo scenario peggiore (costo per acquisizione più alto). Puoi essere sicuro che il ROI effettivo sia superiore ai calcoli.
>
>Esempio: supponendo di aver speso 20 $ per una campagna che ha generato 10 nuovi utenti e 10 acquirenti ripetuti, il costo effettivo per nuovo utente è di 1 $. Ma, partendo dal presupposto che tutti i costi sono andati ad acquisire nuovi utenti, il costo per acquisizione è di 2 dollari.

**1. Per iniziare, crea un grafico che segmenta il costo annuncio per campagne:**

1. Crea un [!UICONTROL Metric] che somma le tue spese nel tempo
1. Vai a [!UICONTROL Data > Metrics]
1. Selezionare `Add New Metric` e selezionare la tabella [!DNL `Adwords...`] che registra i dati dei costi [!DNL AdWords].
1. Nell&#39;editor delle metriche, assegna un nome alla metrica (ad esempio, [!UICONTROL AdWord Cost])
1. Utilizzando i menu a discesa, eseguire un **Sum** nella colonna `adCost` della tabella [!DNL Adwords...] (Modifica) ordinata in base alla colonna `date`.
   ![Messaggio di successo dopo l&#39;aggiunta di una nuova metrica](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1. Fai clic su `Back to Metric List` in alto e vai a qualsiasi dashboard.

1. Creare un rapporto che segmenta la spesa per campagne
1. In qualsiasi dashboard, fare clic su [!UICONTROL Add Report > Create report]
1. Seleziona la metrica [!UICONTROL Adword Cost] appena creata
1. Imposta [!UICONTROL Time period] su `All-time` e [!UICONTROL Interval] su `None`
1. Nella scheda `Group by`, aggiungere `campaign` come [!UICONTROL grouping field] e fare clic su `Add All` nella casella.
1. Questo report mostra il costo [!DNL AdWords] costante per campagne

**2. Crea un report che conta i nuovi utenti per campagne:**

1. In qualsiasi dashboard, fare clic su **[!UICONTROL Add Report > Create report]**
1. Selezionare la metrica `New users` che conta il numero di nuovi utenti registrati nel tempo
1. Imposta [!UICONTROL Time period] su `All-time` e [!UICONTROL Interval] su `None`
1. Nella scheda `Group by` aggiungere `campaign` come `grouping field` e fare clic su **`Add All`** nella casella
1. Questo rapporto mostra i tuoi utenti registrati sempre per campagne

**3. Crea un report che segmenta l&#39;LTV utente medio per campagne:**

1. In qualsiasi dashboard, fare clic su **[!UICONTROL Add Report > Create report]**
1. Seleziona la metrica `Average lifetime revenue` che calcola i ricavi medi dell&#39;utente nel corso della sua vita
1. Imposta [!UICONTROL Time period] su `All-time` e [!UICONTROL Interval] su `None`
1. Nella scheda `Group by`, aggiungi `campaign` o `utm\_campaign` come [!UICONTROL grouping field] e fai clic su `Add All` nella casella
1. Questo rapporto mostra i ricavi medi del ciclo di vita dell’utente per campagna

**Infine, calcola il ROI della campagna riunendo queste tre analisi in un unico rapporto:**

1. In qualsiasi dashboard, fare clic su **[!UICONTROL Add Report > Create new report]**
1. Aggiungi come input, utilizza le tre metriche utilizzate in precedenza. A ciascuno viene assegnata una lettera (ad esempio,\[`A`\], \[`B`\] e \[`C`\])
1. [!UICONTROL Cost]: aggiungi la metrica Costo AdWords - questa è la variabile \[A\]. In questo modo viene restituito il costo per campagne.
1. [!UICONTROL Users]: aggiungere la metrica Nuovi utenti. Si tratta della variabile \[B\]. Restituisce il numero di utenti per campagne.
1. [!UICONTROL LTV]: aggiungere la metrica Ricavi medi ciclo di vita. Si tratta della variabile \[`C`\]. In questo modo viene restituito LTV per campagne.

1. Fare clic sull&#39;icona Nascondi accanto alla parola Grafico per spostare l&#39;attenzione sulla tabella
1. Ora puoi utilizzare `Add Formula` per combinare queste metriche, nel modo seguente:
1. [!UICONTROL ROI]: immettere la formula `(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])`, se \[`A`\] rappresenta `Ad Cost by Campaigns`, \[`B`\] rappresenta `New users by campaigns` e \[`C`\] `LTV by campaigns`. Questo restituisce il rapporto tra (costo medio per acquisizione dell’LTV utente) / (costo medio per acquisizione)
1. [!UICONTROL Avg Return per User]: immettere la formula **\[`C`\]-(\[`A`\]/\[`B`\])**. In questo modo viene restituito il margine medio realizzato da un utente calcolando (LTV utente medio) - (costo medio per acquisizione).
1. [!UICONTROL CPA]: immettere la formula **`\[A\]/\[B\]`**. Restituisce il costo effettivo della campagna per acquisizione.
1. Altre metriche potenziali da includere dai dati [!DNL AdWords] includono le somme di `Impressions` e `adClicks` (dai dati [!DNL AdWords]), insieme al totale di `number of orders` effettuate tramite una determinata campagna.
1. Può anche essere interessante calcolare il ROI in base a LTV 30 giorni e 90 giorni dopo che un utente si è registrato o ha effettuato un primo acquisto.

1. Puoi fare clic e trascinare le metriche e le formule per riordinare le colonne del rapporto
1. Assegna un nome al rapporto e assicurati di salvarlo come tabella.

## Campagne sui prodotti

Stai eseguendo annunci pubblicitari specifici per il prodotto? In tal caso, puoi misurare il ROI di tali campagne calcolando i ricavi/costi per prodotti specifici.

>[!NOTE]
>
>Questo esempio presuppone che tutti i costi della campagna siano stati utilizzati esclusivamente per generare acquisti di prodotti specifici. Supponendo che tutti i costi siano stati spesi per la generazione di acquisti, il ROI risultante rappresenta lo scenario peggiore (costo più alto per acquisto). Puoi essere sicuro che il ROI effettivo sia superiore a questo calcolo. Esempio: supponendo di aver speso 20 $ per una campagna che ha generato 10 nuovi utenti e 10 acquisti, il costo effettivo per acquisto è di 1 $. Presumendo che tutti i costi siano andati ad acquisire nuovi utenti, il costo per acquisto è di 2 $.

Prima di iniziare, [invia un ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) per unire le dimensioni seguenti alla tabella degli elementi di riga (`sales\_flat\_order\_item, order\_item`):

* Origine dell’ordine (se tieni traccia solo dell’origine di riferimento a livello di utente, quindi unisci all’origine dell’utente)
* Campagna dell’ordine (se tieni traccia solo dell’origine di riferimento a livello di utente, quindi partecipa alla campagna dell’utente)
* Canale dell&#39;ordine (se tieni traccia solo dell&#39;origine di riferimento a livello di utente, poi unisciti al canale dell&#39;utente)

**1. Per iniziare, crea un grafico che restituisce i ricavi per campagna per prodotti specifici:**

1. In qualsiasi dashboard, fare clic su **[!UICONTROL Add Report > Create new report]**
1. Seleziona la metrica `Revenue by items` che calcola i ricavi a livello di elementi riga
1. Imposta [!UICONTROL Time period] su `All-time` e [!UICONTROL Interval] su `None`
1. Nella scheda `Filter by`, aggiungi `product name 'IN'` Prodotto `A`, Prodotto `B`, Prodotto `C`, ...&quot; e includi tutti i nomi di prodotto target della campagna separati da una virgola (ad esempio, `product name 'IN' yellow t-shirt`, `red t-shirt, blue t-shirt`)
1. Nella scheda `Group by`, aggiungi `order's campaign` o `order's utm\_campaign` come campo `grouping` e fai clic su **[!UICONTROL Add All]** nella casella
1. Questo rapporto mostra i ricavi per prodotti specifici per campagne

**2. Per calcolare il ROI, combinare nuovamente le metriche in un unico rapporto:**

1. In qualsiasi dashboard, fare clic su **[!UICONTROL Add Report > Create new report]**
1. Aggiungi la metrica `Revenue by items` seguendo il filtro e raggruppa per istruzioni dal rapporto campagna per prodotti specifici e fai clic su **[!UICONTROL Hide]** sotto il valore scalare della metrica
1. Aggiungere ora la metrica [!DNL AdWords Cost], seguendo il filtro e raggruppando per direzioni dal report `Ad cost by campaigns` esplorato nella sezione `User acquisition campaigns` sopra; quindi fare clic su **[!UICONTROL Hide]** sotto il valore scalare della metrica
1. Dopo aver impostato queste metriche, aggiungi le seguenti formule:
1. [!UICONTROL ROI]: immettere la formula `\[A\]/\[B\]`, se `\[A\]` rappresenta `Revenue per campaign for specific product(s)` e `\[B\]` rappresenta `Ad cost by campaigns`. Restituisce il rapporto tra (Ricavi per prodotti specifici) e (Costo campagna)
1. [!UICONTROL Return]: immettere la formula `\[A\]-\[B\]`. Restituisce il margine medio realizzato da un utente calcolando (LTV utente medio) - (costo medio per acquisizione)
   1. (Facoltativo) [!UICONTROL Revenue]: scopri la metrica `Revenue by items` per visualizzare i ricavi per prodotti specifici per campagna
   1. (Facoltativo) [!UICONTROL Cost]: scopri la metrica `AdWords Cost` per visualizzare il costo delle campagne

1. Assegna un nome al report e assicurati di salvarlo come tabella

**3. Ripeti i passaggi 1 e 2 per ciascuno dei prodotti o gruppi di prodotti annunciati.**

## Documentazione correlata

* [Tracciare l&#39;origine di riferimento dell&#39;ordine tramite  [!DNL Google Analytics] E-Commerce](../importing-data/integrations/google-ecommerce.md)
* [Tracciare l&#39;origine di riferimento dell&#39;utente nel database](../analysis/google-track-user-acq.md)
* [Tenere traccia dei dati relativi a dispositivi utente, browser e sistema operativo nel database](../analysis/track-usr-dev-browser.md)
* [Scopri le fonti e i canali di acquisizione più importanti](../analysis/most-value-source-channel.md)
* [Connetti il tuo account  [!DNL Google Adwords] ](../importing-data/integrations/google-adwords.md)
* [Come funziona l&#39;attribuzione  [!DNL Google Analytics] UTM?](../analysis/utm-attributes.md)
* [Cinque best practice per l&#39;assegnazione di tag UTM in [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
