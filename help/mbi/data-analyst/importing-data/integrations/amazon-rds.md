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

I passaggi per la connessione [!DNL RDS] variano a seconda del tipo di database in uso e dell&#39;utilizzo di una connessione crittografata, ad esempio [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md)), ma ecco le nozioni di base.

## Autorizza [!DNL Commerce Intelligence] per accedere al database

Nella pagina delle credenziali (**[!UICONTROL Manage Data** > **Integrations]**) per ogni database viene visualizzata una casella contenente gli indirizzi IP che è necessario autorizzare per la connessione[!DNL RDS] a [!DNL Commerce Intelligence]: `54.88.76.97` e `34.250.211.151`. Ecco una panoramica della `MySQL credentials` pagina, in cui è stata evidenziata la casella Indirizzo IP:

![](../../../assets/RDS_IP.png)

Per [!DNL Commerce Intelligence] per connettersi correttamente al tuo [!DNL RDS] devi aggiungere questi indirizzi IP al gruppo di sicurezza del database appropriato tramite la console di gestione di AWS. Questi indirizzi IP possono essere aggiunti a un gruppo esistente oppure è possibile crearne uno. È importante che il gruppo sia autorizzato ad accedere all’istanza a cui desideri connetterti [!DNL Commerce Intelligence].

Quando si aggiunge [!DNL Commerce Intelligence] indirizzi IP, assicurati di aggiungere un `/32` alla fine dell’indirizzo per indicare a [!DNL Amazon] che è un indirizzo IP esatto. Non preoccuparti; l’interfaccia di AWS indica chiaramente che è necessario.

## Creare un `Linux` utente per [!DNL Commerce Intelligence] {#linux}

>[!NOTE]
>
>Questo passaggio è necessario solo se si utilizza una connessione crittografata. Per istruzioni su come eseguire questa operazione, fare riferimento all&#39;argomento relativo alla configurazione del database in uso (ad esempio MySQL). Il `Linux` L&#39;utente ci consente di creare un `SSH tunnel`, che è il metodo più sicuro per inviare dati tramite Internet.

## Creare un utente del database per [!DNL Commerce Intelligence]

Questa è la parte del processo in cui, a seconda del database in uso, i passaggi variano. L’idea è la stessa: creare un utente per [!DNL Commerce Intelligence] utilizzato per accedere al database. Istruzioni per la creazione di un database [!DNL Commerce Intelligence] L&#39;utente è disponibile nell&#39;argomento di configurazione relativo al database in uso.

## Immetti le informazioni di connessione in [!DNL Commerce Intelligence]

Dopo aver concesso [!DNL Commerce Intelligence] accedere alla tua istanza e creare un utente per noi, l’ultima cosa da fare è immettere le informazioni di connessione in [!DNL Commerce Intelligence].

Pagine delle credenziali per `MySQL`, `Microsoft SQL`, e `PostgreSQL` sono accessibili tramite `Integrations` page (**[!UICONTROL Manage Data** > **Integrations]**) facendo clic su **[!UICONTROL Add Integration]**. Quando viene visualizzato l’elenco delle integrazioni, fai clic sull’icona del database in uso per passare alla pagina delle credenziali. Se al momento non disponi dell’accesso all’integrazione necessaria, contatta il team del tuo account Adobe.

Per completare la creazione della connessione, sono necessarie le seguenti informazioni:

* L&#39;indirizzo pubblico dell&#39;istanza di Servizi Desktop remoto: disponibile nella [!DNL AWS] console di gestione.
* La porta utilizzata dall&#39;istanza di database: Alcuni database dispongono di una porta predefinita che popola automaticamente `Port` campo. Queste informazioni si trovano anche nella documentazione di configurazione del database.
* Nome utente e password dell&#39;utente creato per [!DNL Commerce Intelligence].

Se utilizzi una connessione crittografata, modifica il `Encrypted` attiva la pagina delle credenziali del database su `Yes`. Verrà visualizzato un modulo aggiuntivo per l&#39;impostazione della crittografia:

![](../../../assets/sql-integration-encrypted-yes.png)


