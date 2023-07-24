---
title: Analisi dell'attività del sito Web e dei tassi di conversione dei clienti
description: Scopri come impostare una dashboard per monitorare l’attività del sito web (incluse visualizzazioni di pagina, sessioni e utenti) e il tasso di conversione dei clienti nel tempo.
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
role: Admin, User
feature: Reports, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 0%

---

# Analisi dell&#39;attività del sito Web

[!DNL Adobe Commerce Intelligence] consente di integrare facilmente i dati sui costi pubblicitari con il resto dei dati. Questo non solo ti consente di comprendere l’attività del sito web, ma ti consente anche di derivare la percentuale di visitatori del sito web che diventano un utente registrato o effettuano un acquisto.

Questo argomento illustra come impostare una dashboard che tenga traccia dell’attività sul sito web, incluse visualizzazioni di pagina, sessioni e utenti, e del tasso di conversione dei clienti nel tempo.

## Prerequisiti

**Importa i dati sui costi della pubblicità** - Connetti [!DNL [Google AdWords]](../importing-data/integrations/google-adwords.md) a [!DNL Adobe Commerce Intelligence] - questo sincronizza automaticamente [!DNL AdWords] spese in Commerce Intelligence.

**Tracciare i dati del canale di acquisizione dell&#39;utente** - Per legare [!DNL Google AdWords] dati a ordini specifici nel database, è necessario [tracciare l’acquisizione degli utenti](../analysis/google-track-user-acq.md) tramite [!DNL Google Analytics E-commerce]. Questo consente di collegare ogni ordine con una sorgente UTM e un supporto.

## Campagne di acquisizione utente

Questa raccolta di rapporti viene creata utilizzando quanto segue:

* Metriche generate automaticamente quando connetti il tuo [!DNL Google AdWords] dati
* Metriche di base che dovrebbero essere già disponibili sul tuo account, come `Number of orders` e `New users`
* Dimension creati quando si accede al [!DNL Google Analytics Ecommerce] dati nel database, come origine utm dell&#39;ordine e supporto utm dell&#39;ordine. Contatta il team di supporto se questi campi non sono attualmente disponibili nel tuo account

## Creazione dei rapporti

**Per iniziare, crea un rapporto che mostra il numero di visualizzazioni di pagina, sessioni e utenti nel tempo:**

1. Crea un rapporto.
1. Clic **[!UICONTROL Add Metric]**, quindi passare il puntatore del mouse sulla [!DNL Google Analytics] nella parte inferiore del menu a discesa e seleziona `Page Views`.
1. Aggiungi un’altra metrica, muovendo di nuovo [!DNL Google Analytics] , questa volta selezionando `Sessions`.
1. Aggiungi una terza metrica, muovendo di nuovo sul [!DNL Google Analytics] , questa volta selezionando `Users`.
1. Ora puoi impostare un intervallo di tempo mobile, da 31 giorni fa a 1 giorno fa, e regolare l’intervallo di tempo in base a `by day`.
1. Assegna un nome al report (ad esempio, `Page views, sessions and users by day`) e fai clic su **[!UICONTROL Save]**.

**Il secondo rapporto esamina il numero di visualizzazioni di pagina nell’ultimo anno:**

1. Crea un rapporto.
1. Clic **[!UICONTROL Add Metric]**, passare il puntatore del mouse [!DNL Google Analytics] nella parte inferiore del menu a discesa e seleziona _Visualizzazioni pagina_.
1. Modifica il periodo di tempo in un intervallo mobile, da 13 mesi fa a 1 mese fa, e regola l’intervallo di tempo in base a `by month`.
1. Assegna un nome al report, ad esempio `Page views by month,` e fai clic su **[!UICONTROL Save]**.

**Il terzo grafico esamina il tasso di mancato recapito nell’ultimo anno:**

