---
title: Gestione dashboard
description: Scopri come gestire le autorizzazioni utente per i dashboard di tua proprietà, eliminare i dashboard non più necessari e impostare un dashboard predefinito.
exl-id: 32c21093-2a7d-4d8e-afc0-19bd702f9b36
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Gestire un dashboard

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../administrator/user-management/user-management.md).

In **[!DNL Manage Data** > **Dashboards]** è possibile gestire le autorizzazioni utente per i dashboard di tua proprietà, eliminare i dashboard non più necessari e impostare un dashboard predefinito. Questo argomento riguarda:

1. [Ridenominazione delle dashboard](#rename)

1. [Gestione delle autorizzazioni del dashboard](#userperm)

1. [Modifica del dashboard predefinito](#default)

1. [Eliminazione delle dashboard](#delete)

## Rinominare un dashboard {#rename}

Per rinominare un dashboard:

1. Fare clic sul nome del dashboard che si desidera modificare.

2. Immettere il nuovo nome nel campo `Dashboard Name`.

## Gestione autorizzazioni utente {#userperm}

In [!DNL Commerce Intelligence] sono presenti tre livelli di accesso per le dashboard: `View`, `Edit` e `None`.

* `View` consente agli utenti selezionati di visualizzare il dashboard ma non di modificarlo. Gli utenti possono inoltre ridimensionare i grafici, esportare i dati e copiarli nei propri dashboard utilizzando la funzione Salva con nome se dispongono delle autorizzazioni Standard o Admin.

* `Edit` consente agli utenti selezionati di modificare e salvare grafici in questo dashboard se dispongono di autorizzazioni Standard o Admin. Gli utenti con autorizzazioni di modifica possono inoltre condividere dashboard con altri utenti.

* `None` significa che gli utenti selezionati non possono visualizzare o modificare questo dashboard.

Le autorizzazioni utente possono essere modificate in due modi: per tutti gli utenti o per un singolo utente.

1. *Per modificare le autorizzazioni di tutti gli utenti,* utilizza il menu a discesa accanto all&#39;etichetta `Set all users' permissions to…`.

1. *Per modificare le autorizzazioni di un singolo utente,* utilizzare il menu a discesa accanto al nome dell&#39;utente per impostare il livello di accesso desiderato.

## Modificare il dashboard predefinito {#default}

Per modificare il dashboard predefinito per l’account:

1. Fare clic sul nome del dashboard che si desidera impostare come predefinito.

1. Fare clic su **[!UICONTROL Make Default]**.

## Elimina dashboard {#delete}

Per eliminare un dashboard:

1. Fare clic sul nome del dashboard che si desidera eliminare.

1. Fare clic su **[!UICONTROL Delete Dashboard]**.
