---
title: Scegli un generatore di report
description: Scopri come scegliere il Report Builder.
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# Scegli un generatore di report

>[!NOTE]
>&#x200B;>Richiede [Autorizzazioni amministratore](../../administrator/user-management/user-management.md).

Ora che hai più opzioni per la creazione di analisi, a volte può essere difficile sapere esattamente quale sapore del Report Builder soddisfa le tue esigenze. Questo argomento ti guida attraverso la scelta del modo migliore per generare la tua analisi.

## Quando dovrei usare [!DNL SQL Report Builder]? {#whensql}

Osservare alcuni dei motivi più comuni per cui si utilizzerebbe [!DNL SQL Report Builder] su [!DNL traditional Report Builder].

### Se si desidera utilizzare funzioni specifiche di [!DNL SQL]...

Il bello di [!DNL SQL Report Builder] è che consente di utilizzare funzioni attualmente non disponibili in Data Warehouse Manager. In passato, un analista potrebbe aver dovuto intervenire per aiutarti a realizzare appieno la tua visione.

[!DNL SQL Report Builder] supporta funzioni come [`LISTAGG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html) e [`GETDATE`](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html), che non era possibile utilizzare in precedenza. È possibile accedere a [`full list`](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html), ma alcune altre funzioni specifiche di SQL includono:

* [`Bitwise aggregate` funzioni](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* Operatore [`concatenation`](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### Se desideri eseguire alcuni test...

Se si desidera provare tecniche e strategie diverse per individuare il metodo ottimale per l&#39;analisi, è possibile utilizzare [!DNL SQL Report Builder]. La creazione di colonne in Data Warehouse Manager richiede tempo e le colonne create con DWM dipendono dai cicli di aggiornamento.

Nella migliore delle ipotesi, è necessario attendere l’intero ciclo di aggiornamento prima di poter utilizzare la colonna. Se ti rendi conto di aver commesso un errore durante la creazione della colonna, devi attendere *due* cicli: uno per popolare inizialmente la colonna e un altro ciclo per la propagazione delle revisioni.

### Se utilizzi una nuova colonna una sola volta...

Come indicato nella sezione precedente, la creazione di una colonna in Data Warehouse Manager richiede tempo. Se si prevede di utilizzare solo una colonna creata in un report, Adobe consiglia di utilizzare [!DNL SQL Report Builder]. In questo modo non è più necessario attendere il completamento di un ciclo di aggiornamento e tornare al lavoro più rapidamente.

### Se si utilizzano dati con una relazione uno-a-molti...

A volte, la struttura dei dati potrebbe rendere [!DNL SQL Report Builder] una scelta più efficiente e logica per generare l&#39;analisi. La creazione di colonne per le relazioni uno-a-uno è semplice in Data Warehouse Manager, ma le cose possono diventare un po’ confuse quando si tratta di relazioni uno-a-molti.

Supponiamo che un singolo prodotto sia considerato parte di più categorie di prodotti e vorresti visualizzare i ricavi associati a ciascuna categoria di ciascun prodotto. Il tentativo di creare questa relazione utilizzando DWM può essere noioso e difficile, ma la scrittura di una query [!DNL SQL] potrebbe essere un po&#39; più semplice:

![](../../assets/When_should_I_use_the_RB_2.png)

## Quando dovrei usare il Report Builder tradizionale? {#whentraditionalrb}

[!DNL SQL Report Builder] offre maggiore controllo e accesso a funzionalità precedentemente non disponibili, ma potrebbe non essere sempre la scelta giusta. Adobe consiglia inoltre di considerare quanto segue quando si decide quale sapore del generatore di rapporti utilizzare.

### Se stai creando un rapporto semplice...

Se ciò che desideri creare è semplice, l&#39;utilizzo del Report Builder tradizionale può essere molto più veloce rispetto alla scrittura di una query [!DNL SQL] completa. È utile se le colonne necessarie per creare l’analisi si trovano già in Data Warehouse Manager.

### Se condividi il tuo lavoro con altri utenti...

Gli utenti della tua organizzazione utilizzano/visualizzano questa analisi? A seconda delle persone con cui condividi il tuo lavoro, a volte può essere meglio utilizzare Visual Report Builder. Gli utenti possono esaminare rapidamente la definizione in [!DNL Visual Report Builder] anziché leggere una query [!DNL SQL] potenzialmente lunga.

Se alcune persone necessitano del report ma non hanno familiarità con [!DNL SQL], Adobe consiglia di utilizzare il sapore originale di Report Builder. Rende le cose più facili con loro.

## Ritorno a capo {#wrapup}

Sia [!DNL SQL Report Builder] che [!DNL Visual Report Builder] sono adatti per un&#39;ampia varietà di casi d&#39;uso. In genere, questo dipende da quali sono le tue esigenze analitiche e da chi consuma l’analisi.
