---
title: Informazioni su dati e aggiornamenti
description: Scopri come controllare lo stato del ciclo di aggiornamento.
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Informazioni su dati e aggiornamenti

* [Perché i miei dati sono cambiati?](#datachange)
* [Qual è la differenza tra un aggiornamento regolare e un aggiornamento forzato?](#regularforcedupdates)
* [Perché il ciclo di aggiornamento richiede molto tempo?](#updatecycletime)
* [È possibile ricevere una notifica al completamento di un ciclo di aggiornamento?](#notifyupdate)
* [Perché  [!DNL Google ECommerce]  dati sono diversi dal mio database?](#ecommdatabase)
* [Come si risolve una discrepanza di dati?](#datadiscrepancy)

## Perché i miei dati sono cambiati? {#datachange}

I valori dei grafici possono cambiare nel corso della giornata a causa della sincronizzazione di nuovi dati con il Data Warehouse. Inoltre, i valori per le colonne di dati esistenti possono cambiare a causa di [nuovi controlli](../data-warehouse-mgr/cfg-data-rechecks.md). Un nuovo controllo è un processo che cerca i valori modificati nelle colonne di dati, ad esempio uno stato dell&#39;ordine che si sposta da `open` a `shipped`.

Esistono alcuni modi diversi per [controllare lo stato del ciclo di aggiornamento](../../best-practices/check-update-cycle.md), a seconda delle impostazioni delle autorizzazioni dell&#39;utente.

## Qual è la differenza tra un aggiornamento regolare e un aggiornamento forzato? {#regularforcedupdates}

Gli aggiornamenti regolari sono **processi pianificati**, mentre gli aggiornamenti forzati sono **processi manuali avviati da te**. Se sono presenti ore di sospensione attività (o un periodo di tempo in cui [!DNL Commerce Intelligence] non deve aggiornare i dati), forzare un aggiornamento avvia un ciclo che non rispetta i limiti del periodo di sospensione attività.

## Perché il ciclo di aggiornamento richiede molto tempo? {#updatecycletime}

A un tempo di aggiornamento già lungo possono aggiungersi numerosi fattori. Alcuni [metodi di replica](../data-warehouse-mgr/cfg-replication-methods.md), [frequenze di ricontrollo superiori](../data-warehouse-mgr/cfg-data-rechecks.md) e il numero di dashboard e grafici sono solo alcuni dei collaboratori. Adobe consiglia di [riconfigurare alcune impostazioni](../../best-practices/reduce-update-cycle-time.md) e [ottimizzare il database per l&#39;analisi](../../best-practices/opt-db-analysis.md) per ridurre i tempi di aggiornamento.

## È possibile ricevere una notifica al completamento di un ciclo di aggiornamento? {#notifyupdate}

Se è in corso un aggiornamento, nella pagina `Connections` è presente un collegamento che è possibile utilizzare per richiedere una notifica e-mail al termine del ciclo.

## Perché [!DNL Google ECommerce] dati sono diversi dal mio database? {#ecommdatabase}

Le discrepanze tra [!DNL Google Analytics] e il database possono verificarsi per vari motivi. Il tracciamento non è abilitato correttamente, gli utenti che visitano in incognito e gli eventi di clic non funzionano correttamente sono solo alcuni esempi. Se le entrate e gli ordini non sembrano corretti, [consulta questo argomento](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html) per diagnosticare un problema.

## Come si risolve una discrepanza di dati? {#datadiscrepancy}

Adobe sa che la visualizzazione di dati non coerenti può essere un’esperienza frustrante. Prova a utilizzare l&#39;[elenco di controllo per la discrepanza dei dati](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html) o l&#39;[esercitazione sulle esportazioni dei dati](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html) per diagnosticare il problema. Se sei ancora perplesso, [contatta l&#39;assistenza](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
