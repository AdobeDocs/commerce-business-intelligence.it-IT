---
title: Creare set di filtri per le metriche
description: Scopri come creare set di filtri salvati e applicarli alle metriche.
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# Creare set di filtri

Se hai più metriche in [!DNL MBI] che devono essere filtrati in modo simile (ad esempio, per filtrare gli ordini di test), puoi creare set di filtri salvati e applicarli alle metriche. Questo consente di risparmiare tempo, in quanto non è necessario aggiungere singoli filtri durante la creazione o la modifica di una metrica.

Consulta le nostre [video di formazione](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html?lang=en) per saperne di più.

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../administrator/user-management/user-management.md).

1. Fai clic su **[!DNL Manage Data** > **Filter Sets]** nella barra laterale.

   ![](../../assets/create-filter-sets.png)

1. Fai clic su **[!UICONTROL Add Filter Set]** nella parte superiore della pagina.

1. Seleziona la tabella contenente le metriche da filtrare.

   Ad esempio, se desideri filtrare il `Total number of orders` e si basa sul `orders` selezionare la tabella.

1. Assegna un nome al `Filter Set`.

1. Aggiungi tutti i filtri pertinenti.

   Ad esempio, se desideri includere solo gli ordini con uno stato di completamento nel nostro `Total number of orders` applicheremmo un filtro che esclude tutti gli ordini privi di stato = `complete`.

1. Verifica la logica del filtro e che le parentesi e gli operatori siano posizionati correttamente: ad esempio, `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   Un filtro errato è spesso la causa di discrepanze di dati tra [!DNL MBI] rapporti e risultati attesi.

1. Salva il `Filter Set`.

Dopo aver salvato un set di filtri, puoi applicarlo a qualsiasi metrica che utilizza la stessa tabella. Ad esempio, se hai creato un `Filter Set` sulla `orders` tabella, puoi applicarla a *qualsiasi metrica* costruiti su questa tabella, ad esempio `Revenue`.

>[!NOTE]
>
>`Filter Sets` può essere applicato anche alle colonne calcolate in [!DNL MBI]. Puoi richiedere di applicare un set di filtri a una dimensione dati creata in [!DNL MBI] tramite contattando il supporto.

## Correlati

* [Best practice per segmentazione e filtro](../../best-practices/segment-filter.md)
