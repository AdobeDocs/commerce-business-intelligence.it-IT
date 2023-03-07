---
title: Genera[!DNL Google ECommerce]dimensioni
description: Scopri come creare dimensioni che collegano i dati di eCommerce con i tuoi ordini e i dati dei clienti.
exl-id: f8a557ae-01d7-4886-8a1c-c0f245c7bc49
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 0%

---

# Genera [!DNL Google ECommerce] Dimension

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../administrator/user-management/user-management.md).

Ora che hai terminato [connessione[!DNL Google ECommerce]account](../../data-analyst/importing-data/integrations/google-ecommerce.md), cosa puoi fare con tali dati in [!DNL MBI]? Questo articolo illustra come creare dimensioni che collegano i dati di eCommerce con i tuoi ordini e i dati dei clienti.

Le dimensioni coperte consentono di creare analisi che [rispondi alle domande vitali sui canali e sulle campagne di marketing](../../data-analyst/analysis/most-value-source-channel.md). Quale percentuale di reddito proviene da ciascuna origine? In che modo il valore del ciclo di vita dei clienti acquisiti da Facebook è paragonabile a quello di [!DNL Google]?

## Prerequisiti e panoramica

Per creare le dimensioni in questo articolo, è necessario un [!DNL Google ECommerce] tabella, un `orders` tabella e un `customers` tabella. Tali tabelle devono essere [sincronizzato nella tua Data Warehouse](../../data-analyst/data-warehouse-mgr/tour-dwm.md) prima che le dimensioni possano essere create. Le tabelle sincronizzate vengono visualizzate in `Synced Tables` sezione del `Data Warehouse Manager`.

Di seguito è riportato un rapido esempio di sincronizzazione di tabelle e colonne, se è necessario un aggiornamento:

![](../../assets/Syncing_New_Columns.gif)

Dopo aver creato un join da `orders` tabella al [!DNL Google eCommerce] nella tabella seguente vengono create le prime tre dimensioni nell&#39;elenco. Quindi, puoi utilizzare queste dimensioni per creare tre dimensioni utente/cliente nel `customers` tabella. Per terminare, unisci queste colonne al `orders` tabella.

Di seguito sono elencate le dimensioni coperte:

* **Tabella Ordini**

* Dell&#39;ordine [!DNL Google Analytics] sorgente
* Dell&#39;ordine [!DNL Google Analytics] media
* Dell&#39;ordine [!DNL Google Analytics]Una campagna
* Il primo ordine del cliente [!DNL Google Analytics] sorgente
* Il primo ordine del cliente [!DNL Google Analytics] media
* Il primo ordine del cliente [!DNL Google Analytics] campagna

* **Tabella Clienti**

* Il primo ordine del cliente [!DNL Google Analytics] sorgente
* Il primo ordine del cliente [!DNL Google Analytics] media
* Il primo ordine del cliente [!DNL Google Analytics] campagna

## Creazione delle dimensioni

Per creare le quote, aprite [Gestione Date Warehouse](../data-warehouse-mgr/tour-dwm.md) facendo clic su **[!UICONTROL Data]** > **[!UICONTROL Data Warehouse]**.

### Tabella Ordini, arrotondamento 1

Questo esempio crea **Dell&#39;ordine [!DNL Google Analytics] Sorgente** dimensione.

1. Nell&#39;elenco delle tabelle della Data Warehouse, fare clic sulla tabella (in questo caso, `orders`) che contiene le informazioni sull&#39;ordine.
1. Clic **[!UICONTROL Create a Column]**.
1. Denomina la colonna.
1. Seleziona `Joined Column` dal [elenco a discesa delle definizioni](../data-warehouse-mgr/calc-column-types.md). Questo esempio funziona con un [relazione uno-a-uno](../data-warehouse-mgr/table-relationships.md), corrispondente al `eCommerce.transactionID` a una sola riga della `orders` tabella.
1. Successivamente, è necessario definire il percorso o la modalità di connessione della tabella e della colonna utilizzate. Fai clic su `Select a table and column` a discesa.
1. Il percorso necessario non è disponibile, quindi devi crearne uno nuovo. Clic **[!UICONTROL Create new Path]**.
1. Nella finestra visualizzata, imposta `Many` lato a `orders.order\_id`o la colonna nella `orders` tabella che contiene l’ID dell’ordine.
1. Il giorno `One` lato, trova il `Google ECommerce` , quindi impostare la colonna su `transactionID`.

   ![](../../assets/google-ecommerce-table.png)

1. Clic **[!UICONTROL Save]** per creare il percorso.
1. Dopo aver aggiunto il percorso, fai clic su **[!UICONTROL Select table and column]** a discesa.
1. Individua il `ECommerce` e quindi fare clic sul pulsante `Source` colonna. In questo modo gli ordini vengono associati alle informazioni di origine.
1. Una volta tornato nello schema della tabella, fai clic su **[!UICONTROL Save]** di nuovo per creare la quota.

Di seguito viene illustrato l&#39;intero processo:

![](../../assets/help_center.gif)

Quindi, prova a creare **Dell&#39;ordine [!DNL Google Analytics] media** e `campaign`. Non sono state apportate molte modifiche a queste dimensioni, quindi prova. Ma se vi bloccate, potete controllare [fine dell&#39;articolo](#stuck) per vedere cosa è diverso.

