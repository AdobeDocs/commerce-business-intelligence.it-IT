---
title: Esporta dati non elaborati
description: Scopri come esportare i record dal tuo [!DNL MBI] Data Warehouse per avere un'occhiata più da vicino a ciò che alimenta il dashboard.
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# Esporta dati non elaborati

Utilizzando le esportazioni di dati grezzi, puoi esportare i record dal tuo [!DNL MBI] Data Warehouse per avere un&#39;occhiata più da vicino a ciò che alimenta il dashboard. Inoltre, le esportazioni di dati non elaborati possono esserti utili [individuare discrepanze nei dati](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=en).

Le esportazioni di dati grezzi consentono di accedere a colonne e dimensioni aggiuntive generate tramite la denormalizzazione e la pre-aggregazione di metriche rilevanti. Ad esempio: `User's first order date` è una dimensione che puoi esportare per ogni utente in [!DNL MBI], ma potrebbe non essere disponibile nel database.

Questa esercitazione tratta i seguenti argomenti:

* [Selezione dei dati da esportare](#select)
* [Download dell&#39;esportazione (](#download)
* [Accesso alle esportazioni storiche](#historical)

## Passaggio 1: Selezione dei dati da esportare {#select}

Esistono due modi per esportare i dati non elaborati in [!DNL MBI]: a livello di grafico o di tabella.

### Esportazione a livello di tabella nel `Manage Data` Scheda

Per esportare la tabella da `Manage Data` scheda , sarà necessario [Amministratore](../administrator/user-management/user-management.md) autorizzazioni.

1. Fai clic su **[!UICONTROL Manage Data** > ** Esporta dati **> **Esportazione di dati grezzi]** per iniziare.
1. Verrà visualizzata una `Export List` delle esportazioni di dati create di recente, se presenti. Fai clic su **[!UICONTROL Add Export]** per creare una nuova esportazione.
1. La `New Raw Data Export` viene visualizzata la finestra di dialogo . In questa finestra puoi personalizzare l’esportazione selezionando o deselezionando colonne e filtri:

   * `Table` - `Table` seleziona la tabella da cui verranno esportati i dati. Per impostazione predefinita, viene visualizzata la tabella in cui è stato effettuato il navigazione.
   * `Export Name` - In questo campo, immettere il nome dell&#39;esportazione. Ad esempio: `Philadelphia - Daily Revenue`.
   * `Available Columns` - Questo campo elenca le colonne (dimensioni) del database disponibili per l’inclusione nell’esportazione. Per aggiungere una colonna, fare clic sul relativo nome.
   * `Selected Columns` - Questo campo elenca le colonne (dimensioni) attualmente incluse nell’esportazione. Per rimuovere una colonna, fare clic sul relativo nome.
   * `Filter` - In questa sezione sono elencati i filtri attualmente applicati all’esportazione. Questi filtri possono essere modificati; è inoltre possibile aggiungere nuovi filtri per esportare un particolare set di dati.
   * Al termine, fai clic su **[!UICONTROL Export Data]**.

### Esportazione a livello di grafico dal dashboard

1. Fai clic sull’icona a forma di ingranaggio nell’angolo in alto a destra di qualsiasi grafico.
1. Seleziona `Raw Export` dal menu a discesa per visualizzare il `Raw Export` finestra di dialogo.
1. Personalizza l’esportazione scegliendo la `table`, `columns`e `filters` da includere o escludere. Fai riferimento alla sezione precedente per informazioni più dettagliate sui campi in questo modulo.
   >[!NOTE]
   >
   >La tabella visualizzata nel `Table` per impostazione predefinita, il campo è la tabella che attiva il grafico.

1. Al termine, fai clic su **[!UICONTROL Export Data]**.

Diamo un&#39;occhiata all&#39;intero processo a livello di grafico.

![](../assets/Chart-level_export.gif)

## Passaggio 2: Download dell’esportazione {#download}

L’esportazione inizierà l’elaborazione immediatamente dopo aver completato le selezioni nella `Raw Data Export` finestra di dialogo. Poiché alcune esportazioni possono essere di grandi dimensioni, sono limitate a 10 milioni di righe e potrebbero richiedere un po&#39; di tempo per l&#39;esecuzione.

Per verificare che l’esportazione sia pronta, fai clic su **[!UICONTROL Raw Data Exports]** nell’angolo in alto a destra dello schermo. Fai clic su **[!UICONTROL Download]** per scaricare un file ZIP `.csv` file dell&#39;esportazione.

![](../assets/Downloading_export.gif)

## Passaggio 3: Accesso alle esportazioni storiche {#historical}

Per visualizzare le esportazioni passate, fai clic su **[!UICONTROL Raw Data Export]** nell’angolo in alto a destra dello schermo. È possibile accedere ai rapporti in sospeso e completati per un massimo di sette giorni.

Congratulazioni! Lei ha finito.
