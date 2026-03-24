---
title: Gestione di utenti e autorizzazioni di Adobe Commerce
description: Scopri come gestire gli utenti di Commerce Intelligence.
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
role: Admin, User
feature: User Management
TQID: https://experienceleague.adobe.com/T3ZdoQW35n6CAJmDlOlfDVSI1eUA--e4RKZbOMF1BWY
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 406
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
| **Accedere a Data Warehouse Manager** | ✔ |   |   |
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
>_È possibile limitare l&#39;**[!UICONTROL Standard]**&#x200B;accesso di un utente [&#x200B; a metriche specifiche](../../administrator/user-management/restrict-metric-access.md)._
>
>**[!UICONTROL Standard] _gli utenti possono accedere alla fatturazione con un&#39;impostazione di autorizzazione aggiuntiva._
>
>Gli utenti di **[!UICONTROL Read-Only]** possono solo _visualizzare_ dashboard che sono stati condivisi con loro; non possono creare o modificare nulla in [!DNL Commerce Intelligence], né cercare e aggiungere nuovi dashboard al loro account. Adobe consiglia di condividere un set specifico di dashboard con **[!UICONTROL Read-Only]** utenti gestiti da te o da un altro membro del team. Non clonare un set di dashboard.

## Autorizzazioni aggiuntive: fatturazione e tecniche {#billingtech}

Oltre ai livelli di autorizzazione generali, esistono altre due designazioni utente: `Billing` e `Technical`. Queste designazioni devono essere utilizzate con i livelli di autorizzazione generali.

### Fatturazione

`Billing` utenti hanno accesso alla pagina di fatturazione e possono modificare le informazioni di pagamento. Inoltre, possono anche essere contattati da Adobe per le domande di fatturazione.

`Admin` utenti hanno accesso alla scheda `Billing` per impostazione predefinita, ma `Standard` utenti possono anche ottenere l&#39;accesso se hanno la casella di controllo `Billing` selezionata sul loro profilo.

![Pagina fatturazione](../../assets/billing.png)<!--{: width="550" height="363"}-->

### Tecnico

`Technical` utenti non dispongono di autorizzazioni specifiche. Questa impostazione contrassegna semplicemente un contatto tecnico all&#39;interno dell&#39;organizzazione. Adobe può contattare questi utenti per domande tecniche.

`Admin` utenti possono aggiungere nuovi utenti al proprio account facendo clic su **[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]** e seguendo le istruzioni. Dopo la creazione dell&#39;utente in [!DNL Commerce Intelligence], la persona fortunata che si sta invitando riceverà tramite e-mail istruzioni su come completare il processo di configurazione dell&#39;account.

In qualsiasi momento, `Admins` può visualizzare tutti gli utenti nel loro account facendo clic su **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**. In questa pagina vengono visualizzate le autorizzazioni dell’utente e le metriche e dashboard a cui può accedere.