### Tabella Clienti {#customers}

Questo esempio crea **Il primo ordine del cliente [!DNL Google Analytics] sorgente** dimensione.

1. Nell&#39;elenco delle tabelle della Data Warehouse, fare clic sulla tabella (in questo caso, `customers`) che contiene le informazioni del cliente.
1. Clic **[!UICONTROL Create a Column]**.
1. Denomina la colonna.
1. Per questo esempio, seleziona la `is MAX` definizione dal [elenco a discesa delle definizioni](../../data-analyst/data-warehouse-mgr/calc-column-types.md). Il `is MIN` La definizione potrebbe anche funzionare se applicata a una colonna di testo con un solo valore possibile. È importante assicurarsi che vengano impostati i filtri corretti, operazione che si effettua in seguito.
1. Fai clic su **[!UICONTROL Select a table and column]** e seleziona la `orders` tabella, quindi `Order's [!DNL Google Analytics] source` colonna.
1. Clic **[!UICONTROL Save]**.
1. Una volta tornato nello schema della tabella, fai clic su `Options` a discesa, quindi `Filters`.
1. Clic **[!UICONTROL Add Filter Set]** e quindi selezionare `Orders we count` impostata. Si desidera includere solo gli ordini inclusi nella serie di filtri di conteggio, pertanto è importante che questa serie di filtri sia selezionata.
1. Clic **[!UICONTROL Add Filter]**. Si desidera trovare il primo ordine del cliente [!DNL Google Analytics] quindi è necessario aggiungere un filtro:

   _orders.Numero ordine cliente = 1

   _
1. Clic **[!UICONTROL Save]** per creare la quota.

Quindi, prova a creare **Il primo ordine del cliente [!DNL Google Analytics] media** e `campaign`. Non sono state apportate molte modifiche a queste dimensioni, quindi prova. Ma se vi bloccate, potete controllare [fine dell&#39;articolo](#stuck) per vedere cosa è diverso.

### Bonus: tabella Ordini, turno 2

Puoi fermarti qui se lo desideri, ma questa sezione abilita ulteriori analisi portando il **Il primo ordine del cliente [!DNL Google Analytics] dimensioni** creato in [ultima sezione](#customers) in `orders` tabella. La creazione delle dimensioni in questa sezione ti consente di analizzare tutte le metriche basate sulle `orders` tabella - `Revenue`, `Number of orders`, `Distinct buyers`, e così via - utilizzando [!DNL Google Analytics] attributi del primo ordine di un cliente.

Questo esempio si aggiunge a `Customer's first order's [!DNL Google Analytics] source` dimensione al `orders` tabella.

1. Nell&#39;elenco delle tabelle della Data Warehouse, fare clic sulla tabella (in questo caso, `orders`) che contiene le informazioni sull&#39;ordine.
1. Clic **[!UICONTROL Create a Column]**.
1. Denomina la colonna.
1. Seleziona `Joined Column` dal menu a discesa definizione. In questo modo le dimensioni cliente create nella sezione precedente vengono unite al `orders` tabella.
1. Fai clic su **[!UICONTROL Select a table and column]** , quindi seleziona la `customers` tabella e `Customer's first order's [!DNL Google Analytics] source` colonna.
1. Se un percorso non viene popolato automaticamente, selezionare il percorso che meglio connette le tabelle clienti e ordini.
1. Clic **[!UICONTROL Save]** per creare la quota.

Di seguito viene illustrato l&#39;intero processo:

![](../../assets/help_center2.gif)

Completa unendo il `Customer's first order's` media e `campaign` dimensioni per `orders` tabella. Unire le dimensioni e, in caso di problemi, estrarre [fine dell&#39;articolo](#stuck) se ha bisogno di aiuto.

### Ritorno a capo

Hai terminato di creare le dimensioni, il che significa che ora puoi creare potenti analisi che tengono traccia delle prestazioni dei vari canali e campagne. Ricorda che il **le nuove colonne saranno disponibili solo al termine del prossimo aggiornamento**.

Alcune delle dimensioni più popolari sono coperte in questo articolo, ma il cielo è il limite - provare a creare il proprio o sentirsi liberi di ping noi se si desidera aiuto con l&#39;esplorazione di altre opzioni. 

### Sono bloccato! Cos&#39;è diverso? {#stuck}

**`Orders`#1 tabella:** Durante la creazione di `Order's [!DNL Google Analytics]` media e `campaign` dimensioni, la differenza è rappresentata dalle colonne selezionate nel passaggio 12. In questo esempio, la colonna era `Source`.

**`Customers`tabella:** Durante la creazione di `Customer's first order's [!DNL Google Analytics]` media e `campaign` dimensioni, la differenza è rappresentata dalle colonne selezionate nel passaggio 5. In questo esempio, la colonna era `Order's [!DNL Google Analytics]` sorgente.

**`Orders`#2 tabella:** Quando si unisce al `Customer's first order's [!DNL Google Analytics]` media e `campaign` colonne a `orders` tabella, la differenza è rappresentata dalle colonne selezionate nel passaggio 5. In questo esempio, la colonna era `Customer's first order's [!DNL Google Analytics]` sorgente.
