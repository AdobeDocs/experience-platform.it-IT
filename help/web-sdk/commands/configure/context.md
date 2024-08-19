---
title: contesto
description: Raccogli automaticamente i dati relativi a dispositivo, ambiente o posizione.
exl-id: 911cabec-2afb-4216-b413-80533f826b0e
source-git-commit: 89dfe037e28bae51e335dc67185afa42b2c418e3
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 7%

---

# `context`

La proprietà `context` è un array di stringhe che determina ciò che l&#39;SDK Web può raccogliere automaticamente. Anche se questi dati possono fornire un grande valore, omettere alcuni di questi dati può essere utile in modo da poter rispettare l’informativa sulla privacy della tua organizzazione.

## Parole chiave di contesto ed elementi XDM

Se includi una determinata parola chiave di contesto, Web SDK compila automaticamente tutti gli elementi XDM associati. Se si desidera omettere un elemento XDM specifico consentendo ad altri elementi, è possibile cancellare i valori utilizzando [`onBeforeEventSend`](onbeforeeventsend.md). Se invii più eventi a una pagina, Web SDK include questi campi a ogni chiamata `SendEvent`.

### Web

La parola chiave `"web"` raccoglie informazioni sulla pagina corrente.

| Dimensione | Descrizione | Percorso XDM | Esempio di valore |
| --- | --- | --- | --- |
| URL della pagina | URL della pagina corrente. | `xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| URL referrer | URL della pagina precedente visitata. | `xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}

### Dispositivo

La parola chiave `"device"` raccoglie informazioni sul dispositivo dell&#39;utente.

| Dimensione | Descrizione | Percorso XDM | Esempio di valore |
| --- | --- | --- | --- |
| Altezza schermo | Altezza dello schermo in pixel. | `xdm.device.screenHeight` | `900` |
| Larghezza schermo | Larghezza dello schermo in pixel. | `xdm.device.screenWidth` | `1440` |
| Orientamento schermo | Orientamento dello schermo. | `xdm.device.screenOrientation` | `landscape` o `portrait` |

{style="table-layout:auto"}

### Ambiente

La parola chiave `"environment"` raccoglie informazioni sul browser dell&#39;utente.

| Dimensione | Descrizione | Percorso XDM | Esempio di valore |
| --- | --- | --- | --- |
| Tipo di ambiente | Il tipo di ambiente attraverso il quale è emersa l’esperienza. Web SDK imposta sempre questo campo su `browser`. | `xdm.environment.type` | `browser` |
| Altezza del riquadro di visualizzazione | Altezza in pixel dell&#39;area contenuto del browser. | `xdm.environment.browserDetails.viewportHeight` | `679` |
| Larghezza del riquadro di visualizzazione | Larghezza in pixel dell&#39;area contenuto del browser. | `xdm.environment.browserDetails.viewportWidth` | `642` |

{style="table-layout:auto"}

### Contesto del luogo

La parola chiave `"placeContext"` raccoglie informazioni sulla posizione dell&#39;utente.

| Dimensione | Descrizione | Percorso XDM | Esempio di valore |
| --- | --- | --- | --- |
| Ora locale | Timestamp locale per l&#39;utente finale in formato [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) esteso semplificato. | `xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| Offset fuso orario locale | Il numero di minuti di offset dell&#39;utente da GMT. | `xdm.placeContext.localTimezoneOffset` | `360` |
| Codice paese | Il codice del paese dell’utente finale. | `xdm.placeContext.geo.countryCode` | `US` |
| Provincia di Stato | Il codice della provincia dello stato dell&#39;utente finale. | `xdm.placeContext.geo.stateProvince` | `CA` |
| Latitudine | La latitudine della posizione dell&#39;utente finale. | `xdm.placeContext.geo._schema.latitude` | `37.3307447` |
| Longitudine | La longitudine della posizione dell&#39;utente finale. | `xdm.placeContext.geo._schema.longitude` | `-121.8945965` |

{style="table-layout:auto"}


### Timestamp

La parola chiave `timestamp` raccoglie informazioni sulla marca temporale dell&#39;evento. Questa parte del contesto non può essere rimossa.

| Dimensione | Descrizione | Percorso XDM | Esempio di valore |
| --- | --- | --- | --- |
| Timestamp dell’evento | Timestamp UTC per l&#39;utente finale in formato [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) esteso semplificato. | `xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

{style="table-layout:auto"}

### Dettagli di implementazione

La parola chiave `implementationDetails` raccoglie informazioni sulla versione SDK utilizzata per raccogliere l&#39;evento.

