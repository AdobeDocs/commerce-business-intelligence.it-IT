---
title: Analisi dell'attività del sito Web e dei tassi di conversione dei clienti
description: Scopri come impostare una dashboard per monitorare l’attività del sito web (incluse visualizzazioni di pagina, sessioni e utenti) e il tasso di conversione dei clienti nel tempo.
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
role: Admin, User
feature: Reports, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---

# Analisi dell&#39;attività del sito Web

[!DNL Adobe Commerce Intelligence] consente di integrare facilmente i dati relativi ai costi pubblicitari con il resto dei dati. Questo non solo ti consente di comprendere l’attività del sito web, ma ti consente anche di derivare la percentuale di visitatori del sito web che diventano un utente registrato o effettuano un acquisto.

Questo argomento illustra come impostare una dashboard che tenga traccia dell’attività sul sito web, incluse visualizzazioni di pagina, sessioni e utenti, e del tasso di conversione dei clienti nel tempo.

## Prerequisiti

**Importa i dati relativi ai costi pubblicitari** - Connetti [[!DNL [Google AdWords]]](../importing-data/integrations/google-adwords.md) a [!DNL Adobe Commerce Intelligence] - in questo modo sincronizzerai automaticamente la spesa [!DNL AdWords] in Commerce Intelligence.

**Tracciare i dati del canale di acquisizione dell&#39;utente** - Per collegare i dati di [!DNL Google AdWords] a ordini specifici nel database, è necessario [tracciare l&#39;acquisizione dell&#39;utente](../analysis/google-track-user-acq.md) tramite [!DNL Google Analytics E-commerce]. Questo consente di collegare ogni ordine con una sorgente UTM e un supporto.

## Campagne di acquisizione utente

Questa raccolta di rapporti viene creata utilizzando quanto segue:

* Metriche generate automaticamente alla connessione dei dati di [!DNL Google AdWords]
* Metriche di base che dovrebbero essere già disponibili sul tuo account, come `Number of orders` e `New users`
* Le dimensioni create quando si uniscono i dati [!DNL Google Analytics Ecommerce] al database, come l&#39;origine utm dell&#39;ordine e il supporto utm dell&#39;ordine. Contatta il team di supporto se questi campi non sono attualmente disponibili nel tuo account

## Creazione dei rapporti

**Per iniziare, crea un report che mostra il numero di visualizzazioni di pagina, sessioni e utenti nel tempo:**

1. Crea un rapporto.
1. Fai clic su **[!UICONTROL Add Metric]**, quindi passa il mouse sulla sezione [!DNL Google Analytics] nella parte inferiore del menu a discesa e seleziona `Page Views`.
1. Aggiungi un&#39;altra metrica, passando di nuovo sopra la sezione [!DNL Google Analytics], selezionando questa volta `Sessions`.
1. Aggiungi una terza metrica, spostando nuovamente la sezione [!DNL Google Analytics], selezionando questa volta `Users`.
1. Modificare il periodo di tempo in un intervallo mobile, da 31 giorni fa a 1 giorno fa, e regolare l&#39;intervallo di tempo in `by day`.
1. Assegna un nome al report (ad esempio, `Page views, sessions and users by day`) e fai clic su **[!UICONTROL Save]**.

**Il secondo rapporto esamina il numero di visualizzazioni di pagina nell&#39;ultimo anno:**

1. Crea un rapporto.
1. Fare clic su **[!UICONTROL Add Metric]**, passare il mouse sulla sezione [!DNL Google Analytics] nella parte inferiore del menu a discesa e selezionare _Visualizzazioni pagina_.
1. Modificare il periodo di tempo in un intervallo mobile, da 13 mesi fa a 1 mese fa, e regolare l&#39;intervallo di tempo in `by month`.
1. Assegna un nome al report, ad esempio `Page views by month,` e fai clic su **[!UICONTROL Save]**.

**Il terzo grafico esamina il tasso di mancato recapito nell&#39;ultimo anno:**

