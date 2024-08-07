---
title: Formattazione e importazione di dati finanziari
description: Scopri come formattare e importare dati finanziari.
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Formattare e importare dati finanziari

In questo argomento viene descritto il modo migliore per importare i dati finanziari per l&#39;analisi in [!DNL Adobe Commerce Intelligence].

Una tabella di dati bidimensionale a schede incrociate è spesso il formato utilizzato per i dati finanziari. Con i valori suddivisi per etichette in colonne e righe, questo tipo di layout può essere facilmente visualizzabile con gli occhi umani e gli strumenti per fogli di calcolo, ma non è facile per i database.

![](../../mbi/assets/crosstab.png)

Per importare e analizzare questi dati in [!DNL Commerce Intelligence], è necessario appiattire la tabella in un elenco unidimensionale. Quando viene appiattita, ogni valore di dati viene categorizzato da più etichette che si trovano tutte in una singola riga, dove ogni riga è univoca o avrebbe un identificatore univoco, ad esempio una colonna chiave primaria.

![](../../mbi/assets/flattened.png)

## Formattazione dei file di Excel per l&#39;importazione

Per appiattire una tabella bidimensionale utilizzando una tabella pivot [!DNL Excel]:

1. Aprire il file con la tabella dati bidimensionale.
1. Aprire la Creazione guidata Tabella pivot. In [!DNL Windows], il collegamento è `Alt-D`. In [!DNL Mac OS], immettere `Command-Option-P`.
1. Selezionare **[!UICONTROL Multiple consolidated ranges]** e fare clic su **[!UICONTROL Next]**.
1. Selezionare **[!UICONTROL I will create the page fields]** e fare clic su **[!UICONTROL Next]**.
1. Selezionare l&#39;intero set di dati nella tabella bidimensionale, incluse le etichette. Verificare che `0` sia selezionato per il numero di campi pagina desiderati e fare clic su **[!UICONTROL Next]**.
1. Creare la tabella pivot in un nuovo foglio e fare clic su **[!UICONTROL Finish]**.
1. Deselezionare i campi colonna e riga dall&#39;elenco dei campi.
1. Fare doppio clic sul valore numerico risultante per visualizzare i dati di origine appiattiti in un nuovo foglio.
   ![](../../mbi/assets/pivot-table-double-click.png)
1. Salva come file `CSV`.

## Ritorno a capo

La tabella dati è stata convertita in un formato elenco, mantenendo tutte le informazioni originali, e ora può essere [importata in [!DNL Commerce Intelligence]](../data-analyst/importing-data/connecting-data/using-file-uploader.md) per l&#39;analisi.