| Dimensione | Descrizione | Percorso XDM | Esempio di valore |
| --- | --- | --- | --- |
| Nome | Identificatore del kit di sviluppo software (SDK). Questo campo utilizza un URI per migliorare l’univocità tra gli identificatori forniti da diverse librerie software. | `xdm.implementationDetails.name` | Quando si utilizza la libreria autonoma, il valore è `https://ns.adobe.com/experience/alloy`. Quando la libreria viene utilizzata come parte dell&#39;estensione tag, il valore è `https://ns.adobe.com/experience/alloy+reactor`. |
| Versione | Versione del kit di sviluppo software (SDK). | `xdm.implementationDetails.version` | Quando si utilizza la libreria indipendente, il valore è la versione della libreria. Quando la libreria viene utilizzata come parte dell&#39;estensione tag, il valore è la versione della libreria e la versione dell&#39;estensione tag unita con un `+`. Ad esempio, se la versione della libreria è `2.1.0` e la versione dell&#39;estensione tag è `2.1.3`, il valore sarà `2.1.0+2.1.3`. |
| Ambiente | Ambiente in cui sono stati raccolti i dati. Questo è sempre impostato su `browser`. | `xdm.implementationDetails.environment` | `browser` |


### Hint client ad alta entropia {#high-entropy-client-hints}

>[!TIP]
>
>Per informazioni dettagliate su come configurarli, consulta la documentazione su [user agent client hints](../../use-cases/client-hints.md).

La parola chiave `"highEntropyUserAgentHints"` raccoglie informazioni dettagliate sul dispositivo dell&#39;utente. Questi dati sono inclusi nell’intestazione HTTP della richiesta inviata all’Adobe. Una volta arrivati i dati all’interno della rete Edge, l’oggetto XDM compila il rispettivo percorso XDM. Se imposti il rispettivo percorso XDM nella chiamata `sendEvent`, ha la precedenza sul valore dell&#39;intestazione HTTP.

Se si utilizzano le ricerche dei dispositivi durante [la configurazione dello stream di dati](/help/datastreams/configure.md), è possibile cancellare i dati in favore dei valori di ricerca dei dispositivi. Alcuni campi degli hint client e dei campi di ricerca del dispositivo non possono esistere nello stesso hit.

| Proprietà | Descrizione | Intestazione HTTP | Percorso XDM | Esempio |
| --- | --- | --- | --- | --- |
| Versione del sistema operativo | Versione del sistema operativo. | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | `10.15.7` |
| Architettura | Architettura CPU sottostante. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | `x86` |
| Modello dispositivo | Nome del dispositivo utilizzato. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | `Intel Mac OS X 10_15_7` |
| Amarezza | Il numero di bit supportati dall&#39;architettura CPU sottostante. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | `64` |
| Fornitore browser | Azienda che ha creato il browser. Anche l&#39;hint a bassa entropia `Sec-CH-UA` raccoglie questo elemento. | `Sec-CH-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.vendor` | `Google` |
| Nome browser | Browser utilizzato. Anche l&#39;hint a bassa entropia `Sec-CH-UA` raccoglie questo elemento. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | `Chrome` |
| Versione browser | Versione significativa del browser. Anche l&#39;hint a bassa entropia `Sec-CH-UA` raccoglie questo elemento. La versione esatta del browser non viene raccolta automaticamente. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | `105` |

{style="table-layout:auto"}

## Raccogliere informazioni contestuali utilizzando l’estensione tag Web SDK

L&#39;impostazione relativa alle informazioni di contesto è una combinazione di pulsanti di scelta e caselle di controllo durante la [configurazione dell&#39;estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Ogni casella di controllo è associata a una parola chiave di contesto.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Scorri fino alla sezione [!UICONTROL Raccolta dati], quindi seleziona **[!UICONTROL Tutte le informazioni di contesto predefinite]** o **[!UICONTROL Informazioni di contesto specifiche]**.
1. Se si seleziona **[!UICONTROL Informazioni di contesto specifiche]**, abilitare la casella di controllo accanto a ogni elemento informazioni di contesto desiderato.
1. Fai clic su **[!UICONTROL Salva]**, quindi pubblica le modifiche.

## Raccogliere informazioni contestuali utilizzando la libreria JavaScript dell’SDK per web

Impostare la matrice di stringhe `context` durante l&#39;esecuzione del comando `configure`. Se si omette questa proprietà durante la configurazione dell&#39;SDK, tutte le informazioni di contesto tranne `"highEntropyUserAgentHints"` vengono raccolte per impostazione predefinita. Imposta questa proprietà se desideri raccogliere hint client ad alta entropia o se desideri omettere altre informazioni contestuali dalla raccolta di dati. Le stringhe possono essere incluse in qualsiasi ordine.

>[!NOTE]
>
>Se si desidera raccogliere tutte le informazioni di contesto, inclusi gli hint client ad alta entropia, è necessario includere ogni valore nella stringa di matrice `context`. Il valore predefinito `context` omette `highEntropyUserAgentHints` e se si imposta la proprietà `context`, eventuali valori omessi non raccolgono dati.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  context: ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]
});
```
