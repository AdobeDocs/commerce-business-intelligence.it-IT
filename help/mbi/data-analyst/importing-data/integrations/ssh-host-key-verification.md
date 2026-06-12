---
title: Verifica chiave host SSH
description: Scopri come Commerce Intelligence registra le chiavi host SSH, come aggiornarle, risolvere gli errori e quando contattare il supporto per le connessioni del tunnel SSH.
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
source-git-commit: b51e9fceba0c62f4ef3dde340d26cd78641ef3a2
workflow-type: tm+mt
source-wordcount: 1130
ht-degree: 0%

---

# Verifica chiave host SSH {#ssh-host-keys}

[!DNL Commerce Intelligence] utilizza la verifica rigorosa della chiave host SSH per le connessioni al database crittografate (tunnel SSH), tra cui [MySQL](mysql-via-ssh-tunnel.md), [MongoDB](mongodb-via-ssh-tunnel.md) e [PostgreSQL](postgresql.md).

Durante **[!UICONTROL Save & Test]**, il sistema registra le chiavi host SSH bastion per la connessione e le memorizza in modo sicuro per ogni connessione. Dopo la registrazione, la replica e il tunneling hanno esito positivo solo quando le chiavi host live bastion corrispondono a quelle registrate.

Questo modello migliora la sicurezza bloccando gli attacchi man-in-the-middle e le modifiche impreviste dell’host. Significa anche che la rotazione della chiave host, il materiale di attendibilità mancante o le modifiche all&#39;infrastruttura possono emergere come errori della chiave host SSH sulla connessione anziché come errori generici del tunnel.

>[!NOTE]
>
>**Amministratore** indica un utente con autorizzazioni di amministratore per il tuo account [!DNL Commerce Intelligence], non la tua console dell&#39;organizzazione Adobe, a meno che non sia indicato diversamente. Solo gli amministratori possono eseguire **[!UICONTROL Refresh SSH Host Keys]**. Se non trovi questo controllo, chiedi a un amministratore del tuo account di eseguire l’aggiornamento o contatta il supporto Adobe.

Non è possibile modificare, caricare o gestire `known_hosts` file. L’iscrizione e l’aggiornamento vengono eseguiti sull’infrastruttura Adobe assegnata al tuo account.

>[!IMPORTANT]
>
>La rotazione della chiave host richiede un amministratore per eseguire **[!UICONTROL Refresh SSH Host Keys]**. Se le chiavi host bastion sono state modificate o l&#39;identità bastion è cambiata (nome host, IP o porta), l&#39;esecuzione di **[!UICONTROL Save & Test]** di nuovo o il salvataggio della connessione non aggiorna le chiavi registrate. La connessione può continuare a non riuscire finché un amministratore non aggiorna le chiavi host.

## Salva e prova {#save-and-test}

**[!UICONTROL Save & Test]** esegue solo **la registrazione iniziale della chiave host SSH**. È conservativa per progettazione e non ruota né sovrascrive le chiavi già registrate per la connessione.

| Stato chiave host iscritto | Funzionalità di salvataggio e test |
| --- | --- |
| Le chiavi host non sono ancora registrate | **[!UICONTROL Save & Test]** analizza l&#39;host e la porta bastion, registra le chiavi host e le memorizza per questa connessione. |
| Le chiavi host sono già registrate | **[!UICONTROL Save & Test]** ignora l&#39;iscrizione. Non sovrascrive, ruota o elimina le chiavi registrate esistenti, anche se le chiavi di bastione attive non corrispondono più. |
| Le chiavi registrate sono mancanti, vuote o non valide | **[!UICONTROL Save & Test]** non ripristina il materiale attendibile non valido di per sé. Un amministratore deve eseguire **[!UICONTROL Refresh SSH Host Keys]** o contattare il supporto tecnico se gli errori continuano |

Dopo una prima iscrizione riuscita, **[!UICONTROL Save & Test]** esegue la convalida delle credenziali e delle impostazioni di connessione, ma lascia invariate le chiavi host SSH registrate.

## Aggiorna chiavi host SSH {#refresh-ssh-host-keys}

