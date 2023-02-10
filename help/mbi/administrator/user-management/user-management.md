---
title: Gestione di utenti e autorizzazioni
description: Scopri come gestire il tuo [!DNL MBI] utenti.
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# Gestione delle autorizzazioni utente

MBI è destinato a essere un’unica fonte di verità in tutta l’organizzazione. Ogni utente avrà un proprio set di dashboard che può [condividere con altri utenti](../../data-user/dashboards/share-dashboard-with-users.md).

## Livelli di autorizzazione utente

In [!DNL MBI], esistono tre livelli di autorizzazione generali applicabili agli utenti, che vengono selezionati al momento della creazione di un account:

* `Admin`
* `Standard`
* `Read-Only`

Queste autorizzazioni consentono agli utenti di eseguire determinate azioni o di accedere a parti specifiche di [!DNL MBI]. Di seguito è riportata una tabella delle operazioni che ogni livello di autorizzazione può eseguire in MBI:

|  | `Admin` | `Standard` | `Read Only` |
| -----|-----|-----|----|
| **Creare/gestire utenti** | ✔ |  |  |
| **Creazione di riepiloghi e-mail** | ✔ | ✔ |  |
| **Creare/modificare/condividere dashboard** | ✔ | ✔ |  |
| **Visualizzare le dashboard** | ✔ | ✔ | ✔ |
| **Creare/modificare/eliminare rapporti visivi** | ✔ | ✔* |  |
| **Creare/modificare/eliminare rapporti SQL** | ✔ |  |  |
| **Dashboard duplicati** | ✔ |  |  |
| **Aggiungi/gestisci integrazioni** | ✔ |  |  |
| **Accedere a Data Warehouse Manager** | ✔ |  |  |
| **Tabelle e colonne sincronizzate/non sincronizzate** | ✔ |  |  |
| **Creare/modificare metriche** | ✔ |  |  |
| **Creare/modificare set di filtri** | ✔ |  |  |
| **Creare/modificare colonne calcolate** | ✔ |  |  |
| **Crea elenco di rapporti dipendenti** | ✔ |  |  |
| **Riepilogo del sistema di accesso** | ✔ |  |  |
| **Accedere alle impostazioni del fuso orario** | ✔ |  |  |
| **Fatturazione degli accessi** | ✔ | ✔** |  |
| **Contatta il supporto** | ✔ | ✔ | ✔ |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>_Puoi limitare un **[!UICONTROL Standard]**dell&#39;utente [accesso a metriche specifiche](../../administrator/user-management/restrict-metric-access.md)._
>
>**[!UICONTROL Standard] _gli utenti possono accedere a Fatturazione con un’impostazione di autorizzazione aggiuntiva._
>
>**[!UICONTROL Read-Only]** gli utenti possono solo _visualizzare_ dashboard condivisi con loro; non possono creare o modificare nulla in [!DNL MBI], né possono cercare e aggiungere nuove dashboard al proprio account. È consigliabile condividere un set specifico di dashboard con **[!UICONTROL Read-Only]** utenti gestiti da te o da un altro membro del tuo team. Non clonare un set di dashboard per loro.

## Autorizzazioni aggiuntive: Fatturazione e tecnica {#billingtech}

Oltre ai livelli generali di autorizzazione, esistono anche altre due denominazioni utente: `Billing` e `Technical`. Tali denominazioni sono destinate ad essere utilizzate congiuntamente ai livelli generali di autorizzazione.

### Fatturazione

`Billing` gli utenti hanno accesso alla pagina di fatturazione e possono modificare le informazioni di pagamento. Inoltre, possono essere contattati dai nostri team per domande di fatturazione.

`Admin` gli utenti hanno accesso alla scheda Fatturazione per impostazione predefinita, ma gli utenti Standard possono anche accedervi se dispongono della `Billing` selezionare una casella di controllo sul profilo.

![fatturazione](../../assets/billing.png)<!--{: width="550" height="363"}-->

### Tecnico

`Technical` gli utenti non dispongono di autorizzazioni specifiche per loro - questa impostazione contrassegna solo un contatto tecnico all’interno della tua organizzazione. Questi utenti possono essere contattati dai nostri team per domande tecniche.

`Admin` gli utenti possono aggiungere nuovi utenti al proprio account facendo clic su **[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]** e seguendo le istruzioni. Dopo la creazione dell&#39;utente in [!DNL MBI], la persona fortunata che stai invitando riceverà le istruzioni e-mail su come completare il processo di configurazione dell’account.

In qualsiasi momento, `Admins` può visualizzare tutti gli utenti nel loro account facendo clic su **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**. In questa pagina vengono visualizzate le autorizzazioni dell’utente e le metriche e i dashboard a cui hanno accesso.
