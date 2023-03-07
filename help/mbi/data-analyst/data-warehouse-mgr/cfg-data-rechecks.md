---
title: Configurazione dei controlli dei dati
description: Scopri come configurare le colonne di dati con valori modificabili.
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# Configurazione dei controlli dei dati

In una tabella di database possono essere presenti colonne di dati con valori modificabili. Ad esempio, in un `orders`) potrebbe essere presente una colonna denominata `status`. Quando un ordine viene scritto inizialmente nel database, la colonna di stato potrebbe contenere il valore _in sospeso_. L’ordine viene replicato nel tuo [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) con questo `pending` valore.

Gli stati dell’ordine possono tuttavia cambiare, non sono sempre in un `pending` stato. Alla fine potrebbe diventare `complete` o `cancelled`. Per fare in modo che la Data Warehouse sincronizzi questa modifica, la colonna deve essere ricontrollata per verificare la presenza di nuovi valori.

In che modo questo si adatta al [metodi di replica](../data-warehouse-mgr/cfg-replication-methods.md) è stato discusso? L’elaborazione dei nuovi controlli varia in base al metodo di replica scelto. Il `Modified\_At` il metodo di replica è la scelta migliore per l’elaborazione dei valori che si modificano, in quanto non è necessario configurare i nuovi controlli. Il `Auto-Incrementing Primary Key` e `Primary Key Batch Monitoring` i metodi richiedono una ricontrolla configurazione.

Quando si utilizza uno di questi metodi, le colonne modificabili devono essere contrassegnate per la ricontrolla. Esistono tre modi per farlo:

* Processo di controllo eseguito come parte delle colonne dei flag di aggiornamento da ricontrollare.

   >[!NOTE]
   >
   >Il revisore si basa su un processo di campionamento e le colonne che cambiano potrebbero non essere rilevate immediatamente.

* Puoi impostarli autonomamente selezionando la casella di controllo accanto alla colonna in Gestione Date Warehouse, facendo clic su **[!UICONTROL Set Recheck Frequency]** e scegliendo un intervallo di tempo appropriato per verificare la presenza di modifiche.
* Un membro del [!DNL MBI] Il team di Data Warehouse può contrassegnare manualmente le colonne per il nuovo check-in della Data Warehouse. Se sono presenti colonne modificabili, contattare il team per richiedere l&#39;impostazione di nuovi controlli. Includi un elenco di colonne, insieme alla frequenza, nella richiesta.

## Ricontrolla frequenze {#frequency}

**Lo sapevate?**
Impostazione di una nuova verifica su un `primary key` non controlla se nella colonna sono presenti valori modificati. La tabella viene controllata per le righe eliminate e tutte le eliminazioni vengono eliminate dalla Data Warehouse.

Quando una colonna viene contrassegnata per la ricontrolla, è inoltre possibile impostare la frequenza con cui si verifica la ricontrolla. Se una particolare colonna non cambia spesso, è possibile scegliere una verifica meno frequente [ottimizzare il ciclo di aggiornamento](../../best-practices/reduce-update-cycle-time.md).

Le opzioni di frequenza sono:

* `always` - la verifica viene ripetuta durante ogni aggiornamento
* `daily` - la verifica viene effettuata al primo aggiornamento successivo alla mezzanotte per il fuso orario dichiarato
* `weekly` - la verifica viene ripetuta ogni settimana dopo le 21:00 (ora dell’aggiornamento del venerdì) per il fuso orario dichiarato
* `monthly` - la verifica del fuso orario dichiarato viene ripetuta ogni quattro settimane dopo le 21:00
* `once` - si verifica solo nell&#39;aggiornamento successivo (aggiornamento una tantum)

Poiché gli orari di aggiornamento sono correlati alla quantità di dati da sincronizzare, l’Adobe consiglia di scegliere un `daily`, `weekly`, o `monthly` ricontrolla invece di ogni aggiornamento.

## Gestione delle frequenze di ricontrollo {#manage}

È possibile gestire le frequenze di ricontrollo nella Data Warehouse facendo clic sul nome di una tabella e selezionando le singole colonne. Lo stato di sincronizzazione e la frequenza di ricontrollo (il **Modifiche?** ) viene visualizzata per ogni colonna della tabella.

Per modificare la frequenza di ricontrollo, fare clic sulla casella di controllo accanto alle colonne che si desidera modificare. Quindi fai clic su **[!UICONTROL Set Recheck Frequency]** e impostare la frequenza desiderata.

![](../../assets/dwm-recheck.png)

A volte potresti vedere `Paused` nel `Changes?` colonna. Questo valore viene visualizzato quando il [metodo di replica](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) è impostato su `Paused`.

L’Adobe consiglia di rivedere queste colonne per ottimizzare gli aggiornamenti e assicurarsi che vengano ricontrollate le colonne modificabili. Se la frequenza di ricontrollo di una colonna è elevata, data la frequenza con cui i dati cambiano, l’Adobe consiglia di diminuirla per ottimizzare gli aggiornamenti.

Contattaci per domande o per informazioni sui metodi di replica correnti o sui nuovi controlli.

**Correlato:**

* [Riduzione dei tempi di aggiornamento](../../best-practices/reduce-update-cycle-time.md)
* [Ottimizzazione del database per l&#39;analisi](../../best-practices/opt-db-analysis.md)
