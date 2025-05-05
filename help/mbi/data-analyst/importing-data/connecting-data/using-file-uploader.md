---
title: Usa Caricamento File
description: Scopri come inserire tutti i dati in un’unica Data Warehouse.
exl-id: 28db0e78-0222-431d-bbb9-6ef133686603
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1279'
ht-degree: 0%

---

# Usa Caricamento File

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

[!DNL Adobe Commerce Intelligence] è potente non solo per le sue funzioni di visualizzazione, ma perché consente di inserire tutti i dati in un&#39;unica Data Warehouse. Anche i dati che si trovano all&#39;esterno dei database e delle integrazioni possono essere inseriti in [!DNL Commerce Intelligence] utilizzando lo strumento Caricamento file in Gestione Date Warehouse.

Utilizza le campagne pubblicitarie come esempio. Se esegui campagne online e offline, non puoi ottenere l’intera immagine se stai analizzando solo i dati di un’integrazione online. Il caricamento di un foglio di calcolo con i dati della campagna offline consente di analizzare entrambi i set di dati e ottenere una comprensione più solida delle prestazioni della campagna.

## Restrizioni e requisiti {#require}

1. **L&#39;unico formato supportato per i caricamenti di file è `CSV` o`comma separated values`**. Se si utilizza Excel, è possibile utilizzare la funzione Salva con nome per salvare il file nel formato `.csv`.
1. **`CSV`file devono utilizzare`UTF-8 encoding`**. Nella maggior parte dei casi, questo non è un problema. Se riscontri questo errore durante il caricamento di un file, [consulta questo articolo del supporto tecnico](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/resolving-utf-8-errors-for-csv-file-uploads.html?lang=it).
1. **I file non possono superare i 100 MB**. Se il file è più grande, separare la tabella in blocchi e salvarli come file singoli. È possibile aggiungere i dati dopo il caricamento del file iniziale.
1. **Tutte le tabelle devono avere un`primary key`**. Nella tabella deve essere presente almeno una colonna che può essere utilizzata come `primary key` o un identificatore univoco per ogni riga della tabella. Qualsiasi colonna designata come `primary key` può *mai* essere null. Una `primary key` può essere semplice come aggiungere una colonna che dia un numero a ogni riga oppure può essere costituita da due colonne concatenate per creare una colonna di valori univoci (ad esempio, `campaign name` e `date`).

   Se una colonna o più colonne sono designate come univoche ma sono presenti duplicati, le righe duplicate non vengono importate.

## Formattazione dei dati per il caricamento {#formatting}

Prima di caricare i dati in [!DNL Commerce Intelligence], verificare che siano formattati in base alle linee guida illustrate in questa sezione.

### Riga di intestazione {#header}

Per garantire che le colonne siano etichettate e importate correttamente, assicurati che la prima riga del foglio di calcolo sia un’intestazione che descrive i dati in ogni colonna.

I nomi di colonna devono essere univoci e contenere solo lettere, numeri, spazi e i seguenti simboli: `$ % # /`. Se il nome di una colonna contiene una virgola, viene diviso in due colonne al caricamento del file. Inoltre, l’Adobe consiglia di avere meno di 85 colonne nel file per ottimizzare la velocità di aggiornamento.

### Dati con virgole {#commas}

Poiché i file devono essere in formato `CSV`, l&#39;utilizzo delle virgole può causare problemi nel caricamento dei dati. I file `CSV` utilizzano le virgole per indicare i nuovi valori. Pertanto, una colonna con un nome come `Campaigns`, `August` viene letta come due colonne (`Campaigns` e `August`) invece di una, spostando tutti i dati su una riga. L’Adobe consiglia di evitare le virgole laddove possibile. È possibile utilizzare `Data Preview` per verificare se i dati vengono visualizzati correttamente al termine di un aggiornamento.

### Date

