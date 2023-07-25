---
title: Scegli un generatore di report
description: Scopri come scegliere il Report Builder.
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---

# Scegli un generatore di report

>[!NOTE]
>>Richiede [Autorizzazioni amministratore](../../administrator/user-management/user-management.md).

Ora che hai più opzioni per la creazione di analisi, a volte può essere difficile sapere esattamente quale sapore del Report Builder soddisfa le tue esigenze. Questo argomento ti guida attraverso la scelta del modo migliore per generare la tua analisi.

## Quando dovrei usare [!DNL SQL Report Builder]? {#whensql}

Osserva alcuni dei motivi più comuni per cui utilizzeresti il [!DNL SQL Report Builder] oltre il [!DNL traditional Report Builder].

### Se si desidera utilizzare [!DNL SQL]Funzioni specifiche di...

Parte della bellezza del [!DNL SQL Report Builder] consente di utilizzare funzioni non attualmente disponibili in Gestione Date Warehouse. In passato, un analista potrebbe aver dovuto intervenire per aiutarti a realizzare appieno la tua visione.

Il [!DNL SQL Report Builder] supporta funzioni come [`LISTAGG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html) e [`GETDATE`](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html), che in precedenza non era possibile utilizzare. È possibile accedere a [`full list`](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html), ma alcune altre funzioni specifiche di SQL includono:

* [`Bitwise aggregate` funzioni](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* [`concatenation` operatore](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### Se desideri eseguire alcuni test...

Se desideri provare diverse tecniche e strategie per capire cosa funziona meglio per l’analisi, puoi utilizzare [!DNL SQL Report Builder]. La creazione di colonne in Gestione Date Warehouse richiede tempo e le colonne create utilizzando Gestione finestre desktop dipendono dai cicli di aggiornamento.

Nella migliore delle ipotesi, è necessario attendere l’intero ciclo di aggiornamento prima di poter utilizzare la colonna. Se ti rendi conto di aver sbagliato a costruire la colonna, devi aspettare *due* cicli: uno per compilare inizialmente la colonna e un altro ciclo per la propagazione delle revisioni.

### Se utilizzi una nuova colonna una sola volta...

Come indicato nella sezione precedente, la creazione di una colonna in Gestione Date Warehouse richiede tempo. Se prevedi di utilizzare solo una colonna creata in un rapporto, l’Adobe suggerisce di utilizzare [!DNL SQL Report Builder]. In questo modo non è più necessario attendere il completamento di un ciclo di aggiornamento e tornare al lavoro più rapidamente.

### Se si utilizzano dati con una relazione uno-a-molti...

A volte, la struttura dei dati potrebbe rendere [!DNL SQL Report Builder] una scelta più efficiente e logica per creare l’analisi. La creazione di colonne per le relazioni uno-a-uno è semplice in Gestione Date Warehouse, ma le cose possono risultare un po&#39; confuse quando si tratta di relazioni uno-a-molti.

Supponiamo che un singolo prodotto sia considerato parte di più categorie di prodotti e vorresti visualizzare i ricavi associati a ciascuna categoria di ciascun prodotto. Il tentativo di creare questa relazione utilizzando DWM può essere noioso e difficile, ma la scrittura di un [!DNL SQL] la query potrebbe essere un po&#39; più semplice:

![](../../assets/When_should_I_use_the_RB_2.png)

## Quando dovrei usare il Report Builder tradizionale? {#whentraditionalrb}

Mentre il [!DNL SQL Report Builder] offre maggiore controllo e accesso a funzionalità precedentemente non disponibili; è possibile che non sia sempre la scelta giusta. L’Adobe suggerisce di considerare anche quanto segue quando si decide quale sapore del report builder utilizzare.

### Se stai creando un rapporto semplice...

Se quello che si desidera creare è semplice, utilizzare il Report Builder tradizionale può essere molto più veloce che scrivere un [!DNL SQL] query. È utile se le colonne necessarie per creare l&#39;analisi sono già presenti in Gestione Date Warehouse.

### Se condividi il tuo lavoro con altri utenti...

Gli utenti della tua organizzazione utilizzano/visualizzano questa analisi? A seconda della persona con cui condividi il lavoro, a volte può essere meglio mantenere il Report Builder visivo. Gli utenti possono esaminare rapidamente la definizione nella [!DNL Visual Report Builder] rispetto alla lettura di un valore potenzialmente lungo [!DNL SQL] query.

Se ci sono alcune persone che hanno bisogno del report ma non hanno familiarità con [!DNL SQL], Adobe suggerisce di utilizzare il sapore originale del Report Builder. Rende le cose più facili con loro.

## Ritorno a capo {#wrapup}

Entrambe [!DNL SQL Report Builder] e [!DNL Visual Report Builder] sono adatti per un’ampia varietà di casi d’uso. In genere, questo dipende da quali sono le tue esigenze analitiche e da chi consuma l’analisi.
