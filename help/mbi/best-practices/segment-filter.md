---
title: Dimension di dati consigliati per segmentazione e filtro
description: Scopri le best practice per la segmentazione e il filtraggio.
exl-id: 66391bce-bdeb-4e9d-8089-1c796e00d91e
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 0%

---

# Segmentazione e filtro

Una buona segmentazione è ciò che trasforma una statistica superficiale in una metrica di business che guida le decisioni.

Vuoi sapere chi sono i tuoi clienti più importanti? Quali sono i tuoi canali di marketing più importanti? Quali prodotti sono più veloci e perché? Per ottenere una di queste risposte, devi iniziare segmentando i tuoi dati.

Questo argomento tratta i segmenti critici che sono spesso consigliati ai clienti. Inoltre, illustra in dettaglio le domande che questi segmenti possono aiutarti a rispondere. Tecnicamente, i segmenti sono colonne di dati nel database. In entrata [!DNL Adobe Commerce Intelligence], sono denominate dimensioni.

![](../../mbi/assets/mbi-critical-segments.png)


## Segmenti utente

I segmenti utente consentono di comprendere chi sono gli utenti e come si comportano.

* **Età / Anno di nascita**: quanti anni hanno gli utenti? Quanti anni hanno gli utenti più attivi? Di solito è utile inserire i valori negli intervalli per un’analisi più efficace.
* **Genere**: i diversi generi interagiscono in modo diverso con il sito web?
* **Indirizzo**: Da dove provengono gli utenti? Dovresti concentrare le tue attività di marketing su una particolare area geografica? Le campagne pubblicitarie recenti sono state eseguite come previsto nelle aree di destinazione?
* **Origine acquisizione cliente**\: Sapete da quale canale di marketing provengono i vostri utenti? Hanno fatto clic su un annuncio o vi hanno trovato tramite una ricerca? [Segmentazione dei dati per origine di acquisizione dell&#39;utente](../data-analyst/analysis/google-track-user-acq.md) è il primo passo per ottimizzare la nuova acquisizione di clienti. Il secondo passo è spendere più soldi in ciò che funziona e uccidere ciò che non funziona.
* **Dispositivo di registrazione**: gli utenti si sono registrati tramite la tua app mobile o il tuo sito web? iOS o Android™? La base di utenti di dispositivi mobili è abbastanza grande da allocare più risorse per sviluppare il prodotto mobile? Se non tieni ancora traccia di questo, consulta questo argomento [informazioni sul tracciamento del dispositivo utente](../data-analyst/analysis/track-usr-dev-browser.md).
* **Referrer da**: Chi sono i tuoi influencer più influenti? Quanti utenti sono stati segnalati direttamente da altri?
* **Settore**: se sei un’azienda B2B, in quali settori lavorano i tuoi utenti? A quali organizzazioni professionali vale la pena aderire?
* **Risposte al sondaggio**: se esegui indagini sui clienti, utilizza le risposte come segmenti per un livello di profilatura più profondo. Puoi porre domande che integrano ciò che già sai sugli utenti o confermare le tue ipotesi.
* **Importo primo ordine e categoria prodotto**: esiste una correlazione tra il primo ordine di un utente e i modelli di acquisto futuri?

## Segmenti di ordini/eventi

I segmenti di ordini ed eventi consentono di analizzare il comportamento degli utenti e il loro coinvolgimento nel tempo.

* **[!UICONTROL Billing / Shipping Address]**: Da dove proviene la maggior parte degli ordini? C&#39;è una differenza tra gli indirizzi di fatturazione e di spedizione?
* **[!UICONTROL Status]**: quanti ordini non sono stati completati? Qual è il rapporto tra ordini in sospeso negli ultimi sette giorni?
* **[!UICONTROL Customer acquisition source]**: oltre al tracciamento dei dati di acquisizione degli utenti a livello di utente, puoi anche [tracciarlo a livello di ordine o evento](../data-analyst/analysis/google-track-user-acq.md). Un utente che ha effettuato la registrazione tramite un’origine potrebbe continuare ad accedere al sito tramite altre origini.
* **[!UICONTROL Device]**: il numero di ordini da dispositivi mobili è in aumento? Quanti ricavi vengono generati dagli acquisti su dispositivi mobili? (Se non tieni traccia di questo, consulta questo argomento [informazioni sul tracciamento dei dati del dispositivo dell&#39;ordine](../data-analyst/analysis/track-usr-dev-browser.md).
* **[!UICONTROL Fulfillment Center]**: quale dei vostri centri di realizzazione genera il maggior fatturato? Se si analizza la differenza tra l&#39;ora dell&#39;ordine e l&#39;ora di spedizione, quale centro di evasione è più reattivo?
* **[!UICONTROL Delivery Carrier]**: qual è il vettore più popolare? Quale vettore ha il minor numero di articoli restituiti?
* **[!UICONTROL Discount / Coupon Codes]**: Le vostre promozioni stanno generando nuovi profitti? Quanti oggetti in più hanno acquistato i tuoi clienti oltre all&#39;oggetto in vendita? In che modo i coupon influiscono sul valore medio dell’ordine? Qual è il tuo margine medio sugli elementi scontati rispetto a quelli non scontati?
* **[!UICONTROL Satisfaction / Rating]**: Qual è il livello di soddisfazione dei clienti rispetto agli ordini ricevuti? È probabile che i tuoi clienti ti indirizzino la tua attività?

## Segmenti di prodotto

I segmenti di prodotto consentono di prendere decisioni sul merchandising.

* **[!UICONTROL Merchant / Brand]**: una marca specifica vende più velocemente del resto? Quali marchi hanno prestazioni insoddisfacenti?
* **[!UICONTROL Type / Category]**: i diversi segmenti di utenti utilizzano diversi tipi di prodotti? Quali categorie di prodotti generano il business più ripetuto?
* **[!UICONTROL Discount / Coupon Codes]**: le promozioni danneggiano le vendite di prodotti non scontati? In che modo i coupon influiscono sul valore percepito dei prodotti?
* **[!UICONTROL Social Activity]**: C&#39;è una correlazione tra il fermento generato sui social media e la quantità venduta per un prodotto?
* **[!UICONTROL Size / Variant]**: qual è il rapporto di inventario necessario per ogni variante? Quali varianti possono essere vendute a tassi di sconto?

Se sei interessato al merchandising, vedi [come utilizzare i segmenti di prodotto per promuovere il business](../data-analyst/analysis/most-value-source-channel.md).

## Definizione dei profili cliente

Gli esperti di segmentazione potrebbero voler superare le sezioni unidimensionali e iniziare a stabilire profili cliente reali. Ad esempio, le persone di età compresa tra i 13 e i 24 anni che si sono registrate tramite un dispositivo mobile hanno inserito in un gruppo &quot;Giovani e mobili&quot;. Come si comporta questo gruppo rispetto al resto della tua base di utenti?

Questo tipo di analisi è ciò che gli esperti di marketing delle aziende Fortune 1000 fanno tutto il giorno. Prima dell&#39;avvento delle piattaforme di business intelligence basate sul cloud, come [!DNL Commerce Intelligence]Ma era in gran parte fuori dalla portata di tutti noi. Fortunatamente non è più così.

## Tracciamento di nuovi segmenti

Il primo passaggio per segmentare le metriche in base alle dimensioni di cui sopra consiste nell’assicurarsi di tenere traccia di questi dati nel database. Se non viene tracciato, incontra il tuo team tecnico e trova un modo per iniziare a tracciare questi dati.

Dopo aver confermato la registrazione dei dati nel database, [contatta il team di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) per inviare le dimensioni al [!DNL Commerce Intelligence] metriche e grafici. È inoltre possibile utilizzare *Gestione dei campi* strumento per tenere traccia di questi campi in [!DNL Commerce Intelligence].

## Correlato

* [Ottimizzazione del database per l&#39;analisi](../best-practices/opt-db-analysis.md)
