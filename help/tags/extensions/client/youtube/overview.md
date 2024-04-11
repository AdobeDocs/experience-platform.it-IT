---
title: Panoramica dell’estensione di tracciamento di video YouTube
description: Scopri l’estensione tag per il tracciamento di video YouTube in Adobe Experience Platform.
exl-id: 703f7b04-f72f-415f-80d6-45583fa661bc
source-git-commit: 627835011784ffca8487d446c04c6948dfff059d
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 81%

---

# Panoramica dell’estensione di tracciamento di video YouTube

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

**Prerequisiti**

Per ogni proprietà tag in Adobe Experience Platform, le seguenti estensioni devono essere installate e configurate dalla schermata Estensioni:

* Adobe Analytics
* Servizio ID visitatore di Experience Cloud
* Estensione core

Utilizza il [&quot;Incorporare un lettore utilizzando un \&lt;iframe> tag&quot;](https://developers.google.com/youtube/player_parameters#Manual_IFrame_Embeds) frammento di codice dai documenti per sviluppatori di Google nel HTML di ogni pagina web in cui deve essere eseguito il rendering di un lettore video.

Con la versione 2.0.1 di questa estensione è possibile incorporare uno o più video YouTube in una singola pagina web inserendo un attributo `id` con valore univoco nel tag di script iframe e aggiungendo `enablejsapi=1` e `rel=0` alla fine del valore dell’attributo `src`, se non già incluso. Esempio:

`<iframe id="player1" width="560" height="315" src="https://www.youtube.com/embed/xpatB77BzYE?enablejsapi=1" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>`

Questa estensione è progettata anche per verificare dinamicamente la presenza di un valore di attributo ID univoco, come `player1`, a prescindere dalla presenza di parametri di stringhe di query `enablejsapi` e `rel` e dalla corretteza dei rispettivi valori previsti. Di conseguenza, il tag di script di YouTube può essere aggiunto a una pagina web con o senza l’attributo `id` e a prescindere dall’inclusione dei parametri della stringa di query `enablejsapi` e `rel`.

>[!NOTE]
>
>Sulle pagine con più video, ricorda che ogni video utilizza la stessa configurazione impostata nella regola del tag in esecuzione sulla pagina. Ad esempio, se crei una regola con un evento che si attiva quando il video è completato al 50%, ogni video della pagina attiverà la regola al punto di cue del 50%.

Per riscrivere l’iFrame, l’estensione si basa sulla seguente logica:

```javascript
document.onreadystatechange = function () {
 if (document.readyState === 'complete') {
```

Di conseguenza, si verificherà un leggero sfarfallio dopo il caricamento della pagina. Si tratta di un comportamento previsto.

## Elementi dati

All’interno dell’estensione sono disponibili sei elementi dati, nessuno dei quali richiede la configurazione.

* **Posizione testina di riproduzione:** registra la posizione in secondi della testina di riproduzione sulla timeline del video, quando viene richiamato all’interno di una regola di tag.
* **ID video:** specifica l’ID YouTube associato al video.
* **Nome video:** specifica il nome descrittivo del video.
* **URL video:** restituisce l’URL YouTube.com del video attualmente caricato/riprodotto.
* **Durata video:** registra la durata totale in secondi dei contenuti video.
* **Versione estensione:** questo elemento dati registra la versione dell’estensione di tracciamento di YouTube, ad esempio “Video Tracking_YouTube_2.0.0”.

## Eventi

Nell’estensione sono disponibili otto eventi; solo Tracciamento punto di cue personalizzato richiede la configurazione.

* **Disponibilità video:** si attiva quando il video viene codificato ed è pronto per essere riprodotto.
* **Inizio video:** si attiva quando il video viene avviato per la prima volta e quando `player.getCurrentTime() === 0`
* **Ripetizione video:** si attiva quando il video viene codificato e riprodotto dopo l’avvio iniziale. Questo trigger si attiva a ogni ripetizione.
* **Pausa video:** si attiva quando il video viene messo in pausa.
* **Ripresa video:** si attiva quando si riprende la riproduzione del video e quando `player.getCurrentTime() !== 0`
* **Tracciamento punto di cue personalizzato:** questo evento viene attivato quando il video raggiunge la percentuale di soglia video specificata. Ad esempio, se per un video di 60 secondi viene specificato un punto di cue al 50%, l’evento si attiva quando la posizione della testina di riproduzione arriva a 30 secondi. Il tracciamento del punto di cue si applica sia alla riproduzione iniziale che alla ripetizione. Se l’utente fa scorrere la testina di riproduzione passando per il punto di cue, l’evento non si attiva. Gli eventi per un punto di cue vengono attivati solo quando l’indicatore di riproduzione attraversa la posizione calcolata sulla timeline mentre il lettore video è in fase di riproduzione.
* **Buffer video:** viene attivato quando il lettore scarica una determinata quantità di dati prima che di iniziare a riprodurre il video.
* **Video terminato:** si attiva quando un video viene completato del tutto.

## Utilizzo

È possibile impostare una regola di tag per ogni evento video (i sette eventi elencati sopra). Crea una regola di tag specifica per ogni evento di cui desideri tenere traccia. Se non desideri tenere traccia di un evento, ometti semplicemente di creare una regola per esso.

Le regole prevedono tre azioni:

* **Imposta variabili:** imposta le variabili Adobe Analytics (mappa tutti o alcuni elementi di dati inclusi).
* **Invia beacon:** Invia il beacon di Adobe Analytics come chiamata di tracciamento dei collegamenti personalizzata e specifica un valore &quot;Nome collegamento&quot;.
* **Cancella variabili:** cancella le variabili Adobe Analytics.

## Esempio di regola tag per “Video Start”

Devono essere inclusi i seguenti oggetti di estensione video.

* **Eventi**: &quot;Video Start&quot; (questo evento causa l’attivazione della regola quando il visitatore avvia un video YouTube).

* **Condizione**: nessuna

* **Azioni**: utilizza **Estensione Analytics** per mappare l’azione &quot;Imposta variabili&quot;:

   * l’evento per Inizio video;
   * una prop/eVar per l’elemento dati Durata video;
   * una prop/eVar per l’elemento dati ID video;
   * un prop/eVar per l’elemento dati Nome video;
   * una prop/eVar per l’elemento dati URL video.

  Quindi, includi l’azione &quot;Invia beacon&quot; (`s.tl`) con il nome del collegamento &quot;video start&quot;, seguito dall&#39;azione &quot;Cancella variabili&quot;.

>[!TIP]
> 
>Per le implementazioni in cui non è possibile utilizzare più eVar o proprietà per ciascun elemento video, i valori degli elementi dati possono essere concatenati in Platform, analizzati nei rapporti di classificazione utilizzando lo strumento Generatore regole di classificazione, come spiegato in [https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html?lang=it](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html?lang=it), e quindi applicati come segmento in Analysis Workspace.

Per concatenare i valori delle informazioni video, crea un nuovo elemento dati denominato &quot;Video Meta Data&quot; e programmalo per richiamare e assemblare tutti gli elementi dati video (elencati sopra). Ad esempio:

```javascript
var r = [];

r.push('YouTube'); //Player Name
r.push(_satellite.getVar('Video ID'));
r.push(_satellite.getVar('Video Name'));
r.push(_satellite.getVar('Video Duration'));
r.push(_satellite.getVar('Extension Version'));

return r.join('|');
```

Per ulteriori informazioni su come creare e sfruttare in modo efficace gli elementi dati in Platform, leggi [elementi dati](../../../ui/managing-resources/data-elements.md) documentazione.
