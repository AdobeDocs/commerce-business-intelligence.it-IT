---
title: Standardizzazione dei dati con le tabelle di mappatura
description: Scopri come utilizzare le tabelle di mappatura.
exl-id: e452ff87-f298-43d5-acc3-af58e53bd0bc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# Standardizzare i dati con le tabelle di mappatura

Immagine: sei nel `Report Builder`, la costruzione di un `Revenue by State` rapporto. Lei è nella zona. Tutto sta andando a nuoto finché non vai ad aggiungere un `billing state` effettua il raggruppamento al rapporto per visualizzare quanto segue:

![](../../assets/Messy_State_Segments.png)

## Com&#39;è potuto succedere?

Purtroppo, la mancanza di standardizzazione può talvolta causare problemi ai dati e problemi durante la creazione dei rapporti. Nel nostro esempio, potrebbe non esserci stato un menu a discesa o un modo standardizzato per consentire ai nostri clienti di inserire le loro informazioni sullo stato di fatturazione. Questo porta a una varietà di valori - `pa`, `PA`, `penna`, `pennsylvania`e `Pennsylvania` - tutto per lo stesso stato, che certamente porterà a qualche strano risultato nella `Report Builder`.

È possibile che ci sia una risorsa tecnica che può aiutarti a pulire i dati o inserire le colonne necessarie direttamente nel tuo database, ma in caso contrario, abbiamo un&#39;altra soluzione: **la tabella di mappatura**. Una tabella di mappatura consente di pulire e standardizzare in modo rapido e semplice qualsiasi dato problematico mappando i dati a un singolo output.

>[!NOTE]
>
>Non è possibile creare una tabella di mappatura per tabelle consolidate senza l&#39;aiuto del team di supporto. Contattateci per ulteriori informazioni.

## Come la creo? {#how}

**Aggiornamento per la formattazione dei dati:**

* Assicurati che il foglio di calcolo contenga una riga di intestazione.
* Evita di usare le virgole! Ciò causerà problemi quando carichi il file.
* Utilizzare il formato data standard `(YYYY-MM-DD HH:MM:SS)` per le date.
* Le percentuali devono essere indicate come decimali.
* Assicurati che tutti gli zeri iniziali o finali siano mantenuti correttamente.

Prima di immergerti, ti consigliamo di: [esportare i dati della tabella non elaborati](../../tutorials/export-raw-data.md). Osservare prima i dati non elaborati significa poter esplorare tutte le possibili combinazioni per i dati da pulire, garantendo in tal modo che la tabella di mappatura copra tutto.

Per creare una tabella di mappatura, è necessario creare un foglio di calcolo a due colonne che segua la tabella [regole di formattazione per il caricamento dei file](../../data-analyst/importing-data/connecting-data/using-file-uploader.md).

Nella prima colonna, immetti i valori memorizzati nel database con **un solo valore in ogni riga**. Ad esempio: `pa` e `PA` non può trovarsi sulla stessa riga: ogni input deve avere una propria riga. Di seguito è riportato un esempio.

Nella seconda colonna, immetti i valori seguenti **devono**. Continuando con il nostro esempio di stato di fatturazione, se vogliamo `pa`, `PA`, `Pennsylvania`e `pennsylvania` essere `PA`, entravamo `PA` in questa colonna per ogni valore immesso.

![](../../assets/Mapping_table_examples.jpg)

## Cosa devo fare in [!DNL MBI] per usarlo? {#use}

Dopo aver creato la tabella di mappatura, è necessario [caricare il file](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) in [!DNL MBI] e [creare una colonna unita](../../data-analyst/data-warehouse-mgr/calc-column-types.md) che trasferisce il nuovo campo nella tabella desiderata. È possibile eseguire questa operazione dopo la sincronizzazione del file con il data warehouse.

Nel nostro esempio, sposteremo la colonna creata nel `mapping_state` tabella (`state_input`) al `customer_address` tabella utilizzando una colonna unita. Questo ci permetterà di raggrupparci per la pulizia `state_input` nei nostri report invece del `state` colonna.

Per creare `joined` , passare alla tabella a cui verrà reindirizzato il campo in Data Warehouse Manager. Nel nostro esempio, questo sarebbe il `customer_address` tabella.

1. Fai clic su **[!UICONTROL Create a Column]**.
1. Seleziona `Joined Column` dal `Definition` a discesa.
1. Assegna alla colonna un nome che la distingue dal `state` nel database. Noi andremo con noi `billing state (mapped)` possiamo quindi individuare la colonna da utilizzare per la segmentazione nel generatore di report.
1. Il percorso necessario per collegare le tabelle non esiste, quindi dobbiamo crearne uno nuovo. Fai clic su **[!UICONTROL Create new path]**  in `Select a table and column` a discesa.

   Se non si è sicuri di cosa sia la relazione di tabella o come definire correttamente le chiavi primarie ed esterne, estrarre [esercitazione](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md) per un po&#39; di aiuto.

   * Sulla `Many` lato, selezionare la tabella a cui si sta spostando il campo (di nuovo, per noi è `customer_address`) e `Foreign Key` colonna o `state` nel nostro esempio.
   * Sulla `One` lato, seleziona `mapping` la tabella e `Primary key` colonna. In questo caso, selezioniamo il `state_input` dalla colonna `mapping_state` tabella.
   * Ecco come si presenta il nostro percorso:

      ![](../../assets/State_Mapping_Path.png)

1. Al termine, fai clic su **[!UICONTROL Save]** per creare il percorso.
1. Il percorso potrebbe non essere compilato immediatamente dopo il salvataggio. In questo caso, fai clic sul pulsante `Path` e seleziona il percorso appena creato.
1. Fai clic su **[!UICONTROL Save]** per creare la colonna.

Tutto qui!

## Cosa faccio ora? {#wrapup}

Al termine di un ciclo di aggiornamento, potrai utilizzare la nuova colonna unita per segmentare correttamente i dati invece della colonna disordinata dal database. Dai un&#39;occhiata alle nostre opzioni di raggruppamento ora - non più stress casino:

![](../../assets/Clean_State_Segments.png)

Le tabelle di mappatura sono utili per qualsiasi momento in cui si desidera pulire alcuni dati potenzialmente problematici nel data warehouse. Tuttavia, le tabelle di mappatura possono essere utilizzate anche per altri casi d’uso interessanti, come [replica dei canali Google Analytics in MBI](../data-warehouse-mgr/rep-google-analytics-channels.md).

### Correlati

* [Informazioni e valutazione delle relazioni tra tabelle](../data-warehouse-mgr/table-relationships.md)
* [Creazione/eliminazione di percorsi per le colonne calcolate](../data-warehouse-mgr/create-paths-calc-columns.md)
