---
title: Connetti Microsoft SQL Server
description: Scopri come collegare il database SQL di Microsoft a [!DNL MBI] in un processo in quattro fasi.
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# Connetti Microsoft SQL Server

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![](../../../assets/MicrosoftSQLServer-logo.png)

Questo articolo spiega come collegare il tuo `Microsoft SQL` database a [!DNL MBI] in un processo in quattro fasi. Questo processo richiede alcune competenze tecniche relative alle connessioni al server e a SQL e potrebbe richiedere il supporto degli sviluppatori del team.

Noi sosteniamo [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft SQL Azure]e la maggior parte degli altri provider di server cloud. Se hai una domanda sul tuo host particolare, [inviare un ticket di supporto](../../../guide-overview.md) chiedendoci di fornire queste informazioni.

Il nostro sistema deve eseguire query SELECT sul tuo database. Inizialmente per ottenere un&#39;istantanea della struttura del database e quindi regolarmente gli straordinari per mantenere i dati aggiornati. I nostri aggiornamenti sono incrementali e limitiamo la frequenza e il tempo di aggiornamento per evitare qualsiasi carico indesiderato sul server.

Il modo migliore per farlo è collegarci al server di database tramite TCP/IP. Creare un utente che può eseguire solo query SELECT (e, facoltativamente, può selezionare solo i dati dalle tabelle specificate). Questa operazione deve essere eseguita per ciascuno dei server a cui ci si connette [!DNL MBI].

## Collegamento `Microsoft SQL` a [!DNL MBI]:

1. Assicurati che il server consenta connessioni tramite TCP/IP e l&#39;autenticazione in modalità mista.

1. Assicurati che il firewall consenta la connessione dell&#39;IP dedicato del nostro server.

   Puoi trovare l&#39;indirizzo IP che utilizzeremo per connettersi al tuo server nella sezione delle connessioni del tuo `Settings` pagina.

1. Crea un utente da utilizzare per accedere al server di database.  Hai due opzioni; tramite `UI` o tramite `query`:
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) (secondo esempio)

1. Inserisci l&#39;indirizzo IP del server, il nome utente e la password in [!DNL MBI] sotto **[!UICONTROL Manage Data** > **Connections]**.

   ![](../../../assets/manage-data-connections.png)

1. Fai clic su **[!UICONTROL Add a Data Source]**.

1. Selezionare per collegare un `Microsoft SQL` e immetti le tue credenziali nei campi del nuovo `Connections` pagina.

   Se utilizzi `Windows Azure`, è necessario specificare anche un nome di database.
