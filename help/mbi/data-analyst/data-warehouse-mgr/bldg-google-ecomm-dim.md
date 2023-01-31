---
title: Crea[!DNL Google ECommerce]dimensioni
description: Scopri come creare dimensioni per collegare i dati di eCommerce con i tuoi ordini e i dati dei clienti.
exl-id: f8a557ae-01d7-4886-8a1c-c0f245c7bc49
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 0%

---

# Crea [!DNL Google ECommerce] Dimension

>[!NOTE]
>
>Richiede [Autorizzazioni amministratore](../../administrator/user-management/user-management.md).

Ora che hai finito [collegamento[!DNL Google ECommerce]account](../../data-analyst/importing-data/integrations/google-ecommerce.md), cosa puoi fare con quei dati in [!DNL MBI]? In questo articolo, presentiamo le dimensioni di creazione che collegano i dati di e-commerce ai tuoi ordini e ai dati dei clienti.

Le dimensioni che copriremo ti daranno la possibilità di creare analisi che [rispondere a domande fondamentali sui canali e sulle campagne di marketing](../../data-analyst/analysis/most-value-source-channel.md). Qual è la percentuale dei ricavi provenienti da ogni fonte? Come si confronta il valore del ciclo di vita dei clienti acquisiti da Facebook con quello di [!DNL Google]?

## Prerequisiti e panoramica

Per creare le dimensioni in questo articolo, è necessario un [!DNL Google ECommerce] tabella `orders` tabella e `customers` tabella. Queste tabelle devono essere [sincronizzato con il data warehouse](../../data-analyst/data-warehouse-mgr/tour-dwm.md) prima della creazione di dimensioni. Le tabelle sincronizzate vengono visualizzate nel `Synced Tables` della sezione `Data Warehouse Manager`.

Di seguito è riportato un rapido sguardo alla sincronizzazione di tabelle e colonne se hai bisogno di un aggiornamento:

![](../../assets/Syncing_New_Columns.gif)

Dopo aver creato un join dal `orders` della tabella [!DNL Google eCommerce] Le prime tre dimensioni vengono create nell’elenco seguente. Quindi, utilizziamo queste dimensioni per creare tre dimensioni utente/cliente nel `customers` tabella. Per finire, uniamo quelle colonne al `orders` tabella.

Di seguito sono riportate le dimensioni da noi coperte:

* **Tabella ordini**

* Ordine [!DNL Google Analytics] source
* Ordine [!DNL Google Analytics] medium
* Ordine [!DNL Google Analytics]Una campagna
* Il primo ordine del cliente [!DNL Google Analytics] source
* Il primo ordine del cliente [!DNL Google Analytics] medium
* Il primo ordine del cliente [!DNL Google Analytics] campagna

* **Tabella clienti**

* Il primo ordine del cliente [!DNL Google Analytics] source
* Il primo ordine del cliente [!DNL Google Analytics] medium
* Il primo ordine del cliente [!DNL Google Analytics] campagna

## Creazione di dimensioni

Per creare dimensioni, apri la [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md) facendo clic su **[!UICONTROL Data]** > **[!UICONTROL Data Warehouse]**.

### Tabella ordini, arrotondato 1

In questo esempio, creiamo il **Ordine [!DNL Google Analytics] Origine** dimensione.

1. Nell&#39;elenco delle tabelle della Data Warehouse, fai clic sulla tabella (nel nostro caso, `orders`) che contiene le informazioni sull&#39;ordine.
1. Fai clic su **[!UICONTROL Create a Column]**.
1. Denomina la colonna.
1. Seleziona `Joined Column` dal [elenco a discesa delle definizioni](../data-warehouse-mgr/calc-column-types.md). In questo esempio, stiamo lavorando con un [rapporto uno-a-uno](../data-warehouse-mgr/table-relationships.md), che corrispondono `eCommerce.transactionID` a una riga esatta del `orders` tabella.
1. Successivamente, è necessario definire il percorso o il modo in cui la tabella e la colonna in uso sono collegate. Fai clic sul pulsante `Select a table and column` a discesa.
1. Il percorso di cui abbiamo bisogno non è disponibile, quindi dobbiamo crearne uno nuovo. Fai clic su **[!UICONTROL Create new Path]**.
1. Nella finestra visualizzata, imposta la `Many` lato `orders.order\_id`o la colonna nel `orders` che contiene l’ID ordine.
1. Sulla `One` lato, trova `Google ECommerce` quindi impostare la colonna su `transactionID`.

   ![](../../assets/google-ecommerce-table.png)

1. Fai clic su **[!UICONTROL Save]** per creare il percorso.
1. Dopo aver aggiunto il percorso, fai clic sul pulsante **[!UICONTROL Select table and column]** di nuovo a discesa.
1. Individua il `ECommerce` quindi fai clic sulla tabella `Source` colonna. Questo collega gli ordini alle informazioni di origine.
1. Una volta tornato nello schema della tabella, fai clic su **[!UICONTROL Save]** per creare nuovamente la quota.

Ecco un&#39;occhiata all&#39;intero processo:

![](../../assets/help_center.gif)

