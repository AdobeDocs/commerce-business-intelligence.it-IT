---
title: Connettere i dati
description: Scopri come sfogliare le tabelle disponibili per la sincronizzazione in Data Warehouse Manager.
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---

# Connettere i dati

In entrata [!DNL MBI], le origini dati vengono chiamate `integrations`. Dopo un `integration` è connesso correttamente, sarà possibile sfogliare le tabelle disponibili per la sincronizzazione in Gestione Date Warehouse.

Le integrazioni vengono aggiunte e gestite utilizzando `Connections` , accessibile facendo clic su **[!UICONTROL Manage Data** > **Connections]**. Ecco, vedi
* un elenco di tutte le integrazioni connesse al tuo account
* il tipo di integrazione
* stato ([!DNL Google Analytics] e [!DNL Data Import API] le connessioni hanno campi di stato vuoti)
* l&#39;ultima volta che si verifica una connessione (`Last Connection` (colonna Avviata)

![Dati\_Sources\_Table.png](../../../assets/Data_Sources_Table.png)

## Tipi di integrazioni

Esistono quattro modi per inserire i dati in [!DNL MBI]: collega un database, connetti un’integrazione SaaS, carica un `.csv` o utilizza l’API Adobe.

## Integrazioni di database

![Database\_icons.jpg](../../../assets/Database_icons.jpg)

[!DNL MBI] supporta i database SQL e NoSQL, ad esempio [MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md), [MICROSOFT® SQL](../integrations/microsoft-sql-server.md), [MongoDB](../integrations/mongodb-via-ssh-tunnel.md), e [PostgreSQL](../integrations/postgresql.md).

Mentre è possibile collegare direttamente il database a [!DNL MBI] utilizzando le credenziali del database, Adobe consiglia di utilizzare un metodo di crittografia collaudato, ad esempio un tunnel SSH. In questo modo i dati rimarranno sicuri mentre entrano nella tua Data Warehouse.

A seconda del metodo di connessione e del tipo di database, potrebbero essere necessarie alcune competenze tecniche per completare la configurazione.

## `SaaS` Integrazioni

![](../../../assets/SaaS_icons.jpg)

`SaaS` le integrazioni sono servizi come [[!DNL Google Adwords]](../integrations/google-adwords.md), [[!DNL Salesforce]](../integrations/salesforce.md), e [[!DNL Zendesk]](../integrations/zendesk.md). È importante notare che, poiché i dati di terze parti risiedono sul server del fornitore, non è possibile accedervi direttamente come invece è possibile fare con i dati presenti nel database.

In genere, la configurazione di un’integrazione in [!DNL MBI] è facile come inserire semplicemente le credenziali del tuo account. Alcuni servizi potrebbero richiedere una chiave API per completare l’autorizzazione. Consulta la sezione [sezione integrazioni](../integrations/integrations.md) per istruzioni su come generare le credenziali necessarie.

## Caricamento file

Non sei sicuro di come ottenere dati da un’origine supplementare nella tua Data Warehouse? [Utilizzo di `File Upload` funzionalità](../connecting-data/using-file-uploader.md) è un buon modo per estrarre dati di cui non hai bisogno per prendere decisioni quotidiane. Seguendo le regole di formattazione, puoi caricare rapidamente `.csv` file nella Data Warehouse e unirli ad altre origini dati.

## [!DNL MBI] `Import API`

Se preferisci automatizzare il recupero dei dati da una delle tue origini, puoi utilizzare [!DNL MBI] `Import API`. Fondamentalmente: se non si trova in un database o in un `SaaS` integrazione, `Import API` la funzione è la migliore.

L’utilizzo dell’API richiede un po’ di esperienza tecnica: chi ha familiarità con la scrittura e la manutenzione di un piccolo script Ruby o PHP è più che qualificato.

Per ulteriori informazioni su come iniziare a utilizzare `Import API`, controlla [Sito per sviluppatori](https://developer.adobe.com/commerce/services/reporting/) e [come generare una chiave API](https://developer.adobe.com/commerce/services/reporting/import-api/).

## Aggiungere un’integrazione

Per aggiungere un’integrazione, fai clic su **[!UICONTROL Manage Data** > **Connections]** e quindi fare clic su **[!UICONTROL Add a New Data Source]**. Fai clic sull’icona dell’integrazione da aggiungere e segui le istruzioni riportate negli articoli dell’Aiuto per configurare:

* [Domande frequenti sull’integrazione](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [Disponibile ](../integrations/integrations.md)
* [Consolidamento delle tabelle](../../../best-practices/consolidating-your-tables.md)
* [Limitazione dell&#39;accesso al database](../../../administrator/account-management/restrict-db-access.md)

**Non vedi un&#39;integrazione che desideri?** Per renderle visibili nel tuo account, è necessario attivare alcune integrazioni. Se stai cercando qualcosa, ad esempio, [!DNL Facebook] - ma non è presente nell&#39;elenco, [invia un ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

**Se viene visualizzato uno stato di errore per un’integrazione**, non preoccuparti - controlla il [Sezione Risoluzione dei problemi](https://support.magento.com/hc/en-us/sections/360003078151) per assistenza.