Qualsiasi set di dati che include date deve utilizzare il [formato di data standard](https://dev.mysql.com/doc/refman/5.7/en/datetime.html) `YYYY-MM-DD HH:MM:SS` o `MM/DD/YYYY`.

### Caratteri speciali

Alcuni caratteri speciali non sono accettati. Ad esempio, il simbolo di barra verticale `& # 1 2 4` viene interpretato come la creazione di una colonna e causa errori durante il caricamento di un file.

### Numeri decimali

Per i valori di valuta deve essere selezionato il tipo di dati `Decimal Number` e queste colonne vengono arrotondate automaticamente a due posizioni decimali nella Data Warehouse. Se non si desidera arrotondare i numeri decimali o se il grado di precisione è maggiore, selezionare il tipo di dati `Non-Currency Decimal Number`.

### Percentuali

Le percentuali devono essere immesse come decimali. Ad esempio:

| **Destra:** | **Errore:** |
|-----|-----|
| `.05` | `5%` |
| `.23` | `23` |

{style="table-layout:auto"}

### Valori con zeri iniziali e/o finali {#zeroes}

Alcuni valori nel file, come codici postali e ID, possono iniziare o terminare con zeri. Per garantire che gli zeri vengano mantenuti e caricati correttamente, puoi modificare il tipo di formattazione (ad esempio, [da numero a testo](https://support.microsoft.com/en-us/office/format-numbers-as-text-583160db-936b-4e52-bdff-6f1863518ba4?ui=en-us&amp;rs=en-us&amp;ad=us)) o applicare la formattazione dei numeri.

Utilizzare `US ZIP codes` come esempio di modifica della formattazione dei numeri. In [!DNL Excel], evidenziare la colonna contenente `ZIP codes` e [modificare il formato del numero](https://support.microsoft.com/en-us/office/display-numbers-as-postal-codes-61b55c9f-6fe3-4e54-96ca-9e85c38a5a1d?ui=en-us&amp;rs=en-us&amp;ad=us) in `ZIP code`. È inoltre possibile selezionare un formato numerico personalizzato e nella finestra `Type` immettere `00000`. Tieni presente che questo metodo potrebbe presentare problemi se alcuni codici sono formattati come `00000` e altri come `00000-0000`.

`Type` può essere [formattato in modo diverso per altri tipi di dati](https://support.microsoft.com/en-us/office/keeping-leading-zeros-and-large-numbers-1bf7b935-36e1-4985-842f-5dfa51f85fe7?correlationid=e1d4c2d3-cd5d-4a14-999d-437800274a90&amp;ui=en-us&amp;rs=en-us&amp;ad=us), ad esempio gli ID. Se la lunghezza di un `ID` è di nove cifre, ad esempio, `Type` potrebbe essere `000000000` o `000-000-000`. `123456` verrebbe modificato in `000-123-456`.

Per le risorse [!DNL Google Docs] e [!DNL Apple Numbers], fare riferimento all&#39;elenco [Correlati](#related) nella parte inferiore di questa pagina.

## Caricamento dei dati {#uploading}

Dopo aver formattato correttamente il foglio di calcolo e averlo compatibile con [!DNL Commerce Intelligence], aggiungilo alla Data Warehouse.

1. Per iniziare, passa a **[!UICONTROL Data** > **File Uploads]**.

1. Fare clic sulla scheda **[!UICONTROL Upload to New Table]**.

1. Fare clic su **[!UICONTROL Choose File]** e selezionare il file. Fare clic su **[!UICONTROL Open]** per avviare il caricamento.

   Al termine del caricamento, verrà visualizzato l&#39;elenco delle colonne [!DNL Commerce Intelligence] trovate nel file.

1. Verificare che i nomi delle colonne e i tipi di dati siano corretti. In particolare, verifica che tutte le colonne di data vengano lette come date e non come numeri.

   >[!NOTE]
   >
   >`datatype` è importante, quindi non saltare questo passaggio.

1. Selezionare la colonna o le colonne che compongono `primary key` per la tabella utilizzando le caselle di controllo sotto l&#39;icona chiave.

1. Denomina la tabella.

1. Fare clic su **[!UICONTROL Save Table]**.

*Operazione completata.Il messaggio* viene visualizzato nella parte superiore dello schermo dopo il salvataggio della tabella.

Se hai bisogno di una visione, osserva l’intero processo:

![](../../../assets/fileupload.gif)

Le tabelle caricate vengono visualizzate nella sezione **Caricamenti file** dell&#39;elenco delle tabelle (sia nelle opzioni Tutte le tabelle che nelle tabelle sincronizzate) in Gestione Date Warehouse:

![](../../../assets/upload-tables.png)

## Aggiornamento o aggiunta di dati a una tabella esistente {#appending}

Hai dei nuovi dati da aggiungere a un file che hai già caricato? Nessun problema - è possibile aggiornare e aggiungere facilmente i dati in [!DNL Commerce Intelligence].

1. Per iniziare, passa a **[!UICONTROL Manage Data** > **File Uploads]**.

1. Fare clic sulla scheda **[!UICONTROL Edit/Upload `.csv`alle tabelle esistenti]**.

1. Nel menu a discesa, fai clic sul nome della tabella da aggiornare o aggiungere.

1. Utilizza il menu a discesa per selezionare l’opzione per la gestione delle righe duplicate:

   | Opzione | Descrizione |
   |---|---|
   | `Overwrite old row with new row` | In questo modo i dati esistenti vengono sovrascritti con i nuovi dati se una riga ha la stessa chiave primaria sia nella tabella esistente che nel nuovo file. Questo è il metodo da utilizzare per le colonne con valori che cambiano nel tempo, ad esempio una colonna Stato. I dati esistenti vengono sovrascritti e aggiornati con i nuovi dati. Le righe con chiavi primarie non presenti nella tabella esistente vengono aggiunte come nuove righe. |
   | `Retain old row; discard new row` | In questo modo i nuovi dati vengono ignorati se una riga ha la stessa chiave primaria sia nella tabella esistente che nel nuovo file. |
   | `Purge all existing rows first and ignore duplicate keys within the file` | In questo modo tutti i dati esistenti verranno eliminati e sostituiti con i nuovi dati del file. Utilizza questa opzione solo se non hai bisogno di nessuno dei dati nella tabella esistente. |

1. Fare clic su **[!UICONTROL Choose File]** e selezionare il file.

1. Fare clic su **[!UICONTROL Open]** per avviare il caricamento.

   Al termine del caricamento, [!DNL Commerce Intelligence] convaliderà la struttura dati nel file. *Operazione completata.Il messaggio* viene visualizzato nella parte superiore dello schermo dopo il salvataggio della tabella.

## Disponibilità dei dati {#availability}

Proprio come le colonne calcolate, i dati provenienti dai caricamenti di file sono disponibili al termine del successivo ciclo di aggiornamento. Se durante il caricamento del file era in corso un aggiornamento, i dati non saranno disponibili fino a dopo il successivo aggiornamento. Una volta completato il ciclo di aggiornamento, è possibile passare alla scheda `Data Preview` nella Data Warehouse per verificare che il file sia stato caricato correttamente e che i dati vengano visualizzati come previsto.

## Ritorno a capo {#wrapup}

In questo argomento sono state trattate solo le nozioni di base sull&#39;utilizzo dell&#39;importazione dei dati, ma è possibile eseguire operazioni più avanzate. Consulta gli articoli correlati per informazioni sulla formattazione e l’importazione di dati finanziari, di e-commerce, di spesa pubblicitaria e di altri tipi di dati.

Inoltre, il caricamento dei file non è l&#39;unico modo per inserire i dati in [!DNL Commerce Intelligence]. Le funzioni dell&#39;[API di importazione dati](https://developer.adobe.com/commerce/services/reporting/import-api/) consentono di inviare dati arbitrari alla Data Warehouse [!DNL Commerce Intelligence].

## Correlato {#related}

* [Formattazione e importazione di dati finanziari](../../../best-practices/format-import-financial-data.md)
* [Importazione offline/altri dati di spesa degli annunci](../connecting-data/import-offline-ad-data.md)
* [Previsti[!DNL Google ECommerce] dati](../integrations/google-ecommerce-data.md)

## Risorse di terze parti

* [Guida alla formattazione dei dati numerici](http://www.dummies.com/how-to/content/how-to-choose-a-number-format-in-your-numbers-spre.html)
* [[!DNL Google Docs] Guida alla formattazione dei dati](https://support.google.com/docs/answer/56470?hl=en)
