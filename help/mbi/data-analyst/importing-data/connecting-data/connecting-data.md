---
title: Connettere i dati
description: Scopri come sfogliare le tabelle disponibili per la sincronizzazione in Data Warehouse Manager.
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Connettere i dati

In entrata [!DNL Adobe Commerce Intelligence], le origini dati vengono chiamate `integrations`. Dopo un `integration` è connesso correttamente, sarà possibile sfogliare le tabelle disponibili per la sincronizzazione in Gestione Date Warehouse.

Le integrazioni vengono aggiunte e gestite utilizzando `Connections` , accessibile facendo clic su **[!UICONTROL Manage Data** > **Connections]**. Qui puoi vedere:

* un elenco di tutte le integrazioni connesse al tuo account

* il tipo di integrazione

* stato ([!DNL Google Analytics] e [!DNL Data Import API] le connessioni hanno campi di stato vuoti)

* l&#39;ultima volta che si verifica una connessione (`Last Connection Started` (colonna) è stato eseguito

![Dati\_Sources\_Table.png](../../../assets/Data_Sources_Table.png)

## Tipi di integrazioni

Esistono quattro modi per inserire i dati in [!DNL Commerce Intelligence]: collega un database, connetti un’integrazione SaaS, carica un `.csv` o utilizza l’API Adobe.

## Integrazioni di database

![Database\_icons.jpg](../../../assets/Database_icons.jpg)

[!DNL Commerce Intelligence] supporta i database SQL e NoSQL, ad esempio [MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md), [MICROSOFT SQL](../integrations/microsoft-sql-server.md), [MongoDB](../integrations/mongodb-via-ssh-tunnel.md), e [PostgreSQL](../integrations/postgresql.md).

Mentre è possibile collegare direttamente il database a [!DNL Commerce Intelligence] utilizzando le credenziali del database, Adobe consiglia di utilizzare un metodo di crittografia collaudato, ad esempio un tunnel SSH. In questo modo i dati rimarranno sicuri mentre entrano nella tua Data Warehouse.

A seconda del metodo di connessione e del tipo di database, potrebbero essere necessarie alcune competenze tecniche per completare la configurazione.

## `SaaS` Integrazioni

![](../../../assets/SaaS_icons.jpg)spree-commerce-logo.png

`SaaS` le integrazioni sono servizi come [[!DNL Google Adwords]](../integrations/google-adwords.md), [[!DNL Salesforce]](../integrations/salesforce.md), e [[!DNL Zendesk]](../integrations/zendesk.md). Poiché i dati di terze parti risiedono sul server del fornitore, non è possibile accedervi direttamente come con i dati del database.

In genere, la configurazione di un’integrazione in [!DNL Commerce Intelligence] è facile come inserire semplicemente le credenziali del tuo account. Alcuni servizi potrebbero richiedere una chiave API per completare l’autorizzazione. Consulta la sezione [sezione integrazioni](../integrations/integrations.md) per istruzioni su come generare le credenziali necessarie.

## Caricamento file

Non sei sicuro di come ottenere dati da un’origine supplementare nella tua Data Warehouse? [Utilizzo di `File Upload` funzionalità](../connecting-data/using-file-uploader.md) è un buon modo per estrarre dati di cui non hai bisogno per prendere decisioni quotidiane. Seguendo le regole di formattazione, puoi caricare rapidamente `.csv` file nella Data Warehouse e unirli ad altre origini dati.

## [!DNL Commerce Intelligence] `Import API`

Se preferisci automatizzare il recupero dei dati da una delle tue origini, puoi utilizzare [!DNL Commerce Intelligence] `Import API`. Fondamentalmente, se non si trova in un database o in un `SaaS` integrazione, `Import API` la funzione è la migliore.

L’utilizzo dell’API richiede un po’ di esperienza tecnica: chi ha familiarità con la scrittura e la manutenzione di un piccolo script Ruby o PHP è più che qualificato.

Per ulteriori informazioni su come iniziare a utilizzare `Import API`, controlla [Sito per sviluppatori](https://developer.adobe.com/commerce/services/reporting/) e [come generare una chiave API](https://developer.adobe.com/commerce/services/reporting/import-api/).

## Aggiungere un’integrazione

Per aggiungere un’integrazione, fai clic su **[!UICONTROL Manage Data** > **Connections]** e quindi fare clic su **[!UICONTROL Add a New Data Source]**. Fai clic sull’icona dell’integrazione da aggiungere e segui le istruzioni contenute negli argomenti dell’Aiuto per configurare:

* [Domande frequenti sull’integrazione](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [Disponibile ](../integrations/integrations.md)
* [Consolidamento delle tabelle](../../../best-practices/consolidating-your-tables.md)
* [Limitazione dell&#39;accesso al database](../../../administrator/account-management/restrict-db-access.md)

**Non vedi un&#39;integrazione che desideri?** Per renderle visibili nel tuo account, è necessario attivare alcune integrazioni. Se stai cercando qualcosa come [!DNL Facebook] ma non è elencato, [invia un ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

**Se viene visualizzato uno stato di errore per un’integrazione**, controlla [Sezione Risoluzione dei problemi](https://support.magento.com/hc/en-us/sections/360003078151) per assistenza.
