---
title: Dimension di dati consigliati per segmentazione e filtraggio
description: Scopri le best practice per segmentazione e filtro.
exl-id: 66391bce-bdeb-4e9d-8089-1c796e00d91e
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%

---

# Segmentazione e filtraggio

Una buona segmentazione è ciò che trasforma una statistica superficiale in una metrica aziendale che guida le decisioni.

Vuoi sapere chi sono i tuoi clienti più importanti? Quali sono i tuoi canali di marketing più importanti? Quale dei vostri prodotti si muove più velocemente e perché? Per arrivare a una qualsiasi di queste risposte, devi iniziare segmentando i tuoi dati.

In questo articolo, condividiamo alcuni segmenti critici che spesso consigliamo ai nostri clienti. Inoltre, approfondiamo le domande a cui questi segmenti possono aiutarti a rispondere. Tecnicamente, i segmenti sono colonne di dati nel database. In [!DNL MBI], le chiamiamo dimensioni.

![](../../mbi/assets/mbi-critical-segments.png)


## Segmenti utente

I segmenti di utenti consentono di comprendere chi sono i tuoi utenti e come si comportano.

* **Età / Anno di nascita**: Quanti anni hanno i tuoi utenti? Quanti anni hanno gli utenti più attivi? In genere ha senso raggruppare i valori in intervalli per eseguire analisi più efficaci.
* **Genere**: Gli uomini e le donne interagiscono con il tuo sito web in modo diverso?
* **Indirizzo**: Da dove vengono i tuoi utenti? Devi concentrare le tue attività di marketing su una determinata regione? Le campagne pubblicitarie recenti sono state eseguite come previsto nelle aree di destinazione?
* **Origine acquisizione cliente**\: Sai da quale canale di marketing provengono i tuoi utenti? Hanno cliccato su un annuncio o vi hanno trovato tramite ricerca? [Segmentazione dei dati per origine di acquisizione utente](../data-analyst/analysis/google-track-user-acq.md) è il primo passo per ottimizzare la nuova acquisizione da parte del cliente. Il secondo passo è spendere più soldi in ciò che funziona e uccidere ciò che non è.
* **Dispositivo di registrazione**: Gli utenti si sono registrati tramite la tua app mobile o il tuo sito web? iOS o Android? La base di utenti per dispositivi mobili è abbastanza grande da allocare più risorse per sviluppare il prodotto mobile? (Se non stai ancora tenendo traccia di questo argomento, consulta questo argomento [informazioni sul dispositivo utente di tracciamento](../data-analyst/analysis/track-usr-dev-browser.md).
* **A cui fa riferimento**: Chi sono i vostri più influenti? Quanti utenti sono stati indirizzati direttamente da altri?
* **Industria**: Se sei un&#39;azienda B2B, in quali settori lavorano i tuoi utenti? Quali organizzazioni commerciali vale la pena di aderire?
* **Risposte al sondaggio**: Se esegui sondaggi sui clienti, utilizza le risposte come segmenti per un livello di profilazione più profondo. Puoi porre domande complementari a quanto già sai sugli utenti o confermare le tue ipotesi.
* **Importo del primo ordine e categoria di prodotti**: Esiste una correlazione tra il primo ordine di un utente e i futuri modelli di acquisto?

## Segmenti Ordini / Eventi

I segmenti di ordine ed evento consentono di analizzare il comportamento e il coinvolgimento degli utenti nel tempo.

* **[!UICONTROL Billing / Shipping Address]**: Da dove vengono la maggior parte dei vostri ordini? C&#39;è una differenza tra gli indirizzi di fatturazione e di spedizione?
* **[!UICONTROL Status]**: Quanti dei tuoi ordini non sono stati completati? Qual è il rapporto tra gli ordini in sospeso negli ultimi sette giorni?
* **[!UICONTROL Customer acquisition source]**: Oltre a monitorare i dati di acquisizione degli utenti a livello di utente, puoi anche [tracciarlo a livello di ordine o evento](../data-analyst/analysis/google-track-user-acq.md). Un utente che si è registrato tramite una fonte potrebbe benissimo continuare ad accedere al tuo sito tramite altre fonti.
* **[!UICONTROL Device]**: Il numero di ordini di telefonia mobile sta aumentando? Quanti dei vostri ricavi vengono attualmente generati tramite acquisti mobili? (Se non stai ancora tenendo traccia di questo argomento, consulta questo argomento [informazioni sui dati dei dispositivi dell’ordine di tracciamento](../data-analyst/analysis/track-usr-dev-browser.md).
* **[!UICONTROL Fulfillment Center]**: Quale dei centri di realizzazione genera il maggior fatturato? Se stai analizzando la differenza tra il tempo di ordine e il tempo di spedizione, quale centro di evasione è più reattivo?
* **[!UICONTROL Delivery Carrier]**: Qual è il vettore più popolare? Quale vettore ha il minor numero di articoli restituiti?
* **[!UICONTROL Discount / Coupon Codes]**: Le tue promozioni generano davvero un&#39;attività extra? Quanti articoli extra hanno acquistato i tuoi clienti oltre all&#39;articolo in vendita? In che modo i coupon influiscono sul valore medio dell&#39;ordine? Qual è il margine medio sugli articoli scontati rispetto a quelli non scontati?
* **[!UICONTROL Satisfaction / Rating]**: Quanto sono soddisfatti i vostri clienti con i loro ordini? È probabile che i clienti ti contengano?

## Segmenti di prodotto

I segmenti di prodotto ti aiutano a prendere decisioni sul merchandising.

* **[!UICONTROL Merchant / Brand]**: Un marchio specifico vende più velocemente del resto? Quali marchi hanno prestazioni inferiori?
* **[!UICONTROL Type / Category]**: I diversi segmenti di utenti godono di diversi tipi di prodotti? Quali categorie di prodotti generano il business più ripetuto?
* **[!UICONTROL Discount / Coupon Codes]**: Le promozioni danneggiano le vendite di prodotti non scontati? In che modo i coupon influiscono sul valore percepito dei tuoi prodotti?
* **[!UICONTROL Social Activity]**: Esiste una correlazione tra il ronzio generato sui social media e la quantità venduta per un prodotto?
* **[!UICONTROL Size / Variant]**: Qual è il rapporto di inventario necessario per ogni variante? Quali varianti possono essere vendute ai tassi di sconto?

Se sei interessato al merchandising, controlla un post di blog dove esploriamo [come utilizzare i segmenti di prodotto per promuovere la ripetizione dell&#39;attività](../data-analyst/analysis/most-value-source-channel.md).

## Stabilire profili cliente

Gli esperti di segmentazione possono voler andare oltre le sezioni unidimensionali e iniziare a stabilire profili reali dei clienti. Ad esempio, le persone di età compresa tra i 13 e i 24 anni registrate tramite un dispositivo mobile inseriscono un gruppo &quot;Young &amp; Mobile&quot;. Come si confronta il comportamento di questo gruppo con il resto della base utenti?

Questo tipo di analisi è ciò che fanno gli esperti di marketing delle aziende Fortune 1000 tutto il giorno. Prima dell&#39;avvento di piattaforme di business intelligence basate su cloud come [!DNL MBI]Era in gran parte fuori portata per tutti noi. Fortunatamente non è più così.

## Tracciamento dei nuovi segmenti

Il primo passo per segmentare le metriche in base alle dimensioni di cui sopra è assicurarti di tenere traccia di questi dati nel database. Se non viene tracciato, incontra il tuo team tecnico e trova un modo per iniziare a tracciare questi dati.

Una volta confermato che i dati sono tracciati nel database, [contatta il nostro team di supporto](../guide-overview.md) per spingere le dimensioni al [!DNL MBI] metriche e grafici o semplicemente utilizza il nostro strumento di gestione dei campi per tenere traccia di questi campi in [!DNL MBI].

## Correlati

* [Ottimizzazione del database per l’analisi](../best-practices/opt-db-analysis.md)
