---
title: Replica dei canali di Google Analytics tramite origini di acquisizione
description: Scopri come replicare i canali di Google Analytics utilizzando le origini di acquisizione.
exl-id: e7248fe4-94db-4cdf-8f58-1f65061a207d
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# Google Analytics che utilizzano origini di acquisizione

## Cosa sono i canali? {#channels}

Creazione di segmenti personalizzati per vedere le prestazioni di traffico diverso e osservare le tendenze (nel bene o nel male) è uno degli usi più potenti per  [!DNL Google Analytics ]. Una classe di segmenti esistente per impostazione predefinita in [!DNL Google Analytics ] sono `Channels`. I canali sono un raggruppamento di modi comuni in cui le persone arrivano al tuo sito.  [!DNL Google Analytics ] ordina automaticamente i molti modi in cui acquisisci un utente - che si tratti di social media, pay-per-click, e-mail o collegamenti di riferimento - e li raggruppa in un bucket o in un canale.

## Perché non visualizzo il mio `channels` in MBI? {#nochannels}

`Channels` sono blocchi di dati semplici e aggregati. Per ordinare le acquisizioni nei bucket Canale, Google imposta regole e definizioni distinte utilizzando parametri specifici: una combinazione di acquisizione [Origine](https://support.google.com/analytics/answer/1033173?hl=en) (origine del traffico) e acquisizione [Media](https://support.google.com/analytics/answer/6099206?hl=en) (la categoria generale della fonte).

Anche se questi blocchi possono aiutarti a capire da dove proviene il traffico, questi dati non vengono effettivamente taggati per canale, ma da una combinazione di Origine e Media. Poiché Google invia informazioni sul canale come due punti di dati separati, i raggruppamenti di canali non vengono visualizzati automaticamente in [!DNL MBI].

## Quali sono i raggruppamenti di canali predefiniti? Come vengono creati?

Per impostazione predefinita, Google ti imposta con 8 canali diversi. Diamo un&#39;occhiata alle regole che determinano come vengono create:

| Canale | Che cos&#39;è? | Come viene creato? |
|---|---|---|
| Diretta | Chiunque venga direttamente nel tuo sito. | Origine = `Direct`<br>AND Medium = `(not set); OR Medium = (none)` |
| Ricerca organica | Traffico classificato organicamente nei motori di ricerca non pagati. | Media = `organic` |
| Riferimento | Traffico proveniente da un collegamento esterno che non è Ricerca organica o da siti web che non sono social network. | Media = `referral` |
| Ricerca a pagamento | Traffico con un codice di tracciamento UTM in cui il supporto è &quot;cpc&quot;, &quot;ppc&quot; o &quot;paidsearch&quot; E è una rete di distribuzione di annunci che non corrisponde a &quot;Content&quot;. | Media = `^(cpc|ppc|paidsearch)$`<br>E Rete di distribuzione degli annunci `Content` |
| Social | Traffico di riferimento proveniente da uno qualsiasi dei [400 reti sociali](https://www.annielytics.com/blog/analytics/sites-google-analytics-includes-in-social-reports/) e non sono taggati come annunci. | Riferimento origine social = `Yes`<br>O Media = `^(social|social-network|social-media|sm|social network|social media)$` |
| E-mail | Traffico da sessioni a cui viene applicato un tag tramite un &quot;e-mail&quot;. | Codice di tracciamento UTM di Medium = `email` |
| Visualizzazione | Traffico con un codice di tracciamento UTM in cui il supporto è visualizzato o cpm. Include anche l’interazione AdWords in cui la rete di distribuzione degli annunci corrisponde a &quot;Content&quot; | Media = `^(display|cpm|banner)$`<br>Rete di distribuzione degli annunci OR = `Content`<br>AND Formato annuncio `Text` |
| Altro | Sessioni da altri canali pubblicitari, esclusa la ricerca a pagamento, con tag su un supporto di &quot;cpc&quot;, &quot;ppc&quot;, &quot;cpm, &quot;cpv&quot;, &quot;cpa&quot;, &quot;cpp&quot;, &quot;affiliate&quot;. | Media = `^(cpv|cpa|cpp|content-text)$` |

{style=&quot;table-layout:auto&quot;}

## Come posso ricreare questi raggruppamenti di canali nella mia Data Warehouse? {#recreate}

Ora che sapete che i canali sono solo combinazioni di sorgenti e mezzi, è un processo semplice in 3 fasi per ricreare questi raggruppamenti nella vostra Data Warehouse.

1. **Abilita la tua[!DNL Google ECommerce]integrazione**

   [Una volta attivato](../importing-data/integrations/google-ecommerce.md), assicurati di [Sincronizzazione](../{{ site.baseurl }}/data-analyst/data-warehouse-mgr/tour-dwm.html#syncing) la **medium** e **source** campi nella tua Data Warehouse. Una volta completato questo processo, i dati di acquisizione di origine e media verranno inseriti nella tua Data Warehouse.

1. **Caricare una mappatura dei raggruppamenti di canali Google**

   Per risparmiare tempo, Commerce ha già creato una tabella con i raggruppamenti predefiniti mappati come file che è possibile [scaricare](../../assets/ga-channel-mapping.csv).

   Se sei un professionista di Google Analytics e hai creato i tuoi canali, vuoi aggiungere le tue regole specifiche alla tabella di mappatura prima di caricare il file in [!DNL MBI].

   Portalo nella tua Data Warehouse come [Caricamento file](../importing-data/connecting-data/using-file-uploader.md).

   ![](../../assets/Setting_Primary_Keys.png)

1. **Stabilire una relazione tra[!DNL Google ECommerce]Caricamento file e mappature**

   Per stabilire una relazione tra[!DNL Google ECommerce]e la tabella di mappatura, [inviare una richiesta di assistenza](../../guide-overview.md) al nostro team di Data Analyst e fai riferimento a questo articolo. L’analista creerà una nuova colonna calcolata denominata **Canale** nella tabella ECommerce. **Dopo un ciclo completo di aggiornamento**, questa colonna sarà pronta per essere utilizzata in un Filtro o Raggruppa per.

Congratulazioni! Ora hai dei raggruppamenti di canali Google Analytics nella tua Data Warehouse, il che significa che puoi analizzare i dati da una nuova prospettiva:

![Segmentazione della metrica Numero di ordini per canale](../../assets/GA_Channel_Gif.gif)

In questo esempio, abbiamo iniziato con la segmentazione semplice **Numero di ordini** metrica per **Canale**. Ora tocca a te - vai a testare la tua nuova colonna e vedi quali tendenze puoi identificare nei tuoi dati del canale Google Analytics!

## Documentazione correlata

* [Utilizzo del Report Builder](../../tutorials/using-visual-report-builder.md)
* [Previsto[!DNL Google ECommerce]dati](../importing-data/integrations/google-ecommerce-data.md)
* [Costruzione[!DNL Google ECommerce]dimensioni con i dati relativi all’ordine e al cliente](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [Quali sono le fonti e i canali di acquisizione più importanti?](../analysis/most-value-source-channel.md)
