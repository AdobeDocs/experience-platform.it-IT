---
title: Informazioni raccolte automaticamente
description: Panoramica dei dati raccolti automaticamente da Adobe Experience Platform Web SDK.
source-git-commit: 89b981104e3cbe597d1556484f4365866bf2a11d
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 3%

---

# Informazioni raccolte automaticamente

Adobe Experience Platform Web SDK raccoglie automaticamente alcune informazioni pronte all’uso. Se la tua organizzazione non desidera raccogliere automaticamente questi dati, puoi utilizzare `context` opzione in [`configure` comando](../fundamentals/configuring-the-sdk.md).

Parole chiave escluse dal `context` non sono inclusi nella raccolta dati. Se il `context` l’array non esiste in `configure` , vengono raccolti automaticamente tutti i dati della tabella seguente.

| Nome | Descrizione | `context` parola chiave array | Percorso XDM | Esempio di valore |
| --- | --- | --- | --- | --- |
| Altezza schermo | Altezza dello schermo in pixel. | `device` | `events[].xdm.device.screenHeight` | `900` |
| Larghezza schermo | Larghezza dello schermo in pixel. | `device` | `events[].xdm.device.screenWidth` | `1440` |
| Orientamento schermo | Orientamento dello schermo. | `device` | `events[].xdm.device.screenOrientation` | `landscape` oppure `portrait` |
| Tipo di ambiente | Il tipo di ambiente attraverso il quale è emersa l’esperienza. Adobe Experience Platform Web SDK imposta sempre questo campo su `browser`. | `environment` | `events[].xdm.environment.type` | `browser` |
| Altezza del riquadro di visualizzazione | Altezza in pixel dell&#39;area contenuto del browser. | `environment` | `events[].xdm.environment.browserDetails.viewportHeight` | `679` |
| Larghezza del riquadro di visualizzazione | Larghezza in pixel dell&#39;area contenuto del browser. | `environment` | `events[].xdm.environment.browserDetails.viewportWidth` | `642` |
| Nome SDK | Identificatore SDK. Questo campo utilizza un URI per migliorare l’univocità tra gli identificatori forniti da diverse librerie software. Quando si utilizza la libreria autonoma, il valore è `https://ns.adobe.com/experience/alloy`. Quando la libreria viene utilizzata come parte dell’estensione tag, il valore è `https://ns.adobe.com/experience/alloy+reactor`. | | `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |
| Versione SDK | Quando si utilizza la libreria indipendente, il valore è la versione della libreria. Quando la libreria viene utilizzata come parte dell’estensione tag, il valore è una concatenazione della versione della libreria e della versione dell’estensione tag. | | `events[].xdm.implementationDetails.version` | `2.1.0+2.1.3` |
| Ambiente | Ambiente in cui sono stati raccolti i dati. Adobe Experience Platform Web SDK imposta sempre questo campo su `browser`. | | `events[].xdm.implementationDetails.environment` | `browser` |
| Ora locale | Timestamp locale per l’utente finale in formato ISO esteso semplificato [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | `placeContext` | `events[].xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| Offset fuso orario locale | Numero di minuti di offset dell&#39;utente da GMT. | `placeContext` | `events[].xdm.placeContext.localTimezoneOffset` | `360` |
| Marca temporale | Il timestamp UTC per l’utente finale in formato ISO esteso semplificato [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | Sempre incluso | `events[].xdm.timestamp` | `YYYY-08-07T22:47:17.129Z` |
| URL della pagina corrente | URL della pagina corrente. | `web` | `events[].xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| URL referrer | URL della pagina precedente visitata. | `web` | `events[].xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}
