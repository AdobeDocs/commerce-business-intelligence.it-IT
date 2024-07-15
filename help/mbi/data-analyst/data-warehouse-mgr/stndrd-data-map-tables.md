---
title: Standardizzare i dati con le tabelle di mappatura
description: Scopri come utilizzare le tabelle di mappatura.
exl-id: e452ff87-f298-43d5-acc3-af58e53bd0bc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---

# Standardizzare i dati con le tabelle di mappatura

Immagina di essere in `Report Builder` a creare un report `Revenue by State`. Tutto sta andando bene finché non tenti di aggiungere un raggruppamento `billing state` al report e vedi questo:

![](../../assets/Messy_State_Segments.png)

## Com&#39;è potuto succedere?

Sfortunatamente, la mancanza di standardizzazione può a volte causare confusione nei dati e problemi durante la creazione dei rapporti. In questo esempio, potrebbe non essere disponibile un menu a discesa o un metodo standardizzato per consentire ai clienti di immettere le informazioni sullo stato di fatturazione. Ciò porta a vari valori - `pa`, `PA`, `penna`, `pennsylvania` e `Pennsylvania` - tutti per lo stesso stato, il che porta ad alcuni strani risultati in `Report Builder`.

È possibile che esista una risorsa tecnica che possa aiutarti a pulire i dati o a inserire le colonne necessarie direttamente nel database. In caso contrario, esiste un&#39;altra soluzione: **la tabella di mapping**. Una tabella di mappatura consente di pulire e standardizzare in modo rapido e semplice qualsiasi dato disordinato mappando i dati su un singolo output.

>[!NOTE]
>
>Non è possibile creare una tabella di mapping per le tabelle consolidate senza l&#39;assistenza del team di supporto Adobe.

## Come si crea? {#how}

**Aggiornamento formattazione dati:**

* Assicurati che il foglio di calcolo abbia una riga di intestazione.
* Evita di usare le virgole. Questo causa problemi quando carichi il file.
* Utilizzare il formato data standard `(YYYY-MM-DD HH:MM:SS)` per le date.
* Le percentuali devono essere immesse come decimali.
* Assicurati che eventuali zeri iniziali o finali siano correttamente conservati.

Prima di iniziare, Adobe consiglia di [esportare i dati della tabella non elaborati](../../tutorials/export-raw-data.md). Osservare prima i dati non elaborati significa poter esplorare tutte le possibili combinazioni per i dati da pulire, garantendo in tal modo che la tabella di mappatura copra tutto.

Per creare una tabella di mappatura, devi creare un foglio di calcolo a due colonne che segua le [regole di formattazione per i caricamenti di file](../../data-analyst/importing-data/connecting-data/using-file-uploader.md).

Nella prima colonna immettere i valori memorizzati nel database con **un solo valore in ogni riga**. Ad esempio, `pa` e `PA` non possono essere sulla stessa riga: ogni input deve avere la propria riga. Vedi di seguito per un esempio.

Nella seconda colonna immettere i valori **da**. Continuando con l&#39;esempio dello stato di fatturazione, se desideri che `pa`, `PA`, `Pennsylvania` e `pennsylvania` siano semplicemente `PA`, immetti `PA` in questa colonna per ogni valore di input.

![](../../assets/Mapping_table_examples.jpg)

## Cosa devo fare in [!DNL Commerce Intelligence] per usarlo? {#use}

Dopo aver creato la tabella di mapping, è necessario [caricare il file](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) in [!DNL Commerce Intelligence] e [creare una colonna unita](../../data-analyst/data-warehouse-mgr/calc-column-types.md) che riposiziona il nuovo campo nella tabella desiderata. Puoi eseguire questa operazione dopo che il file è stato sincronizzato con la Data Warehouse.

In questo esempio la colonna creata nella tabella `mapping_state` (`state_input`) viene spostata nella tabella `customer_address` utilizzando una colonna unita in join. Questo consente di eseguire il raggruppamento in base alla colonna `state_input` pulita nei report anziché alla colonna `state`.

Per creare la colonna `joined`, passare alla tabella in cui il campo verrà spostato in Gestione Date Warehouse. In questo esempio, la tabella `customer_address`.

1. Fare clic su **[!UICONTROL Create a Column]**.
1. Selezionare `Joined Column` dal menu a discesa `Definition`.
1. Assegnare alla colonna un nome che la differenzi dalla colonna `state` del database. Assegna un nome alla colonna `billing state (mapped)` in modo da sapere quale colonna utilizzare durante la segmentazione nel Report Builder.
1. Il percorso necessario per connettere le tabelle non esiste, pertanto è necessario crearne uno. Fare clic su **[!UICONTROL Create new path]** nel menu a discesa `Select a table and column`.

   Se non si è sicuri della relazione tra tabelle o di come definire correttamente le chiavi primarie ed esterne, consultare [l&#39;esercitazione](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md) per ottenere assistenza.

   * Sul lato `Many`, selezionare la tabella in cui si sta spostando il campo (di nuovo, per noi è `customer_address`) e la colonna `Foreign Key`, o colonna `state`, nell&#39;esempio.
   * Sul lato `One`, selezionare la tabella `mapping` e la colonna `Primary key`. In questo caso, selezionare la colonna `state_input` dalla tabella `mapping_state`.
   * Ecco un’anteprima del percorso:

     ![](../../assets/State_Mapping_Path.png)

1. Al termine, fare clic su **[!UICONTROL Save]** per creare il percorso.
1. Il percorso potrebbe non essere popolato immediatamente dopo il salvataggio. In questo caso, fare clic sulla casella `Path` e selezionare il percorso creato.
1. Fare clic su **[!UICONTROL Save]** per creare la colonna.

## Cosa faccio ora? {#wrapup}

Al termine di un ciclo di aggiornamento, potrai utilizzare la nuova colonna unita per segmentare correttamente i dati anziché la colonna confusa dal database. Esaminare le opzioni di raggruppamento ora, senza ulteriori problemi di stress:

![](../../assets/Clean_State_Segments.png)

Le tabelle di mappatura sono utili per ogni momento in cui si desidera eliminare alcuni dati potenzialmente confusi nella Data Warehouse. Tuttavia, le tabelle di mappatura possono essere utilizzate anche per altri casi d&#39;uso interessanti, come [replicare il tuo [!DNL Google Analytics channels] in [!DNL Commerce Intelligence]](../data-warehouse-mgr/rep-google-analytics-channels.md).

### Correlato

* [Informazioni e valutazione delle relazioni tra tabelle](../data-warehouse-mgr/table-relationships.md)
* [Creazione/eliminazione di percorsi per colonne calcolate](../data-warehouse-mgr/create-paths-calc-columns.md)
