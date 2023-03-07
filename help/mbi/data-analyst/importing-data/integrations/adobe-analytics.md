---
title: Connettere Adobe Analytics
description: Scopri come unire l’attenzione end-to-end del cliente al percorso di [!DNL Adobe Analytics] e l’eCommerce su cui fai affidamento [!DNL MBI].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---

# Connetti [!DNL Adobe Analytics]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![](../../../assets/adobe-analytic-slogo.png)

Il [!DNL Adobe Analytics] integrazione per [!DNL MBI] consente di unire l&#39;attenzione end-to-end al percorso del cliente di [!DNL Adobe Analytics] e l’eCommerce su cui fai affidamento [!DNL MBI]. In questo modo è possibile avere un quadro completo delle prestazioni complessive del negozio.

In particolare, [!DNL Adobe Analytics] integrazione per [!DNL MBI] fornisce funzionalità che consentono agli esercenti di iniziare a combinare i set di dati di Commerce e Analytics.
- Crea una connessione dal tuo [!DNL Adobe Analytics] account in [!DNL MBI].
- Seleziona fino a 25 metriche e dimensioni da una suite di rapporti per replicarle nel tuo [!DNL MBI] Data Warehouse.
- Usa tutti gli standard [!DNL MBI] funzionalità per trasformare, unire e creare report sulle replicate [!DNL Adobe Analytics] dati.

## Prerequisiti per la connessione

Per la connessione sono necessarie le seguenti informazioni:
- [!DNL Adobe Analytics] credenziali di accesso
- `Name` e/o `ID` di [!DNL Adobe Analytics] suite di rapporti da cui replicare i dati
- Elenco di metriche e dimensioni da replicare in [!DNL MBI]

## Collegamento di [!DNL Adobe Analytics] Integrazione per MBI

1. Vai a `Integrations` pagina in **[!DNL Manage Data** > **Integrations]**.
1. Clic **[!UICONTROL Add an Integration]**, situato sul lato destro dello schermo.
1. Fai clic su **[!UICONTROL Adobe Analytics]** per accedere alla pagina che ti consente di autorizzare il tuo [!DNL Adobe Analytics] connessione dell’account.
1. Clic **[!UICONTROL Authorize with Adobe Analytics]**.
1. Immetti il [!DNL Adobe Analytics] credenziali. Dopo aver ricevuto l’autorizzazione, verrai reindirizzato a [!DNL MBI].
1. Viene visualizzato un elenco delle suite di rapporti disponibili. Seleziona la suite di rapporti da cui desideri importare i dati, quindi fai clic su **[!UICONTROL Continue]**.
1. Viene visualizzata la schermata di selezione delle metriche e delle dimensioni. Seleziona almeno una metrica e almeno una dimensione, fino a un totale combinato di 25 metriche e dimensioni. Cerca per nome o scorri per trovare i componenti, quindi fai clic sulle caselle di controllo per selezionare. Clic **[!UICONTROL Continue]**.
1. La suite di rapporti selezionata viene visualizzata in una tabella. Clic **[!UICONTROL Save]** per confermare la selezione.
1. Informa il [!DNL MBI] Il team di supporto che richiede l’autorizzazione per l’integrazione e che esegue automaticamente il processo di connessione iniziale.

Dopo l&#39;esecuzione del processo di connessione iniziale, la tabella sarà disponibile nella pagina Data Warehouse, sotto `All Tables` scheda. Seleziona le colonne da replicare per visualizzare i dati dopo il prossimo aggiornamento completo.
