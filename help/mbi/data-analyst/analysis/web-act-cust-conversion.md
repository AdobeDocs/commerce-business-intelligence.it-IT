---
title: Analisi dell’attività del sito web e dei tassi di conversione dei clienti
description: Scopri come impostare un dashboard per monitorare l’attività del sito web, incluse le visualizzazioni di pagina, le sessioni e gli utenti, nonché il tasso di conversione del cliente nel tempo.
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---

# Analisi dell’attività del sito web

[!DNL MBI] consente di integrare facilmente i dati sui costi pubblicitari con il resto dei dati. Questo consente non solo di comprendere l’attività del sito web, ma anche di derivare la percentuale di visitatori del sito web che diventano utenti registrati o effettuano un acquisto.

In questo articolo, mostriamo come impostare un dashboard per monitorare l’attività del sito web, incluse le visualizzazioni di pagina, le sessioni e gli utenti, nonché il tasso di conversione del cliente nel tempo.

## Prerequisiti

**Importare i dati dei costi pubblicitari** - Connetti [!DNL [Google AdWords]](../importing-data/integrations/google-adwords.md) a [!DNL MBI] - sincronizzerà automaticamente il tuo [!DNL AdWords] spesa in BI.

**Tracciare i dati del canale di acquisizione utente** - Per collegare il tuo [!DNL Google AdWords] dati a specifici ordini nel database, [tracciare l&#39;acquisizione degli utenti](../analysis/google-track-user-acq.md) tramite [!DNL Google Analytics E-commerce], che ci consente di collegare ogni ordine con una sorgente utm e un supporto.

## Campagne di acquisizione utente

Questa raccolta di rapporti viene creata utilizzando quanto segue:

* Metriche generate automaticamente al momento della connessione [!DNL Google AdWords] dati
* Metriche di base già disponibili sul tuo account, come `Number of orders` e `New users`
* Dimension creati al momento dell&#39;unione [!DNL Google Analytics Ecommerce] dati al database, come origine utm dell&#39;ordine e supporto utm dell&#39;ordine. Contatta il nostro team di supporto se questi campi non sono attualmente disponibili nel tuo account

## Creazione dei report

**Inizia creando un rapporto che mostra il numero di visualizzazioni di pagina, sessioni e utenti nel tempo:**

1. Crea un nuovo rapporto.
1. Fai clic su **[!UICONTROL Add Metric]**, quindi passate il puntatore del mouse [!DNL Google Analytics] nella parte inferiore del menu a discesa e seleziona `Page Views`.
1. Aggiungi un’altra metrica, muovendo di nuovo sopra il [!DNL Google Analytics] questa volta, seleziona `Sessions`.
1. Aggiungi una terza metrica, nuovamente posizionata sopra il [!DNL Google Analytics] questa volta, seleziona `Users`.
1. Ora cambia il tuo periodo di tempo in un intervallo mobile, da 31 giorni fa a 1 giorno fa, e regola l&#39;intervallo di tempo a `by day`.
1. Assegna un nome al report (ad esempio, `Page views, sessions and users by day`) e fai clic su **[!UICONTROL Save]**.

**Il nostro secondo rapporto esamina il numero di visualizzazioni di pagina nell’ultimo anno:**

1. Crea un nuovo rapporto.
1. Fai clic su **[!UICONTROL Add Metric]**, passa il mouse [!DNL Google Analytics] nella parte inferiore del menu a discesa e seleziona _Visualizzazioni pagina_.
1. Cambia il tuo periodo di tempo in un intervallo mobile, da 13 mesi fa a 1 mese fa, e regola l&#39;intervallo di tempo a `by month`.
1. Assegna un nome al tuo report, come `Page views by month,` e fai clic su **[!UICONTROL Save]**.

**Il terzo grafico esamina il tasso di mancato recapito nell’ultimo anno:**

1. Crea un nuovo rapporto.
1. Fai clic su **[!UICONTROL Add Metric]**, passa il mouse [!DNL Google Analytics] nella parte inferiore del menu a discesa e seleziona _Frequenza di rimbalzo_.
1. Cambia il tuo periodo di tempo in un intervallo mobile, da 13 mesi fa a 1 mese fa, e regola l&#39;intervallo di tempo a `by month`.
1. Assegna un nome al tuo report, come `Bounce rate by month`e fai clic su **[!UICONTROL Save]**.

**Ora, osserva la lunghezza media della sessione dei nuovi visitatori rispetto ai visitatori di ritorno:**

1. Crea un nuovo rapporto.
1. Fai clic su **UICONTROL Aggiungi metrica**, passa il mouse [!DNL Google Analytics] nella parte inferiore del menu a discesa e seleziona `Average Session Length`.
1. Cambia il tuo periodo di tempo in un intervallo mobile, da 13 mesi fa a 1 mese fa, e regola l&#39;intervallo di tempo a `by month`?
1. Aggiungi un `Group by` e seleziona `New or returning visitor`.  Controlla la `Show All` box; quindi fai clic su **[!UICONTROL Apply]**.
1. Assegna un nome al tuo report, come `Average session length`e fai clic su **[!UICONTROL Save]**.

**Successivamente, dai un&#39;occhiata ai tuoi principali domini di riferimento negli ultimi 30 giorni:**

1. Crea un nuovo rapporto.
1. Fai clic su **[!UICONTROL Add Metric]**, passa il mouse [!DNL Google Analytics] nella parte inferiore del menu a discesa e seleziona `Sessions`.
1. Cambia il tuo periodo di tempo in un intervallo mobile, da 31 giorni fa a 1 giorno fa, e regola l&#39;intervallo di tempo a `none`.
1. Aggiungi un `Group by` e seleziona `ga:source`.  Controlla la _Mostra tutto_ box; quindi fai clic su **[!UICONTROL Apply]**.
1. Aggiungi un altro `group by` e seleziona `ga:medium`. Di nuovo, controlla la `Show All` box; quindi fai clic su **[!UICONTROL Apply]**.
1. Assegna un nome al tuo report, come `Top 20 Referring Domains, 30 Days`e fai clic su **[!UICONTROL Save]**.

**Infine, dai un&#39;occhiata alla conversione:**

1. Crea un nuovo rapporto.
1. Aggiungi le metriche seguenti:

* `New users`
   * Fai clic su **[!UICONTROL Hide]** sotto il nome della metrica

* `Number of orders`
   * Aggiungi un filtro per `Customer's order number` = 1 e fai clic su **[!UICONTROL Apply]**
   * Rinomina la metrica facendo clic sul nome della metrica, chiamandola `Number of first orders`,quindi fai clic su **[!UICONTROL Hide]**

* `Number of orders`
   * **[!UICONTROL Hide]** la metrica

* `Users`
   * **[!UICONTROL Hide]** la metrica
   * Modifica il periodo di tempo in `24 months ago to now`e regola l&#39;intervallo di tempo in `by month`.
   * Aggiungi le formule seguenti facendo clic su **[!UICONTROL Formula]**.
   * A/D, quindi fai clic su **[!UICONTROL Apply]**
   * Rinomina la formula `Registration conversion`
   * B/D, quindi fai clic su **[!UICONTROL Apply]**
   * Rinomina la formula `First order conversion`
   * C/D, quindi fai clic su **[!UICONTROL Apply]**
   * Rinomina la formula `Any order conversion`

* Ora dai un nome al tuo rapporto, come `Conversion by month`, quindi fai clic su **[!UICONTROL Save]**.

## Passaggi successivi

Ora che hai accesso ai dati sul tuo traffico web e sui tassi di conversione, puoi iniziare a estrarre questo per guidare le decisioni aziendali. Quali sono i siti migliori per indirizzare il traffico verso il sito?  Quale delle tue campagne è più efficace nell&#39;acquisire clienti con un lifetime value elevato?

Man mano che modifichi la spesa pubblicitaria e la strategia di marketing, puoi continuare a tenere traccia dei risultati in [!DNL MBI], iterazione su questo dashboard per soddisfare le priorità in evoluzione della tua azienda.
