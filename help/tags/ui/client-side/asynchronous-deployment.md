---
title: Implementazione asincrona
description: Scopri come distribuire in modo asincrono le librerie di tag Adobe Experience Platform sul tuo sito web.
source-git-commit: 5f810ada57eeb12a56de603d974a091b888dc9d2
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 59%

---

# Implementazione asincrona

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

La distribuzione delle prestazioni e non di blocco delle librerie JavaScript richieste dai nostri prodotti è sempre più importante per gli utenti Adobe Experience Cloud. Strumenti come [[!DNL Google PageSpeed]](https://developers.google.com/speed/pagespeed/insights/) consigliano agli utenti di modificare il modo in cui distribuiscono le librerie di Adobi sul loro sito. Questo articolo spiega come utilizzare le librerie JavaScript di Adobe in modo asincrono.

## Sincrona e asincrona

### Distribuzione sincrona

Le librerie vengono spesso caricate in modo sincrono nel tag `<head>` di una pagina. Esempio:

```markup
<script src="example.js"></script>
```

Per impostazione predefinita, il browser analizza il documento e raggiunge questa riga, quindi inizia a recuperare il file JavaScript dal server. Il browser attende fino alla restituzione del file, quindi analizza ed esegue il file JavaScript. Infine, continua ad analizzare il resto del documento HTML.

Se il parser si trova in un tag `<script>` prima di eseguire il rendering del contenuto visibile, la visualizzazione del contenuto avviene in ritardo. Se il file JavaScript caricato non è strettamente necessario per mostrare il contenuto agli utenti, stai facendo aspettare i visitatori inutilmente. Maggiori sono le dimensioni della la libreria, maggiore è il ritardo. Per questo motivo, strumenti di benchmark delle prestazioni del sito Web come [!DNL Google PageSpeed] o [!DNL Lighthouse] spesso contrassegnano gli script caricati in modo sincrono.

Le librerie di gestione dei tag possono crescere rapidamente se devi gestire molti tag.

### Implementazione asincrona

Puoi caricare qualsiasi libreria in modo asincrono aggiungendo un attributo `async` al tag `<script>`. Esempio:

```markup
<script src="example.js" async></script>
```

Questo indica al browser che, quando questo tag di script viene analizzato, deve iniziare a caricare il file JavaScript ma, invece di attendere il caricamento e l&#39;esecuzione della libreria, deve continuare ad analizzare ed eseguire il rendering del resto del documento.

## Valutazioni sulla distribuzione asincrona

Come descritto in precedenza, nelle distribuzioni sincrone il browser mette in pausa ed esegue il rendering della pagina durante il caricamento e l’esecuzione della libreria di tag di Adobe Experience Platform. Nelle distribuzioni asincrone, al contrario, il browser continua ad analizzare ed eseguire il rendering della pagina durante il caricamento della libreria. Deve essere presa in considerazione la variabilità di quando la libreria di tag potrebbe terminare il caricamento in relazione all’analisi e al rendering delle pagine.

Innanzitutto, poiché la libreria di tag può terminare il caricamento prima o dopo l’analisi e l’esecuzione della parte inferiore della pagina, non dovresti più chiamare `_satellite.pageBottom()` dal codice della pagina (`_satellite` non sarà disponibile fino al caricamento della libreria). Questo è spiegato in [Caricamento del codice di incorporamento dei tag in modo asincrono](#loading-the-tags-embed-code-asynchronously).

In secondo luogo, il caricamento della libreria di tag può terminare prima o dopo l&#39;evento del browser [`DOMContentLoaded`](https://developer.mozilla.org/it-IT/docs/Web/Events/DOMContentLoaded) (DOM Ready).

A causa di questi due punti, vale la pena dimostrare come i tipi di evento [Library Loaded](../../extensions/web/core/overview.md#library-loaded-page-top), [Page Bottom](../../extensions/web/core/overview.md#page-bottom), [DOM Ready](../../extensions/web/core/overview.md#page-bottom) e [Window Loaded](../../extensions/web/core/overview.md#window-loaded) dall&#39;estensione Core quando si carica una libreria di tag in modo asincrono.

Se la proprietà tag contiene le quattro regole seguenti:

* Regola A: utilizza il tipo di evento Library Loaded
* Regola B: utilizza il tipo di evento Page Bottom
* Regola C: utilizza il tipo di evento DOM Ready
* Regola A: utilizza il tipo di evento Window Loaded

A prescindere da quando termina il caricamento della libreria di tag, l’esecuzione di tutte le regole è garantita nel seguente ordine:

Regola A → Regola B → Regola C → Regola D

Sebbene l’ordine sia sempre applicato, alcune regole potrebbero essere eseguite immediatamente al termine del caricamento della libreria di tag, mentre altre potrebbero essere eseguite in un secondo momento. Al termine del caricamento della libreria di tag si verifica quanto segue:

1. La regola A viene eseguita immediatamente.
1. Se l&#39;evento `DOMContentLoaded` del browser (DOM Ready) si è già verificato, la regola B e la regola C vengono eseguite immediatamente. In caso contrario, le regole B e C vengono eseguite successivamente quando si verifica l’evento del browser [`DOMContentLoaded`](https://developer.mozilla.org/en-US/docs/Web/Events/DOMContentLoaded).
1. Se l’evento del browser [`load`](https://developer.mozilla.org/it-IT/docs/Web/Events/load) (Windows Loaded) si è già verificato, la regola D viene eseguita immediatamente. In caso contrario, la regola D verrà eseguita successivamente quando si verifica l’evento del browser [`load`](https://developer.mozilla.org/en-US/docs/Web/Events/load). Nota che se hai installato la libreria di tag seguendo le istruzioni, la libreria di tag *sempre* termina prima dell&#39;esecuzione dell&#39;evento del browser [`load`](https://developer.mozilla.org/en-US/docs/Web/Events/load).

Quando applichi questi principi al tuo sito Web, prendi in considerazione quanto segue:

* **Una regola che utilizza il tipo di evento Library Loaded potrebbe essere eseguita prima del caricamento completo del livello di dati.**  Questo può comportare l&#39;esecuzione delle azioni della regola con dati mancanti, perché i dati non erano ancora disponibili sulla pagina. Questi tipi di problemi possono essere attenuati modificando la configurazione delle regole. Ad esempio, invece di avere una regola attivata dal tipo di evento Library Loaded, potresti invece utilizzare i tipi di evento Custom Event o Direct Call, attivati dal codice della pagina al termine del caricamento del livello di dati.
* **Il tipo di evento Page Bottom, in particolare, non specifica il valore quando la libreria viene caricata in modo asincrono.**  Considera invece Library Loaded, DOM Ready, Window Loaded o altri tipi di eventi.

Se noti che qualcosa non sta funzionando nel modo corretto, è probabile che si stiano verificando dei problemi di tempistica. Le implementazioni che richiedono tempistiche precise potrebbero dover utilizzare listener di eventi e il tipo di evento Custom Event o Direct Call per rendere le implementazioni più solide e coerenti.

## Caricamento del codice di incorporamento dei tag in modo asincrono

I tag consentono di attivare il caricamento asincrono quando si crea un codice di incorporamento quando si configura un [ambiente](../publishing/environments.md). Puoi anche configurare un caricamento asincrono autonomamente:

1. Aggiungi un attributo asincrono al tag `<script>` per caricare lo script in modo asincrono.

   Per il codice di incorporamento dei tag, significa modificare quanto segue:

   ```markup
   <script src="//www.yoururl.com/launch-EN1a3807879cfd4acdc492427deca6c74e.min.js"></script>
   ```

   in questo:

   ```markup
   <script src="//www.yoururl.com/launch-EN1a3807879cfd4acdc492427deca6c74e.min.js" async></script>
   ```

1. Rimuovi eventuale codice precedentemente aggiunto in fondo al tag:

   ```markup
   <script type="text/javascript">_satellite.pageBottom();</script>
   ```

   Questo codice comunica a Platform che il parser del browser ha raggiunto il fondo della pagina. È probabile che i tag non siano stati caricati ed eseguiti prima di questo momento, pertanto la chiamata a `_satellite.pageBottom()` genera un errore e il tipo di evento Page Bottom potrebbe non comportarsi come previsto.
