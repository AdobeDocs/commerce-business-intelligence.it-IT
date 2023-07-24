---
title: Replica dei canali Google Analytics tramite origini di acquisizione
description: Scopri come replicare i canali Google Analytics utilizzando le origini di acquisizione.
exl-id: e7248fe4-94db-4cdf-8f58-1f65061a207d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 0%

---

# [!DNL Google Analytics] utilizzo di origini di acquisizione

## Cosa sono i canali? {#channels}

La creazione di segmenti personalizzati per vedere le prestazioni di diversi tipi di traffico e osservare le tendenze è uno degli utilizzi più potenti per [!DNL Google Analytics]. Una classe di segmenti esistente per impostazione predefinita in [!DNL Google Analytics] sono `Channels`. I canali sono un raggruppamento di modi comuni in cui le persone accedono al tuo sito.  [!DNL Google Analytics] ordina automaticamente i diversi modi in cui si acquisisce un utente (tramite social media, pay-per-click, e-mail o collegamenti di riferimento) e li raggruppa in un bucket, o Canale.

## Perché non vedo il mio `channels` in Commerce Intelligence? {#nochannels}

`Channels` sono contenitori di dati semplici e aggregati. Per ordinare le acquisizioni in blocchi di canale: [!DNL Google] stabilisce regole e definizioni distinte utilizzando parametri specifici: una combinazione di acquisizione [Sorgente](https://support.google.com/analytics/answer/1033173?hl=en) (origine del traffico) e acquisizione [Medio](https://support.google.com/analytics/answer/6099206?hl=en) (la categoria generale della sorgente).

Anche se l’utilizzo di questi bucket può aiutarti a capire da dove proviene il traffico, questi dati non vengono taggati per canale, ma da una combinazione di Origine e Media. Perché [!DNL Google] invia informazioni sul canale come due punti dati separati; i raggruppamenti di canali non vengono visualizzati automaticamente in [!DNL Commerce Intelligence].

## Quali sono i raggruppamenti di canali predefiniti? Come vengono create?

Per impostazione predefinita, [!DNL Google] imposta otto canali diversi. Di seguito sono riportate le regole che determinano la modalità di creazione dei canali.

| **Canale** | **Che cos&#39;è?** | **Come viene creato?** |
|---|---|---|
| Diretto | Chiunque entri direttamente nel tuo sito. | Origine = `Direct`<br>AND Medio = `(not set); OR Medium = (none)` |
| Ricerca organica | Traffico che è stato classificato in modo organico nei motori di ricerca non pagati. | Media = `organic` |
| Referral | Traffico proveniente da un collegamento esterno che non è Ricerca organica o da siti web che non sono social network. | Media = `referral` |
| Ricerca a pagamento | Traffico con un codice di tracciamento UTM in cui il mezzo è &quot;cpc&quot;, &quot;ppc&quot; o &quot;paidsearch&quot; e è una rete di distribuzione di annunci che non corrisponde a &quot;Content&quot; (Contenuto). | Media = `^(cpc|ppc|paidsearch)$`<br>E ≠ di rete per la distribuzione di annunci `Content` |
| Social | Traffico di riferimento proveniente da uno dei seguenti elementi: [400 social network](https://www.annielytics.com/blog/analytics/sites-google-analytics-includes-in-social-reports/) e non vengono taggati come annunci. | Referral origine social = `Yes`<br>OR Medio = `^(social|social-network|social-media|sm|social network|social media)$` |
| E-mail | Traffico proveniente da sessioni a cui viene applicato un tag &quot;e-mail&quot;. | Codice di tracciamento UTM di Medium = `email` |
| Visualizzazione | Traffico con codice di tracciamento UTM in cui il supporto è display o cpm. Include anche l’interazione AdWords in cui la rete di distribuzione degli annunci corrisponde a &quot;Content&quot; (Contenuto) | Media = `^(display|cpm|banner)$`<br>O Rete di distribuzione di annunci = `Content`<br>≠ del formato dell’annuncio AND `Text` |
| Altro | Sessioni da altri canali pubblicitari (esclusa la Ricerca a pagamento) contrassegnate con un supporto di &quot;cpc&quot;, &quot;ppc&quot;, &quot;cpm, &quot;cpv&quot;, &quot;cpa&quot;, &quot;cpp&quot;, &quot;affiliate&quot;. | Media = `^(cpv|cpa|cpp|content-text)$` |

{style="table-layout:auto"}

## Come posso ricreare questi raggruppamenti di canali nella mia Data Warehouse? {#recreate}

Ora che sai che i canali sono solo combinazioni di sorgenti e media, è facile ricreare questi raggruppamenti nella tua Data Warehouse in tre fasi.

1. **Abilita[!DNL Google ECommerce]integrazione**

   [Quando abilitato](../importing-data/integrations/google-ecommerce.md), assicurati di [sincronizzazione](.../{{ site.baseurl }}/data-analyst/data-warehouse-mgr/tour-dwm.html#syncing) il **media** e **sorgente** campi nella Data Warehouse. Al termine dell&#39;operazione, i dati di acquisizione di origine e di supporto verranno inseriti nella Data Warehouse.

1. **Carica una mappatura dei raggruppamenti di canali di Google**

   Adobe Commerce crea una tabella con i raggruppamenti predefiniti mappati come file che puoi [scaricare](../../assets/ga-channel-mapping.csv).

   Se sei un [!DNL Google Analytics] e creato i tuoi canali, desideri aggiungere le tue regole specifiche alla tabella di mappatura prima di caricare il file in [!DNL Commerce Intelligence].

   Portalo nella tua Data Warehouse come [Caricamento file](../importing-data/connecting-data/using-file-uploader.md).

   ![](../../assets/Setting_Primary_Keys.png)

1. **Stabilire una relazione tra[!DNL Google ECommerce]Caricamento di file di mappature e**

   Per stabilire una relazione tra[!DNL Google ECommerce] e la tabella di mappatura, [invia una richiesta di assistenza](../../guide-overview.md#Submitting-a-Support-Ticket) rivolgiti al tuo team di analista dati e fai riferimento a questo argomento. L’analista crea una nuova colonna calcolata denominata **Canale** nella tabella ECommerce. **Dopo un ciclo di aggiornamento completo**, questa colonna sarà pronta per essere utilizzata in una `Filter` o `Group by`.

Ora hai [!DNL Google Analytics Channel] raggruppamenti nella tua Data Warehouse, il che significa che puoi analizzare i dati da una nuova prospettiva:

![Segmentazione della metrica Numero di ordini per canale](../../assets/GA_Channel_Gif.gif)

In questo esempio, hai iniziato con la segmentazione del **Numero di ordini** metrica per **Canale**. Prova la nuova colonna e scopri le tendenze che puoi identificare nel [!DNL Google Analytics Channel] dati!

## Documentazione correlata

* [Utilizzo del Report Builder](../../tutorials/using-visual-report-builder.md)
* [Previsto[!DNL Google ECommerce]dati](../importing-data/integrations/google-ecommerce-data.md)
* [Generazione[!DNL Google ECommerce]dimensioni con dati di ordini e clienti](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [Quali sono le fonti e i canali di acquisizione più importanti?](../analysis/most-value-source-channel.md)
