---
title: Controlla dati Zendesk
description: Scopri come esportare i dati Zendesk.
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/EQmiSbzzvOONQ8-F1U9uMVpgXUKd2PEjcLXLVSgQSm8
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
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
source-wordcount: 269
ht-degree: 0%

---

# Controlla dati Zendesk

Hai trovato qualcosa di strano nei tuoi [[!DNL Zendesk] dati](../integrations/exp-zendesk-data.md)? Per individuare il problema, è necessario esplorare i dati. È possibile eseguire l&#39;operazione esportando i dati di [!DNL Zendesk] in un file scaricabile.

## Abilitazione dell’esportazione dei dati

Esportazione dati non attualmente abilitata per tutti gli account [!DNL Zendesk]. Per attivare questa funzionalità, [invia un ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=it), specificando il nome del sottodominio [!DNL Zendesk].

>[!NOTE]
>
>Solo `Enterprise` e `Plus` piani hanno attualmente accesso a questa funzione.

Dopo aver abilitato l&#39;esportazione dei dati, solo gli amministratori di un dominio e-mail specifico possono esportare i dati dall&#39;account [!DNL Zendesk]. Questo dominio e-mail è in genere lo stesso dominio e-mail di [!DNL Zendesk]. Il dominio e-mail del proprietario dell’account viene utilizzato come predefinito, ma puoi modificarlo se necessario.

## Esportazione in un file scaricabile

1. Fare clic sull&#39;icona Admin (logo ingranaggio) nella barra laterale e scegliere **[!UICONTROL Manage** > **Reports]**.
1. Fare clic sulla scheda **[!UICONTROL Export]**.
1. Fare clic su **[!UICONTROL Request file]** accanto a Esportazione XML completa come illustrato nell&#39;immagine seguente.

   A questo punto, inizia una build; ricevi una notifica tramite e-mail al completamento.
   ![report_export_new.png](../../../assets/reports_export_new.png)

1. Fai clic sul collegamento nella notifica e-mail per scaricare un file zip contenente il rapporto.

   Questo link di download è valido per almeno tre giorni.

Questo processo crea un file XML contenente tutte le informazioni memorizzate nell&#39;account [!DNL Zendesk] corrente, inclusi i dati dei ticket (con commenti), i dati utente e i dati account. A questo punto, puoi [inviare un ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=it) (assicurati di allegare il file!) per esaminare più da vicino i tuoi dati. Se il file è troppo grande, condividerlo con il team [!DNL Commerce Intelligence] tramite [!DNL Dropbox] o [!DNL Google Drive].

Per ulteriori informazioni sulle [!DNL Zendesk] esportazioni di file, consulta la [[!DNL Zendesk] documentazione di esportazione ufficiale](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file).