**[!UICONTROL Refresh SSH Host Keys]** aggiornamenti registrati chiavi host SSH quando il bastione è cambiato o quando è necessario ripristinare il materiale attendibile. Un amministratore avvia l&#39;aggiornamento dalla connessione in **[!UICONTROL Data]** > **[!UICONTROL Connections]**.

L’aggiornamento viene eseguito in modo asincrono sull’infrastruttura Adobe assegnata al tuo account. [!DNL Commerce Intelligence] restituisce dopo l&#39;aggiornamento in coda. Non esegue la scansione sulla workstation.

Un aggiornamento di **riscrive** ha registrato le chiavi host solo quando una delle seguenti condizioni è vera:

* Chiavi host registrate mancanti
* Le chiavi host registrate sono vuote
* Impossibile leggere le chiavi host registrate
* Convalida delle chiavi host registrate non riuscita
* Una nuova analisi restituisce righe di chiave host diverse da quelle registrate
* Le impronte digitali acquisite dalla scansione e le chiavi registrate non corrispondono

Se le chiavi registrate sono correnti e valide, l’aggiornamento viene completato senza modificarle.

>[!TIP]
>
>Esegui **[!UICONTROL Refresh SSH Host Keys]** dopo che il team ruoterà le chiavi host SSH sul bastione, modificherà il nome host o l&#39;IP del bastione o sostituirà l&#39;endpoint SSH. Attendere alcuni minuti, quindi eseguire **[!UICONTROL Save & Test]** per confermare la connessione.

## Migrazione account {#migration}

Non si attiva la migrazione dell&#39;account. Adobe esegue gli spostamenti del server dati durante la manutenzione o il ridimensionamento e copia le chiavi host SSH registrate in modo che la verifica rigorosa continui a funzionare dopo lo spostamento.

Dopo che Adobe ti ha notificato che la migrazione è stata completata:

1. Eseguire **[!UICONTROL Save & Test]** per confermare la connessione. L&#39;iscrizione deve essere ignorata se le chiavi sono state copiate correttamente.
1. Se gli errori della chiave host SSH persistono, chiedere a un amministratore di eseguire **[!UICONTROL Refresh SSH Host Keys]**, attendere alcuni minuti, quindi eseguire di nuovo **[!UICONTROL Save & Test]**.
1. Contattare il supporto Adobe se gli errori continuano dopo **[!UICONTROL Save & Test]** e fino a due **[!UICONTROL Refresh SSH Host Keys]** tentativi.

## Messaggi di errore della chiave host SSH {#ssh-host-key-errors}

Lo stato della connessione mostra un singolo messaggio di chiave host SSH semplice da usare. Gli errori OpenSSH non elaborati non vengono visualizzati nel dashboard.

La tabella seguente mappa i messaggi comuni alle probabili cause e ai passaggi successivi tipici.

