---
title: Identificazione delle fonti e dei canali di marketing più importanti
description: Scopri alcuni rapporti che puoi utilizzare per scoprire i canali di marketing più importanti.
exl-id: 8d25bc80-ea60-47db-b01b-04a23a24c14d
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 0%

---

# Identificare le origini di marketing corrette

Hai ricercato il tuo pubblico, creato la tua campagna, investito in alcuni canali di marketing. Ora che è passato un po&#39; di tempo, come stanno andando quei canali? Quale canale ha attirato il maggior numero di nuovi utenti? Qual è la fonte che ha contribuito maggiormente al fatturato totale?

Con [!DNL Adobe Commerce Intelligence], puoi segmentare facilmente i ricavi e gli utenti per origine di riferimento, che corrisponda a [[!DNL [Google Analytics' UTM fields]]](https://support.google.com/analytics/answer/1191184?hl=en) o a campi dati personalizzati. Questa segmentazione ti consente di trovare i canali con le prestazioni migliori e di investire meglio nel budget di marketing.

Questo argomento esplora alcuni rapporti che puoi utilizzare per scoprire i tuoi canali di marketing più importanti:

* [Nuovi utenti per origini](#newusersbysource)
* [Ricavi medi nel ciclo di vita per origine utente](#avglifetimerev)
* [Valore medio ordine per origine utente](#avgorderval)
* [Ricavi per data di registrazione utente e origini](#revbyregdateandsource)
* [Ripeti ordini per origine utente](#repeatordersbysource)

## Prerequisiti {#prereqs}

Per generare le analisi in questo argomento, devi accedere ai dati di origine di acquisizione marketing/riferimento. Se non lo stai già tracciando, devi inserire [dati origine riferimento ordine da [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md) in [!DNL Adobe Commerce Intelligence] prima di poter continuare. Inoltre, l’aggiunta di informazioni sul dispositivo utente alle analisi ti consente di vedere quale tecnologia vengono utilizzati i tuoi riferimenti.

## Nuovi utenti per origine {#newusersbysource}

La valutazione delle prestazioni delle origini di riferimento è fondamentale per determinare i canali più importanti. Questo rapporto mostra il numero di utenti appena registrati, per origine di acquisizione, nel tempo, consentendo in tal modo di tenere traccia delle prestazioni delle origini di riferimento nell’acquisizione di nuovi utenti registrati.

Per creare il report nel [Report Builder](../../tutorials/using-visual-report-builder.md), aggiungere al report la metrica **Nuovi utenti** (o una metrica equivalente che conta il numero di nuovi utenti nel tempo). Quindi, effettua le seguenti operazioni:

1. Impostare [!UICONTROL Time Period] sul periodo di registrazione che si desidera analizzare.
1. Imposta [!UICONTROL Interval] su mensile.
1. Impostare [!UICONTROL Group By] sull&#39;origine di acquisizione (o riferimento) e selezionare le origini che si desidera includere.
1. Questo esempio utilizza `stacked columns` [!UICONTROL chart type].

Di seguito è riportata una procedura dettagliata:

![Creazione di un nuovo utente per report di origine.](../../assets/New_Users_by_source.gif)

## Ricavi medi nel ciclo di vita per origine utente {#avglifetimerev}

Individuare i canali che portano nuovi utenti è importante, ma quanto sono importanti in generale queste referenze? Questo rapporto mostra i ricavi medi nel corso della vita degli utenti da fonti di acquisizione specifiche nel tempo. In altre parole, questo consente di vedere se gli utenti acquisiti da una particolare origine spendono di più con te nel corso della loro vita rispetto a un gruppo di utenti acquisiti da un’origine diversa.

Per creare questo report nel Report Builder, aggiungi al report la metrica **Ricavi medi vita**. Quindi, effettua le seguenti operazioni:

1. Impostare [!UICONTROL Time Period] sul periodo di tempo da analizzare.
1. Imposta [!UICONTROL Interval] su mensile.
   [!UICONTROL Group By] all&#39;origine di acquisizione (o riferimento) e selezionare le origini che si desidera includere.
1. Questo esempio utilizza il tipo `line chart`.

Di seguito è riportata una procedura dettagliata:

![Creazione di un ricavo medio per la durata di vita per origine utente](../../assets/Lifetime_revenue_by_user_source.gif).

In questo esempio vengono esaminati solo i ricavi relativi al ciclo di vita, ma è anche possibile replicare l&#39;analisi per esaminare [!UICONTROL Number of orders] o [!UICONTROL Distinct buyers] per origine di riferimento.

## Valore medio ordine per origine utente {#avgorderval}

Per avere un’idea migliore di quanto denaro spendono gli utenti da una specifica origine di acquisizione, puoi creare un rapporto che considera il loro valore medio dell’ordine. Questo consente di monitorare se gli utenti acquisiti da una particolare origine spendono di più per ordine rispetto agli utenti di un’altra origine.

Per creare questo report nel Report Builder, aggiungere la metrica **Valore medio ordine**, quindi eseguire le operazioni seguenti:

1. Impostare [!UICONTROL Time Period] sul periodo di registrazione che si desidera analizzare.
1. Imposta [!UICONTROL Time Interval] su mensile.
1. Impostare [!UICONTROL Group By] sull&#39;origine di acquisizione (o riferimento) e selezionare le origini che si desidera includere.
1. In questo esempio viene utilizzato il tipo di grafico **colonne in pila**.

Di seguito è riportata una procedura dettagliata:

![Creazione di un valore ordine medio per report di origine utente.](../../assets/Average_order_value_by_source.gif)

## Ricavi totali per data e origine di registrazione utente {#revbyregdateandsource}

L’analisi dei ricavi nel ciclo di vita che è stata trattata in precedenza consente di esaminare i ricavi medi nel ciclo di vita degli utenti acquisiti da origini diverse. Ma cosa succede per i ricavi totali nel ciclo di vita? Questo rapporto ti consente di identificare la quantità complessiva di ricavi generati dagli utenti registrati durante un periodo di tempo specifico e da un’origine specifica.

Per creare questo report nel Report Builder, aggiungere la metrica `Revenue by user registration date`. Se non hai già [creato questa metrica](../../data-user/reports/ess-manage-data-metrics.md), puoi replicare la metrica `Revenue` e modificare `time stamp` in `creation date` dell&#39;utente. Dopo aver aggiunto la metrica, effettua le seguenti operazioni:

1. Impostare [!UICONTROL Time Period] sul periodo di registrazione che si desidera analizzare.
1. Imposta [!UICONTROL Time Interval] su mensile.
1. Impostare [!UICONTROL Group By] sull&#39;origine di acquisizione (o riferimento) e selezionare le origini che si desidera includere.
1. Questo esempio utilizza il tipo di grafico `stacked columns`.

Di seguito è riportata una procedura dettagliata:

![Creazione di un rapporto Ricavi totali per data di registrazione utente e origine.](../../assets/Revenue_by_user_registration_date_and_source.gif)

## Ripeti ordini per origine utente {#repeatordersbysource}

Il rapporto Valore medio ordine mostra, in media, quanti utenti acquisiti da una determinata origine spendono quando si effettua un ordine. Questo rapporto, tuttavia, non mostra se gli stessi utenti sono clienti frequenti. Tuttavia, con la funzione Ripeti ordini da parte delle origini utenti, è possibile verificare se gli utenti di una determinata origine effettuano acquisti più o meno ripetuti.

Per creare questo report nel [Report Builder](../../tutorials/using-visual-report-builder.md), aggiungere la metrica **Numero di ordini**, quindi eseguire le operazioni seguenti:

1. Impostare [!UICONTROL Time Period] sul periodo di registrazione che si desidera analizzare.
1. Imposta [!UICONTROL Time Interval] su mensile.
1. Aggiungi [!UICONTROL filter] in modo che siano inclusi solo gli utenti con ordini ripetuti:

   Numero ordine utente maggiore di 1

1. Impostare [!UICONTROL Group By] sull&#39;origine di acquisizione (o riferimento) e selezionare le origini che si desidera includere.
1. Questo esempio utilizza il tipo di grafico `stacked columns`.

Di seguito è riportata una procedura dettagliata:

![Creazione di un report di ripetizione ordini per origine utente.](../../assets/Repeat_orders_by_user_source.gif)


## Ritorno a capo {#wrapup}

Questo argomento ha toccato solo alcune analisi che puoi utilizzare per analizzare il valore dei tuoi canali di acquisizione e marketing, ma questa è solo la punta dell&#39;iceberg.

## Correlato {#related}

* [Tracciamento dell&#39;origine di riferimento dell&#39;ordine tramite  [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md)
* [Connessione dell&#39;account  [!DNL Google Adwords]  in corso](../importing-data/integrations/google-adwords.md)
* [Creazione di  [!DNL Google ECommerce] dimensioni con ordini e dati cliente](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [Best practice per l&#39;assegnazione di tag UTM in [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
