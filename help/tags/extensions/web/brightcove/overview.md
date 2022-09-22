---
title: Panoramica dell’estensione per il tracciamento di video BrightCove
description: Scopri l’estensione tag per il tracciamento di video BrightCove in Adobe Experience Platform.
exl-id: d27eff21-2abf-4495-8382-08cab32742e0
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 98%

---

# Panoramica dell’estensione per il tracciamento di video BrightCove

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

## Prerequisiti

Per ogni proprietà in Adobe Experience Platform è necessario installare e configurare le seguenti estensioni nella schermata Extension:

* Adobe Analytics
* Servizio ID visitatore di Experience Cloud
* Estensioni core installate

Utilizza lo snippet di codice “In-Page embed code (Advanced)” nell’HTML di ogni pagina web in cui deve essere eseguito il rendering di un lettore video. Lo snippet HTML “In-Page Embed code (Advanced)” si trova nella [documentazione di Brightcove](https://studio.support.brightcove.com/publish/choosing-correct-embed-code.html#inpage). Il seguente collegamento fornisce ulteriori informazioni su [come generare codice da incorporare sia per i lettori video in anteprima che per quelli pubblicati](https://studio.support.brightcove.com/players/generating-player-embed-code.html).

Questa versione dell’estensione 1.1.0 consente di incorporare più video BrightCove in una singola pagina web. Se all’interno dei tag di incorporamento avanzati sono presenti più proprietà `id`, accertati che ciascuna di esse disponga di valori univoci. Ad esempio, `player1`, `player2` e così via.

>[!NOTE]
>
>Sulle pagine con più video, tieni presente che ogni video utilizza lo stesso set di configurazione nella regola tag in esecuzione sulla pagina. Ad esempio, se crei una regola con un evento che si attiva quando il video è completato al 50%, ogni video della pagina attiverà la regola al punto di cue del 50%.

Se la pagina web che utilizza questa estensione che interagisce con il video prima che lo script rilevante sia stato completamente caricato, è possibile eseguire due azioni per risolvere il problema. In primo luogo, la libreria di tag può essere caricata in modo sincrono e, in secondo luogo, si può inserire l’elemento `<script type="text/javascript">\_satellite.pageBottom();\</script\>` prima che il video venga incorporato nella pagina.

Per ulteriori informazioni sui metodi dei componenti e gli eventi utilizzati in questa estensione, consulta la [documentazione dell’API di BrightCove](https://docs.brightcove.com/brightcove-player/1.x/Player.html#vjsplayer).

## Elementi dati

Nell’estensione sono disponibili sette elementi dati, nessuno dei quali richiede la configurazione.

* **Playhead Position:** quando questo elemento dati viene chiamato all’interno di una regola di tag, registra in secondi la posizione della testina di riproduzione sulla timeline del video.
* **Video Account ID:** questo elemento dati registra l’ID dell’account BrightCove che ha pubblicato il video.
* **Video Duration:** questo elemento dati registra la durata totale in secondi dei contenuti video. Inoltre, è possibile creare una metrica calcolata all’interno di Analytics per convertire il numero in secondi, minuti o ore.
* **Video Ad Support:** questo elemento dati specifica se gli annunci sono supportati o meno all’interno del video.
* **Video ID:** questo elemento dati specifica l’ID BrightCove associato al video.
* **Video Name:** questo elemento dati specifica il nome descrittivo del video.
* **Video Tags:** questo elemento dati specifica gli script associati al video.

## Eventi

Nell’estensione sono disponibili sette eventi, solo Custom Cue Point Tracking richiede la configurazione.

* **Custom Cue Point Tracking:** questo evento viene attivato quando il video raggiunge la percentuale di soglia video specificata. Ad esempio, se un video dura 60 secondi e il punto di cue specificato è 50%, l’evento si attiva alla soglia dei 30 secondi.

>[!NOTE]
>
>Ricorda che l’evento viene attivato ogni volta che viene raggiunto il punto di cue. Ad esempio, se l’utente raggiunge la soglia del 50%, cerca il video prima del 50% e poi raggiunge di nuovo il 50%, il trigger si riattiva.

* **Video Completed:** questo evento viene attivato al completamento di un video.
* **Video Loaded Metadata:** questo evento viene attivato quando il lettore riceve le informazioni iniziali sulla durata e sulla dimensione.
* **Video Pause:** questo evento viene attivato quando il video viene messo in pausa.
* **Video Resume:** questo evento viene attivato quando il video viene riavviato dopo essere stato messo in pausa.
* **Video Screen Change:** l’evento viene attivato quando il video passa alla modalità schermo intero o ne esce.
* **Video Start:** questo evento viene attivato quando il contenuto video viene avviato per la prima volta.

## Utilizzo

È possibile impostare una regola di tag per ogni evento video (i sette eventi elencati sopra). Crea una regola di tag specifica per ogni evento di cui desideri tenere traccia. Se non desideri tenere traccia di un evento, ometti semplicemente di creare una regola per esso.

Le regole prevedono tre azioni:

1. Impostare le variabili Adobe Analytics. (Ovvero creare elementi dati per tutti o alcuni degli elementi dati elencati sopra.)
1. Inviare il beacon di Adobe Analytics.
1. Cancellare le variabili Adobe Analytics.

## Esempio di regola tag per “Video Start”

Devono essere inclusi i seguenti oggetti di estensione video:

* **Eventi**

   1. “Video Start”: questo evento causa l’attivazione della regola quando il visitatore avvia la riproduzione di un video BrightCove.

* **Condizione**

   1. Nessuna

* **Azioni**

   1. In un’azione “Set variables” di Analytics, imposta:

      * L’evento per **Video Start** (ad esempio: event17)
      * Una prop/eVar per l’elemento dati **Video Name** (ad esempio: eVar10)
      * Una prop/eVar per l’elemento dati **Video Duration** (ad esempio: eVar11)
      * Una prop/eVar per l’elemento dati **Current Video Place** (ad esempio: eVar12)
   1. L’azione “Send beacon” di Analytics (`s.tl`)
   1. L’azione “Clear variables” di Analytics


>[!TIP]
>
>Per coloro che non desiderano eseguire il provisioning di più eVar o proprietà per ciascun elemento video, esiste un metodo alternativo. I valori degli elementi dati possono essere concatenati all’interno dell’interfaccia utente di Data Collection. Vengono quindi analizzate nei rapporti di classificazione utilizzando lo strumento per la generazione di regole di classificazione. Per ulteriori informazioni, consulta la documentazione dello strumento [Classification Rule Builder Tool](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html?lang=it). Infine, vengono applicati come segmento in Analysis Workspace.
>
>A tale scopo, crea un nuovo elemento dati denominato ad esempio “Video MetaData” e programmalo per inserire tutti gli elementi dati video (elencati sopra) e concatenarli insieme.

```javascript
var r = [];

r.push( \_satellite.getVar( &#39;Video ID&#39; ) );

r.push( \_satellite.getVar( &#39;Video Name&#39; ) );

r.push( \_satellite.getVar( &#39;Video Duraction&#39; ) );


return r.join(&#39;|&#39;);
```
