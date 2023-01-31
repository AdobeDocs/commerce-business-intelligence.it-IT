---
title: Creazione di riepiloghi e-mail automatizzati
description: Scopri come creare riepiloghi e-mail automatizzati.
exl-id: a9aea4fc-9193-467f-8554-3ad77ac3fa73
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Creazione di riepiloghi e-mail automatizzati

I riepiloghi e-mail sono un potente strumento di comunicazione che consente di condividere lo stato attuale e le tendenze della tua attività con i principali soggetti interessati. Con i riepiloghi e-mail puoi:

* Riepilogo grafico e-mail che includono rapporti
* Includi o escludi l’autore del riepilogo e-mail dalla ricezione dell’e-mail
* Pianifica quando l’e-mail viene inviata
* Modificare, eliminare e mettere in pausa i riepiloghi e-mail pianificati esistenti

## Crea nuovo riepilogo e-mail

1. Fai clic su **[!DNL Manage Data]** then **[!UICONTROL Email Summary]** nella barra laterale.

   Se si tratta della prima volta che si crea un riepilogo e-mail, questa pagina non visualizza alcun riepilogo salvato.

1. Fai clic su **[!UICONTROL Create New Email Summary]** nell&#39;angolo in alto a destra.

1. Immettere un nome per il riepilogo.

   Scegli un nome che trasmetta ciò che è incluso nel riepilogo. Ad esempio: `AOV Comparison`.

1. In `Choose Content` seleziona i report da includere nel riepilogo.

   Puoi selezionare fino a 10 rapporti di tua proprietà. Dopo aver selezionato un rapporto, utilizza le icone visualizzate per selezionare se desideri che venga inviato come tabella o grafico. Se il rapporto è stato salvato come numero, è possibile inviarlo solo come numero. Per informazioni sull’invio di un riepilogo e-mail contenente un rapporto con dati non aggiornati, consulta [Gestione delle impostazioni account](../../administrator/account-management/managing-account-settings.md).

   >[!NOTE]
   >
   >`Cohort` i rapporti sono disponibili solo se utilizzi la nuova architettura.

1. (Facoltativo) Seleziona `Send Email To Me` se desideri ricevere l’e-mail.

1. Per includere altri utenti nell’e-mail, inserisci i loro indirizzi e-mail nel `Add Email Recipients` campi separati da virgole, spazi, tabulazioni o punti e virgola.

## Pianifica riepilogo e-mail

In `Set when to send the Email Summary` Puoi specificare quando inviare i riepiloghi delle e-mail. Le opzioni sono:

* `Manual`
* `Once`
* `Repeating`

### Salva riepilogo e-mail da inviare in un secondo momento

1. Seleziona `Manual` dal `Set when to send the Email Summary` campo .

1. Fai clic su **[!UICONTROL Save]**.

   Il riepilogo viene salvato nell’elenco dei riepiloghi delle e-mail.

1. Quando sei pronto per inviare il riepilogo, fai clic sull’icona a forma di ingranaggio e seleziona `Send Now`.

### Invia riepilogo e-mail una volta

1. Seleziona `Once` dal `Set when to send the Email Summary` campo .

1. Specifica la data di inizio nella `Select Start Date` calendario.

1. Specifica l’ora in cui inviare l’e-mail nella `Select time to send` campo .

### Crea pianificazione ripetuta

1. Seleziona `Repeating` dal `Set when to send the Email Summary` campo .

1. In `Set Frequency` campo , seleziona `Daily`, `Weekly`oppure `Monthly`.

1. Specifica la data di inizio nella `Select Start Date` calendario.

1. Specifica l’ora in cui inviare l’e-mail nella `Select time to send` campo .

1. (Facoltativo) Per specificare una data di fine, seleziona `End Date` e selezionare la data di fine dal calendario.

## Modifica riepilogo e-mail esistente

Dopo aver creato e salvato un riepilogo e-mail, il `Email Summaries` visualizza un elenco di tutti i riepiloghi salvati. Puoi espandere (`+`) per ulteriori informazioni. Le colonne di questa visualizzazione sono:

* `Email Name` - Nome del riepilogo e-mail
* `Content` - Tipo di contenuto nel riepilogo, ad esempio i nomi di eventuali rapporti. Per informazioni sull’invio di un riepilogo e-mail contenente un rapporto con dati non aggiornati, consulta [Gestione delle impostazioni account](../../administrator/account-management/managing-account-settings.md).
* `Scheduled` - Frequenza, data e ora di invio del riepilogo e-mail
* `Recipients` - Destinatari del riepilogo e-mail
* `Created Date` - Data di creazione del riepilogo e-mail
* `Status` - `Paused` o `Active`

Fai clic sull’icona a forma di ingranaggio a destra di ogni riga per:

* `Send Now` - Invia immediatamente il riepilogo delle e-mail a tutti i destinatari specificati
* `Edit` - Consente di modificare i dettagli del riepilogo e-mail
* `Pause/Active` - Consente di sospendere la consegna del riepilogo e-mail o di abilitare il riepilogo in base alla configurazione
* `Delete` - Elimina il riepilogo e-mail
