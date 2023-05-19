---
title: Controlla dati Zendesk
description: Scopri come esportare i dati Zendesk.
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---

# Controlla dati Zendesk

Ho trovato qualcosa di strano nel tuo [[!DNL Zendesk] dati](../integrations/exp-zendesk-data.md)? Per individuare il problema, è necessario esplorare i dati. Questo può essere fatto esportando il [!DNL Zendesk] in un file scaricabile.

## Abilitazione dell’esportazione dei dati

L’esportazione dei dati non è attualmente abilitata per tutti [!DNL Zendesk] account. Per attivare questa funzione: [invia un ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html), menzionando il [!DNL Zendesk] nome del sottodominio.

>[!NOTE]
>
>Solo `Enterprise` e `Plus` i piani di hanno attualmente accesso a questa funzione.

Dopo l’abilitazione dell’esportazione dei dati, solo gli amministratori in un dominio e-mail specifico possono esportare i dati dal [!DNL Zendesk] account. Questo dominio e-mail è in genere lo stesso dominio e-mail del [!DNL Zendesk]. Il dominio e-mail del proprietario dell’account viene utilizzato come predefinito, ma puoi modificarlo se necessario.

## Esportazione in un file scaricabile

1. Fai clic sull’icona Amministratore (logo a forma di ingranaggio) nella barra laterale e scegli **[!UICONTROL Manage** > **Reports]**.
1. Fai clic su **[!UICONTROL Export]** scheda.
1. Clic **[!UICONTROL Request file]** accanto a Esportazione XML completa, come illustrato nell&#39;immagine seguente.

   A questo punto, inizia una build; ricevi una notifica tramite e-mail al completamento.
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. Fai clic sul collegamento nella notifica e-mail per scaricare un file zip contenente il rapporto.

   Questo link di download è valido per almeno tre giorni.

Questo processo crea un file XML contenente tutte le informazioni memorizzate nel file [!DNL Zendesk] account, inclusi i dati dei ticket (con commenti), i dati utente e i dati account. A questo punto è possibile: [invia un ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) (assicurati di allegare questo file!) in modo da poter esaminare più da vicino i dati. Se il file è troppo grande, condividilo con [!DNL Commerce Intelligence] team tramite [!DNL Dropbox] o [!DNL Google Drive].

Per ulteriori informazioni su [!DNL Zendesk] esportazioni di file, fare riferimento al [[!DNL Zendesk] esportare la documentazione](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file).