| Messaggio o stato | Che cosa significa | Possibili cause | Passaggio successivo tipico |
| --- | --- | --- | --- |
| Verifica chiave host SSH non riuscita | La chiave host bastione non corrisponde alle chiavi registrate oppure il materiale attendibile non è utilizzabile | Chiavi host SSH ruotate sul bastione; nome host bastione, IP o porta cambiata; chiavi registrate mancanti, vuote, non valide o illeggibili | Confermare **Indirizzo remoto** e **Porta SSH**. Chiedi al tuo team di infrastruttura se le chiavi host bastion sono cambiate. Chiedere a un amministratore di eseguire **[!UICONTROL Refresh SSH Host Keys]**, attendere alcuni minuti, quindi eseguire **[!UICONTROL Save & Test]**. |
| Impossibile registrare le chiavi host SSH | **[!UICONTROL Save & Test]**: impossibile analizzare o archiviare le chiavi host bastion | Bastione non raggiungibile dall&#39;infrastruttura Adobe; errore DNS; il firewall blocca [!DNL Commerce Intelligence] indirizzi IP; errore **Indirizzo remoto** o **Porta SSH**; errore di scansione della chiave host sul bastione | Verificare che il firewall sia stato inserito nell&#39;elenco Consentiti utilizzando gli indirizzi IP [!DNL Commerce Intelligence] nella pagina delle credenziali del database. Verificare che il bastione accetti SSH sulla porta configurata. Correggere i campi di connessione ed eseguire di nuovo **[!UICONTROL Save & Test]**. |
| Chiavi host SSH mancanti o non valide | La verifica rigorosa ha bloccato il tunnel perché il materiale attendibile registrato è assente o danneggiato | La prima connessione non ha mai completato l’iscrizione; aggiornamento precedente non è riuscito; la migrazione non ha copiato le chiavi; problema sull’infrastruttura Adobe | Chiedere a un amministratore di eseguire **[!UICONTROL Refresh SSH Host Keys]**, quindi **[!UICONTROL Save & Test]**. Se l’errore persiste, contatta il supporto. |
| Impossibile completare l&#39;aggiornamento delle chiavi host SSH | L&#39;aggiornamento non ha aggiornato le chiavi registrate | Errore di rete, DNS o scansione durante l’aggiornamento; problema nell’infrastruttura Adobe | Aspettate qualche minuto. Chiedere a un amministratore di eseguire di nuovo **[!UICONTROL Refresh SSH Host Keys]** (secondo tentativo se il primo non è riuscito). Confermare la raggiungibilità del bastione e la sua inserita nell&#39;elenco Consentiti a. Contattare il supporto tecnico se la connessione continua a non riuscire dopo due tentativi di aggiornamento e **[!UICONTROL Save & Test]**. |

## Elenco di controllo per la risoluzione dei problemi {#troubleshooting}

1. Conferma **Indirizzo remoto**, **Porta SSH** e le impostazioni utente Linux corrispondono alle tue impostazioni bastion.
1. Conferma l&#39;autorizzazione del firewall per gli indirizzi IP [!DNL Commerce Intelligence] visualizzati nella pagina delle credenziali del database.
1. Chiedi al tuo team di infrastruttura se le chiavi host SSH sul bastione sono state modificate di recente.
1. Eseguire **[!UICONTROL Save & Test]** per convalidare le impostazioni e registrare le chiavi, se non ne esistono ancora.
1. Chiedere a un amministratore di eseguire **[!UICONTROL Refresh SSH Host Keys]**, attendere alcuni minuti, quindi eseguire di nuovo **[!UICONTROL Save & Test]**. Se il primo aggiornamento non risolve l’errore, ripeti questo passaggio.
1. Se la connessione continua a mostrare un errore della chiave host SSH dopo due tentativi di aggiornamento, fare clic su **[!UICONTROL Contact Support]** nella pagina della connessione (o sul canale di supporto dell&#39;account).

## Quando contattare il supporto Adobe {#contact-support}

Contatta l’assistenza quando:

* Gli errori della chiave host SSH continuano dopo che un amministratore esegue **[!UICONTROL Refresh SSH Host Keys]** due volte e **[!UICONTROL Save & Test]** continua a non riuscire
* **[!UICONTROL Refresh SSH Host Keys]** non viene mai completato o lo stato della connessione non cambia dopo 15-30 minuti
* Gli errori sono iniziati immediatamente dopo la notifica da parte di Adobe della migrazione dell’account o della manutenzione del server dati
* Le impostazioni Bastion e la inserire nell&#39;elenco Consentiti del firewall sono corrette, il team non ha ruotato le chiavi host e non è ancora possibile connettersi
* Per eseguire **[!UICONTROL Refresh SSH Host Keys]** è necessario un amministratore, ma non è disponibile alcun amministratore per l&#39;account

Includi il nome della connessione, l&#39;ora approssimativa dell&#39;ultimo **[!UICONTROL Save & Test]** o tentativo di aggiornamento e se le chiavi host bastion sono state modificate di recente. Non inviare chiavi o passphrase private.

## Correlato {#related}

* [Connetti MySQL tramite tunnel SSH](mysql-via-ssh-tunnel.md)
* [Collegare MongoDB tramite tunnel SSH](mongodb-via-ssh-tunnel.md)
* [Connetti PostgreSQL tramite tunnel SSH](postgresql.md)
* [Reautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=it)
