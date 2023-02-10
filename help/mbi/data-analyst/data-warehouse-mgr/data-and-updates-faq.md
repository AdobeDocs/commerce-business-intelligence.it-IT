---
title: Informazioni su dati e aggiornamenti
description: Scopri come controllare lo stato del ciclo di aggiornamento.
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Informazioni su dati e aggiornamenti

* [Perché i miei dati sono cambiati?](#datachange)
* [Qual è la differenza tra un aggiornamento regolare e forzato?](#regularforcedupdates)
* [Perché il ciclo di aggiornamento richiede molto tempo?](#updatecycletime)
* [Posso ricevere una notifica al completamento di un ciclo di aggiornamento?](#notifyupdate)
* [Perché? [!DNL Google ECommerce] dati diversi dal database?](#ecommdatabase)
* [Come si risolve una discrepanza di dati?](#datadiscrepancy)

## Perché i miei dati sono cambiati? {#datachange}

I valori del grafico possono variare nel corso della giornata a causa della sincronizzazione di nuovi dati con il data warehouse. Inoltre, i valori per le colonne di dati esistenti possono cambiare a causa di [ricontrollo](../data-warehouse-mgr/cfg-data-rechecks.md). Un nuovo controllo è un processo che cerca i valori modificati nelle colonne di dati, ad esempio uno stato dell&#39;ordine che si sposta da `open` a `shipped`.

Ci sono alcuni modi diversi [per controllare lo stato del ciclo di aggiornamento](../../best-practices/check-update-cycle.md), a seconda del tipo di autorizzazioni utente disponibili.

## Qual è la differenza tra un aggiornamento regolare e forzato? {#regularforcedupdates}

Gli aggiornamenti regolari sono **programmato** processi durante gli aggiornamenti forzati **processi manuali avviati dall&#39;utente**. Se hai un orario di sospensione attività o un periodo di tempo in cui [!DNL MBI] non devono aggiornare i dati: se richiedi un aggiornamento, verrà avviato un ciclo che non rispetta i limiti del periodo di sospensione attività.

## Perché il ciclo di aggiornamento richiede molto tempo? {#updatecycletime}

Molti fattori possono essere aggiunti a un tempo di aggiornamento già lungo. Certi [metodi di replica](../data-warehouse-mgr/cfg-replication-methods.md), [frequenze di ricontrollo più elevate](../data-warehouse-mgr/cfg-data-rechecks.md), e il numero di dashboard e grafici sono solo alcuni collaboratori. Consigliamo [riconfigurazione di alcune impostazioni](../../best-practices/reduce-update-cycle-time.md) e [ottimizzazione del database per l’analisi](../../best-practices/opt-db-analysis.md) per ridurre i tempi di aggiornamento.

## Posso ricevere una notifica al completamento di un ciclo di aggiornamento? {#notifyupdate}

Assolutamente! Se è in corso un aggiornamento, sarà presente un collegamento nella sezione `Connections` pagina che puoi utilizzare per richiedere una notifica e-mail al completamento del ciclo.

## Perché?[!DNL Google ECommerce]dati diversi dal database? {#ecommdatabase}

Discrepanze tra [!DNL Google Analytics] e il database può sorgere per una serie di motivi. Il tracciamento non è abilitato correttamente, gli utenti che visitano l’incognito e gli eventi clic non funzionano correttamente sono solo alcuni esempi. Se le entrate e gli ordini non sono corretti, [utilizza questo articolo](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=en) per diagnosticare il problema.

## Come si risolve una discrepanza di dati? {#datadiscrepancy}

Sappiamo che vedere dati incoerenti può essere un&#39;esperienza frustrante. Prova a utilizzare la nostra [Lista di controllo per la discrepanza dei dati](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html?lang=en) o [Esercitazione sull’esportazione dei dati](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=en) per diagnosticare il problema. Se siete ancora imbattuti, [contattare il supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
