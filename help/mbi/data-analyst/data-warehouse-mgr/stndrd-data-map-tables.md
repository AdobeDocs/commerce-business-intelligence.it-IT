---
title: Standardizzare i dati con le tabelle di mappatura
description: Scopri come utilizzare le tabelle di mappatura.
exl-id: e452ff87-f298-43d5-acc3-af58e53bd0bc
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---

# Standardizzare i dati con le tabelle di mappatura

Immagina di essere nel `Report Builder` creazione di un `Revenue by State` rapporto. Tutto sta andando bene finché non provi ad aggiungere un `billing state` Il raggruppamento nel report mostra quanto segue:

![](../../assets/Messy_State_Segments.png)

## Com&#39;è potuto succedere?

Sfortunatamente, la mancanza di standardizzazione può a volte causare confusione nei dati e problemi durante la creazione dei rapporti. In questo esempio, potrebbe non essere disponibile un menu a discesa o un metodo standardizzato per consentire ai clienti di immettere le informazioni sullo stato di fatturazione. Questo porta a diversi valori: `pa`, `PA`, `penna`, `pennsylvania`, e `Pennsylvania` - il tutto per lo stesso stato, il che porta ad alcuni strani risultati nel `Report Builder`.

È possibile che esista una risorsa tecnica che possa aiutarti a pulire i dati o a inserire le colonne necessarie direttamente nel database. In caso contrario, esiste un&#39;altra soluzione: **tabella di mappatura**. Una tabella di mappatura consente di pulire e standardizzare in modo rapido e semplice qualsiasi dato disordinato mappando i dati su un singolo output.

>[!NOTE]
>
>Non è possibile creare una tabella di mapping per le tabelle consolidate senza l&#39;assistenza del team di supporto Adobe.

## Come si crea? {#how}

**Aggiornamento formattazione dati:**

* Assicurati che il foglio di calcolo abbia una riga di intestazione.
* Evita di usare le virgole. Questo causa problemi quando carichi il file.
* Utilizza il formato data standard `(YYYY-MM-DD HH:MM:SS)` per le date.
* Le percentuali devono essere immesse come decimali.
* Assicurati che eventuali zeri iniziali o finali siano correttamente conservati.

Prima di iniziare, Adobe consiglia di: [esportare i dati della tabella non elaborati](../../tutorials/export-raw-data.md). Osservare prima i dati non elaborati significa poter esplorare tutte le possibili combinazioni per i dati da pulire, garantendo in tal modo che la tabella di mappatura copra tutto.

Per creare una tabella di mappatura, è necessario creare un foglio di calcolo a due colonne che segua [regole di formattazione per i caricamenti di file](../../data-analyst/importing-data/connecting-data/using-file-uploader.md).

Nella prima colonna immettere i valori memorizzati nel database con **un solo valore in ogni riga**. Ad esempio: `pa` e `PA` non può essere sulla stessa riga: ogni input deve avere una propria riga. Vedi di seguito per un esempio.

Nella seconda colonna immettere i valori **dovrebbe essere**. Continuando con l&#39;esempio di stato di fatturazione, se si desidera `pa`, `PA`, `Pennsylvania`, e `pennsylvania` per essere `PA`, si immette `PA` in questa colonna per ogni valore di input.

![](../../assets/Mapping_table_examples.jpg)

## Cosa devo fare in [!DNL Commerce Intelligence] per usarlo? {#use}

Al termine della creazione della tabella di mappatura, è necessario [carica il file](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) in [!DNL Commerce Intelligence] e [creare una colonna unita in join](../../data-analyst/data-warehouse-mgr/calc-column-types.md) che riposiziona il nuovo campo nella tabella desiderata. Puoi eseguire questa operazione dopo che il file è stato sincronizzato con la Data Warehouse.

In questo esempio viene spostata la colonna creata in `mapping_state` tabella (`state_input`) al `customer_address` utilizzando una colonna unita in join. Questo ci permette di raggruppare in base al pulito `state_input` nei rapporti anziché nella `state` colonna.

Per creare `joined` , passare alla tabella in cui il campo verrà spostato in Gestione Date Warehouse. In questo esempio, il valore `customer_address` tabella.

1. Clic **[!UICONTROL Create a Column]**.
1. Seleziona `Joined Column` dal `Definition` a discesa.
1. Assegna alla colonna un nome che la differenzi dalla `state` nel database. Denomina la colonna `billing state (mapped)` in modo da poter individuare la colonna da utilizzare durante la segmentazione nel report builder.
1. Il percorso necessario per connettere le tabelle non esiste, pertanto è necessario crearne uno. Clic **[!UICONTROL Create new path]**  nel `Select a table and column` a discesa.

   Se non si è sicuri della relazione tra tabelle o di come definire correttamente le chiavi primarie ed esterne, estrarre [esercitazione](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md) per un po&#39; di aiuto.

   * Il giorno `Many` selezionare la tabella in cui si sta spostando il campo (di nuovo, per noi è `customer_address`) e `Foreign Key` colonna, oppure `state` nell’esempio.
   * Il giorno `One` , selezionare il `mapping` tabella e `Primary key` colonna. In questo caso, seleziona il `state_input` colonna da `mapping_state` tabella.
   * Ecco un’anteprima del percorso:

      ![](../../assets/State_Mapping_Path.png)

1. Al termine, fai clic su **[!UICONTROL Save]** per creare il percorso.
1. Il percorso potrebbe non essere popolato immediatamente dopo il salvataggio - in questo caso, fai clic su `Path` e selezionare il percorso creato.
1. Clic **[!UICONTROL Save]** per creare la colonna.

## Cosa faccio ora? {#wrapup}

Al termine di un ciclo di aggiornamento, potrai utilizzare la nuova colonna unita per segmentare correttamente i dati anziché la colonna confusa dal database. Esaminare le opzioni di raggruppamento ora, senza ulteriori problemi di stress:

![](../../assets/Clean_State_Segments.png)

Le tabelle di mappatura sono utili per ogni momento in cui si desidera eliminare alcuni dati potenzialmente confusi nella Data Warehouse. Tuttavia, le tabelle di mappatura possono essere utilizzate anche per altri casi d’uso interessanti, come [replica di [!DNL Google Analytics channels] in [!DNL Commerce Intelligence]](../data-warehouse-mgr/rep-google-analytics-channels.md).

### Correlato

* [Informazioni e valutazione delle relazioni tra tabelle](../data-warehouse-mgr/table-relationships.md)
* [Creazione/eliminazione di percorsi per colonne calcolate](../data-warehouse-mgr/create-paths-calc-columns.md)
