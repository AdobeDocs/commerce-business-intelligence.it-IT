---
title: Esporta dati non elaborati
description: Scopri come esportare i record dal tuo [!DNL Commerce Intelligence] Data Warehouse per avere una visione più dettagliata di ciò che alimenta il dashboard.
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Esporta dati non elaborati

Utilizzando le esportazioni di dati non elaborati, puoi esportare i record dalla Data Warehouse per ottenere una visione più dettagliata di ciò che alimenta il dashboard. Inoltre, le esportazioni di dati non elaborati possono esserti utili [individuare le discrepanze nei dati](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html).

Le esportazioni di dati non elaborati consentono di accedere a colonne e dimensioni aggiuntive generate tramite la denormalizzazione e la preaggregazione di metriche rilevanti. Ad esempio: `User's first order date` è una dimensione che puoi esportare per ogni utente in [!DNL Commerce Intelligence], anche se potrebbe non essere disponibile nel database.

Questo tutorial tratta i seguenti argomenti:

* [Selezione dei dati da esportare](#select)
* [Download dell&#39;esportazione (](#download)
* [Accesso alle esportazioni storiche](#historical)

## Passaggio 1: selezione dei dati da esportare {#select}

Esistono due modi per esportare i dati non elaborati in [!DNL Commerce Intelligence]:

1. a livello di grafico
1. a livello di tabella

### Esportazione a livello di tabella nel [!UICONTROL Manage Data] Linguetta

Per esportare la tabella da [!UICONTROL Manage Data] scheda, è necessario [Amministratore](../administrator/user-management/user-management.md) autorizzazioni.

1. Clic **[!UICONTROL Manage Data** > ** Esporta dati **> **Esportazione di dati non elaborati]**.
1. Viene visualizzata una `Export List` di esportazioni di dati create di recente, se presenti. Clic **[!UICONTROL Add Export]** per creare un’esportazione.
1. Il `New Raw Data Export` viene visualizzata una finestra di dialogo. In questo caso, puoi personalizzare l’esportazione selezionando o deselezionando colonne e filtri:

   * `Table` - Il `Table` seleziona la tabella da cui vengono esportati i dati. Per impostazione predefinita, viene visualizzata la tabella in cui ci si è spostati.
   * `Export Name` - In questo campo immettere il nome dell&#39;esportazione. Ad esempio: `Philadelphia - Daily Revenue`.
   * `Available Columns` : questo campo elenca le colonne (dimensioni) del database disponibili per l’esportazione. Per aggiungere una colonna, fare clic sul relativo nome.
   * `Selected Columns` - Questo campo elenca le colonne (dimensioni) attualmente incluse nell’esportazione. Per rimuovere una colonna, fare clic sul relativo nome.
   * `Filter` : in questa sezione sono elencati i filtri attualmente applicati all’esportazione. Questi filtri possono essere modificati; è inoltre possibile aggiungere nuovi filtri per esportare un particolare set di dati.
   * Al termine, fai clic su **[!UICONTROL Export Data]**.

### Esportazione a livello di grafico dal dashboard

1. Fai clic sull’icona a forma di ingranaggio nell’angolo in alto a destra di qualsiasi grafico.

1. Seleziona `Raw Export` dal menu a discesa per visualizzare `Raw Export` .

1. Personalizzare l’esportazione scegliendo `table`, `columns`, e `filters` per includere o escludere. Per informazioni più dettagliate sui campi di questo modulo, consulta la sezione precedente.

   >[!NOTE]
   >
   >La tabella visualizzata in `Table` è, per impostazione predefinita, la tabella che attiva il grafico.

1. Al termine, fai clic su **[!UICONTROL Export Data]**.

Osservare l&#39;intero processo a livello di grafico.

![](../assets/Chart-level_export.gif)

## Passaggio 2: Scaricare l’esportazione {#download}

L’esportazione inizierà l’elaborazione immediatamente dopo aver completato le selezioni in `Raw Data Export` . Poiché alcune esportazioni possono essere di grandi dimensioni, sono limitate a 10 milioni di righe e la loro esecuzione potrebbe richiedere del tempo.

Per verificare se l’esportazione è pronta, fai clic su **[!UICONTROL Raw Data Exports]** nell’angolo in alto a destra dello schermo. Clic **[!UICONTROL Download]** per scaricare un file compresso `.csv` file della tua esportazione.

![](../assets/Downloading_export.gif)

## Passaggio 3: Accesso alle esportazioni storiche {#historical}

Per visualizzare le esportazioni precedenti, fai clic su **[!UICONTROL Raw Data Export]** nell&#39;angolo superiore destro dello schermo. È possibile accedere ai report in sospeso e completati per un massimo di sette giorni.