1. Crea un rapporto.
1. Fare clic su **[!UICONTROL Add Metric]**, passare il mouse sulla sezione [!DNL Google Analytics] nella parte inferiore del menu a discesa e selezionare _Percentuale di mancato recapito_.
1. Modificare il periodo di tempo in un intervallo mobile, da 13 mesi fa a 1 mese fa, e regolare l&#39;intervallo di tempo in `by month`.
1. Assegna un nome al report, ad esempio `Bounce rate by month`, e fai clic su **[!UICONTROL Save]**.

**Osserva ora la durata media della sessione dei nuovi visitatori rispetto ai visitatori di ritorno:**

1. Crea un rapporto.
1. Fai clic su **UICONTROL Aggiungi metrica**, passa il mouse sulla sezione [!DNL Google Analytics] nella parte inferiore del menu a discesa e seleziona `Average Session Length`.
1. Modificare il periodo di tempo in un intervallo mobile, da 13 mesi fa a 1 mese fa, e regolare l&#39;intervallo di tempo in `by month`?
1. Aggiungi un `Group by` e seleziona `New or returning visitor`.  Selezionare la casella `Show All`, quindi fare clic su **[!UICONTROL Apply]**.
1. Assegna un nome al report, ad esempio `Average session length`, e fai clic su **[!UICONTROL Save]**.

**Controlla i tuoi domini di riferimento principali negli ultimi 30 giorni:**

1. Crea un rapporto.
1. Fare clic su **[!UICONTROL Add Metric]**, passare il mouse sulla sezione [!DNL Google Analytics] nella parte inferiore del menu a discesa e selezionare `Sessions`.
1. Modificare il periodo di tempo in un intervallo mobile, da 31 giorni fa a 1 giorno fa, e regolare l&#39;intervallo di tempo in `none`.
1. Aggiungi un `Group by` e seleziona `ga:source`.  Selezionare la casella _Mostra tutto_, quindi fare clic su **[!UICONTROL Apply]**.
1. Aggiungi un altro `group by` e seleziona `ga:medium`. Selezionare nuovamente la casella `Show All`, quindi fare clic su **[!UICONTROL Apply]**.
1. Assegna un nome al report, ad esempio `Top 20 Referring Domains, 30 Days`, e fai clic su **[!UICONTROL Save]**.

**Esaminare infine la conversione:**

1. Crea un rapporto.
1. Aggiungi le metriche seguenti:

* `New users`
   * Fai clic su **[!UICONTROL Hide]** sotto il nome della metrica

* `Number of orders`
   * Aggiungi un filtro per `Customer's order number` = 1 e fai clic su **[!UICONTROL Apply]**
   * Rinominare la metrica facendo clic sul nome della metrica, chiamandola `Number of first orders`, quindi fare clic su **[!UICONTROL Hide]**

* `Number of orders`
   * **[!UICONTROL Hide]** la metrica

* `Users`
   * **[!UICONTROL Hide]** la metrica
   * Modificare il periodo di tempo in `24 months ago to now` e regolare l&#39;intervallo di tempo in `by month`.
   * Aggiungere le formule seguenti facendo clic su **[!UICONTROL Formula]**.
   * A/D quindi fare clic su **[!UICONTROL Apply]**
   * Rinomina la formula `Registration conversion`
   * B/D quindi fare clic su **[!UICONTROL Apply]**
   * Rinomina la formula `First order conversion`
   * C/D quindi fare clic su **[!UICONTROL Apply]**
   * Rinomina la formula `Any order conversion`

* Assegnare un nome al report, ad esempio `Conversion by month`, quindi fare clic su **[!UICONTROL Save]**.

## Passaggi successivi

Ora che hai accesso ai dati sul traffico web e ai tassi di conversione, puoi iniziare a estrarre questo per promuovere le decisioni di business, ad esempio quali siti sono più adatti a indirizzare il traffico verso il tuo sito? o Quale delle tue campagne è più efficace nell’acquisire clienti con l’elevato valore del ciclo di vita?

Durante la regolazione della spesa pubblicitaria e della strategia di marketing, è possibile continuare a tenere traccia dei risultati in [!DNL Commerce Intelligence], iterando in questa dashboard per soddisfare le priorità in evoluzione della propria azienda.
