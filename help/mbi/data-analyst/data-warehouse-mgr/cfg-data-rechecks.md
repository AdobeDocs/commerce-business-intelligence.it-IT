---
title: Configurazione dei controlli dati
description: Scopri come configurare colonne di dati con valori modificabili.
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---

# Configurazione dei controlli dati

In una tabella di database possono essere presenti colonne di dati con valori modificabili. Ad esempio, in un `orders`) tabella potrebbe essere presente una colonna denominata `status`. Quando un ordine viene inizialmente scritto nel database, la colonna di stato potrebbe contenere il valore _in sospeso_. L&#39;ordine verrà quindi replicato nel tuo [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) con questo `pending` valore.

Tuttavia, gli stati dell’ordine possono cambiare, ma non saranno sempre in un `pending` stato. Alla fine potrebbe diventare `complete` o `cancelled`. Per garantire che la Data Warehouse sincronizzi questa modifica, è necessario ricontrollare la colonna per individuare nuovi valori.

In che modo questo si adatta al [metodi di replica](../data-warehouse-mgr/cfg-replication-methods.md) ne abbiamo discusso? L&#39;elaborazione dei nuovi controlli varia in base al metodo di replica scelto. La `Modified\_At` il metodo di replica è la scelta migliore per l&#39;elaborazione dei valori che cambiano, in quanto non è necessario configurare i nuovi controlli. La `Auto-Incrementing Primary Key` e `Primary Key Batch Monitoring` i metodi richiedono un nuovo controllo della configurazione.

Quando si utilizza uno di questi metodi, le colonne modificabili devono essere contrassegnate per il nuovo controllo. Esistono tre modi per farlo:

* Un processo di controllo eseguito come parte dell&#39;aggiornamento contrassegna le colonne da ricontrollare.

   >[!NOTE]
   >
   >Il revisore si basa su un processo di campionamento e le colonne mutevoli potrebbero non essere catturate immediatamente.

* Puoi impostarli autonomamente selezionando la casella di controllo accanto alla colonna nel gestore Date Warehouse, facendo clic su **[!UICONTROL Set Recheck Frequency]** e scegliere un intervallo di tempo appropriato per verificare la presenza di modifiche.
* Un membro del [!DNL MBI] Il team Data Warehouse può contrassegnare manualmente le colonne per il nuovo controllo della Data Warehouse. Se conosci colonne modificabili, contatta il team per richiedere che siano impostati nuovi controlli. Includi un elenco di colonne, insieme alla frequenza, con la tua richiesta.

## Controllare le frequenze {#frequency}

**Lo sapevi?**
Impostazione di un nuovo controllo su un `primary key` la colonna non controlla la presenza di valori modificati. La tabella verrà controllata per individuare le righe eliminate e le eventuali eliminazioni verranno quindi eliminate dalla Data Warehouse.

Quando una colonna viene contrassegnata per il nuovo controllo, è anche possibile impostare la frequenza con cui si verifica un nuovo controllo. Se una particolare colonna viene modificata meno spesso, scegliendo un controllo meno frequente è possibile [ottimizzazione del ciclo di aggiornamento](../../best-practices/reduce-update-cycle-time.md).

Le opzioni di frequenza sono:

* `always` - viene eseguito un nuovo controllo durante ogni aggiornamento
* `daily` - il ricontrollo si verifica il primo aggiornamento dopo la mezzanotte per il tuo fuso orario dichiarato
* `weekly` - ricontrollo avviene dopo le 9 del pomeriggio, aggiornamento ogni settimana del venerdì per il tuo fuso orario dichiarato
* `monthly` - ricontrollo avviene dopo le 9 del pomeriggio aggiornamento del venerdì ogni 4 settimane per il tuo fuso orario dichiarato
* `once` - si verifica solo nell&#39;aggiornamento successivo (un aggiornamento una tantum)

Poiché i tempi di aggiornamento sono correlati alla quantità di dati da sincronizzare, si consiglia di scegliere un `daily`, `weekly`oppure `monthly` ricontrolla invece di ogni aggiornamento.

## Gestione delle frequenze di ricontrollo {#manage}

È possibile controllare nuovamente le frequenze nella Data Warehouse facendo clic sul nome di una tabella e quindi selezionando le singole colonne. Lo stato di sincronizzazione e la frequenza di ricontrollo (la **Cambiamenti?** viene visualizzata per ogni colonna della tabella.

Per modificare la frequenza di ricontrollo, fai clic sulla casella di controllo accanto alla colonna o alle colonne che desideri modificare, quindi fai clic sul pulsante **[!UICONTROL Set Recheck Frequency]** e impostare la frequenza desiderata.

![](../../assets/dwm-recheck.png)

A volte potresti vedere `Paused` in `Changes?` colonna. Questo valore viene visualizzato quando la tabella è [metodo di replica](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) è impostato su `Paused`.

È consigliabile rivedere queste colonne per ottimizzare gli aggiornamenti e assicurarsi che vengano ricontrollate le colonne modificabili. Se la frequenza di ricontrollo di una colonna è inutilmente elevata, data la frequenza con cui i dati vengono modificati, consigliamo di ridurla per ottimizzare gli aggiornamenti.

Contattaci con domande o per informazioni sui metodi di replica o sui nuovi controlli correnti.

**Correlati:**

* [Riduzione dei tempi di aggiornamento](../../best-practices/reduce-update-cycle-time.md)
* [Ottimizzazione del database per l&#39;analisi](../../best-practices/opt-db-analysis.md)
