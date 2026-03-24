---
title: Servizi di migrazione dati
description: Scopri tutto ciò che ti serve per inviare una richiesta e iniziare a eseguire la migrazione.
exl-id: 105cd003-98ef-4358-80b9-b3190c2c57b7
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/q8FzCjuqcQC57WLd0201CV46es2CrbAjZx9FGFX-RFw
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 685
ht-degree: 0%

---

# Migrazione dei dati

La migrazione a un nuovo schema di database, server o database di reporting non deve essere troppo complessa. Il [[!DNL Adobe] team dei servizi](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) offre assistenza per la migrazione.

Per garantire una transizione quanto più fluida possibile, è necessario essere il più dettagliati possibile durante l’invio della richiesta di migrazione. Questo argomento contiene tutto il necessario per inviare una richiesta e iniziare a eseguire la migrazione. Fornendoci un quadro completo delle tue esigenze, assicurati che il tuo progetto abbia un ambito appropriato e che la stima sia accurata.

## Introduzione {#started}

Prima di iniziare, è necessario conoscere le risposte alle seguenti domande:

* **Il nuovo database si trova su un nuovo server?** Prima di inviare una richiesta, aggiornare le impostazioni della connessione dati in **[!UICONTROL Manage Data** > **Connections]**. Se è necessario un aggiornamento su come eseguire questa operazione, passare alla sezione [`Integrations`](../integrations/integrations.md) e trovare le istruzioni per il tipo di database utilizzato.

* **Nel nuovo database sono presenti tutti i dati storici o è necessario eseguirne la migrazione?** È possibile consolidare i dati storici e i nuovi dati durante il processo di migrazione. Anche se non hai bisogno di un consolidamento, comunicaci nella tua richiesta.

Dopo aver ricevuto le risposte a quanto sopra, è necessario conoscere il tipo di migrazione. Il nuovo database avrà lo schema [`same`](#sameschema) o uno schema [`different`](#newschema)? Nelle discussioni seguenti trovi istruzioni dettagliate per ciascun tipo di migrazione.

## Migrazione a un nuovo database con lo stesso schema {#sameschema}

Quando si invia la richiesta, verificare che lo schema del database non stia cambiando e che la connessione sia già impostata in [!DNL Adobe Commerce Intelligence].

Se il database ha un nuovo nome, includilo nella richiesta in modo che sia possibile migrare correttamente le dashboard.

Se il nome del database non viene modificato, la migrazione è completa. Le dashboard e i rapporti verranno aggiornati al termine del prossimo aggiornamento completo.

## Migrazione a un nuovo database con uno schema diverso {#newschema}

>[!IMPORTANT]
>
>Se alcune colonne di dati non hanno colonne equivalenti nel nuovo database, è possibile che alcune analisi vadano perse nel processo.

Per completare correttamente questo tipo di migrazione, le colonne di dati esistenti devono corrispondere ai loro equivalenti nel nuovo database. Questo non è obbligatorio, ma l’esecuzione della corrispondenza per Dell consente di velocizzare il tempo di risposta della richiesta e ridurre il prezzo della migrazione.

Se ti senti a tuo agio a fare da solo la corrispondenza, segui queste istruzioni e allega alla tua richiesta il foglio di calcolo finito:

1. Esaminare tutte le tabelle e le colonne attualmente sincronizzate con il Data Warehouse (**[!UICONTROL Manage Data** > **Data Warehouse]**).

1. In un foglio di calcolo creare una scheda per ogni tabella da migrare al nuovo database.

1. In ogni scheda, crea una colonna per tutte le colonne esistenti da migrare. Adobe consiglia di denominarlo in modo analogo a `Existing column name`.

1. È inoltre necessario creare un&#39;altra colonna per gli equivalenti di colonna nel nuovo database in ogni scheda del foglio di calcolo. Adobe consiglia di denominare la colonna in modo analogo a `New column name`.

1. Inserire le colonne esistenti e le relative equivalenti. Se una colonna esistente non ha un nuovo equivalente, immettere `N/A`.

   Inoltre, se esiste un nuovo metodo per calcolare le stesse informazioni nel nuovo database, immetterlo nella colonna [`New column name`].

Ecco un esempio:

![Modello per foglio di calcolo migrazione con schema di database e struttura di tabella](../../../assets/Migration_Spreadsheet.png)

>[!NOTE]
>
>Se alcune colonne di dati non hanno colonne equivalenti nel nuovo database, è possibile che alcune analisi vadano perse nel processo.

## Come si invia una richiesta? {#submitreq}

Puoi contattarci inviando [una richiesta di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

Se hai seguito i passaggi della sezione precedente per creare il foglio di calcolo corrispondente alle colonne, non dimenticare di allegarlo.

## Cosa succede dopo? {#wrapup}

La determinazione dell’ambito del progetto richiede una certa collaborazione tra l’utente e l’analista del team di Commerce Services che esegue la migrazione. La complessità delle modifiche e la reattività dell’utente e dell’analista influiscono direttamente sul tempo necessario per la migrazione. Dopo aver individuato i dettagli, verrà stabilita una sequenza temporale e inviata all&#39;utente con una descrizione del lavoro.
