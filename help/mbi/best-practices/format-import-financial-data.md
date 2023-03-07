---
title: Formattazione e importazione di dati finanziari
description: Scopri come formattare e importare dati finanziari.
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# Formattare e importare dati finanziari

Questo argomento descrive il modo migliore per importare i dati finanziari da analizzare in [!DNL MBI].

Una tabella di dati bidimensionale a schede incrociate è spesso il formato utilizzato per i dati finanziari. Con i valori suddivisi per etichette in colonne e righe, questo tipo di layout può essere facilmente visualizzabile con gli occhi umani e gli strumenti per fogli di calcolo, ma non è facile per i database.

![](../../mbi/assets/crosstab.png)

Per importare e analizzare questi dati in [!DNL MBI], la tabella deve essere appiattita in un elenco unidimensionale. Quando viene appiattita, ogni valore di dati viene categorizzato da più etichette che si trovano tutte in una singola riga, dove ogni riga è univoca o avrebbe un identificatore univoco, ad esempio una colonna chiave primaria.

![](../../mbi/assets/flattened.png)

## Formattazione dei file di Excel per l&#39;importazione

Per appiattire una tabella bidimensionale utilizzando una tabella pivot di Excel:

1. Aprire il file con la tabella dati bidimensionale.
1. Aprire la Creazione guidata Tabella pivot. In Windows, la scelta rapida è `Alt-D`. In Mac OS, immetti `Command-Option-P`.
1. Seleziona **[!UICONTROL Multiple consolidated ranges]** e fai clic su **[!UICONTROL Next]**.
1. Seleziona **[!UICONTROL I will create the page fields]** e fai clic su **[!UICONTROL Next]**.
1. Selezionare l&#39;intero set di dati nella tabella bidimensionale, incluse le etichette. Assicurati che `0` è selezionato per il numero di campi pagina desiderati e fai clic su **[!UICONTROL Next]**.
1. Creare la tabella pivot in un nuovo foglio e fare clic su **[!UICONTROL Finish]**.
1. Deselezionare i campi colonna e riga dall&#39;elenco dei campi.
1. Fare doppio clic sul valore numerico risultante per visualizzare i dati di origine appiattiti in un nuovo foglio.
   ![](../../mbi/assets/pivot-table-double-click.png)
1. Salva come `CSV` file.

Tutto qui! La tabella dati è stata convertita in formato elenco, mantenendo tutte le informazioni originali, e ora può essere [importato in [!DNL MBI]](../data-analyst/importing-data/connecting-data/using-file-uploader.md) per l&#39;analisi.
