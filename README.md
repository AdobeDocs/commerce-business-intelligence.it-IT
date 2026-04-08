---
source-git-commit: 4557430537492370a52030b60750950db8b245da
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 6%

---
# Documentazione tecnica di Adobe Commerce Intelligence

Apprezziamo i contributi della community e dei dipendenti Adobe esterni ai team di documentazione.

## Codice di condotta di Adobe Open Source

Questo progetto ha adottato il [Codice di condotta di Adobe Open Source](code-of-conduct.md) o il [Codice di condotta di .NET Foundation](https://dotnetfoundation.org/code-of-conduct). Per ulteriori informazioni, consulta l’articolo [Contribuzione](contributing.md).

## Informazioni sui contributi ai contenuti di Adobe

Consulta la [Guida per i collaboratori per la documentazione di Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html?lang=it).

Il modo in cui contribuisci dipende da chi sei e dal tipo di modifiche con cui desideri contribuire:

### Modifiche minori

Se stai apportando aggiornamenti minori, visita l&#39;articolo e fai clic sull&#39;area di feedback visualizzata in fondo all&#39;articolo, fai clic su **Opzioni di feedback dettagliate**, quindi fai clic su **Suggerisci una modifica** per passare al file Markdown di origine su GitHub. Utilizza l’interfaccia utente di GitHub per apportare modifiche. Per ulteriori informazioni, consulta la [Guida per i collaboratori per la documentazione di Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html?lang=it).

Le correzioni minori o i chiarimenti inviati per la documentazione e gli esempi di codice in questo archivio sono coperti dalle condizioni d’uso di Adobe.

### Modifiche sostanziali o nuovi articoli da parte dei membri della community

Se fai parte della community Adobe e desideri creare un nuovo articolo o inviare modifiche importanti, utilizza la scheda Issues (Problemi) nell’archivio Git per inviare una segnalazione e avviare una conversazione con il team addetto alla documentazione. Dopo aver accettato un piano, dovrai collaborare con un dipendente per coordinare la pubblicazione dei nuovi contenuti attraverso una combinazione di interventi negli archivi pubblici e privati.

### Modifiche sostanziali da parte dei dipendenti Adobe

Se sei un autore tecnico, un responsabile di programma o uno sviluppatore del team di prodotto per una soluzione Adobe Experience Cloud e il tuo lavoro consiste nel contribuire a o creare articoli tecnici, devi utilizzare l’archivio privato all’indirizzo GHEC.

## Strumenti e configurazione

I collaboratori della community possono utilizzare l’interfaccia utente di GitHub per apportare modifiche di base o eseguire il fork dell’archivio per apportare contributi principali.

Per informazioni dettagliate, consulta la [Guida per i collaboratori per la documentazione di Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html?lang=it).

## Come utilizzare markdown per formattare l’argomento

Tutti gli articoli in questo archivio utilizzano il markdown GitHub. Se non conosci Markdown, consulta:

- [Guida alla sintassi Markdown](https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/markdown-syntax)
- [Scheda di riferimento della sintassi Markdown](https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/cheatsheet)

## Hook di pre-commit per l’ottimizzazione delle immagini

Questo archivio include hook di pre-commit automatizzati che ottimizzano le immagini prima del commit. **Tutti i collaboratori devono abilitare questi hook** per garantire un&#39;ottimizzazione delle immagini coerente e dimensioni ridotte dell&#39;archivio.

### Configurazione rapida

Dopo aver clonato l’archivio, esegui:

```bash
.githooks/setup-hooks.sh
```

### Funzionamento degli hook

- Rileva automaticamente i file immagine di staging (PNG, JPG, JPEG, GIF, SVG)
- Esegui `image_optim` per comprimere e ottimizzare le immagini
- Riposiziona automaticamente nell&#39;area intermedia le immagini ottimizzate
- Assicurati che tutte le immagini salvate siano ottimizzate correttamente

### Vantaggi

- Dimensioni ridotte dell’archivio
- Caricamenti di pagina più rapidi per la documentazione
- Qualità delle immagini coerente per tutti i collaboratori
- Non è richiesta alcuna ottimizzazione manuale

Per istruzioni dettagliate sulla configurazione, la risoluzione dei problemi e la configurazione, vedere [`.githooks/README.md`](.githooks/README.md).

## Guida all’authoring di Experience League

### Introduzione

- [Panoramica introduttiva](https://experienceleague.adobe.com/en/docs/authoring-guide/using/getting-started/getting-started)
- [Configurazione Git](https://experienceleague.adobe.com/en/docs/authoring-guide/using/setup/tools/git-setup)
- [Nozioni di base sulla documentazione Git e GitHub](https://experienceleague.adobe.com/en/docs/authoring-guide/using/setup/tools/git-fundamentals)
- [Video introduttivi](https://experienceleague.adobe.com/en/docs/authoring-guide/using/getting-started/quick-start-guides/quick-start-overview)

### Flussi di lavoro

- [Flusso di lavoro per collaboratori non frequenti](https://experienceleague.adobe.com/en/docs/authoring-guide/using/editing/git-workflow-infrequent-user)
- [Richieste pull GitHub](https://experienceleague.adobe.com/en/docs/authoring-guide/using/editing/public-github)

### Authoring

- [Best practice per l&#39;authoring](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/authoring-best-practices)
- [Guida alla sintassi Markdown](https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/markdown-syntax)
- [Scheda di riferimento della sintassi Markdown](https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/cheatsheet)
- [Utilizzo delle tabelle](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/tables)
- [Aggiunta di collegamenti](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/linking)
- [Spostamento e ristrutturazione del contenuto](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/restructure-new)
