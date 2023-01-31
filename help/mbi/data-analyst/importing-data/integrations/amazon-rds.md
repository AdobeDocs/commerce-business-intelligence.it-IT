---
title: Collegare Amazon RDS
description: Scopri i passaggi per la connessione dell’istanza RDS.
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# Collegare Amazon RDS

Amazon Relational Database Services (RDS) è un servizio di database gestito che viene eseguito su motori di database di cui si è probabilmente già a conoscenza - [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md), [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md)e [[!DNL PostgreSQ]](../integrations/postgresql.md).

I passaggi per la connessione dell’istanza RDS variano leggermente a seconda del tipo di database che si sta utilizzando (utilizzare i link qui sopra per le istruzioni dettagliate per ogni database) e se si sta utilizzando o meno una connessione crittografata (come un [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md)), ma ecco le nozioni di base:

## Autorizzare [!DNL MBI] per accedere al database

Nella pagina delle credenziali (**[!UICONTROL Manage Data** > **Integrations]**) per ogni database, verrà visualizzata una casella contenente gli indirizzi IP che sarà necessario autorizzare per collegare RDS a MBI: `54.88.76.97` e `34.250.211.151`. Ecco un&#39;occhiata alla `MySQL credentials` pagina, dove abbiamo evidenziato la casella dell’indirizzo IP:

![](../../../assets/RDS_IP.png)

Per [!DNL MBI] per connettersi correttamente all’istanza RDS, è necessario aggiungere questi indirizzi IP al gruppo di sicurezza del database appropriato tramite la console di gestione AWS. Questi indirizzi IP possono essere aggiunti a un gruppo esistente oppure è possibile crearne uno nuovo; è importante che il gruppo sia autorizzato ad accedere all’istanza a cui si desidera connettersi [!DNL MBI].

Quando si aggiunge la variabile [!DNL MBI] Indirizzi IP, assicurati di aggiungere un `/32` alla fine dell’indirizzo per indicare ad Amazon che si tratta di un indirizzo IP esatto. Non preoccupatevi; l’interfaccia di AWS chiarirà che ciò è necessario.

## Crea un `Linux` utente per [!DNL MBI] {#linux}

>[!NOTE]
>
>Questo passaggio è necessario solo se si utilizza una connessione crittografata. Per istruzioni su come eseguire questa operazione, consulta l’articolo di configurazione per il database in uso (ad esempio: MySQL). La `Linux` l’utente ci consentirà di creare un `SSH tunnel`, che è il metodo più sicuro per inviare dati su Internet.

## Creare un utente di database per MBI

Questa è la parte del processo in cui, a seconda del database in uso, i passaggi variano. L&#39;idea è la stessa, tuttavia: creerai un utente per [!DNL MBI] che verrà utilizzato per accedere al database. Istruzioni per la creazione di un database [!DNL MBI] L&#39;utente si trova nell&#39;articolo di configurazione del database in uso.

## Immettere le informazioni di connessione in MBI

Dopo aver concesso [!DNL MBI] accesso alla tua istanza e creato un utente per noi, l&#39;ultima cosa che devi fare è inserire le informazioni di connessione in [!DNL MBI].

Le pagine delle credenziali per `MySQL`, `Microsoft SQL`e `PostgreSQL` sono accessibili tramite `Integrations` page (**[!UICONTROL Manage Data** > **Integrations]**) facendo clic su **[!UICONTROL Add Integration]**. Quando viene visualizzato l’elenco delle integrazioni, fai clic sull’icona del database che stai utilizzando per passare alla pagina delle credenziali. Se al momento non hai accesso all’integrazione necessaria, contatta il tuo CSM.

Per completare la creazione della connessione, sono necessarie le seguenti informazioni:

* Indirizzo pubblico della tua istanza RDS: Questa si trova nella console di gestione di AWS.
* La porta utilizzata dall&#39;istanza di database: Alcuni database dispongono di una porta predefinita che popolerà automaticamente il `Port` campo . Queste informazioni si trovano anche nella documentazione di configurazione del database.
* Nome utente e password dell’utente per il quale hai creato [!DNL MBI].

Se utilizzi una connessione crittografata, modifica la `Encrypted` attiva la pagina delle credenziali del database su `Yes`. Verrà visualizzato un modulo aggiuntivo per la configurazione della crittografia:

![](../../../assets/sql-integration-encrypted-yes.png)

Questo è tutto quello che c&#39;è da fare! Connessione dell&#39;istanza RDS completata.
