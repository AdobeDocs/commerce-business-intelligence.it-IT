---
title: Modificare la tabella operativa di una metrica
description: Scopri come modificare la tabella di dati utilizzata da una metrica per eseguire la sua operazione.
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Modificare la tabella operativa di una metrica

In alcuni casi, puoi decidere di modificare la tabella di dati utilizzata da una metrica per eseguire la sua operazione. Ad esempio, se disponi di una nuova tabella Utenti, vuoi migrare le metriche relative all’utente dalla tabella &quot;Utenti\_Vecchio&quot; per utilizzare la tabella &quot;Utenti\_Nuovo&quot;.

1. Vai a **[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. Clic **[!UICONTROL Edit]** accanto alla metrica per la quale si desidera cambiare `operational` tabella.
1. Nell’editor, fai clic su **[!UICONTROL Change]**.

   ![](../../assets/change-metrics-1.png)
1. Ora seleziona la nuova tabella su cui desideri basare questa metrica.
1. Successivamente, devi far corrispondere le dimensioni dati esistenti con quelle corrispondenti nella nuova tabella. Ad esempio, se disponevi di una colonna denominata `User's registration date`, è sufficiente selezionare la colonna nella nuova tabella in cui vengono registrati gli stessi dati di data. (Se nella nuova tabella non sono presenti colonne corrispondenti, vedere il passaggio successivo)

   ![](../../assets/change-metrics-2.png)

1. Se nella nuova tabella non è presente una colonna corrispondente, è possibile: **crearlo nella tabella dati** o [contatta l’assistenza](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) se si tratta di una colonna di calcolo o di una dimensione creata da [!DNL MBI]). È inoltre possibile **eliminare la dimensione dalla metrica**. Per eliminare una dimensione non più necessaria, torna semplicemente all’editor della metrica e seleziona le dimensioni da eliminare in `Dimensions`.

   ![](../../assets/change-metrics-3.png)
