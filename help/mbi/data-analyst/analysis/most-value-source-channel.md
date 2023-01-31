---
title: Identificazione delle origini e dei canali di marketing più importanti
description: Scopri alcuni rapporti che puoi utilizzare per scoprire i tuoi canali di marketing più importanti.
exl-id: 8d25bc80-ea60-47db-b01b-04a23a24c14d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 0%

---

# Identificare le origini di marketing di successo

Hai fatto ricerche sul pubblico, hai creato la campagna, hai investito in alcuni canali di marketing. Ora che è passato un po&#39; di tempo, come stanno funzionando quei canali? Quale canale ha portato il maggior numero di nuovi utenti? Quale fonte ha contribuito di più al vostro fatturato totale?

Con [!DNL MBI], puoi segmentare facilmente i ricavi e gli utenti per origine di riferimento, indipendentemente dal fatto che corrisponda a [!DNL [Google Analytics' UTM fields]](https://support.google.com/analytics/answer/1191184?hl=en) o campi dati personalizzati. Questa segmentazione ti consentirà di trovare i canali con le prestazioni migliori e di investire meglio il tuo budget di marketing.

In questo articolo, esaminiamo alcuni rapporti che puoi utilizzare per scoprire i tuoi canali di marketing più importanti:

* [Nuovi utenti per origini](#newusersbysource)
* [Ricavi medi per ciclo di vita per origine utente](#avglifetimerev)
* [Valore medio dell&#39;ordine per origine utente](#avgorderval)
* [Entrate per data di registrazione utente e origini](#revbyregdateandsource)
* [Ripeti ordini per origine utente](#repeatordersbysource)

## Prerequisiti {#prereqs}

Per creare le analisi in questo articolo, devi accedere ai dati di origine di acquisizione di marketing o di riferimento. Se non lo stai già tracciando, dovrai portare [ordinare dati di origine del riferimento da [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md) in [!DNL MBI] prima di continuare. Inoltre, l’aggiunta di informazioni sul dispositivo utente alle analisi consente di vedere quale tecnologia vengono utilizzati i riferimenti.

## Nuovi utenti per origine {#newusersbysource}

Valutare le prestazioni delle fonti di riferimento è fondamentale per determinare i canali più preziosi. Questo rapporto mostra il numero di utenti appena registrati, per fonte di acquisizione, nel tempo, consentendo di tenere traccia delle prestazioni delle fonti di riferimento nell’acquisizione di nuovi utenti registrati.

Per creare questo rapporto nel [Report Builder](../../tutorials/using-visual-report-builder.md), aggiungi **Nuovi utenti** metrica (o metrica equivalente che conta il numero di nuovi utenti nel tempo) al rapporto. Quindi procedi come segue:

1. Imposta la [!UICONTROL Time Period] al periodo di registrazione che si desidera analizzare.
1. Imposta la [!UICONTROL Interval] mensile.
1. Imposta [!UICONTROL Group By] per acquisire (o referral) la sorgente e selezionare le sorgenti da includere.
1. Per questo esempio, abbiamo utilizzato il `stacked columns` [!UICONTROL chart type].

Ecco una passeggiata visiva:

![Creazione di un rapporto Nuovi utenti per origine.](../../assets/New_Users_by_source.gif)

## Ricavi medi per ciclo di vita per origine utente {#avglifetimerev}

Trovare i canali che portano nuovi utenti è importante, ma quanto sono preziosi complessivamente questi riferimenti? Questo rapporto mostra il ricavo medio del ciclo di vita degli utenti provenienti da specifiche sorgenti di acquisizione nel tempo. In altre parole, questo ti consente di vedere se gli utenti acquisiti da una particolare fonte spendono con te più di un gruppo di utenti acquisiti da una fonte diversa nel corso della loro vita.

Per creare questo rapporto nel Report Builder, aggiungi il **Ricavi a vita media** al rapporto. Quindi procedi come segue:

1. Imposta la [!UICONTROL Time Period] al periodo di tempo da analizzare.
1. Imposta la [!UICONTROL Interval] mensile.
   [!UICONTROL Group By] per acquisire (o referral) la sorgente e selezionare le sorgenti da includere.
1. Per questo esempio, abbiamo utilizzato il `line chart` digitare.

Ecco una procedura dettagliata visiva:

![Creazione di un ricavo medio a vita per origine utente](../../assets/Lifetime_revenue_by_user_source.gif).

In questo esempio vengono esaminati solo i ricavi del ciclo di vita, ma puoi anche replicare questa analisi per esaminare [!UICONTROL Number of orders] o [!UICONTROL Distinct buyers] per origine di riferimento.

## Valore medio dell&#39;ordine per origine utente {#avgorderval}

Per ottenere una migliore idea di quanto denaro spendono gli utenti di una specifica fonte di acquisizione, puoi creare un rapporto che esamina il loro valore medio dell&#39;ordine. In questo modo potrai verificare se gli utenti acquisiti da una particolare origine spendono più per ordine rispetto agli utenti di un’altra origine.

Per creare questo rapporto nel Report Builder, aggiungi il **Valore medio dell&#39;ordine** e quindi procedi come segue:

1. Imposta la [!UICONTROL Time Period] al periodo di registrazione che si desidera analizzare.
1. Imposta la [!UICONTROL Time Interval] mensile.
1. Imposta [!UICONTROL Group By] per acquisire (o referral) la sorgente e selezionare le sorgenti da includere.
1. Per questo esempio, abbiamo utilizzato il **colonne sovrapposte** tipo di grafico.

Ecco una procedura dettagliata visiva:

![Creazione di un valore dell&#39;ordine medio per report origine utente.](../../assets/Average_order_value_by_source.gif)

## Entrate totali per data di registrazione utente e origine {#revbyregdateandsource}

L’analisi dei ricavi per tutta la durata di vita di cui ci siamo occupati prima ti consente di esaminare i ricavi medi per tutta la vita degli utenti acquisiti da diverse fonti, ma cosa dire dei ricavi per tutta la vita? Questo rapporto ti consente di identificare il volume complessivo dei ricavi generati dagli utenti registrati in un momento specifico e da un’origine specifica.

Per creare questo rapporto nel Report Builder, aggiungi il `Revenue by user registration date` metrica. Se non [creato questa metrica](../../data-user/reports/ess-manage-data-metrics.md) puoi già eseguire questa operazione replicando il `Revenue` e modifica della metrica `time stamp` a `creation date`. Dopo aver aggiunto la metrica, procedi come segue:

1. Imposta la [!UICONTROL Time Period] al periodo di registrazione che si desidera analizzare.
1. Imposta la [!UICONTROL Time Interval] mensile.
1. Imposta [!UICONTROL Group By] per acquisire (o referral) la sorgente e selezionare le sorgenti da includere.
1. Per questo esempio, abbiamo utilizzato il `stacked columns` tipo di grafico.

Ecco una procedura dettagliata visiva:

![Creazione di un totale di ricavi per data di registrazione utente e rapporto origine.](../../assets/Revenue_by_user_registration_date_and_source.gif)

## Ripeti ordini per origine utente {#repeatordersbysource}

Il rapporto Valore ordine medio mostra in media la spesa degli utenti acquisiti da una particolare origine durante l&#39;esecuzione di un ordine. Questo rapporto, tuttavia, non mostra se gli stessi utenti sono clienti ripetuti. Ma con gli ordini di ripetizione per le origini degli utenti, puoi vedere se gli utenti di una particolare origine effettuano acquisti ripetuti più o meno.

Per creare questo rapporto nel [Report Builder](../../tutorials/using-visual-report-builder.md), aggiungi **Numero di ordini** e quindi procedi come segue:

1. Imposta la [!UICONTROL Time Period] al periodo di registrazione che si desidera analizzare.
1. Imposta la [!UICONTROL Time Interval] mensile.
1. Aggiungi un [!UICONTROL filter] in modo che siano inclusi solo gli utenti con ordini di ripetizione:

   Numero ordine dell&#39;utente maggiore di 1

1. Imposta [!UICONTROL Group By] per acquisire (o referral) la sorgente e selezionare le sorgenti da includere.
1. Per questo esempio, abbiamo utilizzato il `stacked columns` tipo di grafico.

Ecco una procedura dettagliata visiva:

![Creazione di un report di ripetizione ordini per origine utente.](../../assets/Repeat_orders_by_user_source.gif)


## Ritorno a capo {#wrapup}

In questo articolo, abbiamo trattato solo alcune analisi che puoi utilizzare per analizzare il valore dei tuoi canali di acquisizione e marketing, ma questa è solo la punta dell&#39;iceberg. Se avete creato un&#39;analisi potente che non abbiamo trattato qui, fateci capire cosa state facendo nei commenti.

## Correlati {#related}

* [Tracciamento dell’origine di riferimento dell’ordine tramite [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md)
* [Collegamento del [!DNL Google Adwords] account](../importing-data/integrations/google-adwords.md)
* [Costruzione [!DNL Google ECommerce] dimensioni con ordini e dati cliente](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [Best practice per l’assegnazione di tag UTM in [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
