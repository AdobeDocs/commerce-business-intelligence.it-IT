---
title: Gestione di utenti e autorizzazioni di Adobe Commerce
description: Scopri come gestire gli utenti di Commerce Intelligence.
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Gestire le autorizzazioni utente

[!DNL Adobe Commerce Intelligence] deve essere un’unica fonte di verità per la tua organizzazione. Ogni utente dispone di un proprio set di dashboard che può [condividi con altri utenti](../../data-user/dashboards/share-dashboard-with-users.md).

## Livelli di autorizzazione utente

In entrata [!DNL Commerce Intelligence], esistono tre livelli di autorizzazione generali che si applicano agli utenti, che vengono selezionati al momento della creazione di un account:

* `Admin`
* `Standard`
* `Read-Only`

Queste autorizzazioni consentono agli utenti di eseguire determinate azioni o di accedere a parti specifiche di [!DNL Commerce Intelligence]. Di seguito è riportata una tabella delle operazioni che ogni livello di autorizzazione può eseguire in [!DNL Commerce Intelligence]:

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
>**[!UICONTROL Read-Only]** gli utenti possono solo _visualizza_ le dashboard condivise con loro; non possono creare o modificare nulla in [!DNL Commerce Intelligence], né possono cercare e aggiungere nuove dashboard al proprio account. L’Adobe consiglia di condividere un set specifico di dashboard con **[!UICONTROL Read-Only]** utenti gestiti dall&#39;utente o da un altro membro del team. Non clonare un set di dashboard.

## Autorizzazioni aggiuntive: fatturazione e tecniche {#billingtech}

Oltre ai livelli di autorizzazione generali, esistono altre due denominazioni utente: `Billing` e `Technical`. Queste designazioni devono essere utilizzate con i livelli di autorizzazione generali.

### Fatturazione

`Billing` Gli utenti possono accedere alla pagina di fatturazione e modificare le informazioni di pagamento. Inoltre, possono anche essere contattati da un Adobe per le domande di fatturazione.

`Admin` gli utenti hanno accesso al `Billing` per impostazione predefinita, ma `Standard` Gli utenti possono accedere anche se dispongono di `Billing` selezionata nel profilo.

![fatturazione](../../assets/billing.png)<!--{: width="550" height="363"}-->

### Tecnico

`Technical` Gli utenti non dispongono di autorizzazioni specifiche: questa impostazione contrassegna semplicemente un contatto tecnico all’interno della tua organizzazione. Questi utenti possono essere contattati da un Adobe per domande tecniche.

`Admin` gli utenti possono aggiungere nuovi utenti al proprio account facendo clic su **[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]** e seguendo le istruzioni. Dopo la creazione dell’utente in [!DNL Commerce Intelligence], la persona fortunata che stai invitando riceverà e-mail di istruzioni su come completare il processo di configurazione dell’account.

In qualsiasi momento, `Admins` può visualizzare tutti gli utenti nel loro account facendo clic su **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**. In questa pagina vengono visualizzate le autorizzazioni dell’utente e le metriche e dashboard a cui può accedere.
