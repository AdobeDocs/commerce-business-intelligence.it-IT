---
title: Esporta dati non elaborati
description: Scopri come esportare i record dal tuo [!DNL Commerce Intelligence] Data Warehouse per avere una visione più dettagliata di ciò che alimenta il tuo dashboard.
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# Esporta dati non elaborati

Utilizzando le esportazioni di dati non elaborati, puoi esportare i record dal Data Warehouse per avere una visione più dettagliata di ciò che alimenta il dashboard. Inoltre, le esportazioni di dati non elaborati possono aiutarti a [individuare le discrepanze di dati](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html).

Le esportazioni di dati non elaborati consentono di accedere a colonne e dimensioni aggiuntive generate tramite la denormalizzazione e la preaggregazione di metriche rilevanti. `User's first order date`, ad esempio, è una dimensione che è possibile esportare per ogni utente in [!DNL Commerce Intelligence], mentre potrebbe non essere disponibile nel database.

Questo tutorial tratta i seguenti argomenti:

* [Selezione dei dati da esportare](#select)
* [Download dell&#39;esportazione (](#download)
* [Accesso alle esportazioni storiche](#historical)

## Passaggio 1: selezione dei dati da esportare {#select}

Esistono due modi per esportare i dati non elaborati in [!DNL Commerce Intelligence]:

1. a livello di grafico
1. a livello di tabella

### Esportazione a livello di tabella nella scheda [!UICONTROL Manage Data]

Per esportare la tabella dalla scheda [!UICONTROL Manage Data], sono necessarie [autorizzazioni amministratore](../administrator/user-management/user-management.md).

1. Fai clic su **[!UICONTROL Manage Data** > ** Esporta dati **> **Esportazione dati non elaborati]**.
1. Viene visualizzato un `Export List` delle esportazioni di dati create di recente, se presenti. Fare clic su **[!UICONTROL Add Export]** per creare un&#39;esportazione.
1. Viene visualizzata la finestra di dialogo `New Raw Data Export`. In questo caso, puoi personalizzare l’esportazione selezionando o deselezionando colonne e filtri:

   * `Table` - Il campo `Table` seleziona la tabella da cui vengono esportati i dati. Per impostazione predefinita, viene visualizzata la tabella in cui ci si è spostati.
   * `Export Name` - In questo campo immettere il nome dell&#39;esportazione. Esempio: `Philadelphia - Daily Revenue`.
   * `Available Columns` - Questo campo elenca le colonne (dimensioni) del database disponibili per l&#39;esportazione. Per aggiungere una colonna, fare clic sul relativo nome.
   * `Selected Columns` - Questo campo elenca le colonne (dimensioni) attualmente incluse nell&#39;esportazione. Per rimuovere una colonna, fare clic sul relativo nome.
   * `Filter` - In questa sezione sono elencati i filtri attualmente applicati all&#39;esportazione. Questi filtri possono essere modificati; è inoltre possibile aggiungere nuovi filtri per esportare un particolare set di dati.
   * Al termine, fare clic su **[!UICONTROL Export Data]**.

### Esportazione a livello di grafico dal dashboard

1. Fai clic sull’icona a forma di ingranaggio nell’angolo in alto a destra di qualsiasi grafico.

1. Seleziona `Raw Export` dal menu a discesa per visualizzare la finestra di dialogo `Raw Export`.

1. Personalizzare l&#39;esportazione scegliendo `table`, `columns` e `filters` da includere o escludere. Per informazioni più dettagliate sui campi di questo modulo, consulta la sezione precedente.

   >[!NOTE]
   >
   >La tabella visualizzata nel campo `Table` è, per impostazione predefinita, la tabella che attiva il grafico.

1. Al termine, fare clic su **[!UICONTROL Export Data]**.

Osservare l&#39;intero processo a livello di grafico.

![](../assets/Chart-level_export.gif)

## Passaggio 2: Scaricare l’esportazione {#download}

L&#39;elaborazione dell&#39;esportazione inizierà subito dopo aver completato le selezioni nella finestra di dialogo `Raw Data Export`. Poiché alcune esportazioni possono essere di grandi dimensioni, sono limitate a 10 milioni di righe e la loro esecuzione potrebbe richiedere del tempo.

Per verificare se l&#39;esportazione è pronta, fare clic su **[!UICONTROL Raw Data Exports]** nell&#39;angolo superiore destro della schermata. Fai clic su **[!UICONTROL Download]** per scaricare un file `.csv` compresso della tua esportazione.

![](../assets/Downloading_export.gif)

## Passaggio 3: Accesso alle esportazioni storiche {#historical}

Per visualizzare le esportazioni precedenti, fare clic su **[!UICONTROL Raw Data Export]** nell&#39;angolo superiore destro dello schermo. È possibile accedere ai report in sospeso e completati per un massimo di sette giorni.
