---
title: Genera [!DNL Google ECommerce] dimensioni
description: Scopri come creare dimensioni che collegano i dati di eCommerce con i tuoi ordini e i dati dei clienti.
exl-id: f8a557ae-01d7-4886-8a1c-c0f245c7bc49
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# Genera [!DNL Google ECommerce] Dimension

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../administrator/user-management/user-management.md).

Ora che hai terminato di [connettere il tuo account[!DNL Google ECommerce]](../../data-analyst/importing-data/integrations/google-ecommerce.md), cosa puoi fare con questi dati in [!DNL Commerce Intelligence]? Questo argomento illustra come creare dimensioni che collegano i dati di eCommerce con gli ordini e i dati dei clienti.

Le dimensioni trattate consentono di creare analisi che [rispondono a domande fondamentali sui canali e sulle campagne di marketing](../../data-analyst/analysis/most-value-source-channel.md). Quale percentuale di reddito proviene da ciascuna origine? Come si confronta il valore del ciclo di vita di [!DNL Facebook] clienti acquisiti con quello di [!DNL Google]?

## Prerequisiti e panoramica

Per creare le dimensioni in questo argomento, sono necessarie una tabella [!DNL Google ECommerce], una tabella `orders` e una tabella `customers`. Prima di poter creare le dimensioni, queste tabelle devono essere [sincronizzate con la Data Warehouse](../../data-analyst/data-warehouse-mgr/tour-dwm.md). Le tabelle sincronizzate vengono visualizzate nella sezione `Synced Tables` di `Data Warehouse Manager`.

Di seguito è riportato un rapido esempio di sincronizzazione di tabelle e colonne, se è necessario un aggiornamento:

![](../../assets/Syncing_New_Columns.gif)

Dopo aver creato un join dalla tabella `orders` alla tabella [!DNL Google eCommerce], si creano le prime tre dimensioni nell&#39;elenco seguente. Utilizzare quindi tali dimensioni per creare tre dimensioni utente/cliente nella tabella `customers`. Per terminare, unire queste colonne alla tabella `orders`.

Di seguito sono elencate le dimensioni coperte:

* **Tabella ordini**

* Origine [!DNL Google Analytics] dell&#39;ordine
* Supporto [!DNL Google Analytics] dell&#39;ordine
* Campagna [!DNL Google Analytics]A dell&#39;ordine
* Origine [!DNL Google Analytics] del primo ordine del cliente
* Supporto [!DNL Google Analytics] del primo ordine del cliente
* Campagna [!DNL Google Analytics] del primo ordine del cliente

* **Tabella clienti**

* Origine [!DNL Google Analytics] del primo ordine del cliente
* Supporto [!DNL Google Analytics] del primo ordine del cliente
* Campagna [!DNL Google Analytics] del primo ordine del cliente

## Creazione delle dimensioni

Per creare le dimensioni, aprire [Gestione Date Warehouse](../data-warehouse-mgr/tour-dwm.md) facendo clic su **[!UICONTROL Data]** > **[!UICONTROL Data Warehouse]**.

### Tabella Ordini, arrotondamento 1

In questo esempio viene creata la dimensione [!DNL Google Analytics] di Source **dell&#39;ordine**.

1. Nell&#39;elenco delle tabelle della Data Warehouse fare clic sulla tabella (in questo caso, `orders`) contenente le informazioni sull&#39;ordine.
1. Fare clic su **[!UICONTROL Create a Column]**.
1. Denomina la colonna.
1. Selezionare `Joined Column` dal menu a discesa [definizione](../data-warehouse-mgr/calc-column-types.md). Questo esempio funziona con una [relazione uno-a-uno](../data-warehouse-mgr/table-relationships.md), che corrisponde alla colonna `eCommerce.transactionID` esattamente a una riga della tabella `orders`.
1. Successivamente, è necessario definire il percorso o la modalità di connessione della tabella e della colonna utilizzate. Fare clic sul menu a discesa `Select a table and column`.
1. Il percorso necessario non è disponibile, quindi devi crearne uno nuovo. Fare clic su **[!UICONTROL Create new Path]**.
1. Nella finestra visualizzata, impostare il lato `Many` su `orders.order\_id` o la colonna nella tabella `orders` che contiene l&#39;ID ordine.
1. Sul lato `One`, trovare la tabella `Google ECommerce`, quindi impostare la colonna su `transactionID`.

   ![](../../assets/google-ecommerce-table.png)

1. Fare clic su **[!UICONTROL Save]** per creare il percorso.
1. Dopo aver aggiunto il percorso, fare di nuovo clic sul menu a discesa **[!UICONTROL Select table and column]**.
1. Individuare la tabella `ECommerce`, quindi fare clic sulla colonna `Source`. In questo modo gli ordini vengono associati alle informazioni di origine.
1. Una volta ripristinato lo schema della tabella, fare di nuovo clic su **[!UICONTROL Save]** per creare la dimensione.

Di seguito viene illustrato l&#39;intero processo:

![](../../assets/help_center.gif)

Quindi, provare a creare il **supporto [!DNL Google Analytics] dell&#39;ordine** e `campaign`. Non sono state apportate molte modifiche a queste dimensioni, quindi prova. Ma se ti blocchi, puoi controllare [la fine di questo articolo](#stuck) per vedere le differenze.

