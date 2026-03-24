---
title: Riduci la durata del ciclo di aggiornamento
description: Scopri come ridurre la durata del ciclo di aggiornamento.
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
role: Admin, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager, Dashboards
TQID: https://experienceleague.adobe.com/DFlzL9E95teiWI31j7qWRU8Ab6GkbFX7iPPdaxGq48A
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 398
ht-degree: 0%

---

# Riduzione del tempo di elaborazione del ciclo di aggiornamento

[!DNL Adobe Commerce Intelligence] si sincronizza con il tuo database nel corso della giornata per replicare nuovi dati, assicurandosi che le tue dashboard mostrino sempre le informazioni più recenti.

A un tempo di aggiornamento già lungo possono aggiungersi molti fattori. Alcuni metodi di replica, frequenze di ricontrollo più elevate e il numero di dashboard e grafici sono solo alcuni dei contributi. In questi argomenti vengono illustrate alcune best practice per ridurre i tempi di aggiornamento.

## Diminuisci frequenza di ricontrollo

In una tabella di database possono essere presenti colonne di dati con valori modificabili. Ad esempio, in una tabella **orders** potrebbe essere presente una colonna denominata **status**. Quando un ordine viene scritto inizialmente nel database, la colonna di stato potrebbe contenere il valore `pending`. L&#39;ordine è replicato nel tuo [Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md) con questo valore `pending`.

Le colonne modificabili devono essere [ricontrollate per verificare la presenza di valori aggiornati](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) nel tempo. Per impostazione predefinita, [!DNL Commerce Intelligence] ricontrolla queste colonne durante ogni aggiornamento, ma se è presente una grande quantità di dati da ricontrollare e replicare, questo può influire negativamente sul tempo di aggiornamento. Invece di eseguire nuovi controlli durante ogni aggiornamento, Adobe consiglia di impostare la frequenza di nuovi controlli su giornaliera, settimanale o mensile.

## Utilizzare i metodi di replica incrementali

Come accennato in precedenza, i tempi di aggiornamento lunghi sono direttamente correlati alla quantità di dati da ricontrollare e replicare. [I metodi di replica incrementali](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) possono ridurre notevolmente la quantità di dati elaborati durante il ciclo di aggiornamento. Se possibile, Adobe consiglia di utilizzare questi metodi o di modificare il database per supportare un metodo incrementale.

## Rimuovere i grafici inutilizzati dai dashboard

Al termine del ciclo di aggiornamento, [!DNL Commerce Intelligence] esegue un&#39;operazione cache per tutti i grafici. Una cache memorizza i dati in modo che le richieste future di informazioni possano essere completate più rapidamente. In [!DNL Commerce Intelligence], ciò significa che i dashboard vengono caricati rapidamente perché non è necessario che i grafici eseguano query sui dati ogni volta che vengono caricati.

Poiché [!DNL Commerce Intelligence] esegue solo operazioni di cache per i grafici presenti in un dashboard, la rimozione dei grafici inutilizzati dai dashboard riduce il tempo di aggiornamento. Tieni presente che lo stesso grafico potrebbe trovarsi in più dashboard. Rivolgiti al team per assicurarti che siano stati rimossi anche eventuali grafici non utilizzati.

>[!NOTE]
>
>La rimozione dei grafici dal dashboard non comporta l&#39;eliminazione del grafico. Puoi [aggiungerlo nuovamente in qualsiasi momento](../data-user/dashboards/add-charts-dashboard.md).

## Ottimizzazione del database per l&#39;analisi

Oltre a rivalutare le frequenze di ricontrollo, i metodi di replica e l&#39;utilità dei grafici, è anche possibile [ottimizzare il database per l&#39;analisi](../best-practices/opt-db-analysis.md).

## Ritorno a capo

Se il tempo di aggiornamento sembra ancora lento anche dopo l&#39;implementazione di queste raccomandazioni, [contatta il team di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
