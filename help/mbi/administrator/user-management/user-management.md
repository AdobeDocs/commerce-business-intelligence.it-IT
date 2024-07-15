---
title: Gestione di utenti e autorizzazioni di Adobe Commerce
description: Scopri come gestire gli utenti di Commerce Intelligence.
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
role: Admin, User
feature: User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# Gestire le autorizzazioni utente

[!DNL Adobe Commerce Intelligence] deve essere un&#39;unica fonte di verità per tutta l&#39;organizzazione. Ogni utente dispone di un proprio set di dashboard che può [condividere con altri utenti](../../data-user/dashboards/share-dashboard-with-users.md).

## Livelli di autorizzazione utente

In [!DNL Commerce Intelligence] sono disponibili tre livelli di autorizzazione generali applicabili agli utenti, selezionati al momento della creazione di un account:

* `Admin`
* `Standard`
* `Read-Only`

Queste autorizzazioni consentono agli utenti di eseguire determinate azioni o di accedere a parti specifiche di [!DNL Commerce Intelligence]. Di seguito è riportata una tabella delle operazioni che ogni livello di autorizzazione può eseguire in [!DNL Commerce Intelligence]:

|   | `Admin` | `Standard` | `Read Only` |
| -----|-----|-----|----|
| **Crea/gestisci utenti** | ✔ |   |   |
| **Crea riepilogo e-mail** | ✔ | ✔ |   |
| **Creare/modificare/condividere dashboard** | ✔ | ✔ |   |
| **Visualizza dashboard** | ✔ | ✔ | ✔ |
| **Creare/modificare/eliminare rapporti visivi** | ✔ | ✔* |   |
| **Creare/modificare/eliminare i report SQL** | ✔ |  |   |
| **Clona dashboard** | ✔ |   |   |
| **Aggiungi/gestisci integrazioni** | ✔ |   |   |
| **Accedere a Gestione Date Warehouse** | ✔ |   |   |
| **Sincronizza/Annulla sincronizzazione tabelle e colonne** | ✔ |   |   |
| **Crea/modifica metriche** | ✔ |   |   |
| **Crea/modifica set di filtri** | ✔ |   |   |
| **Crea/modifica colonne calcolate** | ✔ |   |   |
| **Crea elenco di report dipendenti** | ✔ |   |   |
| **Riepilogo accesso** | ✔ |   |   |
| **Accedere alle impostazioni del fuso orario** | ✔ |   |   |
| **Accedi alla fatturazione** | ✔ | ✔** |   |
| **Contatta il supporto** | ✔ | ✔ | ✔ |

{style="table-layout:auto"}

>[!NOTE]
>
>_È possibile limitare l&#39;[accesso di un utente **[!UICONTROL Standard]**a metriche specifiche](../../administrator/user-management/restrict-metric-access.md)._
>
>**[!UICONTROL Standard] _gli utenti possono accedere alla fatturazione con un&#39;impostazione di autorizzazione aggiuntiva._
>
>Gli utenti di **[!UICONTROL Read-Only]** possono solo _visualizzare_ dashboard che sono stati condivisi con loro; non possono creare o modificare nulla in [!DNL Commerce Intelligence], né cercare e aggiungere nuovi dashboard al loro account. L&#39;Adobe consiglia di condividere un set specifico di dashboard con **[!UICONTROL Read-Only]** utenti gestiti dall&#39;utente o da un altro membro del team. Non clonare un set di dashboard.

## Autorizzazioni aggiuntive: fatturazione e tecniche {#billingtech}

Oltre ai livelli di autorizzazione generali, esistono altre due designazioni utente: `Billing` e `Technical`. Queste designazioni devono essere utilizzate con i livelli di autorizzazione generali.

### Fatturazione

`Billing` utenti hanno accesso alla pagina di fatturazione e possono modificare le informazioni di pagamento. Inoltre, possono anche essere contattati da un Adobe per le domande di fatturazione.

`Admin` utenti hanno accesso alla scheda `Billing` per impostazione predefinita, ma `Standard` utenti possono anche ottenere l&#39;accesso se hanno la casella di controllo `Billing` selezionata sul loro profilo.

![fatturazione](../../assets/billing.png)<!--{: width="550" height="363"}-->

### Tecnico

`Technical` utenti non dispongono di autorizzazioni specifiche. Questa impostazione contrassegna semplicemente un contatto tecnico all&#39;interno dell&#39;organizzazione. Questi utenti possono essere contattati da un Adobe per domande tecniche.

`Admin` utenti possono aggiungere nuovi utenti al proprio account facendo clic su **[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]** e seguendo le istruzioni. Dopo la creazione dell&#39;utente in [!DNL Commerce Intelligence], la persona fortunata che si sta invitando riceverà tramite e-mail istruzioni su come completare il processo di configurazione dell&#39;account.

In qualsiasi momento, `Admins` può visualizzare tutti gli utenti nel loro account facendo clic su **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**. In questa pagina vengono visualizzate le autorizzazioni dell’utente e le metriche e dashboard a cui può accedere.
