---
title: Riduci la durata del ciclo di aggiornamento
description: Scopri come ridurre la durata del ciclo di aggiornamento.
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
role: Admin, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '398'
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
