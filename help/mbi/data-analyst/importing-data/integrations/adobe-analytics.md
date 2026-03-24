---
title: Connettere Adobe Analytics
description: Scopri come unire l'obiettivo di percorso del cliente end-to-end di  [!DNL Adobe Analytics]  e l'obiettivo di e-commerce su cui fai affidamento [!DNL Commerce Intelligence].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/KkiKySM2q8ewqhQ1kdUjLuTM4iOpzrZb5Ok-UvBBpJE
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 312
ht-degree: 0%

---

# Connetti [!DNL Adobe Analytics]

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../../administrator/user-management/user-management.md).

![Logo Adobe Analytics](../../../assets/adobe-analytic-slogo.png)

L&#39;integrazione di [!DNL Adobe Analytics] per [!DNL Adobe Commerce Intelligence] consente di riunire l&#39;attenzione del percorso clienti end-to-end di [!DNL Adobe Analytics] e l&#39;attenzione eCommerce su cui ci si basa da [!DNL Commerce Intelligence]. In questo modo è possibile avere un quadro completo delle prestazioni complessive del negozio.

In particolare, l&#39;integrazione di [!DNL Adobe Analytics] per [!DNL Commerce Intelligence] fornisce funzionalità per consentire ai commercianti di iniziare a combinare i set di dati [!DNL Adobe Commerce] e [!DNL Adobe Analytics].

- Crea una connessione dal tuo account [!DNL Adobe Analytics] esistente in [!DNL Commerce Intelligence].

- Seleziona fino a 25 metriche e dimensioni da una suite di rapporti per replicarle nel Data Warehouse.

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

Dopo l&#39;esecuzione del processo di connessione iniziale, la tabella sarà disponibile nella pagina Data Warehouse, nella scheda `All Tables`. Seleziona le colonne da replicare per visualizzare i dati dopo il prossimo aggiornamento completo.
