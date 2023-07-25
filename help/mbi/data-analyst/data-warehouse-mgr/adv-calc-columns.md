---
title: Tipi di colonne calcolate avanzate
description: Scopri le nozioni di base per la maggior parte dei casi di colonna d’uso, ma potresti desiderare una colonna calcolata un po’ più complessa di quella che può essere creata dal gestore della Data Warehouse.
exl-id: 9871fa19-95b3-46e4-ae2d-bd7c524d12db
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 4%

---

# Tipi di colonne calcolate avanzate

Molte analisi che potresti voler creare comportano l’utilizzo di un **nuova colonna** che desideri `group by` o `filter by`. Il [Creazione di colonne calcolate](../data-warehouse-mgr/creating-calculated-columns.md) Questo tutorial illustra le nozioni di base per la maggior parte dei casi d’uso, ma potresti voler trovare una colonna calcolata un po’ più complessa di quella che può essere creata da Data Warehouse Manager.
{: #top}

Questi tipi di colonne possono essere creati dal team Adobe di analisti Data Warehouse. Per definire una nuova colonna calcolata, fornisci le seguenti informazioni:

1. Il **`definition`** di questa colonna (inclusi input, formule o formattazione)
1. Il **`table`** su cui desideri creare la colonna
1. Qualsiasi **`example data points`** che descrivono cosa deve contenere la colonna

Di seguito sono riportati alcuni esempi comuni di colonne calcolate avanzate che gli utenti spesso ritengono utili:

* [Ordina (o classifica) evento in sequenza](#compareevents)
* [Trovare il tempo tra due eventi](#twoevents)
* [Confrontare i valori di evento sequenziali](#sequence)
* [Converti valuta](#currency)
* [Conversione dei fusi orari](#timezone)
* [Qualcos&#39;altro](#else)

## Sto tentando di ordinare gli eventi in sequenza {#compareevents}

Questo è denominato **numero evento** colonna calcolata. Ciò significa che stai cercando di trovare la sequenza in cui si sono verificati gli eventi per un particolare proprietario dell’evento, ad esempio un cliente o un utente.

Ecco un esempio:

| **`event\_id`** | **`owner\_id`** | **`timestamp`** | **`Owner's event number`** |
|-----|-----|-----|-----|
| 1 | `A` | 2015-01-01 00:00:00 | 1 |
| 2 | `B` | 2015-01-01 00:30:00 | 1 |
| 3 | `A` | 2015-01-01 02:00:00 | 2 |
| 4 | `A` | 2015-01-02 13:00:00 | 3 |
| 5 | `B` | 2015-01-03 13:00:00 | 2 |

{style="table-layout:auto"}

Una colonna calcolata relativa al numero di evento può essere utilizzata per osservare le differenze di comportamento tra eventi nuovi, eventi ripetuti o eventi ennesimi nei dati.

Desideri visualizzare la colonna del numero di ordine del cliente in azione? Fai clic sull’immagine per visualizzarla utilizzata come dimensione Raggruppa per in un rapporto.

![Utilizzo di una colonna calcolata del numero evento per il raggruppamento in base al numero di ordine del cliente.](../../assets/EventNumber.gif)<!--{: style="max-width: 500px;"}-->

Per creare questo tipo di colonna calcolata, è necessario conoscere:

* Tabella in cui si desidera creare la colonna
* Campo che identifica il proprietario degli eventi (`owner\_id` in questo esempio)
* Campo in base al quale si desidera ordinare gli eventi (`timestamp` in questo esempio)

[Torna all&#39;inizio](#top)

## Sto cercando di trovare il tempo tra due eventi. {#twoevents}

Questo è chiamato `date difference` colonna calcolata. Ciò significa che stai tentando di trovare il tempo tra due eventi appartenenti a un singolo record, in base ai timestamp dell’evento.

Ecco un esempio:

| `id` | `timestamp\_1` | `timestamp\_2` | `Seconds between timestamp\_2 and timestamp\_1` |
|-----|-----|-----|-----|
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style="table-layout:auto"}

Una colonna calcolata sulla differenza di data può essere utilizzata per creare una metrica che calcola il tempo medio o mediano tra due eventi. Fare clic sull&#39;immagine seguente per verificare come `Average time to first order` metrica utilizzata in un rapporto.

![Utilizzo di una colonna calcolata sulla differenza di data per calcolare il tempo medio al primo ordine.](../../assets/DateDifference.gif)<!--{: style="max-width: 500px;"}-->

Per creare questo tipo di colonna calcolata, è necessario conoscere:

* Tabella in cui si desidera creare la colonna
* I due timestamp tra i quali desideri conoscere la differenza

[Torna all&#39;inizio](#top)

## Sto tentando di confrontare valori di evento sequenziali. {#sequence}

Questo è chiamato **confronto sequenziale degli eventi**. Ciò significa che stai tentando di trovare il delta tra un valore (valuta, numero, marca temporale) e il valore corrispondente per l’evento precedente del proprietario.

Ecco un esempio:

| **`event\_id`** | **`owner\_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|-----|-----|-----|-----|
| 1 | `A` | 2015-01-01 00:00:00 | NULL |
| 2 | `B` | 2015-01-01 00:30:00 | NULL |
| 3 | `A` | 2015-01-01 02:00:00 | 7720 |
| 4 | `A` | 2015-01-02 13:00:00 | 126000 |
| 5 | `B` | 2015-01-03 13:00:00 | 217800 |

{style="table-layout:auto"}

Un confronto sequenziale degli eventi può essere utilizzato per trovare il tempo medio o mediano tra ciascun evento sequenziale. Fai clic sull&#39;immagine seguente per visualizzare **Tempo medio e medio tra ordini** in azione.

=![Utilizzo di una colonna calcolata per il confronto sequenziale degli eventi per calcolare il tempo medio e mediano tra gli ordini.](../../assets/SeqEventComp.gif)<!--{: style="max-width: 500px;"}-->

Per creare questo tipo di colonna calcolata, è necessario conoscere:

* Tabella in cui si desidera creare la colonna
* Campo che identifica il proprietario degli eventi (`owner\_id` nell&#39;esempio)
* Il campo del valore tra cui si desidera visualizzare la differenza per ogni evento sequenziale (`timestamp` in questo esempio)

[Torna all&#39;inizio](#top)

## Sto provando a convertire la valuta. {#currency}

A **conversione valuta** nella colonna calcolata gli importi delle transazioni vengono convertiti da una valuta registrata a una valuta di dichiarazione, in base al tasso di cambio al momento dell&#39;evento.

Ecco un esempio:

| **`id`** | **`timestamp`** | **`transaction\_value\_EUR`** | **`transaction\_value\_USD`** |
|-----|-----|-----|-----|
| `1` | 2015-01-01 00:00:00 | 30 | 33.57 |
| `2` | 2015-01-02 00:00:00 | 50 | 55.93 |

{style="table-layout:auto"}

Per creare questo tipo di colonna calcolata, è necessario conoscere:

* Tabella in cui si desidera creare la colonna
* Colonna dell&#39;importo della transazione da convertire
* Colonna che indica la valuta in cui sono stati registrati i dati (in genere un codice ISO)
* La valuta di dichiarazione preferita

[Torna all&#39;inizio](#top)

## Io sto provando a convertire i fusi orari. {#timezone}

A **conversione del fuso orario** la colonna calcolata converte i timestamp per una particolare origine dati dal fuso orario registrato a quello di reporting.

Ecco un esempio:

| **`id`** | **`timestamp\_UTC`** | **`timestamp\_ET`** |
|-----|-----|-----|
| `1` | 2015-01-01 00:00:00 | 2014-12-31 19:00:00 |
| `2` | 2015-01-01 12:00:00 | 2015-01-01 07:00:00 |

{style="table-layout:auto"}

Per creare questo tipo di colonna calcolata, è necessario conoscere:

* Tabella in cui si desidera creare la colonna
* Colonna timestamp da convertire
* Fuso orario in cui sono stati registrati i dati
* Il fuso orario preferito per la generazione dei rapporti

[Torna all&#39;inizio](#top)

## Sto cercando di fare qualcosa che non è elencato qui. {#else}

Non preoccuparti. Solo perché non è elencato qui non significa che non è possibile. Il team di Adobi degli analisti di Data Warehouse può essere d&#39;aiuto.

Per definire una nuova colonna calcolata: [invia un ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) con dettagli su ciò che desideri creare.

## Documentazione correlata

* [Creazione di colonne calcolate](../data-warehouse-mgr/creating-calculated-columns.md)
* [Tipi di colonna calcolati](../data-warehouse-mgr/calc-column-types.md)
* [Generazione [!DNL Google ECommerce] dimensioni con dati di ordini e clienti](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
