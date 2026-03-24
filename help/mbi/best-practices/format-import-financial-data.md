---
title: Formattazione e importazione di dati finanziari
description: Scopri come formattare e importare dati finanziari.
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
role: Admin, Developer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
TQID: https://experienceleague.adobe.com/O1WKa98rRVw1dcgNQPsORit2gmZNn1Wi7H-Q4J7KcA0
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 278
ht-degree: 0%

---

# Formattare e importare dati finanziari

In questo argomento viene descritto il modo migliore per importare i dati finanziari per l&#39;analisi in [!DNL Adobe Commerce Intelligence].

Una tabella di dati bidimensionale a schede incrociate è spesso il formato utilizzato per i dati finanziari. Con i valori suddivisi per etichette in colonne e righe, questo tipo di layout può essere facilmente visualizzabile con gli occhi umani e gli strumenti per fogli di calcolo, ma non è facile per i database.

![Formato a campi incrociati con dati nel layout di tabella pivot](../../mbi/assets/crosstab.png)

Per importare e analizzare questi dati in [!DNL Commerce Intelligence], è necessario appiattire la tabella in un elenco unidimensionale. Quando viene appiattita, ogni valore di dati viene categorizzato da più etichette che si trovano tutte in una singola riga, dove ogni riga è univoca o avrebbe un identificatore univoco, ad esempio una colonna chiave primaria.

![Formato appiattito con dati nel layout a colonne](../../mbi/assets/flattened.png)

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
   ![Elenco campi tabella pivot di Excel con doppio clic per espandere](../../mbi/assets/pivot-table-double-click.png)
1. Salva come file `CSV`.

## Ritorno a capo

La tabella dati è stata convertita in un formato elenco, mantenendo tutte le informazioni originali, e ora può essere [importata in [!DNL Commerce Intelligence]](../data-analyst/importing-data/connecting-data/using-file-uploader.md) per l&#39;analisi.