### Tabella Clienti {#customers}

In questo esempio viene creata la dimensione [!DNL Google Analytics] di origine **del primo ordine del cliente**.

1. Nell&#39;elenco delle tabelle della Data Warehouse fare clic sulla tabella (in questo caso, `customers`) contenente le informazioni sul cliente.
1. Fare clic su **[!UICONTROL Create a Column]**.
1. Denomina la colonna.
1. Per questo esempio, selezionare la definizione `is MAX` dal menu a discesa [definizione](../../data-analyst/data-warehouse-mgr/calc-column-types.md). La definizione di `is MIN` potrebbe inoltre funzionare se applicata a una colonna di testo con un solo valore possibile. È importante assicurarsi che vengano impostati i filtri corretti, operazione che si effettua in seguito.
1. Fare clic sul menu a discesa **[!UICONTROL Select a table and column]** e selezionare la tabella `orders`, quindi la colonna `Order's [!DNL Google Analytics] source`.
1. Fare clic su **[!UICONTROL Save]**.
1. Una volta tornato nello schema della tabella, fai clic sul menu a discesa `Options`, quindi `Filters`.
1. Fare clic su **[!UICONTROL Add Filter Set]** e quindi selezionare il set `Orders we count`. Si desidera includere solo gli ordini inclusi nella serie di filtri di conteggio, pertanto è importante che questa serie di filtri sia selezionata.
1. Fare clic su **[!UICONTROL Add Filter]**. Desideri trovare l&#39;origine [!DNL Google Analytics] del primo ordine del cliente, quindi devi aggiungere un filtro:

   _orders.Numero ordine cliente = 1

   _
1. Fare clic su **[!UICONTROL Save]** per creare la dimensione.

Quindi, prova a creare **il supporto [!DNL Google Analytics]** e `campaign` del primo ordine del cliente. Non sono state apportate molte modifiche a queste dimensioni, quindi prova. Ma se ti blocchi, puoi controllare [la fine di questo articolo](#stuck) per vedere le differenze.

### Bonus: tabella Ordini, turno 2

Puoi fermarti qui se lo desideri, ma questa sezione abilita ulteriori analisi portando le [!DNL Google Analytics] dimensioni **del primo ordine del cliente create nella [ultima sezione](#customers) nella tabella `orders`.** La creazione delle dimensioni in questa sezione consente di analizzare tutte le metriche create nella tabella `orders` - `Revenue`, `Number of orders`, `Distinct buyers` e così via - utilizzando gli attributi [!DNL Google Analytics] del primo ordine di un cliente.

Questo esempio unisce la dimensione `Customer's first order's [!DNL Google Analytics] source` alla tabella `orders`.

1. Nell&#39;elenco delle tabelle della Data Warehouse fare clic sulla tabella (in questo caso, `orders`) contenente le informazioni sull&#39;ordine.
1. Fare clic su **[!UICONTROL Create a Column]**.
1. Denomina la colonna.
1. Selezionare `Joined Column` dal menu a discesa delle definizioni. In questo modo le dimensioni cliente create nella sezione precedente vengono unite alla tabella `orders`.
1. Fare clic sul menu a discesa **[!UICONTROL Select a table and column]**, quindi selezionare la tabella `customers` e la colonna `Customer's first order's [!DNL Google Analytics] source`.
1. Se un percorso non viene popolato automaticamente, selezionare il percorso che meglio connette le tabelle clienti e ordini.
1. Fare clic su **[!UICONTROL Save]** per creare la dimensione.

Di seguito viene illustrato l&#39;intero processo:

![](../../assets/help_center2.gif)

Completare unendo le dimensioni `Customer's first order's` e `campaign` alla tabella `orders`. Unisciti alle dimensioni e, in caso di problemi, controlla [la fine dell&#39;articolo](#stuck) per ricevere assistenza.

### Ritorno a capo

Hai terminato di creare le dimensioni, il che significa che ora puoi creare potenti analisi che tengono traccia delle prestazioni dei vari canali e campagne. Ricorda che le **nuove colonne non saranno disponibili fino al completamento del prossimo aggiornamento**.

Alcune delle dimensioni più popolari sono trattate in questo argomento, ma il cielo è il limite - provare a creare il proprio o sentirsi liberi di ping noi se si desidera aiuto con l&#39;esplorazione di altre opzioni. 

### Note aggiuntive

Tabella **`Orders`#1**: durante la creazione del supporto `Order's [!DNL Google Analytics]` e delle dimensioni `campaign`, la differenza è rappresentata dalle colonne selezionate al passaggio 12. In questo esempio, la colonna era `Source`.

Tabella **`Customers`**: durante la creazione del supporto `Customer's first order's [!DNL Google Analytics]` e delle dimensioni `campaign`, la differenza è rappresentata dalle colonne selezionate nel passaggio 5. In questo esempio, la colonna era di origine `Order's [!DNL Google Analytics]`.

Tabella **`Orders`#2**: quando si uniscono il supporto `Customer's first order's [!DNL Google Analytics]` e le colonne `campaign` alla tabella `orders`, la differenza è rappresentata dalle colonne selezionate nel passaggio 5. In questo esempio, la colonna era di origine `Customer's first order's [!DNL Google Analytics]`.
