---
title: contesto
description: Raccogli automaticamente i dati relativi a dispositivo, ambiente o posizione.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 5%

---

# `context`

Il `context` La proprietà è un array di stringhe che determina ciò che l’SDK web può raccogliere automaticamente. Anche se questi dati possono fornire un grande valore, omettere alcuni di questi dati può essere utile in modo da poter rispettare l’informativa sulla privacy della tua organizzazione.

## Parole chiave di contesto ed elementi XDM

Se includi una determinata parola chiave di contesto, Web SDK compila automaticamente tutti gli elementi XDM associati. Se desideri omettere uno specifico elemento XDM e consentire ad altri di farlo, puoi cancellare i valori utilizzando [`onBeforeEventSend`](onbeforeeventsend.md). Se invii più eventi a una pagina, l’SDK web include questi campi ogni `SendEvent` chiamare.

### Web

Il `"web"` parola chiave raccoglie informazioni sulla pagina corrente.

| Dimensione | Descrizione | Percorso XDM | Esempio di valore |
| --- | --- | --- | --- |
| URL della pagina | URL della pagina corrente. | `xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| URL referrer | URL della pagina precedente visitata. | `xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}

### Dispositivo

Il `"device"` keyword raccoglie informazioni sul dispositivo dell&#39;utente.

| Dimensione | Descrizione | Percorso XDM | Esempio di valore |
| --- | --- | --- | --- |
| Altezza schermo | Altezza dello schermo in pixel. | `xdm.device.screenHeight` | `900` |
| Larghezza schermo | Larghezza dello schermo in pixel. | `xdm.device.screenWidth` | `1440` |
| Orientamento schermo | Orientamento dello schermo. | `xdm.device.screenOrientation` | `landscape` oppure `portrait` |

{style="table-layout:auto"}

### Ambiente

Il `"environment"` la parola chiave raccoglie informazioni sul browser dell&#39;utente.

| Dimensione | Descrizione | Percorso XDM | Esempio di valore |
| --- | --- | --- | --- |
| Tipo di ambiente | Il tipo di ambiente attraverso il quale è emersa l’esperienza. Web SDK imposta sempre questo campo su `browser`. | `xdm.environment.type` | `browser` |
| Altezza del riquadro di visualizzazione | Altezza in pixel dell&#39;area contenuto del browser. | `xdm.environment.browserDetails.viewportHeight` | `679` |
| Larghezza del riquadro di visualizzazione | Larghezza in pixel dell&#39;area contenuto del browser. | `xdm.environment.browserDetails.viewportWidth` | `642` |

{style="table-layout:auto"}

### Contesto del luogo

Il `"placeContext"` la parola chiave raccoglie informazioni sulla posizione dell&#39;utente.

| Dimensione | Descrizione | Percorso XDM | Esempio di valore |
| --- | --- | --- | --- |
| Ora locale | Timestamp locale per l’utente finale in versione estesa semplificata [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) formato. | `xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| Offset fuso orario locale | Il numero di minuti di offset dell&#39;utente da GMT. | `xdm.placeContext.localTimezoneOffset` | `360` |

{style="table-layout:auto"}

### Hint client ad alta entropia

Il `"highEntropyUserAgentHints"` keyword raccoglie informazioni dettagliate sul dispositivo dell&#39;utente. Questi dati sono inclusi nell’intestazione HTTP della richiesta inviata all’Adobe. Una volta arrivati i dati all’interno della rete Edge, l’oggetto XDM compila il rispettivo percorso XDM. Se imposti il rispettivo percorso XDM nel `sendEvent` , ha la precedenza sul valore dell&#39;intestazione HTTP.

Se utilizzi le ricerche dei dispositivi quando [configurazione dello stream di dati](/help/datastreams/configure.md), i dati possono essere cancellati a favore dei valori di ricerca del dispositivo. Alcuni campi degli hint client e dei campi di ricerca del dispositivo non possono esistere nello stesso hit.

| Dimensione | Descrizione | Intestazione HTTP | Percorso XDM | Esempio di valore |
| --- | --- | --- | --- | --- |
| Versione del sistema operativo | Versione del sistema operativo. | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | |
| Architettura | Architettura CPU sottostante. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | |
| Modello dispositivo | Nome del dispositivo utilizzato. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | |
| numero di bit | Il numero di bit supportati dall&#39;architettura CPU sottostante. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | |
| Fornitore browser | Azienda che ha creato il browser. L’hint a bassa entropia `Sec-CH-UA` raccoglie anche questo elemento. | `Sec-CH-UA-Full-Version-List` | | |
| Nome browser | Browser utilizzato. L’hint a bassa entropia `Sec-CH-UA` raccoglie anche questo elemento. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | |
| Versione browser | Versione significativa del browser. L’hint a bassa entropia `Sec-CH-UA` raccoglie anche questo elemento. La versione esatta del browser non viene raccolta automaticamente. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | |

{style="table-layout:auto"}

## Raccogliere informazioni contestuali utilizzando l’estensione tag Web SDK

L&#39;impostazione relativa alle informazioni contestuali è una combinazione di pulsanti di scelta e caselle di controllo quando [configurazione dell’estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Ogni casella di controllo è associata a una parola chiave di contesto.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** il [!UICONTROL Adobe Experience Platform Web SDK] Card.
1. Scorri verso il basso fino a [!UICONTROL Raccolta dati] , quindi selezionare una delle seguenti opzioni **[!UICONTROL Tutte le informazioni di contesto predefinite]** o **[!UICONTROL Informazioni specifiche sul contesto]**.
1. Se si seleziona **[!UICONTROL Informazioni specifiche sul contesto]**, abilita la casella di controllo accanto a ciascun elemento di informazioni di contesto desiderato.
1. Clic **[!UICONTROL Salva]**, quindi pubblica le modifiche.

## Raccogliere informazioni contestuali utilizzando la libreria JavaScript di Web SDK

Imposta il `context` matrice di stringhe durante l&#39;esecuzione di `configure` comando. Se ometti questa proprietà durante la configurazione dell’SDK, tutte le informazioni sul contesto tranne `"highEntropyUserAgentHints"` viene raccolto per impostazione predefinita. Imposta questa proprietà se desideri raccogliere hint client ad alta entropia o se desideri omettere altre informazioni contestuali dalla raccolta di dati. Le stringhe possono essere incluse in qualsiasi ordine.

>[!NOTE]
>
>Se desideri raccogliere tutte le informazioni di contesto, inclusi gli hint client ad alta entropia, devi includere ogni valore nella sezione `context` stringa di matrice. Il valore predefinito `context` valore omesso `highEntropyUserAgentHints`, e se si imposta `context` , eventuali valori omessi non raccolgono i dati.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "context": ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]
});
```
