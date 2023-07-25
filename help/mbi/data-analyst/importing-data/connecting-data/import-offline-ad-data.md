---
title: Importare altri dati sulla spesa pubblicitaria
description: Scopri come importare i dati offline o di altri annunci in [!DNL Commerce Intelligence].
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Importare altri dati sulla spesa pubblicitaria

Il caricamento dei dati sulla spesa pubblicitaria consente di misurare il ROI della campagna sposando i costi pubblicitari e `customer lifetime value (CLV)` degli utenti acquisiti dalle campagne.

## Caricamento dei dati sui costi della pubblicità

Il primo passaggio nell’analisi dei dati relativi ad annunci spesi è ottenere i dati. Poiché la maggior parte delle piattaforme pubblicitarie ti consentono di esportare rapporti, Adobe consiglia di esportare i dati non elaborati dalla piattaforma di annunci e caricarli direttamente in [!DNL Commerce Intelligence] senza alcuna manipolazione. Puoi eseguire operazioni sui dati presenti nella Data Warehouse, quindi non è necessario raddoppiare gli sforzi.

Dopo aver esportato i dati sulla spesa pubblicitaria, utilizza [`File Upload` funzionalità](../connecting-data/using-file-uploader.md) per inserire i dati nella Data Warehouse. Puoi caricare nuovi dati nello stesso [!DNL Commerce Intelligence] tabella nel tempo.

## Origini offline

Oltre alle campagne online, è possibile che siano presenti anche annunci non in linea, ad esempio alla radio o su un cartellone pubblicitario. Per tenere conto di questi casi, puoi caricare manualmente un foglio di calcolo con i dati dei costi in [!DNL Commerce Intelligence].

La struttura della tabella illustrata di seguito è consigliata per la creazione di un `.csv` file per registrare i dati relativi alle spese pubblicitarie. Nella parte inferiore di questo argomento viene inoltre allegato un file modello da utilizzare come esempio. Le colonne consigliate sono:

* `ID` : identificatore univoco per ogni riga di dati utilizzata dal database come chiave primaria. Deve essere diverso per ogni riga.
* `Date` : data di esecuzione della campagna, in formato aaaa-mm-gg.
* `Amount` - Questo è l&#39;importo speso per la campagna.
* `campaign` - Nome della campagna. Se sta usando [!DNL Google Analytics] per tenere traccia degli altri dati sulla spesa pubblicitaria, questi devono corrispondere al nome utm\_campaign.
* `source` - Nome di origine. Se sta usando [!DNL Google Analytics], deve corrispondere al `utm_source` nome.
* `other` (Facoltativo) - Puoi anche incorporare colonne aggiuntive che ti aiutano a segmentare campagne e costi. Può anche essere un modo per riepilogare diversi nomi di campagne UTM diversi in un’unica campagna coerente a scopo di tracciamento. Invece di impostarlo manualmente, potrebbe essere utile utilizzare una ricerca V in un secondo foglio per far corrispondere ogni nome della campagna all’altro nome e segnalarlo qui in modo dinamico.

## Correlato

* [Connetti [!DNL AdWords] dati](../integrations/google-adwords.md)
* [Aumentare il ROI nelle campagne pubblicitarie](../../analysis/roi-ad-camp.md)
