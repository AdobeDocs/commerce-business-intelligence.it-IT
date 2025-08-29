---
source-git-commit: 6233779ba2e2a99ed229f8aa97497eb8d9d877f7
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 5%

---
# Documentazione tecnica di Adobe Commerce Intelligence

Apprezziamo i contributi della community e dei dipendenti Adobe esterni ai team di documentazione.

## Codice di condotta di Adobe Open Source

Questo progetto ha adottato il [Codice di condotta di Adobe Open Source](code-of-conduct.md) o il [Codice di condotta di .NET Foundation](https://dotnetfoundation.org/code-of-conduct). Per ulteriori informazioni, consulta l’articolo [Contribuzione](contributing.md).

## Informazioni sui contributi ai contenuti di Adobe

Consulta la [Guida per i collaboratori per la documentazione di Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html).

Il modo in cui contribuisci dipende da chi sei e dal tipo di modifiche con cui desideri contribuire:

### Modifiche minori

Se stai apportando aggiornamenti minori, visita l&#39;articolo e fai clic sull&#39;area di feedback visualizzata in fondo all&#39;articolo, fai clic su **Opzioni di feedback dettagliate**, quindi fai clic su **Suggerisci una modifica** per passare al file Markdown di origine su GitHub. Utilizza l’interfaccia utente di GitHub per apportare modifiche. Per ulteriori informazioni, consulta la [Guida per i collaboratori per la documentazione di Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html).

Le correzioni minori o i chiarimenti inviati per la documentazione e gli esempi di codice in questo archivio sono coperti dalle condizioni d’uso di Adobe.

### Modifiche sostanziali o nuovi articoli da parte dei membri della community

Se fai parte della community Adobe e desideri creare un nuovo articolo o inviare modifiche importanti, utilizza la scheda Issues (Problemi) nell’archivio Git per inviare una segnalazione e avviare una conversazione con il team addetto alla documentazione. Dopo aver accettato un piano, dovrai collaborare con un dipendente per coordinare la pubblicazione dei nuovi contenuti attraverso una combinazione di interventi negli archivi pubblici e privati.

### Modifiche sostanziali da parte dei dipendenti Adobe

Se sei un autore tecnico, un responsabile di programma o uno sviluppatore del team di prodotto per una soluzione Adobe Experience Cloud ed è tuo compito creare o contribuire ad articoli tecnici, devi utilizzare l&#39;archivio privato all&#39;indirizzo `https://git.corp.adobe.com/AdobeDocs`.

## Strumenti e configurazione

I collaboratori della community possono utilizzare l’interfaccia utente di GitHub per apportare modifiche di base o eseguire il fork dell’archivio per apportare contributi principali.

Per informazioni dettagliate, consulta la [Guida per i collaboratori per la documentazione di Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html).

## Come utilizzare markdown per formattare l’argomento

Tutti gli articoli in questo archivio utilizzano il markdown GitHub. Se non conosci Markdown, consulta:

- [Nozioni di base su Markdown](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)
- [Foglio di riferimento per il markdown stampabile](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf)

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
