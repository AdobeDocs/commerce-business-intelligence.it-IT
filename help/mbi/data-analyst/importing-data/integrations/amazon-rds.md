---
title: Connettere Amazon RDS
description: Scopri i passaggi per la connessione dell’istanza RDS.
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
source-git-commit: 6f018ab220f2ae573cbc9016f9efb83c27a254be
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# Connettere Amazon RDS

Amazon Relational Database Services (RDS) è un servizio di database gestito che viene eseguito su motori di database che probabilmente già conoscete: [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md), [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md), e [[!DNL PostgreSQ]](../integrations/postgresql.md).

I passaggi per la connessione all&#39;istanza RDS variano leggermente a seconda del tipo di database utilizzato (utilizzare i collegamenti riportati sopra per istruzioni dettagliate su ciascun database) e del fatto che si utilizzi o meno una connessione crittografata (ad esempio [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md)), ma ecco le nozioni di base:

## Autorizza [!DNL MBI] per accedere al database

Nella pagina delle credenziali (**[!UICONTROL Manage Data** > **Integrations]**) per ogni database verrà visualizzata una casella contenente gli indirizzi IP che è necessario autorizzare per la connessione di RDS a MBI: `54.88.76.97` e `34.250.211.151`. Ecco una panoramica della `MySQL credentials` pagina, in cui è stata evidenziata la casella Indirizzo IP:

![](../../../assets/RDS_IP.png)

Per [!DNL MBI] per connettersi correttamente all&#39;istanza RDS, è necessario aggiungere questi indirizzi IP al gruppo di sicurezza del database appropriato tramite la console di gestione di AWS. Questi indirizzi IP possono essere aggiunti a un gruppo esistente oppure è possibile crearne uno nuovo. È importante che il gruppo sia autorizzato ad accedere all’istanza a cui desideri connetterti [!DNL MBI].

Quando si aggiunge [!DNL MBI] indirizzi IP, assicurati di aggiungere un `/32` alla fine dell’indirizzo per indicare ad Amazon che si tratta di un indirizzo IP esatto. Non preoccuparti; l’interfaccia di AWS indicherà chiaramente che è necessario farlo.

## Creare un `Linux` utente per [!DNL MBI] {#linux}

>[!NOTE]
>
>Questo passaggio è necessario solo se si utilizza una connessione crittografata. Per istruzioni su come eseguire questa operazione, fare riferimento all&#39;articolo di installazione per il database in uso (ad esempio MySQL). Il `Linux` L&#39;utente ci consentirà di creare un `SSH tunnel`, che è il metodo più sicuro per inviare dati tramite Internet.

## Creare un utente di database per MBI

Questa è la parte del processo in cui, a seconda del database in uso, i passaggi variano. L’idea è la stessa: creerai un utente per [!DNL MBI] che verranno utilizzati per accedere al database. Istruzioni per la creazione di un database [!DNL MBI] L&#39;utente è disponibile nell&#39;articolo di configurazione del database in uso.

## Immetti le informazioni di connessione in MBI

Dopo aver concesso [!DNL MBI] accedere alla tua istanza e creare un utente per noi, l’ultima cosa da fare è immettere le informazioni di connessione in [!DNL MBI].

Pagine delle credenziali per `MySQL`, `Microsoft SQL`, e `PostgreSQL` sono accessibili tramite `Integrations` page (**[!UICONTROL Manage Data** > **Integrations]**) facendo clic su **[!UICONTROL Add Integration]**. Quando viene visualizzato l’elenco delle integrazioni, fai clic sull’icona del database in uso per passare alla pagina delle credenziali. Se al momento non disponi dell’accesso all’integrazione necessaria, contatta il team del tuo account Adobe.

Per completare la creazione della connessione, sono necessarie le seguenti informazioni:

* L&#39;indirizzo pubblico dell&#39;istanza RDS: si trova nella console di gestione AWS.
* La porta utilizzata dall&#39;istanza di database: Alcuni database dispongono di una porta predefinita che popolerà automaticamente `Port` campo. Queste informazioni si trovano anche nella documentazione di configurazione del database.
* Nome utente e password dell&#39;utente creato per [!DNL MBI].

Se utilizzi una connessione crittografata, modifica il `Encrypted` attiva la pagina delle credenziali del database su `Yes`. Verrà visualizzato un modulo aggiuntivo per l&#39;impostazione della crittografia:

![](../../../assets/sql-integration-encrypted-yes.png)

Questo è tutto! Connessione dell&#39;istanza RDS completata.
