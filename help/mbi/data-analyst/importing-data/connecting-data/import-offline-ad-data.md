---
title: Importare altri dati sulla spesa pubblicitaria
description: Scopri come importare i dati di spesa degli annunci offline o di altro tipo in  [!DNL Commerce Intelligence].
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Importare altri dati sulla spesa pubblicitaria

Il caricamento dei dati sulla spesa pubblicitaria ti consente di misurare il ROI della campagna sposando il costo pubblicitario e il `customer lifetime value (CLV)` degli utenti acquisiti dalle campagne.

## Caricamento dei dati sui costi della pubblicità

Il primo passaggio nell’analisi dei dati relativi ad annunci spesi è ottenere i dati. Poiché la maggior parte delle piattaforme pubblicitarie ti consente di esportare rapporti, Adobe consiglia di esportare i dati non elaborati dalla piattaforma pubblicitaria e caricarli direttamente in [!DNL Commerce Intelligence] senza alcuna manipolazione. Puoi eseguire operazioni sui dati presenti nella Data Warehouse, quindi non è necessario raddoppiare gli sforzi.

Dopo aver esportato i dati di spesa dell&#39;annuncio, utilizzare la funzionalità [`File Upload`](../connecting-data/using-file-uploader.md) per inserire i dati nella Data Warehouse. Nel tempo è possibile caricare nuovi dati nella stessa tabella [!DNL Commerce Intelligence].

## Origini offline

Oltre alle campagne online, è possibile che siano presenti anche annunci non in linea, ad esempio alla radio o su un cartellone pubblicitario. Per tenere conto di questi casi, è possibile caricare manualmente un foglio di calcolo con i dati dei costi in [!DNL Commerce Intelligence].

La struttura della tabella illustrata di seguito è consigliata per la creazione di un file `.csv` per la registrazione dei dati di spesa degli annunci. Nella parte inferiore di questo argomento viene inoltre allegato un file modello da utilizzare come esempio. Le colonne consigliate sono:

* `ID` - Identificatore univoco per ogni riga di dati utilizzata dal database come chiave primaria. Deve essere diverso per ogni riga.
* `Date` - Data di esecuzione della campagna, in formato aaaa-mm-gg.
* `Amount` - Questo è l&#39;importo speso per la campagna.
* `campaign` - Nome della campagna. Se utilizzi [!DNL Google Analytics] per tenere traccia degli altri dati sulla spesa pubblicitaria, deve corrispondere al nome utm\_campaign.
* `source` - Questo è il nome di origine. Se utilizzi [!DNL Google Analytics], deve corrispondere al nome `utm_source`.
* `other` (facoltativo) - Puoi anche incorporare colonne aggiuntive per segmentare campagne e costi. Può anche essere un modo per riepilogare diversi nomi di campagne UTM diversi in un’unica campagna coerente a scopo di tracciamento. Invece di impostarlo manualmente, potrebbe essere utile utilizzare una ricerca V in un secondo foglio per far corrispondere ogni nome della campagna all’altro nome e segnalarlo qui in modo dinamico.

## Correlato

* [Connetti [!DNL AdWords]  dati](../integrations/google-adwords.md)
* [Aumentare il ROI nelle campagne pubblicitarie](../../analysis/roi-ad-camp.md)
