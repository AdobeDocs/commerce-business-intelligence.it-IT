---
title: Modificare la tabella operativa di una metrica
description: Scopri come modificare la tabella di dati utilizzata da una metrica per eseguire la sua operazione.
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/9yJ1Zc2NLDvXYO16UvDkeWE0hD1jx0-Ne3AyFFHX5ns
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
source-wordcount: 231
ht-degree: 0%

---

# Modificare la tabella operativa di una metrica

In alcuni casi, puoi decidere di modificare la tabella di dati utilizzata da una metrica per eseguire la sua operazione. Ad esempio, se si dispone di una nuova tabella utenti, si desidera migrare le metriche relative all&#39;utente dalla tabella `Users\_Old` per utilizzare la tabella `Users\_New`.

1. Vai a **[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. Fare clic su **[!UICONTROL Edit]** accanto alla metrica per la quale si desidera cambiare la tabella `operational`.
1. Nell&#39;editor, fare clic su **[!UICONTROL Change]**.

   ![Pagina di definizione della metrica con le impostazioni della tabella operativa](../../assets/change-metrics-1.png)
1. Seleziona la nuova tabella su cui desideri basare questa metrica.
1. Abbina le dimensioni dati esistenti a quelle corrispondenti nella nuova tabella. Se ad esempio si dispone di una colonna denominata `User's registration date`, è sufficiente selezionare la colonna nella nuova tabella che registra gli stessi dati di data. (Se nella nuova tabella non sono presenti colonne corrispondenti, vedere il passaggio successivo)

   ![Menu a discesa di selezione tabella che mostra le tabelle disponibili](../../assets/change-metrics-2.png)

1. Se nella nuova tabella non è presente una colonna corrispondente, è possibile **crearla nella tabella dati** o [contattare il supporto tecnico](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) se si tratta di una colonna di calcolo o di una dimensione creata da [!DNL Commerce Intelligence]. Puoi anche **eliminare la dimensione dalla metrica**. Per eliminare una dimensione non più necessaria, tornare all&#39;editor della metrica e selezionare le dimensioni da eliminare in `Dimensions`.

   ![Menu a discesa per la selezione delle colonne operative](../../assets/change-metrics-3.png)
