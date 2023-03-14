---
title: Implementazione asincrona
description: Scopri come implementare in modo asincrono le librerie tag di Adobe Experience Platform nel tuo sito web.
exl-id: ed117d3a-7370-42aa-9bc9-2a01b8e7794e
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 92%

---

# Implementazione asincrona {#asynchronous-deployment}

>[!CONTEXTUALHELP]
>id="platform_tags_asynchronous_deployment"
>title="Implementazione asincrona"
>abstract="Se questa opzione è abilitata, quando questo tag script viene analizzato il browser inizierà a caricare il file JavaScript, ma invece di attendere che la libreria venga caricata ed eseguita, continuerà ad analizzare ed eseguire il rendering del resto del documento. Questo può migliorare le prestazioni della pagina web, ma ha importanti implicazioni quando si tratta di come vengono eseguite determinate regole. Per ulteriori informazioni, consulta la documentazione ."

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Per gli utenti di Adobe Experience Cloud, assumono sempre maggiore importanza sia le prestazioni, sia la possibilità di implementare le librerie JavaScript richieste dai prodotti Adobe senza che questo comporti alcun blocco del sistema. Strumenti come [[!DNL Google PageSpeed]](https://developers.google.com/speed/pagespeed/insights/) consigliano agli utenti di modificare le modalità di implementazione delle librerie Adobe nei loro siti. Questo articolo spiega come utilizzare le librerie JavaScript di Adobe in modo asincrono.

## Sincrona e asincrona

### Distribuzione sincrona

Le librerie vengono spesso caricate in modo sincrono nel tag `<head>` di una pagina. Esempio:

```markup
<script src="example.js"></script>
```

Per impostazione predefinita, il browser analizza il documento e raggiunge questa riga, quindi inizia a recuperare il file JavaScript dal server. Il browser attende fino alla restituzione del file, quindi analizza ed esegue il file JavaScript. Infine, continua ad analizzare il resto del documento HTML.

Se il parser si trova in un tag `<script>` prima di eseguire il rendering del contenuto visibile, la visualizzazione del contenuto avviene in ritardo. Se il file JavaScript caricato non è strettamente necessario per mostrare il contenuto agli utenti, stai facendo aspettare i visitatori inutilmente. Maggiori sono le dimensioni della la libreria, maggiore è il ritardo. Per questo motivo, strumenti di benchmark delle prestazioni del sito Web come [!DNL Google PageSpeed] o [!DNL Lighthouse] spesso contrassegnano gli script caricati in modo sincrono.

Le librerie di gestione dei tag possono crescere rapidamente in presenza di numerosi tag da gestire.

### Implementazione asincrona

Puoi caricare qualsiasi libreria in modo asincrono aggiungendo un attributo `async` al tag `<script>`. Esempio:

```markup
<script src="example.js" async></script>
```

Questo indica al browser che, quando questo tag di script viene analizzato, deve iniziare a caricare il file JavaScript ma, invece di attendere il caricamento e l&#39;esecuzione della libreria, deve continuare ad analizzare ed eseguire il rendering del resto del documento.

## Valutazioni sulla distribuzione asincrona

Come descritto in precedenza, nelle implementazioni sincrone, il browser interrompe l’analisi e il rendering della pagina mentre viene caricata ed eseguita la libreria di tag di Adobe Experience Platform. Nelle distribuzioni asincrone, al contrario, il browser continua ad analizzare ed eseguire il rendering della pagina durante il caricamento della libreria. Occorre quindi considerare quando verrà completato il caricamento della libreria di tag, in relazione all’analisi e al rendering delle pagine.

Innanzitutto, poiché il caricamento della libreria di tag può terminare prima o dopo l’analisi e l’esecuzione della pagina, non chiamare più `_satellite.pageBottom()` dal codice della pagina (`_satellite` sarà disponibile solo dopo che sarà stata caricata la libreria). Questa situazione è descritta in [Caricamento del codice di incorporamento di tag in modo asincrono](#loading-the-tags-embed-code-asynchronously).

In secondo luogo, il caricamento della libreria di tag può terminare prima o dopo l’evento [`DOMContentLoaded`](https://developer.mozilla.org/it-IT/docs/Web/Events/DOMContentLoaded) del browser (DOM Ready).

A causa di questi due punti, vale la pena dimostrare come funzionano i tipi di evento [Library Loaded](../../extensions/client/core/overview.md#library-loaded-page-top), [Page Bottom](../../extensions/client/core/overview.md#page-bottom), [DOM Ready](../../extensions/client/core/overview.md#page-bottom) e [Window Loaded](../../extensions/client/core/overview.md#window-loaded) dell’estensione Core durante il caricamento asincrono di una libreria di tag.

Se la proprietà tag contiene le quattro regole seguenti:

* Regola A: utilizza il tipo di evento Library Loaded
* Regola B: utilizza il tipo di evento Page Bottom
* Regola C: utilizza il tipo di evento DOM Ready
* Regola A: utilizza il tipo di evento Window Loaded

A prescindere da quando termina il caricamento della libreria di tag, tutte le regole vengono eseguite nel seguente ordine:

Regola A → Regola B → Regola C → Regola D

Anche se questo ordine viene sempre applicato, alcune regole potrebbero essere eseguite immediatamente al termine del caricamento della libreria di tag, mentre altre in un secondo momento. Al termine del caricamento della libreria di tag si verifica quanto segue:

1. La regola A viene eseguita immediatamente.
1. Se l&#39;evento `DOMContentLoaded` del browser (DOM Ready) si è già verificato, la regola B e la regola C vengono eseguite immediatamente. In caso contrario, le regole B e C vengono eseguite successivamente quando si verifica l’evento del browser [`DOMContentLoaded`](https://developer.mozilla.org/it-IT/docs/Web/Events/DOMContentLoaded).
1. Se l’evento del browser [`load`](https://developer.mozilla.org/it-IT/docs/Web/Events/load) (Windows Loaded) si è già verificato, la regola D viene eseguita immediatamente. In caso contrario, la regola D verrà eseguita successivamente quando si verifica l’evento del browser [`load`](https://developer.mozilla.org/it-IT/docs/Web/Events/load). Tieni presente che, se hai installato la libreria di tag seguendo le istruzioni, il suo caricamento viene *sempre* completato prima che venga eseguito l’evento [`load`](https://developer.mozilla.org/it-IT/docs/Web/Events/load) del browser.

Quando applichi questi principi al tuo sito Web, prendi in considerazione quanto segue:

* **Una regola che utilizza il tipo di evento Library Loaded potrebbe essere eseguita prima del caricamento completo del livello di dati.**  Questo può comportare l&#39;esecuzione delle azioni della regola con dati mancanti, perché i dati non erano ancora disponibili sulla pagina. Questi tipi di problemi possono essere attenuati modificando la configurazione delle regole. Ad esempio, invece di avere una regola attivata dal tipo di evento Library Loaded, potresti invece utilizzare i tipi di evento Custom Event o Direct Call, attivati dal codice della pagina al termine del caricamento del livello di dati.
* **Il tipo di evento Page Bottom, in particolare, non specifica il valore quando la libreria viene caricata in modo asincrono.**  Considera invece Library Loaded, DOM Ready, Window Loaded o altri tipi di eventi.

Se noti che qualcosa non sta funzionando nel modo corretto, è probabile che si stiano verificando dei problemi di tempistica. Le implementazioni che richiedono tempistiche precise potrebbero dover utilizzare listener di eventi e il tipo di evento Custom Event o Direct Call per rendere le implementazioni più solide e coerenti.

## Caricamento del codice di incorporamento dei tag in modo asincrono

I tag dispongono di un pulsante per attivare il caricamento asincrono quando si crea un codice di incorporamento durante la configurazione di un [ambiente](../publishing/environments.md). Puoi anche configurare un caricamento asincrono autonomamente:

1. Aggiungi un attributo asincrono al tag `<script>` per caricare lo script in modo asincrono.

   Nel caso del codice di incorporamento di tag, significa modificare quanto segue:

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

   Questo codice comunica a Platform che il parser del browser ha raggiunto il fondo della pagina. Poiché probabilmente i tag non saranno ancora caricati e in esecuzione in questo momento, la chiamata a `_satellite.pageBottom()` restituisce un errore e il tipo di evento Page Bottom potrebbe non comportarsi come previsto.
