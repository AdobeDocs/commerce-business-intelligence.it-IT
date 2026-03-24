---
title: Creare set di filtri per le metriche
description: Scopri come creare set di filtri salvati e applicarli alle metriche.
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/Y3SA-ypB62c0mwZ6uqAOQUyrISc5Tu8yqClrGwXspoU
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 277
ht-degree: 0%

---

# Creare set di filtri

Se in [!DNL Commerce Intelligence] sono presenti più metriche che devono essere filtrate in modo simile (ad esempio, filtrare gli ordini di test), è possibile creare set di filtri salvati e applicarli alle metriche. In questo modo si risparmia tempo, poiché non è necessario aggiungere singoli filtri durante la creazione o la modifica di una metrica.

Per ulteriori informazioni, consulta il [video di formazione](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html).

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
