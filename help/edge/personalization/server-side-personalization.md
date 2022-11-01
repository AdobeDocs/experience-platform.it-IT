---
title: Personalizzazione lato server tramite API server di rete Edge
description: Questo articolo illustra come utilizzare l'API di Server di rete Edge per distribuire la personalizzazione lato server sulle proprietà web.
keywords: personalizzazione; api del server; rete perimetrale; lato server;
source-git-commit: 3e7084953a5e158059074c857bfce4940a83661b
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 2%

---


# Personalizzazione lato server tramite API server di rete Edge

## Panoramica {#overview}

La personalizzazione lato server comporta l’utilizzo di [API server di rete Edge](../../server-api/overview.md) per personalizzare l&#39;esperienza del cliente sulle proprietà web.

Nell’esempio descritto in questo articolo, il contenuto di personalizzazione viene recuperato lato server, utilizzando l’API server. Quindi, viene eseguito il rendering di HTML lato server, in base al contenuto di personalizzazione recuperato.

La tabella seguente mostra un esempio di contenuto personalizzato e non personalizzato.

| Pagina di esempio senza personalizzazione | Pagina di esempio con personalizzazione |
|---|---|
| ![Esempio di pagina web senza personalizzazione](assets/plain.png) | ![Esempio di pagina web con personalizzazione](assets/personalized.png) |

## Considerazioni {#considerations}

### Cookie {#cookies}

I cookie vengono utilizzati per mantenere l&#39;identità utente e le informazioni sui cluster.  Quando si utilizza un&#39;implementazione lato server, l&#39;application server gestisce la memorizzazione e l&#39;invio di questi cookie durante il ciclo di vita della richiesta.

| Cookie | Finalità | Memorizzato da | Inviato da |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | Contiene i dettagli dell’identità utente. | Server dell’applicazione | Server dell’applicazione |
| `kndctr_AdobeOrg_cluster` | Indica il cluster di rete Edge da utilizzare per soddisfare le richieste. | Server dell’applicazione | Server dell’applicazione |

### Inserimento di richieste {#request-placement}

Le richieste di personalizzazione sono necessarie per ottenere le proposte e inviare una notifica di visualizzazione. Quando si utilizza un&#39;implementazione lato server, l&#39;application server invia tali richieste all&#39;API server di rete Edge.

| Richiesta | Realizzato da |
|---|---|
| Richiesta di interazione per recuperare le proposte | Application server che chiama l&#39;API server di rete Edge. |
| Richiesta di interazione per inviare notifiche di visualizzazione | Application server che chiama l&#39;API server di rete Edge. |

## Applicazione di esempio {#sample-app}

Il processo descritto di seguito utilizza un&#39;applicazione di esempio che puoi utilizzare come punto di partenza per sperimentare e per saperne di più su questo tipo di personalizzazione.

Puoi scaricare questo esempio e personalizzarlo in base alle tue esigenze. Ad esempio, puoi modificare le variabili di ambiente in modo che l’app di esempio raccolga le offerte dalla configurazione del tuo Experience Platform.

Per farlo, apri la `.env` nella directory principale dell’archivio e modifica le variabili in base alla configurazione. Riavvia l’app di esempio e sei pronto per sperimentare utilizzando il tuo contenuto di personalizzazione.

### Esecuzione del campione {#running-sample}

Per eseguire l’app di esempio, procedi come segue.