Quindi, prova a creare **Ordine [!DNL Google Analytics] medium** e `campaign`. Non cambierà molto per queste dimensioni, quindi provateci. Ma se ti imbatti, puoi controllare [la fine del presente articolo](#stuck) per vedere cosa è diverso.

### Tabella clienti {#customers}

In questo esempio, creiamo il **Il primo ordine del cliente [!DNL Google Analytics] source** dimensione.

1. Nell&#39;elenco delle tabelle della Data Warehouse, fai clic sulla tabella (nel nostro caso, `customers`) che contiene le informazioni sul cliente.
1. Fai clic su **[!UICONTROL Create a Column]**.
1. Denomina la colonna.
1. Per questo esempio, selezioniamo il `is MAX` la definizione di [elenco a discesa delle definizioni](../../data-analyst/data-warehouse-mgr/calc-column-types.md). La `is MIN` La definizione può funzionare anche se applicata a una colonna di testo con un solo valore possibile. La parte importante è garantire l&#39;impostazione di filtri adeguati, come facciamo in seguito.
1. Fai clic sul pulsante **[!UICONTROL Select a table and column]** e seleziona il menu a discesa `orders` tabella, quindi `Order's [!DNL Google Analytics] source` colonna.
1. Fai clic su **[!UICONTROL Save]**.
1. Una volta tornato nello schema della tabella, fai clic su `Options` a discesa, quindi `Filters`.
1. Fai clic su **[!UICONTROL Add Filter Set]** quindi seleziona la `Orders we count` impostato. Vogliamo includere solo gli ordini inclusi negli ordini per i quali contiamo il set di filtri, pertanto è importante che questo set di filtri sia selezionato.
1. Fai clic su **[!UICONTROL Add Filter]**. Vogliamo trovare il primo ordine del cliente [!DNL Google Analytics] sorgente, quindi è necessario aggiungere un filtro:

   _orders.Numero dell&#39;ordine del cliente = 1

   _
1. Fai clic su **[!UICONTROL Save]** per creare la dimensione.

Quindi, prova a creare **Il primo ordine del cliente [!DNL Google Analytics] medium** e `campaign`. Non cambierà molto per queste dimensioni, quindi provateci. Ma se ti imbatti, puoi controllare [la fine del presente articolo](#stuck) per vedere cosa è diverso.

### Bonus: Tabella ordini, round 2

Puoi fermarti qui, se lo desideri, ma questa sezione consente ulteriori analisi portando la **Il primo ordine del cliente [!DNL Google Analytics] dimensioni** abbiamo creato [ultima sezione](#customers) nel `orders` tabella. La creazione delle dimensioni in questa sezione ti consente di analizzare tutte le metriche create sul tuo `orders` tabella - `Revenue`, `Number of orders`, `Distinct buyers`, e così via - utilizzando [!DNL Google Analytics] attributi del primo ordine del cliente.

In questo esempio, ci uniamo al `Customer's first order's [!DNL Google Analytics] source` alla dimensione `orders` tabella.

1. Nell&#39;elenco delle tabelle della Data Warehouse, fai clic sulla tabella (nel nostro caso, `orders`) che contiene le informazioni sull&#39;ordine.
1. Fai clic su **[!UICONTROL Create a Column]**.
1. Denomina la colonna.
1. Seleziona `Joined Column` dal menu a discesa definizione . In questo modo le dimensioni del cliente create nella sezione precedente verranno unite al `orders` tabella.
1. Fai clic sul pulsante **[!UICONTROL Select a table and column]** , quindi seleziona il `customers` la tabella e `Customer's first order's [!DNL Google Analytics] source` colonna.
1. Se un percorso non viene compilato automaticamente, selezionare il percorso che meglio connette i clienti e le tabelle degli ordini.
1. Fai clic su **[!UICONTROL Save]** per creare la dimensione.

Ecco un&#39;occhiata all&#39;intero processo:

![](../../assets/help_center2.gif)

Completare unendo i `Customer's first order's` media e `campaign` le dimensioni `orders` tabella. Fai un tentativo, e come abbiamo detto prima, controlla [la fine dell&#39;articolo](#stuck) se hai bisogno di aiuto.

### Ritorno a capo

Abbiamo finito di creare le dimensioni, il che significa che ora possiamo creare analisi potenti che monitorano le prestazioni dei nostri vari canali e campagne. Sappiamo che non vede l&#39;ora di iniziare, ma ricorda **le nuove colonne saranno disponibili solo al completamento dell&#39;aggiornamento successivo**.

Abbiamo coperto alcune delle dimensioni più popolari in questo articolo, ma il cielo è il limite - prova a creare il tuo o sentire libero di ping a noi se si desidera aiuto esplorare altre opzioni. 

### Sono bloccato! cosa è diverso? {#stuck}

**`Orders`tabella n. 1:** Durante la creazione del `Order's [!DNL Google Analytics]` media e `campaign` dimensioni, la differenza sarà rappresentata dalle colonne selezionate al passaggio 12. Nel nostro esempio, la colonna era `Source`.

**`Customers`tabella:** Durante la creazione del `Customer's first order's [!DNL Google Analytics]` media e `campaign` dimensioni, la differenza sarà rappresentata dalle colonne selezionate al passaggio 5. Nel nostro esempio, la colonna era `Order's [!DNL Google Analytics]` sorgente.

**`Orders`tabella n. 2:** Quando si unisce `Customer's first order's [!DNL Google Analytics]` media e `campaign` alle colonne `orders` tabella, la differenza sarà rappresentata dalle colonne selezionate al passaggio 5. Nel nostro esempio, la colonna era `Customer's first order's [!DNL Google Analytics]` sorgente.
