---
title: Panoramica dell’estensione di tracciamento di video YouTube
description: Scopri l’estensione tag di tracciamento video di YouTube in Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 49%

---

# Panoramica dell’estensione di tracciamento di video YouTube

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

**Prerequisiti**

Ogni proprietà tag in Adobe Experience Platform richiede che le seguenti estensioni siano installate e configurate dalla schermata Estensioni:

* Adobe Analytics
* Servizio ID visitatore di Experience Cloud
* Estensione core

Utilizza lo snippet di codice [&quot;Incorpora un lettore utilizzando un tag \&lt;iframe\>&quot;](https://developers.google.com/youtube/player_parameters#Manual_IFrame_Embeds) dei documenti per sviluppatori di Google nell&#39;HTML di ogni pagina Web in cui deve essere eseguito il rendering di un lettore video.

Questa estensione, versione 2.0.1, supporta l’incorporazione di uno o più video YouTube in una singola pagina web inserendo un attributo `id` con un valore univoco nel tag script iframe e aggiungendo `enablejsapi=1` e `rel=0` alla fine del valore dell’attributo `src`, se non è già incluso. Esempio:

`<iframe id="player1" width="560" height="315" src="https://www.youtube.com/embed/xpatB77BzYE?enablejsapi=1" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>`

Questa estensione è progettata anche per verificare dinamicamente la presenza di un valore di attributo ID univoco, come `player1`, indipendentemente dall&#39;esistenza dei parametri delle stringhe query `enablejsapi` e `rel` e dalla correttezza dei valori previsti. Di conseguenza, il tag di script di YouTube può essere aggiunto a una pagina web con o senza l’attributo `id` e a prescindere dall’inclusione dei parametri della stringa di query `enablejsapi` e `rel`.

>[!NOTE]
>
>Sulle pagine con più di un video, ogni video utilizza lo stesso set di configurazione nella regola di tag in esecuzione sulla pagina. Ad esempio, se crei una regola con un evento che si attiva quando il video è completato al 50%, ogni video della pagina attiverà la regola al punto di cue del 50%.

Per riscrivere l’iFrame, l’estensione si basa sulla seguente logica:

```javascript
document.onreadystatechange = function () {
 if (document.readyState === 'complete') {
```

Pertanto, si verifica un leggero sfarfallio dopo il caricamento della pagina. Si tratta di un comportamento previsto.

## Elementi dati

All’interno dell’estensione sono disponibili sei elementi dati, nessuno dei quali richiede la configurazione.

* **Playhead Position:** registra la posizione in secondi della testina di riproduzione sulla timeline del video, quando viene richiamata all’interno di una regola di tag.
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
* **Tracciamento punto di cue personalizzato:** questo evento viene attivato quando il video raggiunge la percentuale di soglia video specificata. Ad esempio, se un video dura 60 secondi e il punto di cue specificato è 50%, l&#39;evento si attiva quando la posizione dell&#39;indicatore di riproduzione è uguale a 30 secondi. Il tracciamento del punto di cue si applica sia alla riproduzione iniziale che alla ripetizione. Tieni presente che se l’utente cerca in un punto di cue, l’evento non si attiva. Gli eventi dei punti di cue si attivano solo quando l&#39;indicatore di riproduzione attraversa la posizione del punto di cue calcolato sulla timeline e il lettore video è in riproduzione.
* **Buffer video:** viene attivato quando il lettore scarica una determinata quantità di dati prima che di iniziare a riprodurre il video.
* **Video terminato:** si attiva quando un video viene completato del tutto.

## Utilizzo

È possibile impostare una regola di tag per ogni evento video (i sette eventi elencati sopra). Crea una regola di tag specifica per ogni evento di cui desideri tenere traccia. Se non desideri tenere traccia di un evento, ometti semplicemente di creare una regola per esso.

Le regole prevedono tre azioni:

* **Imposta variabili:** imposta le variabili Adobe Analytics (mappa tutti o alcuni elementi di dati inclusi).
* **Invia beacon:** invia il beacon Adobe Analytics come chiamata di tracciamento dei collegamenti personalizzata e specifica un valore “Nome collegamento”.
* **Cancella variabili:** cancella le variabili Adobe Analytics.

## Esempio di regola tag per &quot;Video Start&quot;

Devono essere inclusi i seguenti oggetti estensione video.

* **Eventi**: &quot;Video Start&quot; (questo evento causa l’attivazione della regola quando il visitatore avvia la riproduzione di un video YouTube).

* **Condizione**: nessuna

* **Azioni**: Utilizza l&#39;azione **Estensione Analytics** per impostare le variabili, per mappare:

   * l’evento per Inizio video;
   * una prop/eVar per l’elemento dati Durata video;
   * una prop/eVar per l’elemento dati ID video;
   * un prop/eVar per l’elemento dati Nome video;
   * una prop/eVar per l’elemento dati URL video.

   Quindi, includi l’azione &quot;Invia beacon&quot; (`s.tl`) con nome di collegamento &quot;avvio video&quot;, seguita da un’azione &quot;Cancella variabili&quot;.

>[!TIP]
> 
>Per le implementazioni in cui non è possibile utilizzare più eVar o proprietà per ciascun elemento video, i valori degli elementi dati possono essere concatenati in Platform, analizzati nei rapporti di classificazione utilizzando lo strumento per la generazione di regole di classificazione, come spiegato in [https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html?lang=it) e quindi applicati come segmento in Analysis Workspace.

Per concatenare i valori delle informazioni video, crea un nuovo elemento di dati denominato “Video Meta Data” e programmalo per richiamare e assemblare tutti gli elementi dati video (elencati sopra). Esempio:

```javascript
var r = ””;

r.push('YouTube'); //Player Name
r.push(_satellite.getVar('Video ID'));
r.push(_satellite.getVar('Video Name'));
r.push(_satellite.getVar('Video Duration'));
r.push(_satellite.getVar('Extension Version'));

return r.join('|');
```
