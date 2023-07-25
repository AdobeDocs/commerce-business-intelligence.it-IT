---
title: Creare riepiloghi e-mail automatizzati
description: Scopri come creare riepiloghi e-mail automatizzati.
exl-id: a9aea4fc-9193-467f-8554-3ad77ac3fa73
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Creare riepiloghi e-mail automatizzati

I riepiloghi e-mail sono un potente strumento di comunicazione che puoi utilizzare per condividere lo stato e le tendenze della tua attività con le parti interessate. I riepiloghi delle e-mail consentono di:

* Riepiloghi grafici e-mail che includono i rapporti
* Includi o escludi l’autore del riepilogo e-mail dalla ricezione dell’e-mail
* Pianificare l’invio dell’e-mail
* Modifica, elimina e sospendi i riepiloghi e-mail pianificati esistenti

## Crea nuovo riepilogo e-mail

1. Clic **[!DNL Manage Data]** allora **[!UICONTROL Email Summary]** nella barra laterale.

   Se è la prima volta che crei un riepilogo e-mail, questa pagina non mostra alcun riepilogo salvato.

1. Clic **[!UICONTROL Create New Email Summary]** in alto a destra.

1. Immettere un nome per il riepilogo.

   Scegli un nome che trasmetta ciò che è incluso nel riepilogo. Ad esempio: `AOV Comparison`.

1. In `Choose Content` , selezionare i rapporti che si desidera includere nel riepilogo.

   Puoi selezionare fino a dieci rapporti di tua proprietà. Dopo aver selezionato un rapporto, utilizza le icone visualizzate per selezionare se desideri che il rapporto venga inviato come tabella o grafico. Se il report è stato salvato come numero, è possibile inviarlo solo come numero. Per informazioni sull’invio di un riepilogo e-mail contenente un rapporto con dati non aggiornati, consulta [Gestione delle impostazioni dell’account](../../administrator/account-management/managing-account-settings.md).

   >[!NOTE]
   >
   >`Cohort` i rapporti sono disponibili solo se utilizzi la nuova architettura.

1. (Facoltativo) Seleziona `Send Email To Me` se desideri ricevere l’e-mail.

1. Per includere altri utenti nell’e-mail, inserisci i loro indirizzi e-mail in `Add Email Recipients` campo separato da virgole, spazi, tabulazioni o punti e virgola.

## Riepilogo pianificazione e-mail

In `Set when to send the Email Summary` , puoi specificare quando inviare i riepiloghi e-mail. Le opzioni sono:

* `Manual`
* `Once`
* `Repeating`

### Salva riepilogo e-mail da inviare in un secondo momento

1. Seleziona `Manual` dal `Set when to send the Email Summary` campo.

1. Clic **[!UICONTROL Save]**.

   In questo modo il riepilogo viene salvato nell’elenco dei riepiloghi e-mail.

1. Quando sei pronto per inviare il riepilogo, fai clic sull’icona a forma di ingranaggio e seleziona `Send Now`.

### Invia riepilogo e-mail una volta

1. Seleziona `Once` dal `Set when to send the Email Summary` campo.

1. Specifica la data di inizio nel `Select Start Date` calendario.

1. Specifica l’ora in cui inviare l’e-mail in `Select time to send` campo.

### Crea pianificazione ripetuta

1. Seleziona `Repeating` dal `Set when to send the Email Summary` campo.

1. In `Set Frequency` campo, seleziona `Daily`, `Weekly`, o `Monthly`.

1. Specifica la data di inizio nel `Select Start Date` calendario.

1. Specifica l’ora in cui inviare l’e-mail in `Select time to send` campo.

1. (Facoltativo) Per specificare una data di fine, seleziona `End Date` e selezionare la data di fine dal calendario.

## Modifica riepilogo e-mail esistente

Dopo aver creato e salvato un riepilogo e-mail, il `Email Summaries` pagina visualizza un elenco di tutti i riepiloghi salvati. È possibile espandere (`+`) per ulteriori informazioni. Le colonne in questa visualizzazione sono:

* `Email Name` - Nome del riepilogo e-mail
* `Content` - Tipo di contenuto all’interno del riepilogo, ad esempio i nomi di eventuali rapporti. Per informazioni sull’invio di un riepilogo e-mail contenente un rapporto con dati non aggiornati, consulta [Gestione delle impostazioni dell’account](../../administrator/account-management/managing-account-settings.md).
* `Scheduled` - Frequenza, data e ora di invio del riepilogo e-mail
* `Recipients` - Destinatari del riepilogo e-mail
* `Created Date` - Data di creazione del riepilogo e-mail
* `Status` - `Paused` o `Active`

Fai clic sull’icona a forma di ingranaggio a destra di ciascuna riga per:

* `Send Now` - Invia immediatamente il riepilogo e-mail a tutti i destinatari specificati
* `Edit` - Consente di modificare i dettagli del riepilogo e-mail
* `Pause/Active` - Consente di sospendere la consegna del riepilogo dell’e-mail o di abilitare il riepilogo in base alla configurazione
* `Delete` - Elimina il riepilogo e-mail
