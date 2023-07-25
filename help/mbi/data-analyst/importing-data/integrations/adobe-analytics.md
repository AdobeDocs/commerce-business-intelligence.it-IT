---
title: Connettere Adobe Analytics
description: Scopri come unire l’attenzione end-to-end del cliente al percorso di [!DNL Adobe Analytics] e l’eCommerce su cui fai affidamento [!DNL Commerce Intelligence].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Connetti [!DNL Adobe Analytics]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![](../../../assets/adobe-analytic-slogo.png)

Il [!DNL Adobe Analytics] integrazione per [!DNL Adobe Commerce Intelligence] consente di unire l&#39;attenzione end-to-end al percorso del cliente di [!DNL Adobe Analytics] e l’eCommerce su cui fai affidamento [!DNL Commerce Intelligence]. In questo modo è possibile avere un quadro completo delle prestazioni complessive del negozio.

In particolare, [!DNL Adobe Analytics] integrazione per [!DNL Commerce Intelligence] offre agli esercenti la possibilità di combinare [!DNL Adobe Commerce] e [!DNL Adobe Analytics] set di dati.

- Crea una connessione dal tuo [!DNL Adobe Analytics] account in [!DNL Commerce Intelligence].

- Seleziona fino a 25 metriche e dimensioni da una singola suite di rapporti per replicarle nella tua Data Warehouse.

- Usa tutti gli standard [!DNL Commerce Intelligence] funzionalità per trasformare, unire e creare report sulle replicate [!DNL Adobe Analytics] dati.

## Prerequisiti per la connessione

Per la connessione sono necessarie le seguenti informazioni:

- [!DNL Adobe Analytics] credenziali di accesso

- `Name` e/o `ID` di [!DNL Adobe Analytics] suite di rapporti da cui replicare i dati

- Elenco di metriche e dimensioni da replicare in [!DNL Commerce Intelligence]

## Collegamento di [!DNL Adobe Analytics] Integrazione per [!DNL Commerce Intelligence]

1. Vai a `Integrations` pagina in **[!DNL Manage Data** > **Integrations]**.

1. Clic **[!UICONTROL Add an Integration]**.

1. Fai clic su **[!UICONTROL Adobe Analytics]** per accedere alla pagina che ti consente di autorizzare il tuo [!DNL Adobe Analytics] connessione dell’account.

1. Clic **[!UICONTROL Authorize with Adobe Analytics]**.

1. Immetti il [!DNL Adobe Analytics] credenziali. Dopo aver ricevuto l’autorizzazione, verrai reindirizzato a [!DNL Commerce Intelligence].

1. Viene visualizzato un elenco delle suite di rapporti disponibili. Seleziona la suite di rapporti da cui desideri importare i dati, quindi fai clic su **[!UICONTROL Continue]**.

1. Viene visualizzata la schermata di selezione delle metriche e delle dimensioni. Seleziona almeno una metrica e almeno una dimensione, fino a un totale combinato di 25 metriche e dimensioni. Cerca per nome o scorri per trovare i componenti, quindi fai clic sulle caselle di controllo per selezionare. Clic **[!UICONTROL Continue]**.

1. La suite di rapporti selezionata viene visualizzata in una tabella. Clic **[!UICONTROL Save]** per confermare la selezione.

1. Informa il [!DNL Commerce Intelligence] [Team di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) che la tua integrazione è autorizzata ed eseguono per te il processo di connessione iniziale.

Dopo l&#39;esecuzione del processo di connessione iniziale, la tabella sarà disponibile nella pagina Data Warehouse, sotto `All Tables` scheda. Seleziona le colonne da replicare per visualizzare i dati dopo il prossimo aggiornamento completo.
