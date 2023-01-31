---
title: Gestione delle impostazioni account
description: Scopri come personalizzare una serie di impostazioni account per il data warehouse.
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# Personalizzazione delle impostazioni account

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore.](../../administrator/user-management/user-management.md)

Nel tuo [!DNL MBI] account, è possibile personalizzare una serie di impostazioni account per il data warehouse. Per accedervi, seleziona il nome della tua organizzazione nell’angolo in alto a destra di qualsiasi schermata e fai clic su **[!UICONTROL Account Settings]** dal menu a discesa .

* **[!UICONTROL Client Name:]** Questa impostazione viene visualizzata nell’angolo in alto a destra di tutte le dashboard e altrove nell’account. Se si desidera modificare **[!UICONTROL "Vandelay Industries Co., Ltd]** a **[!UICONTROL "Vandelay]** Ecco dove farlo.

* **[!UICONTROL Currency:]** Questa è la *valuta predefinita* per tutti i valori monetari nel tuo account. Ogni volta che un valore decimale o valuta viene sincronizzato nel data warehouse, questa impostazione determina il simbolo posizionato prima di tale valore all&#39;interno dei report.

* **[!UICONTROL Blackout Hours:]** Questa impostazione assicura che, nelle ore selezionate del giorno, il data warehouse non acceda ai database connessi. Tutte le ore sono espresse a zero ore e in ora solare orientale (EST). Ad esempio, se non si desidera accedere al database di produzione tra le ore 9:00 EST e le ore 1:00 EST, digitare la seguente matrice di cifre: **9, 10, 11, 12**.

* **[!UICONTROL Forced update hours:]** Questa impostazione assicura che un aggiornamento del data warehouse inizi automaticamente nel tuo account *sull&#39;ora* hai specificato. Come per le ore di blackout, anche queste sono in ET. Ad esempio, se desideri che gli aggiornamenti di data warehouse inizino automaticamente a **mezzanotte** e **mezzogiorno** EST, digitare la seguente matrice di cifre: **0, 12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** Questa opzione indica al sistema cosa fare nelle situazioni in cui è pianificato l’invio di un riepilogo e-mail *prima dei dati in uno dei relativi rapporti* è rinfrescato fino al presente. Se scegli **No**, il tuo account salterà l’invio dell’e-mail all’ora pianificata e la invierà una volta che i tuoi dati saranno stati aggiornati. Se scegli **[!UICONTROL Yes]**, il tuo account invierà l’e-mail, includerà un messaggio che spiega che i dati sono obsoleti e invierà un’altra e-mail una volta che i tuoi dati saranno stati aggiornati.

* **[!UICONTROL Enable data updates:]** Questa opzione assicura che gli aggiornamenti dati vengano eseguiti sull’account. Se si modifica l’impostazione in **[!UICONTROL No]**, le sincronizzazioni dei dati e i calcoli delle colonne si arresteranno completamente nel tuo account.

>[!NOTE]
>
>Assicurati di selezionare **[!UICONTROL Save Customizations]** dopo aver apportato eventuali modifiche.
