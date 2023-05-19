---
title: Connetti Microsoft SQL Server
description: Scopri come connettere il database SQL di Microsoft a [!DNL Commerce Intelligence] in un processo in quattro fasi.
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# Connetti [!DNL Microsoft SQL] Server

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![](../../../assets/MicrosoftSQLServer-logo.png)

Questo argomento spiega come collegare [!DNL Microsoft SQL] database a [!DNL Commerce Intelligence] in un processo in quattro fasi. Questo processo richiede alcune competenze tecniche relative alle connessioni server e a SQL e potrebbe richiedere il supporto degli sviluppatori del team.

[!DNL Commerce Intelligence] supporta [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft SQL Azure]e la maggior parte degli altri provider di server cloud. Se hai una domanda sul tuo particolare ospite, [invia un ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) chiedendoci di fornire queste informazioni.

Il sistema deve eseguire le query SELECT sul database. Questa operazione viene eseguita inizialmente per ottenere un’istantanea della struttura del database e quindi regolarmente nel corso del tempo per mantenere i dati aggiornati. Gli aggiornamenti sono incrementali e Adobe limita la frequenza e il tempo di aggiornamento per evitare carichi indesiderati sul server.

Il modo migliore per eseguire questa operazione è connettersi al server di database tramite TCP/IP. Creare un utente che possa eseguire solo query SELECT e, facoltativamente, che possa selezionare solo i dati delle tabelle specificate. Questa operazione deve essere eseguita per ogni server a cui ci si connette [!DNL Commerce Intelligence].

## Connessione `Microsoft SQL` a [!DNL Commerce Intelligence]:

1. Verificare che il server consenta connessioni su TCP/IP e autenticazione in modalità mista.

1. Verificare che il firewall consenta la connessione dell&#39;IP dedicato del server.

   L&#39;indirizzo IP utilizzato per la connessione al server è disponibile nella sezione delle connessioni del `Settings` pagina.

1. Creare un utente da utilizzare per accedere al server di database. Sono disponibili due opzioni: tramite `UI` o tramite un `query`:
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) (secondo esempio)

1. Immettere l&#39;indirizzo IP del server, il nome utente e la password in [!DNL Commerce Intelligence] in **[!UICONTROL Manage Data** > **Connections]**.

   ![](../../../assets/manage-data-connections.png)

1. Clic **[!UICONTROL Add a Data Source]**.

1. Seleziona per collegare un `Microsoft SQL` e immettere le credenziali nei campi del nuovo `Connections` pagina.

   Se sta usando `Windows Azure`, è necessario specificare anche un nome di database.
