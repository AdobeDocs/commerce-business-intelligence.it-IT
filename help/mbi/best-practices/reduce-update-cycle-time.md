---
title: Riduzione del tempo del ciclo di aggiornamento
description: Scopri come ridurre il tempo del ciclo di aggiornamento.
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---

# Riduzione del tempo di elaborazione del ciclo di aggiornamento

[!DNL MBI] sincronizza con il database durante l’intera giornata per replicare nuovi dati, in modo che le dashboard mostrino sempre le informazioni più recenti.

Molti fattori possono essere aggiunti a un tempo di aggiornamento già lungo. Alcuni metodi di replica, frequenze di ricontrollo più elevate e il numero di dashboard e grafici sono solo alcuni collaboratori. In questi argomenti vengono illustrate alcune best practice per ridurre i tempi di aggiornamento.

## Diminuisce la frequenza di ricontrollo

In una tabella di database possono essere presenti colonne di dati con valori modificabili. Ad esempio, in un **ordini** tabella potrebbe essere presente una colonna denominata **status**. Quando un ordine viene inizialmente scritto nel database, la colonna di stato potrebbe contenere il valore `pending`. L&#39;ordine verrà quindi replicato nel tuo [Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md) con questo `pending` valore.

Le colonne modificabili devono essere [ricontrollato i valori aggiornati](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) nel tempo. Per impostazione predefinita, [!DNL MBI] ricontrolla queste colonne durante ogni aggiornamento, ma se c&#39;è una grande quantità di dati da ricontrollare e replicare, può influire negativamente sul tempo di aggiornamento. Invece di eseguire nuovi controlli durante ogni aggiornamento, consigliamo di impostare la frequenza di ricontrollo su giornaliera, settimanale o mensile.

## Utilizzare i metodi di replica incrementale

Come accennato in precedenza, i tempi di aggiornamento lunghi sono direttamente correlati alla quantità di dati da ricontrollare e replicare. [Metodi di replica incrementale](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) può ridurre notevolmente la quantità di dati elaborati durante il ciclo di aggiornamento. Laddove possibile, si consiglia di utilizzare questi metodi o apportare modifiche al database per supportare un metodo incrementale.

## Rimuovere i grafici inutilizzati dalle dashboard

Al termine del ciclo di aggiornamento, [!DNL MBI] esegue un’operazione cache per tutti i grafici. Una cache memorizza i dati in modo che le richieste future di informazioni possano essere completate più rapidamente. In [!DNL MBI], ciò significa che le dashboard verranno caricate rapidamente perché i grafici non devono eseguire query sui dati ogni volta che vengono caricati.

Da [!DNL MBI] esegue solo le operazioni di cache per i grafici trovati in un dashboard, la rimozione dei grafici non utilizzati dalle dashboard diminuirà il tempo di aggiornamento. Tieni presente che lo stesso grafico potrebbe trovarsi su più dashboard: verifica con il tuo team per assicurarti che siano stati rimossi anche tutti i grafici non utilizzati.

>[!NOTE]
>
>La rimozione dei grafici dal dashboard non comporta l&#39;eliminazione del grafico. È possibile [aggiungilo di nuovo in qualsiasi momento](../data-user/dashboards/add-charts-dashboard.md).

## Ottimizzazione del database per l&#39;analisi

Oltre a rivalutare le frequenze di ricontrollo, i metodi di replica e l&#39;utilità del grafico, puoi anche [ottimizzazione del database per l&#39;analisi](../best-practices/opt-db-analysis.md).

## Ritorno a capo

Se il tempo di aggiornamento continua a sembrare lento anche dopo l’implementazione di queste raccomandazioni, [contatta il nostro team di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
