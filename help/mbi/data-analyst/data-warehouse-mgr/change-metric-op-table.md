---
title: Modificare la tabella operativa di una metrica
description: Scopri come modificare la tabella di dati utilizzata da una metrica per eseguire il suo funzionamento.
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# Modificare la tabella operativa di una metrica

In alcuni casi, puoi decidere di modificare la tabella di dati utilizzata da una metrica per eseguire il suo funzionamento. Ad esempio, se hai una nuova tabella utenti, vuoi eseguire la migrazione delle metriche relative all&#39;utente dalla tabella &quot;Utenti\_vecchi&quot; per utilizzare la tabella &quot;Utenti\_nuovi&quot;.

1. Vai a **[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. Fai clic su **[!UICONTROL Edit]** accanto alla metrica per la quale desideri cambiare il `operational` tabella.
1. Nell’editor, fai clic su **[!UICONTROL Change]**.

   ![](../../assets/change-metrics-1.png)
1. Ora seleziona la nuova tabella su cui desideri basare questa metrica.
1. Successivamente, dovrai far corrispondere le dimensioni dati esistenti a quelle corrispondenti nella nuova tabella. Ad esempio, se avevi una colonna denominata `User's registration date`, seleziona semplicemente quale colonna della nuova tabella registra gli stessi dati di data. Se nella nuova tabella non sono presenti colonne corrispondenti, vedere il passaggio successivo.

   ![](../../assets/change-metrics-2.png)

1. Se nella nuova tabella non è presente una colonna corrispondente, è possibile **crearla nella tabella dati** o [contattare il supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) se si tratta di una colonna o di una dimensione di calcolo effettuata da [!DNL MBI]) o semplicemente **elimina la dimensione dalla metrica**. Per eliminare una dimensione di cui non hai più bisogno, torna semplicemente all’editor della metrica e seleziona le dimensioni da eliminare in `Dimensions`.

   ![](../../assets/change-metrics-3.png)
