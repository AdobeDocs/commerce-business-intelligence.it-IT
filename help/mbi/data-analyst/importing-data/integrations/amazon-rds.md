---
title: Connettere Amazon RDS
description: Scopri i passaggi per la connessione dell’istanza RDS.
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# Connetti [!DNL Amazon RDS]

[!DNL Amazon Relational Database Services (RDS)] è un servizio di database gestito che viene eseguito su motori di database che probabilmente sono già noti:

* [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md)
* [[!DNL PostgreSQL]](../integrations/postgresql.md)

I passaggi per la connessione all&#39;istanza [!DNL RDS] variano a seconda del tipo di database utilizzato e se si utilizza una connessione crittografata (come [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md)), ma le nozioni di base sono le seguenti.

## Autorizza [!DNL Commerce Intelligence] ad accedere al tuo database

Nella pagina delle credenziali (**[!UICONTROL Manage Data** > **Integrations]**) di ogni database viene visualizzata una casella contenente gli indirizzi IP che è necessario autorizzare per la connessione di R[!DNL RDS] a [!DNL Commerce Intelligence]: `54.88.76.97` e `34.250.211.151`. Di seguito viene fornita una panoramica della pagina `MySQL credentials`, in cui è stata evidenziata la casella dell&#39;indirizzo IP:

![](../../../assets/RDS_IP.png)

Affinché [!DNL Commerce Intelligence] si connetta correttamente all&#39;istanza di [!DNL RDS], è necessario aggiungere questi indirizzi IP al gruppo di sicurezza del database appropriato tramite la console di gestione di AWS. Questi indirizzi IP possono essere aggiunti a un gruppo esistente oppure è possibile crearne uno. È importante che il gruppo sia autorizzato ad accedere all&#39;istanza a cui si desidera connettersi [!DNL Commerce Intelligence].

Quando si aggiungono gli indirizzi IP [!DNL Commerce Intelligence], assicurarsi di aggiungere `/32` alla fine dell&#39;indirizzo per indicare a [!DNL Amazon] che si tratta di un indirizzo IP esatto. Non preoccuparti; l’interfaccia di AWS indica chiaramente che è necessario.

## Crea un utente `Linux` per [!DNL Commerce Intelligence] {#linux}

>[!NOTE]
>
>Questo passaggio è necessario solo se si utilizza una connessione crittografata. Per istruzioni su come eseguire questa operazione, fare riferimento all&#39;argomento relativo alla configurazione del database in uso (ad esempio MySQL). L&#39;utente `Linux` ci consente di creare un `SSH tunnel`, che è il metodo più sicuro per inviare dati tramite Internet.

## Crea un utente del database per [!DNL Commerce Intelligence]

Questa è la parte del processo in cui, a seconda del database in uso, i passaggi variano. L&#39;idea è la stessa: si crea un utente per [!DNL Commerce Intelligence], che viene utilizzato per accedere al database. Le istruzioni per la creazione di un utente del database [!DNL Commerce Intelligence] sono disponibili nell&#39;argomento di installazione relativo al database in uso.

## Immetti le informazioni di connessione in [!DNL Commerce Intelligence]

Dopo aver concesso a [!DNL Commerce Intelligence] l&#39;accesso alla tua istanza e creato un utente per noi, l&#39;ultima cosa da fare è immettere le informazioni di connessione in [!DNL Commerce Intelligence].

Le pagine delle credenziali per `MySQL`, `Microsoft SQL` e `PostgreSQL` sono accessibili tramite la pagina `Integrations` (**[!UICONTROL Manage Data** > **Integrations]**) facendo clic su **[!UICONTROL Add Integration]**. Quando viene visualizzato l’elenco delle integrazioni, fai clic sull’icona del database in uso per passare alla pagina delle credenziali. Se al momento non disponi dell’accesso all’integrazione necessaria, contatta il team del tuo account Adobe.

Per completare la creazione della connessione, sono necessarie le seguenti informazioni:

* Indirizzo pubblico dell&#39;istanza di Servizi Desktop remoto: disponibile nella console di gestione [!DNL AWS].
* Porta utilizzata dall&#39;istanza di database: alcuni database dispongono di una porta predefinita che popola automaticamente il campo `Port`. Queste informazioni si trovano anche nella documentazione di configurazione del database.
* Nome utente e password dell&#39;utente creato per [!DNL Commerce Intelligence].

Se si utilizza una connessione crittografata, modificare l&#39;opzione `Encrypted` nella pagina delle credenziali del database in `Yes`. Verrà visualizzato un modulo aggiuntivo per l&#39;impostazione della crittografia:

![](../../../assets/sql-integration-encrypted-yes.png)


