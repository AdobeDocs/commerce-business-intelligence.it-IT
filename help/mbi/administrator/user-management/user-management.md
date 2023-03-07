---
title: Gestione di utenti e autorizzazioni
description: Scopri come gestire il tuo [!DNL MBI] utenti.
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# Gestire le autorizzazioni utente

MBI è concepito come un&#39;unica fonte di verità per tutta l&#39;organizzazione. Ogni utente dispone di un proprio set di dashboard che può [condividi con altri utenti](../../data-user/dashboards/share-dashboard-with-users.md).

## Livelli di autorizzazione utente

In entrata [!DNL MBI], esistono tre livelli di autorizzazione generali che si applicano agli utenti, che vengono selezionati al momento della creazione di un account:

* `Admin`
* `Standard`
* `Read-Only`

Queste autorizzazioni consentono agli utenti di eseguire determinate azioni o di accedere a parti specifiche di [!DNL MBI]. Di seguito è riportata una tabella delle operazioni che ogni livello di autorizzazione può eseguire in MBI:

|  | `Admin` | `Standard` | `Read Only` |
| -----|-----|-----|----|
| **Crea/gestisci utenti** | ✔ |  |  |
| **Creare riepiloghi e-mail** | ✔ | ✔ |  |
| **Creare/modificare/condividere dashboard** | ✔ | ✔ |  |
| **Visualizza dashboard** | ✔ | ✔ | ✔ |
| **Creare/modificare/eliminare rapporti visivi** | ✔ | ✔* |  |
| **Creare/modificare/eliminare i report SQL** | ✔ |  |  |
| **Clona dashboard** | ✔ |  |  |
| **Aggiungere/gestire le integrazioni** | ✔ |  |  |
| **Accedere a Gestione Date Warehouse** | ✔ |  |  |
| **Sincronizza/Annulla sincronizzazione tabelle e colonne** | ✔ |  |  |
| **Creare/modificare metriche** | ✔ |  |  |
| **Creare/modificare set di filtri** | ✔ |  |  |
| **Crea/modifica colonne calcolate** | ✔ |  |  |
| **Creare un elenco di rapporti dipendenti** | ✔ |  |  |
| **Riepilogo del sistema di accesso** | ✔ |  |  |
| **Accedere alle impostazioni del fuso orario** | ✔ |  |  |
| **Fatturazione degli accessi** | ✔ | ✔** |  |
| **Contatta il supporto** | ✔ | ✔ | ✔ |

{style="table-layout:auto"}

>[!NOTE]
>
>_È possibile limitare una **[!UICONTROL Standard]**dell&#39;utente [accesso a metriche specifiche](../../administrator/user-management/restrict-metric-access.md)._
>
>**[!UICONTROL Standard] _Gli utenti possono accedere a Fatturazione con un’impostazione di autorizzazione aggiuntiva._
>
>**[!UICONTROL Read-Only]** gli utenti possono solo _visualizza_ le dashboard condivise con loro; non possono creare o modificare nulla in [!DNL MBI], né possono cercare e aggiungere nuove dashboard al proprio account. L’Adobe consiglia di condividere un set specifico di dashboard con **[!UICONTROL Read-Only]** utenti gestiti dall&#39;utente o da un altro membro del team. Non clonare un set di dashboard.

## Autorizzazioni aggiuntive: fatturazione e tecniche {#billingtech}

Oltre ai livelli di autorizzazione generali, esistono altre due denominazioni utente: `Billing` e `Technical`. Queste designazioni devono essere utilizzate con i livelli di autorizzazione generali.

### Fatturazione

`Billing` Gli utenti possono accedere alla pagina di fatturazione e modificare le informazioni di pagamento. Inoltre, possono anche essere contattati da un Adobe per le domande di fatturazione.

`Admin` gli utenti hanno accesso al `Billing` per impostazione predefinita, ma `Standard` Gli utenti possono accedere anche se dispongono di `Billing` selezionata nel profilo.

![fatturazione](../../assets/billing.png)<!--{: width="550" height="363"}-->

### Tecnico

`Technical` Gli utenti non dispongono di autorizzazioni specifiche: questa impostazione contrassegna semplicemente un contatto tecnico all’interno della tua organizzazione. Questi utenti possono essere contattati da un Adobe per domande tecniche.

`Admin` gli utenti possono aggiungere nuovi utenti al proprio account facendo clic su **[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]** e seguendo le istruzioni. Dopo la creazione dell’utente in [!DNL MBI], la persona fortunata che stai invitando riceverà e-mail di istruzioni su come completare il processo di configurazione dell’account.

In qualsiasi momento, `Admins` può visualizzare tutti gli utenti nel loro account facendo clic su **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**. In questa pagina vengono visualizzate le autorizzazioni dell’utente e le metriche e dashboard a cui può accedere.
