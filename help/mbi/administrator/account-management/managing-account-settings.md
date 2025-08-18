---
title: Gestione delle impostazioni dell'account
description: Scopri come personalizzare le impostazioni del tuo account per Data Warehouse.
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
role: Admin, User
feature: Accounts
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Personalizzazione delle impostazioni dell&#39;account

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore.](../../administrator/user-management/user-management.md)

Nel tuo account [!DNL Commerce Intelligence], puoi personalizzare le impostazioni del tuo account per Data Warehouse. Per accedervi, seleziona il nome della tua organizzazione nell&#39;angolo superiore destro di qualsiasi schermata, quindi scegli **[!UICONTROL Account Settings]** dal menu a discesa.

* **[!UICONTROL Client Name:]** Questa impostazione viene visualizzata nell&#39;angolo superiore destro di tutte le dashboard e altrove nell&#39;account. Se desideri modificare **[!UICONTROL "Vandelay Industries Co., Ltd]** in solo **[!UICONTROL "Vandelay]**, è qui che devi farlo.

* **[!UICONTROL Currency:]** Questa è la *valuta predefinita* per tutti i valori monetari nel tuo account. Ogni volta che un valore decimale o di valuta viene sincronizzato nel Data Warehouse, questa impostazione determina il simbolo posizionato prima di tale valore all’interno dei rapporti.

* **[!UICONTROL Blackout Hours:]** Questa impostazione garantisce che, durante le ore selezionate della giornata, Data Warehouse non acceda ai database connessi. Tutte le ore sono espresse a ora zero e nell’ora solare orientale (EST). Se ad esempio non si desidera accedere al database di produzione tra le ore 9:00 a.m. EST e 1:00 a.m. EST, digitare la seguente matrice di cifre: **9, 10, 11, 12**.

* **[!UICONTROL Forced update hours:]** Questa impostazione garantisce l&#39;avvio automatico di un aggiornamento di Data Warehouse nell&#39;account *durante le ore* specificate. Come per le ore di sospensione attività, anche queste sono in ET. Se ad esempio si desidera che gli aggiornamenti di Data Warehouse inizino automaticamente alle **mezzanotte** e alle **mezzogiorno** EST, digitare la seguente matrice di cifre: **0, 12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** Questa opzione gestisce le situazioni in cui è pianificato l&#39;invio di un riepilogo e-mail *prima dell&#39;aggiornamento dei dati in uno dei report*. Se scegli **No**, il tuo account non invierà l&#39;e-mail all&#39;ora pianificata. Al contrario, il tuo account lo invia una volta che i dati sono stati aggiornati. Se scegli **[!UICONTROL Yes]**, il tuo account invia l&#39;e-mail, include un messaggio in cui viene spiegato che i dati non sono aggiornati e invia un&#39;altra e-mail dopo l&#39;aggiornamento dei dati.

* **[!UICONTROL Enable data updates:]** Questa opzione garantisce che gli aggiornamenti dei dati vengano eseguiti sul tuo account. Se si modifica l&#39;impostazione in **[!UICONTROL No]**, le sincronizzazioni dei dati e i calcoli delle colonne si interrompono nell&#39;account.

>[!NOTE]
>
>Assicurati di selezionare **[!UICONTROL Save Customizations]** dopo aver apportato eventuali modifiche.
