---
title: Creare set di filtri per le metriche
description: Scopri come creare set di filtri salvati e applicarli alle metriche.
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# Creare set di filtri

Se hai più metriche in [!DNL MBI] che devono essere filtrati in modo simile (ad esempio, escludendo gli ordini di test), puoi creare set di filtri salvati e applicarli alle metriche. In questo modo si risparmia tempo, poiché non è necessario aggiungere singoli filtri durante la creazione o la modifica di una metrica.

Consulta la [video di formazione](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html?lang=en) per ulteriori informazioni.

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../administrator/user-management/user-management.md).

1. Clic **[!DNL Manage Data** > **Filter Sets]** nella barra laterale.

   ![](../../assets/create-filter-sets.png)

1. Clic **[!UICONTROL Add Filter Set]** nella parte superiore della pagina.

1. Seleziona la tabella contenente le metriche da filtrare.

   Ad esempio, se desideri filtrare il `Total number of orders` ed è basato su `orders` tabella, selezionare la tabella.

1. Denomina il `Filter Set`.

1. Aggiungi tutti i filtri pertinenti.

   Ad esempio, se si desidera includere solo gli ordini con lo stato completato nel `Total number of orders` metrica, si applica un filtro che esclude tutti gli ordini il cui stato non è = `complete`.

1. Verifica la logica del filtro e che le parentesi e gli operatori siano posizionati correttamente: ad esempio, `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   Un filtro errato è spesso la causa di discrepanze di dati tra [!DNL MBI] report e i risultati previsti.

1. Salva il `Filter Set`.

Dopo aver salvato un set di filtri, puoi applicarlo a qualsiasi metrica che utilizza la stessa tabella. Ad esempio, se hai creato un’ `Filter Set` il `orders` tabella, è possibile applicarla a *qualsiasi metrica* basato su questa tabella, ad esempio `Revenue`.

>[!NOTE]
>
>`Filter Sets` può essere applicato anche alle colonne calcolate in [!DNL MBI]. È possibile richiedere di applicare un set di filtri a una dimensione dati creata in [!DNL MBI] tramite contattando l’assistenza.

## Correlato

* [Best practice per la segmentazione e il filtraggio](../../best-practices/segment-filter.md)
