---
title: Modifica in serie dei grafici nei dashboard
description: Scopri come utilizzare la funzione di modifica in serie in [!DNL Commerce Intelligence].
exl-id: 576ffabb-5e5d-4251-9662-951e2cd30f31
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
TQID: 'https://experienceleague.adobe.com/FcFTKq9TvldFwo7nl-bGRyup1uxscjrnOutJcA-h-5c'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: 06e518d4-11ae-5c20-98b0-ce8ab05d7166
    internal-label: Dashboards
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%
---
# Modifica in serie dei grafici nei dashboard

La funzione di modifica in serie consente di modificare facilmente i nomi dei grafici e le date nei dashboard. Ad esempio, si desidera che tutti i grafici di un dashboard specifico facciano riferimento a un singolo store e a un report su base mensile anziché trimestrale. Anziché modificare tutto manualmente, lasciare che la funzionalità `bulk-editing` esegua il lavoro. In questo argomento imparerai a utilizzare:

* [Funzionalità  [!DNL Find/Replace] ](#findreplace)

* [Funzionalità  [!DNL Prepend Name] ](#prepend)

* [Funzionalità  [!DNL Change Dates] ](#dates)

Detto questo, considera questo - *Queste modifiche devono essere permanenti?* In caso contrario, è consigliabile clonare il dashboard e quindi modificare le date nel nuovo dashboard. In questo modo è possibile mantenere il dashboard originale senza interrompere le modifiche necessarie.

>[!NOTE]
>
>Se stai modificando numerosi rapporti, il processo di aggiornamento potrebbe richiedere un po’ di tempo.

## Utilizzo di [!DNL Find/Replace] {#findreplace}

1. Fai clic sull&#39;icona a forma di ingranaggio (![icona ingranaggio](../../assets/gear-icon.png)) accanto al nome del dashboard, quindi sulla finestra [!UICONTROL Bulk Edit Reports].

1. Fare clic su **[!UICONTROL Chart Title Find and Replace]** nel popup.

1. Nel campo `Chart Title Find` digitare le parole o i caratteri che si desidera trovare.

1. Nel campo `Replace With` digitare le parole o i caratteri che devono sostituire il contenuto del campo `Find`.

1. Fare clic su **[!UICONTROL Update Reports]**.

Esempio:

![modifica in blocco](../../assets/bulk_edit.gif)

## Anteprima di `Chart Names` {#prepend}

1. Fai clic sull&#39;icona a forma di ingranaggio (![icona ingranaggio](../../assets/gear-icon.png)) accanto al nome del dashboard, quindi sulla finestra [!UICONTROL Bulk Edit Reports].

1. Fare clic su **[!UICONTROL Prepend Report Names]** nel popup.

1. Digitare le parole o i caratteri con cui si desidera anteporre i grafici.

1. Fare clic su **[!UICONTROL Update Reports]**.

Esempio:

![aggiungi](../../assets/prepend.gif)

## Modifica di `Dates` {#dates}

1. Fai clic sull&#39;icona a forma di ingranaggio (![icona ingranaggio](../../assets/gear-icon.png)) accanto al nome del dashboard, quindi seleziona la finestra [!UICONTROL Bulk Edit Reports].

1. Fare clic su **[!UICONTROL Change Dates]** nella finestra popup.

1. Imposta i nuovi `Start/End Date` e `Time Interval`. È inoltre possibile lasciare invariati questi campi.

1. Fare clic su **[!UICONTROL Update Reports]**.

Esempio:

![modifica date](../../assets/dates.gif)
