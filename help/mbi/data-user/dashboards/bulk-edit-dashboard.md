---
title: Modifica in serie dei grafici nei dashboard
description: Scopri come utilizzare la funzione di modifica in serie in [!DNL MBI].
exl-id: 576ffabb-5e5d-4251-9662-951e2cd30f31
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Modifica in serie dei grafici nei dashboard

La funzione di modifica in serie consente di modificare facilmente i nomi dei grafici e le date nei dashboard. Ad esempio, si desidera che tutti i grafici di un dashboard specifico facciano riferimento a un singolo store e a un report su base mensile anziché trimestrale. Invece di modificare tutto manualmente, lasciare che `bulk-editing` funzionalità per eseguire il lavoro. In questo articolo imparerai a utilizzare:

* [Il ](#findreplace)

* [Il ](#prepend)

* [Il ](#dates)

Detto questo, considera questo - *Queste modifiche devono essere permanenti?* In caso contrario, è consigliabile clonare il dashboard e quindi modificare le date nel nuovo dashboard. In questo modo è possibile mantenere il dashboard originale senza interrompere le modifiche necessarie.

>[!NOTE]
>
>Se stai modificando numerosi rapporti, il processo di aggiornamento potrebbe richiedere un po’ di tempo.

## Utilizzo di `Find/Replace` {#findreplace}

1. Fare clic sull&#39;ingranaggio (![](../../assets/gear-icon.png)) accanto al nome del dashboard, quindi il [!UICONTROL Bulk Edit Reports] finestra.

1. Clic **[!UICONTROL Chart Title Find and Replace]** nella finestra popup.

1. In `Chart Title Find` digitare le parole o i caratteri che si desidera trovare.

1. In `Replace With` digitare le parole o i caratteri che devono sostituire i caratteri contenuti nel campo `Find` campo.

1. Clic **[!UICONTROL Update Reports]**.

Esempio:

![modifica collettiva](../../assets/bulk_edit.gif)

## Anteprima `Chart Names` {#prepend}

1. Fare clic sull&#39;ingranaggio (![](../../assets/gear-icon.png)) accanto al nome del dashboard, quindi il [!UICONTROL Bulk Edit Reports] finestra.

1. Clic **[!UICONTROL Prepend Report Names]** nella finestra popup.

1. Digitare le parole o i caratteri con cui si desidera anteporre i grafici.

1. Clic **[!UICONTROL Update Reports]**.

Esempio:

![anticipare](../../assets/prepend.gif)

## Modifica `Dates` {#dates}

1. Fare clic sull&#39;ingranaggio (![](../../assets/gear-icon.png)) accanto al nome del dashboard, quindi seleziona la `!UICONTROL Bulk Edit Reports` finestra.

1. Clic **[!UICONTROL Change Dates]** nella finestra popup.

1. Imposta il nuovo `Start/End Date` e `Time Interval`. È inoltre possibile lasciare invariati questi campi.

1. Clic **[!UICONTROL Update Reports]**.

Esempio:

![modifica delle date](../../assets/dates.gif)
