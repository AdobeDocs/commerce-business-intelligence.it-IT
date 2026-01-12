---
title: Creare riepiloghi e-mail automatizzati
description: Scopri come creare riepiloghi e-mail automatizzati.
exl-id: a9aea4fc-9193-467f-8554-3ad77ac3fa73
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: a65ededb203b7551fdfcb31cff130ef85b01fbe3
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 0%

---

# Creare riepiloghi e-mail automatizzati

I riepiloghi e-mail sono un potente strumento di comunicazione che puoi utilizzare per condividere lo stato e le tendenze della tua attività con le parti interessate. Con i riepiloghi delle e-mail, puoi:

* Riepiloghi grafici e-mail che includono i rapporti
* Includi o escludi l’autore del riepilogo e-mail dalla ricezione dell’e-mail
* Pianificare l’invio dell’e-mail
* Modifica, elimina e sospendi i riepiloghi e-mail pianificati esistenti

## Crea nuovo riepilogo e-mail

1. Fare clic su **[!DNL Manage Data]** e quindi su **[!UICONTROL Email Summary]** nella barra laterale.

   Se è la prima volta che crei un riepilogo e-mail, questa pagina non mostra alcun riepilogo salvato.

1. Fare clic su **[!UICONTROL Create New Email Summary]** nell&#39;angolo superiore destro.

1. Immettere un nome per il riepilogo.

   Scegli un nome che trasmetta ciò che è incluso nel riepilogo. Ad esempio, `AOV Comparison`.

1. Nella sezione `Choose Content` selezionare i report che si desidera includere nel riepilogo.

   Sono disponibili due opzioni per l’aggiunta di contenuto:

   * **Seleziona singoli rapporti** - Scegli rapporti specifici dai dashboard
   * **Seleziona l&#39;intero dashboard** - Includi tutti i report di un dashboard così come vengono visualizzati nel layout del dashboard

   Puoi selezionare fino a dieci rapporti di tua proprietà. Dopo aver selezionato un rapporto, utilizza le icone visualizzate per selezionare se desideri che il rapporto venga inviato come tabella o grafico. Se il report è stato salvato come numero, è possibile inviarlo solo come numero. Per informazioni sull&#39;invio di un riepilogo e-mail contenente un report con dati non aggiornati, vedere [Gestione delle impostazioni account](../../administrator/account-management/managing-account-settings.md).

   Per aggiungere interi dashboard, sono disponibili le seguenti opzioni di formato ed eliminazione:

   * Modificare il formato del report in un grafico o in una tabella
   * Non includere i report nell’e-mail
   * Seleziona questa opzione per includere un file CSV per i rapporti tabulari: in questo modo i destinatari possono accedere ai dati non elaborati ed esportabili direttamente dalla propria casella in entrata.

   >[!NOTE]
   >
   >I report `Cohort` sono disponibili solo se si utilizza la nuova architettura.

   >[!NOTE]
   >
   >Gli allegati CSV di grandi dimensioni sono supportati fino a un totale combinato di 25 MB per e-mail.

1. (Facoltativo) Selezionare `Send Email To Me` se si desidera ricevere l&#39;e-mail.

1. Per includere altri utenti nell&#39;e-mail, immettere i propri indirizzi e-mail nel campo `Add Email Recipients` separati da virgole, spazi, tabulazioni o punti e virgola.

## Pianifica riepilogo e-mail

Nel campo `Set when to send the Email Summary`, puoi specificare quando inviare i riepiloghi dell&#39;e-mail. Le opzioni sono:

* `Manual`
* `Once`
* `Repeating`

### Salva riepilogo e-mail da inviare in un secondo momento

1. Selezionare `Manual` dal campo `Set when to send the Email Summary`.

1. Fare clic su **[!UICONTROL Save]**.

   In questo modo il riepilogo viene salvato nell’elenco dei riepiloghi e-mail.

1. Quando sei pronto a inviare il riepilogo, fai clic sull&#39;icona a forma di ingranaggio e seleziona `Send Now`.

### Invia riepilogo e-mail una volta

1. Selezionare `Once` dal campo `Set when to send the Email Summary`.

1. Specificare la data di inizio nel calendario `Select Start Date`.

1. Specificare l&#39;ora di invio dell&#39;e-mail nel campo `Select time to send`.

### Crea pianificazione ripetuta

1. Selezionare `Repeating` dal campo `Set when to send the Email Summary`.

1. Nel campo `Set Frequency`, selezionare `Daily`, `Weekly` o `Monthly`.

1. Specificare la data di inizio nel calendario `Select Start Date`.

1. Specificare l&#39;ora di invio dell&#39;e-mail nel campo `Select time to send`.

1. (Facoltativo) Per specificare una data di fine, selezionare `End Date` e selezionare la data di fine dal calendario.

## Modifica riepilogo e-mail esistente

Dopo aver creato e salvato un riepilogo e-mail, nella pagina `Email Summaries` viene visualizzato un elenco di tutti i riepiloghi salvati. È possibile espandere (`+`) in ogni riga per ulteriori informazioni. Le colonne in questa visualizzazione sono:

* `Email Name` - Nome del riepilogo e-mail
* `Content` - Tipo di contenuto all&#39;interno del riepilogo, ad esempio i nomi dei report
* `Scheduled` - Frequenza, data e ora di invio del riepilogo e-mail
* `Recipients` - Destinatari del riepilogo e-mail
* `Created Date` - Data di creazione del riepilogo e-mail
* `Status` - `Paused` o `Active`

>[!NOTE]
>
>Per informazioni sull&#39;invio di un riepilogo e-mail contenente un report con dati non aggiornati, vedere [Gestione delle impostazioni account](../../administrator/account-management/managing-account-settings.md).

Fai clic sull’icona a forma di ingranaggio a destra di ciascuna riga per:

* `Send Now` - Invia immediatamente il riepilogo e-mail a tutti i destinatari specificati
* `Edit` - Modifica i dettagli del riepilogo e-mail
* `Pause/Active` - Sospendi o attiva la consegna di riepilogo e-mail
* `Delete` - Elimina riepilogo e-mail
