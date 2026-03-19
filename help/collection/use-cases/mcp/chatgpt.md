---
title: Raccogliere dati analitici e applicare la personalizzazione nelle app ChatGPT (raccolta dati MCP)
description: Utilizza un server MCP ibrido + pattern di applyResponse del Web SDK per inviare eventi a Adobe Experience Platform Edge Network ed eseguire il rendering della personalizzazione all’interno dell’interfaccia utente di un’app ChatGPT.
keywords: Adobe Experience Platform, Web SDK, Edge Network, MCP, app ChatGPT, applyResponse, endpoint di interazione, personalizzazione, analytics
source-git-commit: c848f821ea911c82531c6784a17df0116572cd86
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 0%

---

# Raccogliere dati analitici e applicare la personalizzazione nelle app ChatGPT (raccolta dati MCP)

Questo caso d’uso mostra come collegare un’app ChatGPT (server Model Context Protocol + componenti facoltativi dell’interfaccia utente) all’Edge Network di Adobe Experience Platform. Questo tipo di raccolta dati ti consente di registrare analisi per interazioni conversazionali che richiamano i tuoi strumenti e consegnano decisioni di personalizzazione da Edge Network in un widget renderizzato da ChatGPT.

>[!NOTE]
>
>Questo documento viene aggiornato in base agli ultimi aggiornamenti disponibili sia dai team di raccolta dati di Adobe che dagli ultimi aggiornamenti tecnologici di OpenAI. Adobe prevede quindi che questo documento si evolverà nel tempo e consiglia di verificare nuovamente la disponibilità di aggiornamenti.

Questo caso d’uso preferisce un approccio ibrido, che utilizza sia un’implementazione lato server per la raccolta dei dati che un’implementazione lato client per il rendering di contenuti personalizzati. Questo approccio è ideale, in quanto il richiamo dello strumento MCP è il momento più affidabile per raccogliere le analisi. Il widget viene eseguito in un contesto di browser ed è la posizione giusta per memorizzare l’identità (in un cookie) e applicare le decisioni di personalizzazione.

