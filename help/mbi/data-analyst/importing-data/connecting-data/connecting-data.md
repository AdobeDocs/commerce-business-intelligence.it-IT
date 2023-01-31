---
title: Connetti i tuoi dati
description: Scopri come sfogliare le tabelle disponibili per la sincronizzazione in Data Warehouse Manager.
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---

# Collegare i dati

In [!DNL MBI], le origini dati sono chiamate `integrations`. Dopo un `integration` la connessione è riuscita e sarà possibile sfogliare le tabelle disponibili per la sincronizzazione in Data Warehouse Manager.

Le integrazioni vengono aggiunte e gestite utilizzando l’ `Connections` , accessibile facendo clic su **[!UICONTROL Manage Data** > **Connections]**. Qui puoi vedere un elenco di tutte le integrazioni connesse al tuo account, il tipo di integrazione, lo stato ([!DNL Google Analytics] e [!DNL Data Import API] le connessioni avranno campi di stato vuoti) e l’ultima volta che viene eseguito un test di connessione (`Last Connection` Colonna avviata).

![Data\_Sources\_Table.png](../../../assets/Data_Sources_Table.png)

## Tipi di integrazioni

Sono disponibili quattro modi per immettere i dati in [!DNL MBI]: collegare un database, collegare un’integrazione SaaS, caricare un `.csv` o utilizza la nostra API.

## Integrazioni del database

![Database\_icone.jpg](../../../assets/Database_icons.jpg)

[!DNL MBI] supporta database basati su SQL e NoSQL come [MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md), [Microsoft SQL](../integrations/microsoft-sql-server.md), [MongoDB](../integrations/mongodb-via-ssh-tunnel.md)e [PostgreSQL](../integrations/postgresql.md).

Mentre è possibile collegare direttamente il database a [!DNL MBI] utilizzando le credenziali del database, si consiglia di utilizzare un metodo di crittografia collaudato come un tunnel SSH. In questo modo i dati rimarranno sicuri e sicuri durante l&#39;accesso al data warehouse.

A seconda del metodo di connessione e del tipo di database, potrebbe essere necessaria un&#39;esperienza tecnica per completare la configurazione.

## `SaaS` Integrazioni

![](../../../assets/SaaS_icons.jpg)

`SaaS` le integrazioni sono servizi come [[!DNL Google Adwords]](../integrations/google-adwords.md), [[!DNL Salesforce]](../integrations/salesforce.md)e [[!DNL Zendesk]](../integrations/zendesk.md). È importante notare che, poiché i dati di terze parti risiedono sul server del fornitore, non è possibile accedervi direttamente come è possibile con i dati nel database.

Nella maggior parte dei casi, l’impostazione di un’integrazione in [!DNL MBI] è facile come semplicemente inserire le credenziali del tuo account. Alcuni servizi potrebbero richiedere una chiave API per completare l’autorizzazione. controlla il [sezione integrazioni](../integrations/integrations.md) per istruzioni su come generare le credenziali necessarie.

## Caricamento file

Non sei sicuro di come ottenere dati da un&#39;origine supplementare nel tuo data warehouse? [Utilizzo della `File Upload` caratteristica](../connecting-data/using-file-uploader.md) è un buon modo per inserire dati che non sono necessari per il processo decisionale quotidiano. Seguendo le nostre regole di formattazione, puoi caricare rapidamente `.csv` file nel data warehouse e uniscili ad altre origini dati.

## [!DNL MBI] `Import API`

Se preferisci automatizzare il recupero dei dati da una delle tue sorgenti, puoi utilizzare la [!DNL MBI] `Import API`. In sostanza: se non si trova in un database o in un `SaaS` integrazione, `Import API` La funzione è la tua migliore scommessa.

L&#39;utilizzo dell&#39;API richiede un po&#39; di competenze tecniche: chi è a suo agio con la scrittura e il mantenimento di un piccolo script Ruby o PHP sarà più che qualificato.

Per ulteriori informazioni su come iniziare a utilizzare `Import API`, controlla [Sito web per sviluppatori](https://developer.adobe.com/commerce/services/reporting/) e [come generare una chiave API](https://developer.adobe.com/commerce/services/reporting/import-api/).

## Aggiungere un’integrazione

Per aggiungere un’integrazione, fai clic su **[!UICONTROL Manage Data** > **Connections]** quindi fai clic su **[!UICONTROL Add a New Data Source]**. Fai clic sull&#39;icona dell&#39;integrazione che desideri aggiungere e segui le istruzioni contenute nei nostri articoli di aiuto per configurare le cose:

* [Domande frequenti sull’integrazione](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [Disponibile ](../integrations/integrations.md)
* [Consolidamento delle tabelle](../../../best-practices/consolidating-your-tables.md)
* [Limitazione dell’accesso al database](../../../administrator/account-management/restrict-db-access.md)

**Non trovi un&#39;integrazione desiderata?** Per renderle visibili nel tuo account, è necessario attivare alcune integrazioni. Se cerchi qualcosa, ad esempio [!DNL Facebook] - ma non è elencato, [inviare un ticket di supporto](../../../guide-overview.md).

**Se viene visualizzato uno stato di errore per un’integrazione**, non andare nel panico - controlla il [Sezione Risoluzione dei problemi](https://support.magento.com/hc/en-us/sections/360003078151) per aiuto.