1. Clona [questo archivio](https://github.com/adobe/alloy-samples) alla macchina locale.
2. Apri un terminale e passa alla `personalization-server-side` cartella.
3. Eseguire `npm install`.
4. Eseguire `npm start`.
5. Apri il browser Web e passa a `http://localhost`.

## Panoramica del processo {#process}

Questa sezione descrive i passaggi utilizzati per recuperare il contenuto di personalizzazione.

1. [Express](https://expressjs.com/) viene utilizzato per un&#39;implementazione lato server snella. Questo consente di gestire le richieste e l&#39;indirizzamento del server di base.
2. Il browser richiede la pagina web. Qualsiasi cookie precedentemente memorizzato dal browser, con prefisso `kndctr_`, sono inclusi.
3. Quando la pagina viene richiesta dall’app server, viene inviato un evento al [endpoint di raccolta dati interattivo](../../../server-api/interactive-data-collection.md) per recuperare il contenuto della personalizzazione. L’app di esempio utilizza metodi helper per per semplificare la creazione e l’invio di richieste all’API (consulta [aepEdgeClient.js](https://github.com/adobe/alloy-samples/blob/main/common/aepEdgeClient.js)). La `POST` la richiesta contiene un `event` e `query`. I cookie del passaggio precedente, se disponibili, sono inclusi nella `meta>state>entries` array.

   ```js
   fetch(
   "https://edge.adobedc.net/ee/v2/interact?dataStreamId=abc&requestId=123",
   {
      headers: {
         accept: "*/*",
         "accept-language": "en-US,en;q=0.9",
         "cache-control": "no-cache",
         "content-type": "text/plain; charset=UTF-8",
         pragma: "no-cache",
         "sec-fetch-dest": "empty",
         "sec-fetch-mode": "cors",
         "sec-fetch-site": "cross-site",
         "sec-gpc": "1",
         "Referrer-Policy": "strict-origin-when-cross-origin",
         Referer: "http://localhost/",
      },
      body: JSON.stringify({
         event: {
         xdm: {
            web: {
               webPageDetails: {
               URL: "http://localhost/",
               },
               webReferrer: {
               URL: "",
               },
            },
            identityMap: {
               FPID: [
               {
                  id: "xyz",
                  authenticatedState: "ambiguous",
                  primary: true,
               },
               ],
            },
            timestamp: "2022-06-23T22:21:00.878Z",
         },
         data: {},
         },
         query: {
         identity: {
            fetch: ["ECID"],
         },
         personalization: {
            schemas: [
               "https://ns.adobe.com/personalization/default-content-item",
               "https://ns.adobe.com/personalization/html-content-item",
               "https://ns.adobe.com/personalization/json-content-item",
               "https://ns.adobe.com/personalization/redirect-item",
               "https://ns.adobe.com/personalization/dom-action",
            ],
            decisionScopes: ["__view__", "sample-json-offer"],
         },
         },
         meta: {
         state: {
            domain: "localhost",
            cookiesEnabled: true,
            entries: [
               {
               "key": "kndctr_XXX_AdobeOrg_identity",
               "value": "abc123"
               },
               {
               "key": "kndctr_XXX_AdobeOrg_cluster",
               "value": "or2"
               }
            ],
         },
         },
      }),
      method: "POST",
   }
   ).then((res) => res.json());
   ```

4. L’offerta Target dall’attività basata su moduli viene letta dalla risposta e utilizzata durante la produzione della risposta di HTML.
5. Per le attività basate su moduli, gli eventi di visualizzazione devono essere inviati manualmente nell’implementazione per indicare quando è stata visualizzata l’offerta. In questo esempio, la notifica viene inviata lato server durante il ciclo di vita della richiesta.

   ```js
   function sendDisplayEvent(aepEdgeClient, req, propositions, cookieEntries) {
   const address = getAddress(req);
   
   aepEdgeClient.interact(
      {
         event: {
         xdm: {
            web: {
               webPageDetails: { URL: address },
               webReferrer: { URL: "" },
            },
            timestamp: new Date().toISOString(),
            eventType: "decisioning.propositionDisplay",
            _experience: {
               decisioning: {
               propositions: propositions.map((proposition) => {
                  const { id, scope, scopeDetails } = proposition;
   
                  return {
                     id,
                     scope,
                     scopeDetails,
                  };
               }),
               },
            },
         },
         },
         query: { identity: { fetch: ["ECID"] } },
         meta: {
         state: {
            domain: "",
            cookiesEnabled: true,
            entries: [...cookieEntries],
         },
         },
      },
      {
         Referer: address,
      }
   );
   }
   ```

6. [!DNL Visual Experience Composer (VEC)] le offerte vengono ignorate, poiché possono essere sottoposte a rendering solo tramite SDK web.
7. Quando viene restituita la risposta di HTML, i cookie di identità e cluster vengono impostati sulla risposta dal server dell&#39;applicazione.