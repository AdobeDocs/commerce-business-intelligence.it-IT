---
title: Configurazione dei controlli dei dati
description: Scopri come configurare le colonne di dati con valori modificabili.
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# Configurazione dei controlli dei dati

In una tabella di database possono essere presenti colonne di dati con valori modificabili. Ad esempio, in una tabella `orders` potrebbe essere presente una colonna denominata `status`. Quando un ordine viene scritto inizialmente nel database, la colonna di stato potrebbe contenere il valore _pending_. L&#39;ordine è replicato nel tuo [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) con questo valore `pending`.

Gli stati degli ordini possono cambiare, anche se non sono sempre nello stato `pending`. Potrebbe infine diventare `complete` o `cancelled`. Per fare in modo che il Data Warehouse sincronizzi questa modifica, la colonna deve essere ricontrollata per verificare la presenza di nuovi valori.

In che modo questo si adatta ai [metodi di replica](../data-warehouse-mgr/cfg-replication-methods.md) discussi? L’elaborazione dei nuovi controlli varia in base al metodo di replica scelto. Il metodo di replica `Modified\_At` è la scelta migliore per l&#39;elaborazione della modifica dei valori, in quanto non è necessario configurare i nuovi controlli. I metodi `Auto-Incrementing Primary Key` e `Primary Key Batch Monitoring` richiedono una riconfigurazione.

Quando si utilizza uno di questi metodi, le colonne modificabili devono essere contrassegnate per la ricontrolla. Esistono tre modi per farlo:

1. Processo di controllo eseguito come parte delle colonne dei flag di aggiornamento da ricontrollare.

   >[!NOTE]
   >
   >Il revisore si basa su un processo di campionamento e le colonne che cambiano potrebbero non essere rilevate immediatamente.

1. È possibile impostarli autonomamente selezionando la casella di controllo accanto alla colonna in Data Warehouse Manager, facendo clic su **[!UICONTROL Set Recheck Frequency]** e scegliendo un intervallo di tempo appropriato per il controllo delle modifiche.

1. Un membro del team Data Warehouse [!DNL Adobe Commerce Intelligence] può contrassegnare manualmente le colonne per la ricontrolla nel Data Warehouse. Se sono presenti colonne modificabili, contattare il team per richiedere l&#39;impostazione di nuovi controlli. Includi un elenco di colonne, insieme alla frequenza, nella richiesta.

## Ricontrolla frequenze {#frequency}

**Lo sapevi?**
Se si imposta una nuova verifica su una colonna `primary key`, i valori modificati non verranno verificati nella colonna. La tabella viene controllata per le righe eliminate e tutte le eliminazioni vengono eliminate da Data Warehouse.

Quando una colonna viene contrassegnata per la ricontrolla, è inoltre possibile impostare la frequenza con cui si verifica la ricontrolla. Se una colonna specifica non cambia spesso, la scelta di una verifica meno frequente può [ottimizzare il ciclo di aggiornamento](../../best-practices/reduce-update-cycle-time.md).

Le opzioni di frequenza sono:

* `always` - la nuova verifica si verifica durante ogni aggiornamento
* `daily` - la nuova verifica si verifica il primo aggiornamento post-mezzanotte per il tuo fuso orario dichiarato
* `weekly` - la verifica del fuso orario dichiarato viene ripetuta ogni settimana dopo le 21:00
* `monthly` - la verifica del fuso orario dichiarato viene ripetuta ogni quattro settimane dopo le 21:00
* `once` - si verifica solo nell&#39;aggiornamento successivo (aggiornamento una tantum)

Poiché gli orari di aggiornamento sono correlati alla quantità di dati da sincronizzare, Adobe consiglia di scegliere una verifica di nuovo `daily`, `weekly` o `monthly` invece di ogni aggiornamento.

## Gestione delle frequenze di ricontrollo {#manage}

È possibile gestire le frequenze di ricontrollo in Data Warehouse facendo clic sul nome di una tabella e selezionando le singole colonne. Lo stato di sincronizzazione e la frequenza di ricontrollo (le **modifiche?**) per ogni colonna della tabella.

Per modificare la frequenza di ricontrollo, fare clic sulla casella di controllo accanto alle colonne che si desidera modificare. Fare quindi clic sul menu a discesa **[!UICONTROL Set Recheck Frequency]** e impostare la frequenza desiderata.

![Data Warehouse Manager mostra le opzioni di ricontrolla configurazione](../../assets/dwm-recheck.png)

A volte potresti vedere `Paused` nella colonna `Changes?`. Questo valore viene visualizzato quando il metodo di replica [della tabella](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) è impostato su `Paused`.

[!DNL Adobe] consiglia di rivedere queste colonne per ottimizzare gli aggiornamenti e assicurarsi che le colonne modificabili vengano ricontrollate. Se la frequenza di ricontrollo di una colonna è elevata, data la frequenza con cui i dati cambiano, Adobe consiglia di diminuirla per ottimizzare gli aggiornamenti.

Contattaci per domande o per informazioni sui metodi di replica correnti o sui nuovi controlli.

**Correlato:**

* [Riduzione dei tempi di aggiornamento](../../best-practices/reduce-update-cycle-time.md)
* [Ottimizzazione del database per l&#39;analisi](../../best-practices/opt-db-analysis.md)
