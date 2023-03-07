---
title: Informazioni su dati e aggiornamenti
description: Scopri come controllare lo stato del ciclo di aggiornamento.
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---

# Informazioni su dati e aggiornamenti

* [Perché i miei dati sono cambiati?](#datachange)
* [Qual è la differenza tra un aggiornamento regolare e un aggiornamento forzato?](#regularforcedupdates)
* [Perché il ciclo di aggiornamento richiede molto tempo?](#updatecycletime)
* [È possibile ricevere una notifica al completamento di un ciclo di aggiornamento?](#notifyupdate)
* [Perché è [!DNL Google ECommerce] dati diversi dal database?](#ecommdatabase)
* [Come si risolve una discrepanza di dati?](#datadiscrepancy)

## Perché i miei dati sono cambiati? {#datachange}

I valori del grafico possono cambiare nel corso della giornata a causa della sincronizzazione dei nuovi dati con la Data Warehouse. Inoltre, i valori delle colonne di dati esistenti possono cambiare a causa di [ricontrolli](../data-warehouse-mgr/cfg-data-rechecks.md). Un nuovo controllo è un processo che cerca i valori modificati nelle colonne di dati, ad esempio uno stato dell&#39;ordine che si sposta da `open` a `shipped`.

Ci sono alcuni modi diversi [per controllare lo stato del ciclo di aggiornamento](../../best-practices/check-update-cycle.md), a seconda del tipo di autorizzazioni utente di cui disponi.

## Qual è la differenza tra un aggiornamento regolare e un aggiornamento forzato? {#regularforcedupdates}

Gli aggiornamenti regolari sono **pianificato** processi mentre gli aggiornamenti forzati sono **processi manuali avviati da te**. Se sono presenti ore di sospensione attività o un periodo di tempo in cui [!DNL MBI] non deve aggiornare i dati: forzare un aggiornamento avvia un ciclo che non rispetta le limitazioni del periodo di sospensione attività.

## Perché il ciclo di aggiornamento richiede molto tempo? {#updatecycletime}

A un tempo di aggiornamento già lungo possono aggiungersi numerosi fattori. Certi [metodi di replica](../data-warehouse-mgr/cfg-replication-methods.md), [frequenze di ricontrollo più alte](../data-warehouse-mgr/cfg-data-rechecks.md)e il numero di dashboard e grafici sono solo alcuni dei collaboratori. Adobe di consigli [riconfigurazione di alcune impostazioni](../../best-practices/reduce-update-cycle-time.md) e [ottimizzazione del database per l&#39;analisi](../../best-practices/opt-db-analysis.md) per ridurre i tempi di aggiornamento.

## È possibile ricevere una notifica al completamento di un ciclo di aggiornamento? {#notifyupdate}

Se è in corso un aggiornamento, è disponibile un collegamento `Connections` pagina che puoi utilizzare per richiedere una notifica e-mail al termine del ciclo.

## Perché è[!DNL Google ECommerce]dati diversi dal database? {#ecommdatabase}

Discrepanze tra [!DNL Google Analytics] e il database può sorgere per vari motivi. Il tracciamento non è abilitato correttamente, gli utenti che visitano in incognito e gli eventi di clic non funzionano correttamente sono solo alcuni esempi. Se i ricavi e gli ordini non sembrano corretti, [usa questo articolo](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=en) per diagnosticare il problema.

## Come si risolve una discrepanza di dati? {#datadiscrepancy}

Adobe sa che la visualizzazione di dati non coerenti può essere un’esperienza frustrante. Prova a utilizzare il [Elenco di controllo per la discrepanza dei dati](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html?lang=en) o [Tutorial sull’esportazione dei dati](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=en) per diagnosticare il problema. Se sei ancora perplesso, [contatta l’assistenza](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