Questo caso d’uso contiene un esempio di codice pienamente operativo. Per il codice di esempio e le istruzioni di implementazione, vedi [App ChatGPT + Adobe Experience Platform Edge](https://github.com/adobe/alloy-samples/tree/main/chatgpt-app) nell&#39;archivio `alloy-samples` su GitHub.

>[!IMPORTANT]
>
>Questa pagina illustra un’implementazione di riferimento pensata per illustrare un modello di integrazione. Esamina i requisiti di sicurezza, privacy, consenso e produzione prima di adottare l’approccio nell’applicazione.

## Architettura

Ad alto livello, ci sono cinque parti mobili:

1. **Host MCP (ChatGPT)**: ChatGPT richiama gli strumenti esposti dal server MCP e fornisce un identificatore utente pseudonimo stabile nei metadati della richiesta.
1. **Server MCP (back-end)**: di proprietà della tua organizzazione. Implementa strumenti come l’inserimento di elementi nell’elenco, il recupero dei dettagli o l’invio di richieste.
1. **Adobe IMS**: genera problemi con i token di accesso utilizzati dal server MCP per chiamare le API di raccolta dati di Adobe.
1. **Adobe Experience Platform Edge Network**: riceve eventi di esperienza inviati dal server MCP e restituisce conferme di analisi, aggiornamenti dello stato (ad esempio identità) e decisioni di personalizzazione.
1. **Interfaccia Web incorporata (widget front-end di cui è stato eseguito il rendering dall&#39;host MCP)**: visualizza i risultati strutturati e applica i metadati Adobe ricevuti dal back-end del server MCP.

## Flusso di dati

1. **L&#39;utente** richiede a **ChatGPT** di utilizzare il server MCP.
1. **ChatGPT** interpreta l&#39;intento del prompt e chiama lo strumento MCP **backend appropriato**.
1. **Il server MCP back-end** utilizza le API di raccolta dati (`interact` endpoint) per inviare un evento esperienza a **Edge Network** per la raccolta di analisi e la personalizzazione facoltativa.
1. **Edge Network** restituisce gli handle di risposta, inclusi gli aggiornamenti dello stato e le decisioni di personalizzazione, allo **strumento MCP back-end**.
1. **Lo strumento MCP back-end** restituisce un risultato dello strumento contenente dati aziendali in `structuredContent` e metadati Adobe in `_meta` in **ChatGPT**.
1. **ChatGPT** distribuisce il risultato dello strumento al **widget front-end**, che esegue il rendering dei dati aziendali e applica i metadati di Adobe utilizzando il comando `applyResponse` della libreria Web SDK JavaScript. Questo comando idrata lo stato lato client ed esegue il rendering delle decisioni di personalizzazione idonee nell’interfaccia utente.

Le sezioni seguenti illustrano in dettaglio ogni passaggio.

## Passaggio 1: l’utente richiede ChatGPT utilizzando il server MCP

Questo passaggio rappresenta il punto di ingresso per il flusso di lavoro. L’utente fornisce le finalità del linguaggio naturale:

```text
"Use the Adobe Office Information Tool to show me details about which office that is the most pet-friendly."
```

Per ulteriori informazioni, consulta [Creare il server MCP](https://developers.openai.com/apps-sdk/build/mcp-server/) nella documentazione per gli sviluppatori OpenAI.

## Passaggio 2: ChatGPT interpreta l’intento e chiama uno strumento MCP

In base ai metadati del server MCP, ChatGPT interpreta l’intento e richiama il gestore di strumenti appropriato sul server MCP. Questa chiamata allo strumento crea un punto di verità lato server per l’interazione, indipendente dal successo del rendering dell’interfaccia utente. Uno degli strumenti potrebbe avere i seguenti metadati:

```json
{
  "name": "office_details",
  "description": "Fetch details for a single office by ID and return personalization handles for the UI.",
  "inputSchema": {
    "type": "object",
    "properties": {
      "sessionId": { "type": "string", "description": "Server-issued session identifier." },
      "officeId": { "type": "string", "description": "Office identifier." }
    },
    "required": ["sessionId", "officeId"],
    "additionalProperties": false
  },
  "_meta": {
    "ui": {
      "visibility": ["model", "app"]
    }
  }
}
```

Per ulteriori informazioni su come comunicare a ChatGPT cosa fa ogni strumento MCP, consulta [Definire gli strumenti](https://developers.openai.com/apps-sdk/plan/tools/) nella documentazione per gli sviluppatori di OpenAI.

## Passaggio 3: il server MCP invia un evento esperienza ad Edge Network

Quando il server MCP riceve una richiesta, attiva una chiamata all’Edge Network di Adobe Experience Platform per registrare i dati di analisi e, facoltativamente, richiedere decisioni/personalizzazione. Poiché questa richiesta è da server a server, utilizzare l&#39;endpoint [`interact`](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/) autenticato come parte delle [API di raccolta dati](https://developer.adobe.com/data-collection-apis/docs/). Adobe consiglia di utilizzare uno [spazio dei nomi personalizzato](https://experienceleague.adobe.com/it/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities) per trasmettere l&#39;identificatore univoco OpenAI. Assicurati che lo spazio dei nomi creato nell’interfaccia utente Identities e lo spazio dei nomi delle identità definito nella chiamata corrispondano (distinzione maiuscole/minuscole).

```sh
curl -X POST "https://server.adobedc.net/ee/v2/interact?datastreamId={DATASTREAM_ID}"
  -H "Authorization: Bearer {TOKEN}"
  -H "x-gw-ims-org-id: {ORG_ID}"
  -H "x-api-key: {API_KEY}"
  -H "Content-Type: application/json"
  -d '{
    "event": {
      "xdm": {
        "eventType": "office.details.view",
        "identityMap": {
          "{IDENTITY_NAMESPACE}": [
            { "id": "{PSEUDONYMOUS_SUBJECT_ID}", "primary": true }
          ]
        },
        "timestamp": "YYYY-02-20T19:00:00.000Z"
      }
    },
    "query": {
      "personalization": {
        "decisionScopes": ["__view__"]
      }
    },
    "meta": {
      "state": {
        "entries": [
          { "key": "kndctr_orgid_cluster", "value": "{CLUSTER_HINT_IF_KNOWN}" },
          { "key": "kndctr_orgid_identity", "value": "{ECID_BLOB_IF_KNOWN}" }
        ]
      }
    }
  }'
```

## Passaggio 4: Edge Network restituisce gli handle

Quando Edge Network riceve la chiamata `interact`, risponde con un array `handle`. Questo array può includere decisioni di identità e personalizzazione, a seconda della configurazione dello stream di dati. Di seguito è riportato un esempio di risposta:

```json
{
  "requestId": "60a2f...2294d",
  "handle": [
    {
      "type": "locationHint:result",
      "payload": [
        { "scope": "EdgeNetwork", "hint": "or2", "ttlSeconds": 1800 }
      ]
    },
    {
      "type": "state:store",
      "payload": [
        { "key": "kndctr_..._identity", "value": "CiYzM...snTI=", "maxAge": 34128000 },
        { "key": "kndctr_..._cluster", "value": "or2", "maxAge": 1800 }
      ]
    }
  ]
}
```

Il server MCP può quindi estrarre informazioni dalla risposta di Edge Network per mantenere le informazioni sull’identità:

```ts
type EdgeHandle = { type: string; payload?: Array<{ key?: string; value?: string }> };

export function extractStateStore(handles: EdgeHandle[]) {
  const store = handles.find(h => h.type === "state:store");
  const entries = store?.payload ?? [];

  const identity = entries.find(e => e.key?.includes("_identity"))?.value;
  const cluster  = entries.find(e => e.key?.includes("_cluster"))?.value;

  return { identity, cluster };
}
```

## Passaggio 5: il server MCP restituisce l’output strutturato degli strumenti più i metadati Adobe a ChatGPT

La risposta dello strumento MCP include sia l’output strutturato dello strumento che la personalizzazione da Edge Network.

* L&#39;oggetto `structuredContent` contiene dati aziendali da cui ChatGPT può leggere e narrare in modo sicuro.
* L&#39;oggetto `_meta` contiene gli handle di risposta di Adobe e l&#39;oggetto `identityMap` calcolato dal server in modo che il widget possa leggerli senza esporre tali dati a ChatGPT. Mantenere queste informazioni in `_meta.adobe` ti consente di essere coerente sulla posizione in cui si trovano i dati. Il passaggio dello stesso `identityMap` in avanti consente al widget di utilizzare la stessa identità personalizzata su qualsiasi evento successivo lato interfaccia utente.

```json
{
  "content": "Displayed details for office seattle.",
  "structuredContent": {
    "office": {
      "id": "seattle",
      "name": "Seattle",
      "amenities": ["Pet Friendly", "Cafe", "Bike Storage"]
    }
  },
  "_meta": {
    "adobe": {
      "identityMap": {
        "{IDENTITY_NAMESPACE}": [
          { "id": "{PSEUDONYMOUS_SUBJECT_ID}", "primary": true }
        ]
      },
      "handles": [
        {
          "type": "state:store",
          "payload": [
            { "key": "kndctr_..._identity", "value": "..." }
          ]
        },
        {
          "type": "personalization:decisions",
          "payload": [
            { "id": "..." }
          ]
        }
      ]
    }
  }
}
```

Per ulteriori informazioni, consulta [Risultati dello strumento](https://developers.openai.com/apps-sdk/reference/#tool-results) in OpenAI Developer reference.

## Passaggio 6: il widget restituisce il risultato e applica `_adobe.handles` utilizzando `applyResponse`

Il widget esegue il rendering dei dati business da `structuredContent`, quindi legge i metadati Adobe da `_meta.adobe`. In ChatGPT, gli stessi dati sono disponibili per il widget attraverso il livello di compatibilità:

* `window.openai.toolOutput` contiene `structuredContent`
* `window.openai.toolResponseMetadata` contiene `_meta`

Il widget utilizza il comando [`applyResponse`](../../js/commands/applyresponse.md) della libreria JavaScript di Web SDK per idratare lo stato lato client ed eseguire il rendering delle decisioni di personalizzazione restituite dalla chiamata `interact` lato server. Assicurarsi di chiamare il comando [`configure`](../../js/commands/configure/overview.md) prima di chiamare `applyResponse`. Poiché il server MCP ha eseguito una chiamata `interact`, non è necessario chiamare immediatamente il comando [`sendEvent`](../../js/commands/sendevent/overview.md) per l&#39;interazione della chiamata dello strumento.

```js
// Configure the Web SDK before any other commands.
alloy("configure", {
  datastreamId: "YOUR_DATASTREAM_ID",
  orgId: "YOUR_EXPERIENCE_CLOUD_ORG_ID"
});

// Business data exposed to ChatGPT and the widget.
const { office } = window.openai?.toolOutput ?? {};

// Adobe metadata available only to the widget.
const adobe = window.openai?.toolResponseMetadata?.adobe ?? {};
const { identityMap, handles } = adobe;

// Hydrate client-side state and render personalization decisions from the
// server-side interact response.
alloy("applyResponse", {
  renderDecisions: true,
  responseBody: { handle: handles ?? [] }
});
```

Se il widget invia in seguito eventi aggiuntivi lato interfaccia utente, è possibile includere lo stesso `identityMap` in tali chiamate:

```js
alloy("sendEvent", {
  xdm: {
    eventType: "office.details.widgetView",
    identityMap
  }
});
```

Questo modello mantiene l&#39;allineamento dell&#39;utilizzo delle identità lato server e lato interfaccia utente, consentendo comunque alla chiamata `interact` lato server di rimanere l&#39;origine di verità per la raccolta di dati e le decisioni di Analytics.

## Convalida

Una volta configurati tutti i passaggi precedenti, puoi convalidare quanto segue:

* **Raccolta dati:** Verificare che gli eventi raggiungano il set di dati desiderato e che ogni evento venga elaborato come previsto.
* **Personalization:** verifica che le decisioni siano restituite da Edge Network e che siano renderizzate dal tuo widget.

## Considerazioni sulla sicurezza e sulla privacy

* Considera gli identificatori di ChatGPT come sensibili, anche se sono pseudonimi.
* Assicurati di applicare a questo flusso di lavoro il consenso della tua organizzazione e le pratiche di governance dei dati.
* Adobe consiglia di utilizzare i flussi di lavoro OAuth 2.1 per l’autorizzazione.
* Assicurati che i token e i segreti di accesso non raggiungano mai il client o l’interfaccia utente.
