---
title: Panoramica dell’estensione Adobe Medium Analytics (3.x SDK) for Audio and Video
description: Scopri l’estensione tag Adobe Media Analytics (3.x SDK) for Audio and Video in Adobe Experience Platform.
exl-id: 7289d57d-7e7f-4832-9469-3b5a62183a32
source-git-commit: e21ed1e9fd0c2678551cfc664b611076c198a157
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 94%

---

# Panoramica di Adobe Media Analytics (3.x SDK) per estensioni audio e video

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Utilizza questa documentazione per maggiori informazioni sull’installazione, la configurazione e l’implementazione dell’estensione Adobe Media Analytics (3.x SDK) for Audio and Video (estensione Media Analytics). Sono incluse le opzioni disponibili quando si utilizza questa estensione per generare una regola, insieme a esempi e collegamenti a campioni.

L’estensione Media Analytics (MA) aggiunge l’SDK principale JavaScript Media SDK (Media 3.x SDK). Questa estensione fornisce la funzionalità necessaria per aggiungere l’istanza di tracciamento `Media` a un sito o a un progetto abilitato per i tag. L’estensione MA richiede due estensioni aggiuntive:

* [Estensione Analytics](../analytics/overview.md)
* [Estensione Experience Cloud ID](../id-service/overview.md)

>[!IMPORTANT]
>
>Questa estensione viene distribuita con Media 3.x SDK, che non è compatibile con le versioni precedenti quali Media 2.x SDK. Poiché 2.x è stato dichiarato obsoleto, effettua l’aggiornamento alla versione 3.x.

Dopo aver incluso tutte e tre le estensioni precedentemente menzionate nel progetto abilitato per i tag, puoi procedere in uno dei due modi seguenti:

* Utilizza le API `Media` dalla Web app
* Includi, o genera, un&#39;estensione specifica per il lettore che mappa eventi specifici del lettore multimediale nelle API sull&#39;istanza tracker `Media`. Questa istanza viene esposta tramite l&#39;estensione MA.

## Installa e configura l&#39;estensione MA

* **Installazione:** per installare l’estensione MA, apri la proprietà dell’estensione, seleziona **[!UICONTROL Estensioni > Catalogo]**, passa il puntatore del mouse sull’estensione **[!UICONTROL Adobe Media Analytics (3.x SDK) for Audio and Video]**, quindi seleziona **[!UICONTROL Installa]**.

* **Configurazione:** per configurare l’estensione MA, apri la scheda [!UICONTROL Estensioni], passa il puntatore del mouse sull’estensione, quindi fai clic su **[!UICONTROL Configura]**:

![Configurazione dell&#39;estensione MA](../../../images/ext-ma-config.png)

### Opzioni di configurazione:

| Opzione | Descrizione |
| :--- | :--- |
| Collection API Server | Definisce il server API di Media Collection (per ottenere questo server, contatta il rappresentante Adobe) |
| Application Version | Versione dell&#39;app/SDK del lettore multimediale |
| Player Name | Nome del lettore multimediale in uso (ad esempio &quot;AVPlayer&quot;, &quot;HTML5 Player&quot;, &quot;My Custom VideoPlayer&quot;) |
| Channel | Proprietà nome canale |
| Debug Logging | Attiva o disattiva la registrazione |
| Enable SSL | Attiva o disattiva l&#39;invio di ping su HTTPS |
| Export APIs to Window Object | Attivare o disattivare l&#39;esportazione delle API di Media Analytics all&#39;ambito globale |
| Variable Name | Una variabile utilizzata per esportare le API di Media Analytics sotto l&#39;oggetto `window` |

**Promemoria:** l&#39;estensione MA richiede le estensioni [Analytics](../analytics/overview.md) ed [Experience Cloud ID](../id-service/overview.md). Devi aggiungere queste estensioni alla proprietà dell&#39;estensione e configurarle.

## Utilizzo dell&#39;estensione MA

### Utilizzo da una pagina web/JS-app

L’estensione MA esporta le API Media nell’oggetto finestra globale abilitando l’impostazione “Export APIs to Window Objects” nella pagina [!UICONTROL Configurazione]. Esporta le API sotto il nome della variabile configurato. Ad esempio, se il nome della variabile è configurato come `ADB` allora è possibile accedere alle API di Media tramite `window.ADB.Media`.

>[!IMPORTANT]
>
>L’estensione MA esporta le API solo se `window["CONFIGURED_VARIABLE_NAME"]` non è definita e non sostituisce le variabili esistenti.

1. **API di Media:** `window["CONFIGURED_VARIABLE_NAME"].Media`

   Questo espone tutte le API e le costanti di Media SDK: [https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)

1. **Crea un’istanza di tracciamento Media:** `window["CONFIGURED_VARIABLE_NAME"].Media.getInstance`

   **Valore restituito:** un’istanza di tracciamento `Media` per tenere traccia di una sessione multimediale.

   ```javascript
   var Media = window["CONFIGURED_VARIABLE_NAME"].Media;
   
   var tracker = Media.getInstance();
   ```

1. Utilizzando l’istanza di tracciamento Media, segui la [documentazione API JS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) per implementare il tracciamento dei contenuti multimediali.

Ottieni il sample player qui: [MA Sample Player](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x). Il sample player funge da riferimento per mostrare come utilizzare l’estensione MA per supportare Media Analytics direttamente da una Web app.


### Utilizzo da altre estensioni

L’estensione MA espone `media` come modulo condiviso ad altre estensioni. (Per ulteriori informazioni sui moduli condivisi, consulta la [documentazione Moduli condivisi](../../../extension-dev/web/shared.md).)

>[!IMPORTANT]
>
>Puoi accedere ai moduli condivisi solo da altre estensioni. In altre parole, una pagina web/app JavaScript non può accedere ai moduli condivisi, né utilizzare `turbine` (vedi il codice di esempio di seguito) al di fuori di un’estensione.

1. **API di Media:** `media` modulo condiviso

   Questo espone tutte le API e le costanti di Media SDK: [https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)

1. Crea l’istanza di tracciamento Media come segue:

   **Valore restituito:** un’istanza di tracciamento `Media` per tenere traccia di una sessione multimediale.

   ```javascript
   var Media =
     turbine.getSharedModule('adobe-media-analytics', 'media');
   
   var tracker = Media.getInstance();
   ```

1. Utilizzando l’istanza di tracciamento Media, segui la [documentazione API JS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) per implementare il tracciamento dei contenuti multimediali.

>[!NOTE]
>
>**Test:** per questa versione, per testare l’estensione devi caricarla in [Platform](../../../extension-dev/submit/upload-and-test.md), dove puoi accedere a tutte le estensioni dipendenti.
