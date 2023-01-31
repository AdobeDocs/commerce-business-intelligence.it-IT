---
title: Connetti Adobe Analytics
description: Scopri come mettere a fuoco il percorso end-to-end dei clienti [!DNL Adobe Analytics] e l'eCommerce [!DNL MBI].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Connetti [!DNL Adobe Analytics]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![](../../../assets/adobe-analytic-slogo.png)

La [!DNL Adobe Analytics] integrazione per [!DNL MBI] consente di mettere a fuoco il percorso end-to-end dei clienti [!DNL Adobe Analytics] e l&#39;eCommerce [!DNL MBI]per ottenere un quadro più completo delle prestazioni complessive del tuo negozio.

Più specificamente, la [!DNL Adobe Analytics] integrazione per [!DNL MBI] fornisce funzionalità che consentono ai commercianti di iniziare a combinare i set di dati Commerce e Analytics.
- Crea una connessione dal tuo esistente [!DNL Adobe Analytics] tenere conto [!DNL MBI].
- Seleziona fino a 25 metriche e dimensioni da una suite di rapporti per replicarle nel tuo [!DNL MBI] data warehouse.
- Usa tutti gli standard [!DNL MBI] funzionalità per trasformare, unire e creare rapporti sulle repliche [!DNL Adobe Analytics] dati.

## Prerequisiti per la connessione

Per la connessione sono necessarie le seguenti informazioni:
- [!DNL Adobe Analytics] credenziali di accesso
- `Name` e/o `ID` di [!DNL Adobe Analytics] suite di rapporti da cui replicare i dati
- Elenco di metriche e dimensioni in cui replicare [!DNL MBI]

## Collegamento della [!DNL Adobe Analytics] Integrazione per MBI

1. Vai a `Integrations` pagina sotto **[!DNL Manage Data** > **Integrations]**.
1. Fai clic su **[!UICONTROL Add an Integration]**, situato sul lato destro dello schermo.
1. Fai clic sul pulsante **[!UICONTROL Adobe Analytics]** per accedere alla pagina che consente di autorizzare [!DNL Adobe Analytics] connessione dell&#39;account.
1. Fai clic su **[!UICONTROL Authorize with Adobe Analytics]**.
1. Inserisci il tuo [!DNL Adobe Analytics] credenziali. Dopo l&#39;autorizzazione, viene reindirizzato a [!DNL MBI].
1. Viene visualizzato un elenco delle suite di rapporti disponibili. Seleziona la suite di rapporti da cui vuoi importare i dati, quindi fai clic su **[!UICONTROL Continue]**.
1. Viene visualizzata la schermata di selezione delle metriche e delle dimensioni. Seleziona almeno una metrica e almeno una dimensione, fino a un totale combinato di 25 metriche e dimensioni. Cerca per nome o scorri per trovare i componenti, quindi fai clic sulle caselle di controllo da selezionare. Fai clic su **[!UICONTROL Continue]**.
1. La suite di rapporti selezionata viene visualizzata in una tabella. Fai clic su **[!UICONTROL Save]** per confermare la selezione.
1. Informa il [!DNL MBI] Supporta il team autorizzato per l’integrazione e il processo di connessione iniziale verrà eseguito automaticamente.

Dopo l’esecuzione del processo di connessione iniziale, la tabella sarà disponibile nella pagina Data Warehouse, nella sezione `All Tables` scheda . Seleziona le colonne da replicare e i dati verranno visualizzati dopo il prossimo aggiornamento completo.
