---
title: Importare altri dati di spesa degli annunci
description: Scopri come importare dati offline o di altra spesa pubblicitaria in [!DNL MBI].
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Importare altri dati di spesa degli annunci

Il caricamento dei dati di spesa pubblicitaria consente di misurare il ROI della campagna sposando i costi pubblicitari e il cliente `lifetime value (CLV)` degli utenti acquisiti dalle campagne.

## Caricamento dei dati dei costi pubblicitari

Il primo passo nell’analisi dei dati di spesa degli annunci consiste nell’ottenere i dati. Poiché la maggior parte delle piattaforme pubblicitarie consente di esportare i rapporti, ti consigliamo di esportare i dati non elaborati dalla piattaforma di annunci e di caricarli direttamente in [!DNL MBI] senza alcuna manipolazione. È possibile eseguire operazioni sui dati nel data warehouse, in modo da non dover raddoppiare gli sforzi.

Dopo aver esportato i dati di spesa dell’annuncio, utilizza il [`File Upload` caratteristica](../connecting-data/using-file-uploader.md) per inserire i dati nel data warehouse. Puoi caricare nuovi dati sullo stesso [!DNL MBI] tabella nel tempo.

## Origini offline

Oltre alle tue campagne online, potresti avere anche annunci offline, come alla radio o su un cartellone. Per tenere conto di questi casi, puoi caricare manualmente un foglio di calcolo con i dati dei costi in [!DNL MBI].

La struttura della tabella illustrata di seguito è consigliata durante la creazione di un `.csv` per registrare e spendere i dati. Un file modello viene allegato anche nella parte inferiore di questo articolo per fungere da esempio. Le colonne consigliate sono:

* `ID` - Identificatore univoco per ogni riga di dati utilizzata dal database come chiave primaria. Questo deve essere diverso per ogni riga.
* `Date` - Data di esecuzione della campagna, in formato aaaa-mm-gg.
* `Amount` - Importo speso per la campagna.
* `campaign` - Nome della campagna. Se utilizzi [!DNL Google Analytics] per tenere traccia degli altri dati di spesa degli annunci, deve corrispondere al nome utm\_campaign.
* `source` - Nome di origine. Se utilizzi [!DNL Google Analytics], dovrebbe corrispondere a `utm_source` nome.
* `other` (Facoltativo) - Puoi anche incorporare colonne aggiuntive che ti aiuteranno a segmentare campagne e costi. Può anche essere un modo per riassumere diversi nomi di campagne UTM diversi in un’unica campagna coerente a scopo di tracciamento. Anziché impostarlo manualmente, potrebbe essere utile utilizzare una ricerca V in un secondo foglio per far corrispondere ogni Nome campagna all’Altro Nome e generare qui rapporti dinamici.

## Correlati

* [Connetti [!DNL AdWords] dati](../integrations/google-adwords.md)
* [Aumentare il ROI delle campagne pubblicitarie](../../analysis/roi-ad-camp.md)
