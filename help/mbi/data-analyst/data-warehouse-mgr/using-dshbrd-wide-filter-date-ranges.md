---
title: Filtro a livello di dashboard
description: Scopri come apportare modifiche in blocco a tutti i rapporti su un dashboard specifico.
exl-id: 379d0027-8a7a-4062-a66a-4f06c37b806c
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# Filtro a livello di dashboard

Con il filtro a livello di dashboard, puoi apportare modifiche in blocco a tutti i rapporti su un dashboard specifico. Puoi visualizzare rapidamente la stessa analisi per diversi periodi di tempo o per diversi store. Puoi confrontare facilmente le prestazioni di un anno, mese o settimana precedente per negozio. Puoi aggiornare un’intera dashboard per adattarla a una nuova campagna avviata.

## Filtri per data

Per modificare l’intervallo di date o l’intervallo di rapporti su un dashboard, fai clic sull’icona del calendario nell’angolo in alto a destra (![calendario](../../assets/calendar-button.png)).

È possibile scegliere di visualizzare i dati utilizzando un `Fixed Date Range` o vari pre-calcolati `Moving Date Ranges`:

![spostamento di intervalli di date](../../assets/moving_date_ranges.png)

Il `Last Full...` le opzioni di spostamento rappresentano l&#39;ultimo intervallo completato, mentre `This...` è l&#39;intervallo corrente in corso. Ad esempio, se è Giugno, il `Last Full Month` è _1 maggio - 31 maggio_, mentre `This Month` è _1 giugno - Ora_.

Oppure crea il tuo `Custom Moving Range`\:

![intervallo di spostamento personalizzato](../../assets/custom-moving-range.png)

Scegli di modificare anche l’intervallo. Selezione del pulsante predefinito (![intervallo di tempo predefinito](../../assets/time_interval_default.png)) significa che cambia solo l’intervallo di date:

![intervallo di tempo](../../assets/time_interval.png)

Per ripristinare l’intervallo e l’intervallo di date iniziali di tutti i rapporti, fai clic su **[!UICONTROL Restore Defaults]** o fai clic su **[!UICONTROL Cancel]**.

Quando si specifica un filtro data per un dashboard, tale filtro viene applicato solo a tale dashboard. Non viene applicato quando si passa ad altre dashboard.

>[!NOTE]
>
>Attualmente, `Cohort Reports` e `SQL Reports` non sono inclusi quando si applicano modifiche a livello di dashboard.

## Filtri store

Per analizzare le prestazioni di un negozio specifico, fai clic sull’icona dei negozi nell’angolo in alto a destra (![Filtro store](../../assets/store-filter.png)). Per impostazione predefinita, `Store Filter` è impostato su `All Stores`, che visualizza i dati di tutti [visualizzazioni store](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-views.html) disponibili nel sito Commerce.

>[!NOTE]
>
>Un filtro store è abilitato o disabilitato per un intero [!DNL Commerce Intelligence] account. Se un dashboard contiene rapporti che non sono interessati dal filtro (ad esempio rapporti che non sono generati su [!DNL Adobe Commerce] ), questi rapporti non vengono aggiornati quando viene applicato il filtro store. È possibile [contatta l’assistenza](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) se ritieni che un rapporto debba essere aggiornato in base alla selezione dello store o se ritieni che il filtro dello store dell’account sia disabilitato per errore.

Quando selezioni uno store da `Store Filter`, il filtro mantiene la selezione quando ci si sposta tra le dashboard. Mantenere la selezione consente di visualizzare ovunque i dati per lo store selezionato fino a quando non si seleziona `All Stores`.

## Filtri per dashboard condivisi

Per le dashboard condivise, se un utente configura il filtro data, gli altri utenti con accesso al dashboard visualizzano lo stesso filtro applicato. Tuttavia, il filtro store non si applica in questo caso. Se il proprietario del dashboard configura il filtro store e condivide il dashboard, il filtro store configurato non persiste per un altro utente. Un utente deve avere [modifica accesso](../../data-user/dashboards/share-dashboard-with-users.md) a un dashboard per regolare i filtri del dashboard.
