---
title: Riferimento per il test di avviso
description: Scopri in che modo la funzione di revisione esegue il test degli avvisi in Adobe Experience Platform Debugger.
exl-id: ac6f8675-6c34-48b4-b5dd-48e92af217fd
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 37%

---

# Riferimento per la prova di avviso

Questo riferimento fornisce ulteriori informazioni su come la funzione di auditor in Adobe Experience Platform Debugger esegue i test degli avvisi.

>[!NOTE]
>
>Per ulteriori informazioni sui test di auditor in Platform Debugger, consulta la sezione [panoramica delle funzioni di auditor](./overview.md).

Gli avvisi mostrano problemi di cui dovresti essere a conoscenza, ma che non influiscono sul punteggio. Si tratta di raccomandazioni sulle best practice che, in alcuni casi, potrebbero non essere applicabili all’implementazione.

| Test | Peso | Criteri | Consiglio |
| --- | --- | --- | --- |
| Advertising Cloud - Correzione del tag di conversione implementato | 0 | Verifica se viene utilizzato il tag di conversione corretto.<br><br>**Avviso**: L’utilizzo di tag di conversione TubeMogul obsoleti può causare la perdita di dati. | Aggiorna i pixel di conversione ai nuovi tag di conversione di sola immagine di Advertising Cloud. Questa operazione può essere realizzata con la massima facilità [Estensione tag Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - Correzione del tag JS utilizzato | 0 | Advertising Cloud deve utilizzare i tag JavaScript più recenti. | Aggiorna JavaScript di Advertising Cloud alla versione più recente. L’utilizzo di versioni JavaScript obsolete può comportare la perdita di funzionalità. Questa operazione può essere realizzata più facilmente utilizzando [Estensione tag Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - Tag di sola immagine | 0 | Il formato pixel immagine di Advertising Cloud deve corrispondere a uno dei seguenti formati consigliati: <ul><li>`http(s)://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul> | Aggiorna i pixel di Advertising Cloud ai nuovi tag di sola immagine di Advertising Cloud, in modo da poter sfruttare appieno la funzionalità di Advertising Cloud. Questa operazione può essere realizzata con la massima facilità [Estensione tag Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - Sincronizzazione DSP dei pixel del segmento abilitata | 0 | Verifica se il pixel del segmento TubeMogul contiene un’impostazione di sincronizzazione DSP e consiglia di aggiungere l’impostazione al pixel. L&#39;impostazione di sincronizzazione DSP è determinata dall&#39;utilizzo di un parametro di stringa query. Per riepilogare: <ul><li>SE il tag viene attivato su uno dei seguenti elementi:<ul><li>`https://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul></li><li>E il tag contiene il parametro URL `sid=`</li><li>QUINDI controlla se il parametro URL `cs=0` o `cs=1` esiste e, in caso contrario, consiglia `cs=1` devono essere aggiunti a tali pixel in modo che le percentuali di corrispondenza del pubblico possano migliorare.</li></ul> | Aggiungi il parametro URL `cs=1` ai pixel di Advertising Cloud in modo che possa verificarsi la sincronizzazione DSP, che aumenta le percentuali di corrispondenza del pubblico. Questa operazione può essere realizzata con la massima facilità [Estensione tag Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Servizio Experience Cloud ID - Utilizzo di un solo AdobeOrg | 0 | In una normale implementazione ECID, deve essere utilizzato un singolo AdobeOrg. | Verifica l’esistenza di più ID AdobeOrg per questa implementazione. <br><br>[Informazioni aggiuntive](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html) |
| Launch - `pageBottom` posizionamento di callback | 0 | La `_satellite.pageBottom()` per il corretto funzionamento dei tag, la funzione deve essere presente. Aggiungi lo script in linea immediatamente prima della chiusura `</body>` per garantire la funzionalità DTM corretta. Nota: è consigliabile che il tag sia l’ultimo tag presente in `<body>`. Se si trova all&#39;interno del `<body>` tag, può funzionare, ma non è ugualmente consigliabile in quanto potrebbe generare malfunzionamenti o risultati indesiderati. | Aggiungi lo script in linea immediatamente prima della chiusura `</body>` per garantire la funzionalità DTM corretta. <br><br>[Informazioni aggiuntive](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch - Self-Hosted | 0 | La libreria di tag è ospitata nell’istanza Akamai di Adobe all’indirizzo `assets.adobedtm.com`. L’hosting autonomo è l’approccio consigliato per il caricamento dei tag in quanto fornisce un maggiore controllo delle prestazioni del sito web tramite il controllo della cache, riducendo le dipendenze degli script di terze parti e un maggiore controllo del processo di pubblicazione. Le librerie di tag possono essere ospitate e gestite tramite l’hosting web o CDN. | Passa a un hosting autonomo è l’approccio per caricare i tag su una pagina. Sebbene l’hosting di tramite la rete CDN Akamai funzioni nella maggior parte dei casi, l’hosting autonomo migliora le prestazioni della pagina. <br><br>Informazioni aggiuntive:<ul><li>[Guida rapida ai tag](../../tags/ui/client-side/asynchronous-deployment.md)</li><li>[Distribuzione asincrona](../../tags/ui/client-side/asynchronous-deployment.md)</li></ul> |
| Launch - Deve essere distribuito in modo asincrono | 0 | I tag devono essere distribuiti in modo asincrono per ottenere prestazioni ottimali. | Includi il `async` nello script in linea per garantire la funzionalità tag corretta <br><br>[Informazioni aggiuntive](../../tags/ui/client-side/asynchronous-deployment.md) |
| Target - Contenuto in `mboxDefault` | 0 | Il contenuto dovrebbe esistere in `mboxDefault` quando utilizzi `at.js`. | Verifica che il contenuto sia disponibile. <br><br>[Informazioni aggiuntive](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style=&quot;table-layout:auto&quot;}
