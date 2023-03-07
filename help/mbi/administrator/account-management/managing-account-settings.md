---
title: Gestione delle impostazioni dell'account
description: Scopri come personalizzare le impostazioni dell’account per la tua Data Warehouse.
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# Personalizzazione delle impostazioni dell&#39;account

>[!NOTE]
>
>Richiede [Autorizzazioni di amministrazione.](../../administrator/user-management/user-management.md)

Nel tuo [!DNL MBI] dell&#39;account, è possibile personalizzare le impostazioni dell&#39;account per la Data Warehouse. Per accedervi, seleziona il nome della tua organizzazione nell’angolo in alto a destra di qualsiasi schermata, quindi scegli **[!UICONTROL Account Settings]** dal menu a discesa.

* **[!UICONTROL Client Name:]** Questa impostazione viene visualizzata nell’angolo in alto a destra di tutte le dashboard e altrove nell’account. Se desideri modificare **[!UICONTROL "Vandelay Industries Co., Ltd]** a semplicemente **[!UICONTROL "Vandelay]**, ecco dove farlo.

* **[!UICONTROL Currency:]** Questo è il *valuta predefinita* per tutti i valori monetari nel tuo account. Ogni volta che un valore decimale o di valuta viene sincronizzato nella Data Warehouse, questa impostazione determina il simbolo posizionato prima di tale valore all’interno dei rapporti.

* **[!UICONTROL Blackout Hours:]** Questa impostazione garantisce che, durante le ore selezionate della giornata, la Data Warehouse non acceda ai database connessi. Tutte le ore sono espresse a ora zero e nell’ora solare orientale (EST). Ad esempio, se non si desidera accedere al database di produzione tra le ore 9:00 EST e le ore 13:00 EST, digitare la seguente matrice di cifre: **9, 10, 11, 12**.

* **[!UICONTROL Forced update hours:]** Questa impostazione assicura l&#39;avvio automatico di un aggiornamento della Data Warehouse nell&#39;account *durante le ore* hai specificato. Come per le ore di sospensione attività, anche queste sono in ET. Ad esempio, se desideri che gli aggiornamenti di Data Warehouse inizino automaticamente alle **mezzanotte** e **mezzanotte** EST, digitare la seguente matrice di cifre: **0, 12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** Questa opzione gestisce le situazioni in cui è pianificato l’invio di un riepilogo e-mail *prima dei dati in uno dei suoi rapporti* viene aggiornato. Se si sceglie **No**, il tuo account non invierà l’e-mail all’ora pianificata. Al contrario, il tuo account lo invia una volta che i dati sono stati aggiornati. Se si sceglie **[!UICONTROL Yes]**, il tuo account invia l’e-mail, include un messaggio che spiega che i dati non sono aggiornati e invia un’altra e-mail dopo l’aggiornamento dei dati.

* **[!UICONTROL Enable data updates:]** Questa opzione garantisce che gli aggiornamenti dei dati vengano eseguiti sul tuo account. Se si modifica l&#39;impostazione in **[!UICONTROL No]**, le sincronizzazioni dei dati e i calcoli delle colonne si interrompono nell’account.

>[!NOTE]
>
>Assicurati di selezionare **[!UICONTROL Save Customizations]** dopo aver apportato eventuali modifiche.
