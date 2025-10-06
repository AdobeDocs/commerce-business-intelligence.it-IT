---
title: Replica dei canali Google Analytics tramite origini di acquisizione
description: Scopri come replicare i canali Google Analytics utilizzando le origini di acquisizione.
exl-id: e7248fe4-94db-4cdf-8f58-1f65061a207d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---

# [!DNL Google Analytics] con origini di acquisizione

## Cosa sono i canali? {#channels}

La creazione di segmenti personalizzati per visualizzare le prestazioni di traffico diverso e osservare le tendenze è uno degli utilizzi più potenti di [!DNL Google Analytics]. Una classe di segmenti esistente per impostazione predefinita in [!DNL Google Analytics] è `Channels`. I canali sono un raggruppamento di modi comuni in cui le persone accedono al tuo sito.  [!DNL Google Analytics] ordina automaticamente i diversi modi in cui si acquisisce un utente (tramite social media, pay-per-click, e-mail o collegamenti di riferimento) e li raggruppa in un bucket o in un canale.

## Perché non vedo il mio `channels` in Commerce Intelligence? {#nochannels}

`Channels` sono semplici bucket di dati aggregati. Per ordinare le acquisizioni in bucket di canale, [!DNL Google] imposta regole e definizioni distinte utilizzando parametri specifici: una combinazione di acquisizione [Source](https://support.google.com/analytics/answer/1033173?hl=en) (origine del traffico) e acquisizione [Medium](https://support.google.com/analytics/answer/6099206?hl=en) (categoria generale dell&#39;origine).

Anche se l’utilizzo di questi bucket può aiutarti a capire da dove proviene il traffico, questi dati non vengono taggati per canale, ma da una combinazione di Source e Medium. Poiché [!DNL Google] invia le informazioni sul canale come due punti dati separati, i raggruppamenti di canali non vengono visualizzati automaticamente in [!DNL Commerce Intelligence].

## Quali sono i raggruppamenti di canali predefiniti? Come vengono create?

Per impostazione predefinita, [!DNL Google] imposta otto canali diversi. Di seguito sono riportate le regole che determinano la modalità di creazione dei canali.

| **Canale** | **Cos&#39;è?** | **Creazione completata** |
|---|---|---|
| Diretto | Chiunque entri direttamente nel tuo sito. | Source = `Direct`<br> E Medium = `(not set); OR Medium = (none)` |
| Ricerca organica | Traffico che è stato classificato in modo organico nei motori di ricerca non pagati. | Medium = `organic` |
| Referral | Traffico proveniente da un collegamento esterno che non è Ricerca organica o da siti web che non sono social network. | Medium = `referral` |
| Ricerca a pagamento | Traffico con un codice di tracciamento UTM in cui il mezzo è &quot;cpc&quot;, &quot;ppc&quot; o &quot;paidsearch&quot; e è una rete di distribuzione di annunci che non corrisponde a &quot;Content&quot; (Contenuto). | Medium = `^(cpc|ppc|paidsearch)$`<br>E ≠ rete di distribuzione annunci `Content` |
| Social | Traffico di riferimento proveniente da uno dei circa [400 social network](https://www.annielytics.com/blog/analytics/sites-google-analytics-includes-in-social-reports/) e non taggato come annuncio. | Riferimento Source social network = `Yes`<br> O Medium = `^(social|social-network|social-media|sm|social network|social media)$` |
| E-mail | Traffico proveniente da sessioni a cui viene applicato un tag &quot;e-mail&quot;. | Codice di tracciamento UTM di Medium = `email` |
| Visualizzazione | Traffico con codice di tracciamento UTM in cui il supporto è display o cpm. Include anche l’interazione AdWords in cui la rete di distribuzione degli annunci corrisponde a &quot;Content&quot; (Contenuto) | Medium = `^(display|cpm|banner)$`<br>OR Rete di distribuzione di annunci = `Content`<br>AND Formato annunci ≠ `Text` |
| Altro | Sessioni da altri canali pubblicitari (esclusa la Ricerca a pagamento) contrassegnate con un supporto di &quot;cpc&quot;, &quot;ppc&quot;, &quot;cpm, &quot;cpv&quot;, &quot;cpa&quot;, &quot;cpp&quot;, &quot;affiliate&quot;. | Medium = `^(cpv|cpa|cpp|content-text)$` |

{style="table-layout:auto"}

## Come posso ricreare questi raggruppamenti di canali nel mio Data Warehouse? {#recreate}

Ora che sai che i canali sono solo combinazioni di origini e media, è facile ricreare questi raggruppamenti nel tuo Data Warehouse in 3 fasi.

1. **Abilita la tua[!DNL Google ECommerce]integrazione**

   [Quando è abilitato](../importing-data/integrations/google-ecommerce.md), assicurati di [sincronizzare]&#x200B;(../{{ site.baseurl }}/data-analyst/data-warehouse-mgr/tour-dwm.html#syncing) i campi **medium** e **source** nel tuo Data Warehouse. Al termine dell&#39;operazione, i dati di acquisizione di origine e di supporto verranno inseriti nel Data Warehouse.

1. **Carica una mappatura dei raggruppamenti di canali di Google**

   Adobe Commerce crea una tabella con i raggruppamenti predefiniti mappati come file che puoi [scaricare](../../assets/ga-channel-mapping.csv).

   Se sei un professionista di [!DNL Google Analytics] e hai creato i tuoi canali, vuoi aggiungere le tue regole specifiche alla tabella di mappatura prima di caricare il file in [!DNL Commerce Intelligence].

   Inseriscilo nel tuo Data Warehouse come [caricamento file](../importing-data/connecting-data/using-file-uploader.md).

   ![Interfaccia di Data Warehouse Manager con le impostazioni della chiave primaria](../../assets/Setting_Primary_Keys.png)

1. **Stabilisci una relazione tra[!DNL Google ECommerce]e il caricamento del file di mapping**

   Per stabilire una relazione tra [!DNL Google ECommerce] e la tabella di mapping, [invia una richiesta di supporto](../../guide-overview.md#Submitting-a-Support-Ticket) al team di Data Analyst e fai riferimento a questo argomento. L&#39;analista crea una nuova colonna calcolata denominata **Canale** nella tabella ECommerce. **Dopo un ciclo di aggiornamento completo**, questa colonna sarà pronta per l&#39;utilizzo in `Filter` o `Group by`.

Nel Data Warehouse sono ora presenti [!DNL Google Analytics Channel] raggruppamenti, il che significa che puoi analizzare i dati da una nuova prospettiva:

![Segmentazione della metrica Numero di ordini per canale](../../assets/GA_Channel_Gif.gif)

In questo esempio hai iniziato con la segmentazione della metrica **Numero di ordini** per **Canale**. Prova la nuova colonna e scopri le tendenze che puoi identificare nei tuoi dati di [!DNL Google Analytics Channel].

## Documentazione correlata

* [Utilizzo di Report Builder](../../tutorials/using-visual-report-builder.md)
* [Previsti[!DNL Google ECommerce]dati](../importing-data/integrations/google-ecommerce-data.md)
* [Creazione di [!DNL Google ECommerce] dimensioni con i dati dell&#39;ordine e del cliente](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [Quali sono le fonti e i canali di acquisizione più importanti?](../analysis/most-value-source-channel.md)
