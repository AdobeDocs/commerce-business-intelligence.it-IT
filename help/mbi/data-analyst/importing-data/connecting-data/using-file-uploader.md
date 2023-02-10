---
title: Utilizza File Uploader
description: Scopri come inserire tutti i tuoi dati in un unico data warehouse.
exl-id: 28db0e78-0222-431d-bbb9-6ef133686603
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '1392'
ht-degree: 0%

---

# Utilizza File Uploader

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

[!DNL MBI] è potente non solo a causa delle sue funzioni di visualizzazione, ma anche perché ti consente di inserire tutti i tuoi dati in un unico data warehouse. Anche i dati che risiedono al di fuori dei database e le integrazioni possono essere inseriti in [!DNL MBI] utilizzando lo strumento Caricamento file in Data Warehouse Manager.

Usiamo le campagne pubblicitarie come esempio. Se esegui campagne sia online che offline, non puoi ottenere l’immagine completa se stai solo analizzando i dati da un’integrazione online. Il caricamento di un foglio di calcolo con i dati della campagna offline consente di analizzare entrambi i set di dati e ottenere una comprensione più approfondita delle prestazioni della campagna.

## Restrizioni e requisiti {#require}

1. **L’unico formato supportato per il caricamento dei file è `CSV` o`comma separated values`**. Se si lavora in Excel, è possibile utilizzare la funzione Salva con nome per salvare il file in `.csv` formato.
1. **`CSV`i file devono utilizzare`UTF-8 encoding`**. Nella maggior parte dei casi, non si tratta di una questione. Se si verifica questo errore durante il caricamento di un file, [consultare questo articolo sull&#39;assistenza](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/resolving-utf-8-errors-for-csv-file-uploads.html?lang=en).
1. **I file non possono superare i 100 MB**. Se il file è più grande di questo, separa la tabella in blocchi e salvala come file singoli. Puoi utilizzare aggiungi i dati dopo il caricamento del file iniziale.
1. **Tutte le tabelle devono avere un`primary key`**. Nella tabella deve essere presente almeno una colonna che può essere utilizzata come `primary key`o un identificatore univoco per ogni riga della tabella. Qualsiasi colonna designata come `primary key` può *mai* essere null. A `primary key` può essere semplice come aggiungere una colonna che dia un numero a ogni riga o può essere concatenata a due colonne per creare una colonna di valori univoci (ad esempio, `campaign name` e `date`).

   Se una colonna o colonne sono indicate come univoche ma sono presenti duplicati, le righe duplicate non verranno importate.

## Formattazione dei dati per il caricamento {#formatting}

Prima di caricare i dati in [!DNL MBI], controlla che sia formattato in base alle linee guida di questa sezione.

### Riga di intestazione {#header}

Per garantire che le colonne siano etichettate e importate correttamente, accertati che la prima riga del foglio di calcolo sia un’intestazione che descriva i dati in ogni colonna.

I nomi delle colonne devono essere univoci e contenere solo lettere, numeri, spazi e simboli: `$ % # /`. Se un nome di colonna contiene una virgola, verrà diviso in due colonne al caricamento del file. Inoltre, consigliamo di contenere meno di 85 colonne nel file per ottimizzare la velocità di aggiornamento.

### Dati con virgole {#commas}

Perché i file devono essere in `CSV` l’utilizzo di virgole può causare problemi durante il caricamento dei dati. `CSV` i file utilizzano le virgole per indicare nuovi valori, quindi una colonna con un nome come `Campaigns`, `August` verrà letto come due colonne (`Campaigns` e `August`) invece di uno, sposta tutti i dati su una riga. Consigliamo di evitare virgole quando possibile. È possibile utilizzare `Data Preview` per verificare se i dati vengono visualizzati correttamente al termine di un aggiornamento.

### Date

Ogni set di dati che include date deve utilizzare [formato data standard](https://dev.mysql.com/doc/refman/5.7/en/datetime.html) `YYYY-MM-DD HH:MM:SS` o `MM/DD/YYYY`.

### Caratteri speciali

Alcuni caratteri speciali non sono accettati. Ad esempio, il simbolo della tubazione `& # 1 2 4` viene interpretato come creazione di una nuova colonna e causerà errori durante il caricamento di un file.

### Numeri decimali

I valori della valuta devono avere il tipo di dati `Decimal Number` selezionate e queste colonne vengono arrotondate automaticamente a due posizioni decimali nel data warehouse. Se non si desidera arrotondare i numeri decimali o se si desidera ottenere un grado di precisione superiore a questo, selezionare la `Non-Currency Decimal Number` tipo di dati.

### Percentuali

Le percentuali devono essere indicate come decimali. Ad esempio:

| **A destra:** | **Sbagliato:** |
|-----|-----|
| `.05` | `5%` |
| `.23` | `23` |

{style=&quot;table-layout:auto&quot;}

### Valori con zero iniziali e/o finali {#zeroes}

Alcuni valori nel file, come i codici ZIP e gli ID, possono iniziare o terminare con uno zero. Per garantire che gli zero siano correttamente mantenuti e caricati, puoi modificare il tipo di formattazione (ad esempio, [da numero a testo](https://support.office.com/en-US/article/format-numbers-as-text-583160db-936b-4e52-bdff-6f1863518ba4)) o applica la formattazione dei numeri.

Utilizziamo `US ZIP codes` come esempio di come modificare la formattazione dei numeri. In [!DNL Excel], evidenzia la colonna contenente `ZIP codes` e [cambiare il formato del numero](https://support.office.com/en-za/article/Display-numbers-as-postal-codes-61b55c9f-6fe3-4e54-96ca-9e85c38a5a1d) a `ZIP code`. È inoltre possibile selezionare un formato di numero personalizzato e nella `Type` finestra, immettere `00000`. Tieni presente che questo metodo potrebbe presentare problemi se alcuni codici sono formattati come `00000` e gli altri `00000-0000`.

La `Type` può [formattato in modo diverso per accogliere altri tipi di dati](https://support.office.com/en-us/article/Keep-leading-zeros-in-number-codes-1bf7b935-36e1-4985-842f-5dfa51f85fe7?CorrelationId=e1d4c2d3-cd5d-4a14-999d-437800274a90&amp;ui=en-US&amp;rs=en-US&amp;ad=US), ad esempio gli ID. Se `ID` è lungo nove cifre, ad esempio `Type` potrebbe `000000000` o `000-000-000`. Ciò cambierebbe `123456` a `000-123-456`.

Per [!DNL Google Docs] e [!DNL Apple Numbers] risorse, consulta [Correlati](#related) nella parte inferiore della pagina.

## Caricamento dei dati {#uploading}

Ora che il foglio di calcolo è formattato correttamente e [!DNL MBI]-friendly, aggiungiamolo al tuo data warehouse.

1. Per iniziare, vai a **[!UICONTROL Data** > **File Uploads]**.

1. Fai clic sul pulsante **[!UICONTROL Upload to New Table]** scheda .

1. Fai clic su **[!UICONTROL Choose File]** e selezionare il file. Fai clic su **[!UICONTROL Open]** per avviare il caricamento.

   Al termine del caricamento, verrà visualizzato un elenco delle colonne [!DNL MBI] trovato nel file .

1. Verifica che i nomi delle colonne e i tipi di dati siano corretti. In particolare, verificare che le colonne di data vengano lette come date e non come numeri.

   >[!NOTE]
   >
   >La `datatype` è estremamente importante, quindi non saltare questo passaggio!

1. Seleziona la colonna (o le colonne) che compongono la `primary key` per la tabella utilizzando le caselle di controllo sotto l’icona chiave.

1. Denomina la tabella.

1. Fai clic su **[!UICONTROL Save Table]**.

A *Successo!* il messaggio viene visualizzato nella parte superiore dello schermo dopo il salvataggio della tabella.

Se hai bisogno di un&#39;immagine, ecco un&#39;occhiata all&#39;intero processo:

![](../../../assets/fileupload.gif)

Le tabelle caricate vengono visualizzate sotto il **Caricamenti di file** nell’elenco delle tabelle (nelle opzioni Tutte le tabelle e Tabelle sincronizzate) in Gestione Date Warehouse:

![](../../../assets/upload-tables.png)

## Aggiornamento o aggiunta di dati a una tabella esistente {#appending}

Hai nuovi dati da aggiungere a un file già caricato? Nessun problema: puoi facilmente aggiornare e aggiungere dati in [!DNL MBI].

1. Per iniziare, vai a **[!UICONTROL Manage Data** > **File Uploads]**.

1. Fai clic sul pulsante **[!UICONTROL Edit/Upload `.csv`alle tabelle esistenti]** scheda .

1. Nel menu a discesa , fai clic sul nome della tabella da aggiornare o aggiungere.

1. Utilizza il menu a discesa per selezionare l’opzione per la gestione delle righe duplicate:

   |  |  |
   |---|---|
   | `Overwrite old row with new row` | In questo modo i dati esistenti verranno sovrascritti con i nuovi dati se una riga ha la stessa chiave primaria sia nella tabella esistente che nel nuovo file. Questo è il metodo da utilizzare per le colonne con valori che cambiano nel tempo, ad esempio una colonna Stato . I dati esistenti verranno sovrascritti e aggiornati con i nuovi dati. Le righe con chiavi primarie non presenti nella tabella esistente verranno aggiunte come nuove righe. |
   | `Retain old row; discard new row` | In questo modo i nuovi dati verranno ignorati se una riga ha la stessa chiave primaria sia nella tabella esistente che nel nuovo file. |
   | `Purge all existing rows first and ignore duplicate keys within the file` | I dati esistenti verranno eliminati e sostituiti con i nuovi dati del file. Utilizzare questa opzione solo se non sono necessari dati nella tabella esistente. |

1. Fai clic su **[!UICONTROL Choose File]** e selezionare il file.

1. Fai clic su **[!UICONTROL Open]** per avviare il caricamento.

   Al termine del caricamento, [!DNL MBI] convalida la struttura dati nel file . A *Successo!* il messaggio viene visualizzato nella parte superiore dello schermo dopo il salvataggio della tabella.

## Disponibilità dei dati {#availability}

Come per le colonne calcolate, i dati provenienti dal caricamento dei file sono disponibili al termine del ciclo di aggiornamento successivo. Se durante il caricamento del file era in corso un aggiornamento, i dati saranno disponibili solo dopo il successivo aggiornamento. Una volta completato un ciclo di aggiornamento, puoi passare alla `Data Preview` in data warehouse per garantire che il file caricato correttamente e i dati vengano visualizzati come previsto.

## Ritorno a capo {#wrapup}

Questo articolo tratta solo le nozioni di base per l&#39;utilizzo dei dati di importazione, ma stiamo scommettendo che si desidera fare qualcosa un po&#39; più avanzato. Consulta gli articoli correlati per informazioni sulla formattazione e l’importazione di dati finanziari, eCommerce, spesa pubblicitaria e altri tipi di dati.

Inoltre, il caricamento dei file non è l’unico modo per inserire i tuoi dati in [!DNL MBI]. La [API di importazione dati](https://developer.adobe.com/commerce/services/reporting/import-api/) le funzioni ti consentono di inviare dati arbitrari [!DNL MBI] data warehouse.

## Correlati {#related}

* [Formattazione e importazione di dati finanziari](../../../best-practices/format-import-financial-data.md)
* [Importazione offline/altri dati di spesa degli annunci](../connecting-data/import-offline-ad-data.md)
* [Previsto[!DNL Google ECommerce] dati](../integrations/google-ecommerce-data.md)

## Risorse di terze parti

* [Guida alla formattazione dei dati numerici](http://www.dummies.com/how-to/content/how-to-choose-a-number-format-in-your-numbers-spre.html)
* [[!DNL Google Docs] Guida alla formattazione dei dati](https://support.google.com/docs/answer/56470?hl=en)
