---
title: Dati di Audit Zendesk
description: Scopri i passaggi per esportare i dati Zendesk.
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Dati di Audit Zendesk

Ho trovato qualcosa di strano nel tuo [[!DNL Zendesk] dati](../integrations/exp-zendesk-data.md)? Per individuare il problema, dobbiamo esplorare i tuoi dati. Questo può essere fatto esportando il tuo [!DNL Zendesk] dati in un file scaricabile.

## Abilitazione dell’esportazione dei dati

L&#39;esportazione dei dati non è attualmente abilitata per tutti [!DNL Zendesk] conti. Per attivare questa funzione, [inviare un ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en), citando il [!DNL Zendesk] nome del sottodominio.

>[!NOTE]
>
>Solo `Enterprise` e `Plus` i piani hanno attualmente accesso a questa funzione.

Dopo l’esportazione dei dati, solo gli amministratori in un dominio e-mail specifico possono esportare i dati dal tuo [!DNL Zendesk] conto. Questo dominio e-mail è in genere lo stesso dominio e-mail del tuo [!DNL Zendesk]. Il dominio e-mail del proprietario dell’account viene utilizzato come predefinito, ma puoi modificarlo se necessario.

## Esportazione in un file scaricabile

1. Fai clic sull’icona Amministratore (logo ingranaggio) nella barra laterale e scegli **[!UICONTROL Manage** > **Reports]**.
1. Fai clic sul pulsante **[!UICONTROL Export]** scheda .
1. Fai clic su **[!UICONTROL Request file]** accanto a Esportazione XML completa come illustrato nell&#39;immagine seguente.

   A questo punto inizierà una costruzione; al termine riceverai una notifica via e-mail.
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. Fai clic sul collegamento nella notifica e-mail per scaricare un file zip contenente il rapporto.

   Questo collegamento di download è valido per almeno tre giorni.

Questo processo crea un file XML contenente tutte le informazioni memorizzate nel [!DNL Zendesk] account, compresi i dati ticket (con commenti), i dati utente e i dati account. A questo punto, puoi [inviare un ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) (assicurati di allegare questo file!) quindi possiamo dare un&#39;occhiata più da vicino ai vostri dati. Se il file è troppo grande, condividetelo con il [!DNL MBI] team via [!DNL Dropbox] o [!DNL Google Drive].

Per ulteriori informazioni [!DNL Zendesk] esportazioni di file, fare riferimento al [[!DNL Zendesk] documentazione di esportazione](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file).