1. Crea un rapporto.
1. Clic **[!UICONTROL Add Metric]**, passare il puntatore del mouse [!DNL Google Analytics] nella parte inferiore del menu a discesa e seleziona _Percentuale non recapitate_.
1. Modifica il periodo di tempo in un intervallo mobile, da 13 mesi fa a 1 mese fa, e regola l’intervallo di tempo in base a `by month`.
1. Assegna un nome al report, ad esempio `Bounce rate by month`, e fai clic su **[!UICONTROL Save]**.

**Ora, osserva la durata media delle sessioni per i nuovi visitatori rispetto ai visitatori di ritorno:**

1. Crea un rapporto.
1. Clic **UICONTROL Add Metric**, passare il puntatore del mouse [!DNL Google Analytics] nella parte inferiore del menu a discesa e seleziona `Average Session Length`.
1. Modifica il periodo di tempo in un intervallo mobile, da 13 mesi fa a 1 mese fa, e regola l’intervallo di tempo in base a `by month`?
1. Aggiungi un `Group by` e seleziona `New or returning visitor`.  Controlla la `Show All` ; quindi fare clic su **[!UICONTROL Apply]**.
1. Assegna un nome al report, ad esempio `Average session length`, e fai clic su **[!UICONTROL Save]**.

**Quindi, osserva i tuoi domini di riferimento principali negli ultimi 30 giorni:**

1. Crea un rapporto.
1. Clic **[!UICONTROL Add Metric]**, passare il puntatore del mouse [!DNL Google Analytics] nella parte inferiore del menu a discesa e seleziona `Sessions`.
1. Modifica il periodo di tempo in un intervallo mobile, da 31 giorni fa a 1 giorno fa, e regola l’intervallo di tempo in `none`.
1. Aggiungi un `Group by` e seleziona `ga:source`.  Controlla la _Mostra tutto_ ; quindi fare clic su **[!UICONTROL Apply]**.
1. Aggiungi un altro `group by` e seleziona `ga:medium`. Di nuovo, controlla `Show All` ; quindi fare clic su **[!UICONTROL Apply]**.
1. Assegna un nome al report, ad esempio `Top 20 Referring Domains, 30 Days`e fai clic su **[!UICONTROL Save]**.

**Infine, considera la conversione:**

1. Crea un rapporto.
1. Aggiungi le metriche seguenti:

* `New users`
   * Clic **[!UICONTROL Hide]** sotto il nome della metrica

* `Number of orders`
   * Aggiungi un filtro per `Customer's order number` = 1 e fare clic su **[!UICONTROL Apply]**
   * Rinominare la metrica facendo clic sul nome della metrica, chiamandola `Number of first orders`, quindi fai clic su **[!UICONTROL Hide]**

* `Number of orders`
   * **[!UICONTROL Hide]** la metrica

* `Users`
   * **[!UICONTROL Hide]** la metrica
   * Modifica il periodo di tempo in `24 months ago to now`, e regola l&#39;intervallo di tempo su `by month`.
   * Aggiungere le formule seguenti facendo clic su **[!UICONTROL Formula]**.
   * A/D, quindi fai clic su **[!UICONTROL Apply]**
   * Rinomina la formula `Registration conversion`
   * B/D, quindi fare clic su **[!UICONTROL Apply]**
   * Rinomina la formula `First order conversion`
   * C/D, quindi fare clic su **[!UICONTROL Apply]**
   * Rinomina la formula `Any order conversion`

* Ora assegna un nome al rapporto, ad esempio `Conversion by month`e quindi fare clic su **[!UICONTROL Save]**.

## Passaggi successivi

Ora che hai accesso ai dati sul traffico web e ai tassi di conversione, puoi iniziare a estrarre questo per promuovere le decisioni di business, ad esempio quali siti sono più adatti a indirizzare il traffico verso il tuo sito? o Quale delle tue campagne è più efficace nell’acquisire clienti con l’elevato valore del ciclo di vita?

Quando modifichi la spesa pubblicitaria e la strategia di marketing, puoi continuare a tenere traccia dei risultati in [!DNL Commerce Intelligence], iterando su questa dashboard per soddisfare le priorità in evoluzione della tua azienda.
