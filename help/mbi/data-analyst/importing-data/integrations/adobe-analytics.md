---
title: Connettere Adobe Analytics
description: Scopri come unire l'obiettivo di percorso del cliente end-to-end di  [!DNL Adobe Analytics]  e l'obiettivo di e-commerce su cui fai affidamento [!DNL Commerce Intelligence].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Connetti [!DNL Adobe Analytics]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![](../../../assets/adobe-analytic-slogo.png)

L&#39;integrazione di [!DNL Adobe Analytics] per [!DNL Adobe Commerce Intelligence] consente di riunire l&#39;attenzione del percorso clienti end-to-end di [!DNL Adobe Analytics] e l&#39;attenzione eCommerce su cui ci si basa da [!DNL Commerce Intelligence]. In questo modo è possibile avere un quadro completo delle prestazioni complessive del negozio.

In particolare, l&#39;integrazione di [!DNL Adobe Analytics] per [!DNL Commerce Intelligence] fornisce funzionalità per consentire ai commercianti di iniziare a combinare i set di dati [!DNL Adobe Commerce] e [!DNL Adobe Analytics].

- Crea una connessione dal tuo account [!DNL Adobe Analytics] esistente in [!DNL Commerce Intelligence].

- Seleziona fino a 25 metriche e dimensioni da una singola suite di rapporti per replicarle nella tua Data Warehouse.

- Utilizza tutte le funzionalità standard di [!DNL Commerce Intelligence] per trasformare, unire e creare report sui dati [!DNL Adobe Analytics] replicati.

## Prerequisiti per la connessione

Per la connessione sono necessarie le seguenti informazioni:

- Credenziali di accesso [!DNL Adobe Analytics]

- `Name` e/o `ID` di [!DNL Adobe Analytics] suite di rapporti per replicare i dati da

- Elenco di metriche e dimensioni da replicare in [!DNL Commerce Intelligence]

## Connessione all&#39;integrazione [!DNL Adobe Analytics] per [!DNL Commerce Intelligence]

1. Passare alla pagina `Integrations` in **[!DNL Manage Data** > **Integrations]**.

1. Fare clic su **[!UICONTROL Add an Integration]**.

1. Fare clic sull&#39;icona **[!UICONTROL Adobe Analytics]** per accedere alla pagina che consente di autorizzare la connessione dell&#39;account [!DNL Adobe Analytics].

1. Fare clic su **[!UICONTROL Authorize with Adobe Analytics]**.

1. Immetti le tue credenziali di [!DNL Adobe Analytics]. Dopo l&#39;autorizzazione, si verrà reindirizzati a [!DNL Commerce Intelligence].

1. Viene visualizzato un elenco delle suite di rapporti disponibili. Selezionare la suite di rapporti da cui importare i dati, quindi fare clic su **[!UICONTROL Continue]**.

1. Viene visualizzata la schermata di selezione delle metriche e delle dimensioni. Seleziona almeno una metrica e almeno una dimensione, fino a un totale combinato di 25 metriche e dimensioni. Cerca per nome o scorri per trovare i componenti, quindi fai clic sulle caselle di controllo per selezionare. Fare clic su **[!UICONTROL Continue]**.

1. La suite di rapporti selezionata viene visualizzata in una tabella. Fai clic su **[!UICONTROL Save]** per confermare la selezione.

1. Informare il [!DNL Commerce Intelligence] [team di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=it) che l&#39;integrazione è autorizzata ed eseguono il processo di connessione iniziale.

Dopo l&#39;esecuzione della connessione iniziale, la tabella sarà disponibile nella pagina Data Warehouse, nella scheda `All Tables`. Seleziona le colonne da replicare per visualizzare i dati dopo il prossimo aggiornamento completo.
