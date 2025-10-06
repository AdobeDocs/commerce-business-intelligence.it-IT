---
title: Creare set di filtri per le metriche
description: Scopri come creare set di filtri salvati e applicarli alle metriche.
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Creare set di filtri

Se in [!DNL Commerce Intelligence] sono presenti più metriche che devono essere filtrate in modo simile (ad esempio, filtrare gli ordini di test), è possibile creare set di filtri salvati e applicarli alle metriche. In questo modo si risparmia tempo, poiché non è necessario aggiungere singoli filtri durante la creazione o la modifica di una metrica.

Per ulteriori informazioni, consulta il [video di formazione](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html?lang=it).

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../administrator/user-management/user-management.md).

1. Fare clic su **[!DNL Manage Data** > **Filter Sets]** nella barra laterale.

   ![Crea un&#39;interfaccia per set di filtri con l&#39;opzione Aggiungi set di filtri](../../assets/create-filter-sets.png)

1. Fai clic su **[!UICONTROL Add Filter Set]** nella parte superiore della pagina.

1. Seleziona la tabella contenente le metriche da filtrare.

   Ad esempio, se desideri filtrare la metrica `Total number of orders` e questa è basata sulla tabella `orders`, seleziona tale tabella.

1. Denomina `Filter Set`.

1. Aggiungi tutti i filtri pertinenti.

   Ad esempio, se desideri includere nella metrica `Total number of orders` solo gli ordini con lo stato completato, applicherai un filtro che esclude tutti gli ordini il cui stato non è = `complete`.

1. Verificare la logica del filtro e che le parentesi e gli operatori siano posizionati correttamente, ad esempio `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   Un filtro errato è spesso la causa delle discrepanze di dati tra i report [!DNL Commerce Intelligence] e i risultati previsti.

1. Salva `Filter Set`.

Dopo aver salvato un set di filtri, puoi applicarlo a qualsiasi metrica che utilizza la stessa tabella. Ad esempio, se hai creato un `Filter Set` nella tabella `orders`, puoi applicarlo a *qualsiasi metrica* creata in questa tabella, ad esempio `Revenue`.

>[!NOTE]
>
>`Filter Sets` può essere applicato anche alle colonne calcolate in [!DNL Commerce Intelligence]. È possibile richiedere di applicare un set di filtri a una dimensione dati creata in [!DNL Commerce Intelligence] tramite il supporto tecnico.

## Correlato

* [Best practice per la segmentazione e il filtraggio](../../best-practices/segment-filter.md)
