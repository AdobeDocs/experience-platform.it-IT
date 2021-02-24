---
title: Utilizzo di  Offer decisioning con Platform Web SDK
description: Adobe Experience Platform Web SDK può distribuire ed eseguire il rendering di offerte personalizzate gestite in  Offer decisioning. Potete creare le offerte e altri oggetti correlati utilizzando l'interfaccia utente o l'API del Offer decisioning .
keywords: ' offer decisioning;decisione;Web SDK;Platform Web SDK;offerte personalizzate;offrire offerte;offerta consegna;offerta di personalizzazione;'
translation-type: tm+mt
source-git-commit: 0b9a92f006d1ec151a0bb11c10c607ea9362f729
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 9%

---


# Utilizzo di  Offer decisioning con Platform Web SDK

>[!NOTE]
>
>L&#39;utilizzo di  Offer decisioning in Adobe Experience Platform Web SDK è attualmente disponibile per l&#39;accesso a determinati utenti in anticipo. Questa funzionalità non è disponibile per tutte le organizzazioni IMS.

Adobe Experience Platform [!DNL Web SDK] è in grado di distribuire ed eseguire il rendering di offerte personalizzate gestite in  Offer decisioning. Potete creare le offerte e altri oggetti correlati utilizzando l&#39;interfaccia utente (interfaccia utente) o le API del Offer decisioning .

## Prerequisiti

* L&#39;organizzazione IMS è abilitata per le decisioni edge
* Offerte, Attività create
* Configurazione Edge pubblicata

## Terminologia

È importante comprendere la seguente terminologia quando si utilizza  Offer decisioning. Per ulteriori informazioni e per visualizzare i termini aggiuntivi, visitare il [ Offer decisioning glossario](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html).

* **Contenitore:** Un contenitore è un meccanismo di isolamento per tenere distanti le diverse preoccupazioni. L&#39;ID contenitore è il primo elemento percorso per tutte le API del repository. Tutti gli oggetti di decisione risiedono all&#39;interno di un contenitore.

* **Ambiti di decisione:** Ad  Offer decisioning, si tratta delle stringhe codificate Base64 di JSON contenenti gli ID attività e di posizionamento che si desidera che il servizio di offer decisioning  utilizzi per proporre offerte.

   *Campo di applicazione della decisione JSON:*

   ```json
   {
     "activityId":"xcore:offer-activity:11cfb1fa93381aca",
     "placementId":"xcore:offer-placement:1175009612b0100c"
   }
   ```

   *Stringa codificata Base64 ambito decisione:*

   ```json
   "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
   ```

   >[!TIP]
   >
   >È possibile copiare il valore dell&#39;ambito decisionale dalla pagina **Activity Overview** nell&#39;interfaccia utente.

   ![](assets/decision-scope-copy.png)

* **Configurazione bordo:** per ulteriori informazioni, consulta la  [documentazione sulla ](../../fundamentals/edge-configuration.md) configurazione del margine.

* **Identità**: Per ulteriori informazioni, consulta questa documentazione in cui sono illustrate le modalità con cui  [Platform Web SDK sfrutta il servizio](../../identity/overview.md) identità.

## Abilitazione  Offer decisioning

Per attivare  Offer decisioning, è necessario effettuare le seguenti operazioni:

1. Abilitato Adobe Experience Platform nella [configurazione dei bordi](../../fundamentals/edge-configuration.md) e selezionare la casella &quot;Offer decisioning &quot;
   ![offer-Decision-edge-config](./assets/offer-decisioning-edge-config.png)
2. Seguite le istruzioni per [installare l&#39;SDK](../../fundamentals/installing-the-sdk.md) (l&#39;SDK può essere installato autonomamente o tramite [ Adobe Experience Platform Launch](http://launch.adobe.com/it). Di seguito è riportata una [guida rapida all&#39;Platform launch](https://docs.adobe.com/content/help/it-IT/launch/using/intro/get-started/quick-start.html).
3. [Configurare l’](../../fundamentals/configuring-the-sdk.md) SDK per  Offer decisioning. Di seguito sono riportati passaggi specifici per  Offer decisioning.
   * SDK installato autonomamente
      1. Configura l&#39;azione &quot;sendEvent&quot; con il tuo `decisionScopes`

      ```javascript
      alloy("sendEvent", {
          ...
          "decisionScopes": [
              "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIwOWMxM2JkZDIyNCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMDZhODRkMDViMTEifQ==",
              "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIyNWI5NTUwNWIxZiIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMjFmOTQzMDE0MmIifQ=="
          ]
      })
      ```
   * SDK installato nel platform launch
      1. [Creare una proprietà Platform launch](https://docs.adobe.com/content/help/it-IT/launch/using/reference/admin/companies-and-properties.html)
      2. [Aggiungere il codice di incorporamento Platform launch](https://docs.adobe.com/content/help/en/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html)
      3. Installa e configura l’estensione SDK Web della piattaforma con la configurazione Edge appena creata selezionando la configurazione dall’elenco a discesa &quot;Configurazione Edge&quot;. Documentazione utile su [estensioni](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html).
         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)
      4. Creare gli elementi [dati ](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/data-elements.html) necessari. Come minimo, è necessario creare una mappa identità SDK piattaforma Web e un elemento dati oggetto XDM SDK piattaforma.
         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)
      5. Crea le tue [regole](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/rules.html).
         * Aggiungere un&#39;azione di invio evento SDK Web piattaforma e aggiungere la `decisionScopes` pertinente alla configurazione dell&#39;azione
            ![send-event-action-DecisionScopes](./assets/send-event-action-decisionScopes.png)
      6. [Crea e pubblica una ](https://docs.adobe.com/content/help/it-IT/launch/using/reference/publish/libraries.html) libreria contenente tutte le regole, gli elementi dati e le estensioni pertinenti che hai configurato


## Richieste e risposte di esempio

### Un valore `decisionScopes`

**Richiesta**

```json
{
  "events": [
    {
      "xdm": {
        "identityMap": {
          "ECID": [
            {
              "id": "91133425615229052182584359620783097099"
            }
          ]
        }
      },
      "query": {
        "personalization": {
          "decisionScopes": [
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
          ]
        }
      }
    }
  ]
}
```

| Proprietà | Obbligatorio | Descrizione | Limiti | Esempio |
|---|---|---|---|---|
| `identityMap` | Sì | Fare riferimento a questa [documentazione del servizio identità](../../identity/overview.md). | Un&#39;identità per richiesta. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | Sì | Un array di stringhe codificate Base64 di JSON contenenti gli ID attività e posizionamento. | Massimo 30 `decisionScopes` per richiesta. | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

**Risposta**

```json
{
  "requestId": "94c4f2f1-9218-43ce-afd3-eb0d853c5174",
  "handle": [
    {
      "payload": [
        {
          "id": "2862bb89-5df2-4bc6-85c2-d8f7e1a091de",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381aca",
            "etag": "2"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b0100c",
            "etag": "1"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:124cc332095cfa74",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-html",
              "etag": "1",
              "data": {
                "id": "xcore:personalized-offer:124cc332095cfa74",
                "format": "text/html",
                "language": [
                  "en-US"
                ],
                "content": "<p>20% Off on shipping</p>",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

| Proprietà | Descrizione | Esempio |
|---|---|---|
| `scope` | Il campo di applicazione della decisione che ha portato alle offerte proposte. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | ID univoco dell&#39;attività dell&#39;offerta. | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | ID univoco del posizionamento dell&#39;offerta. | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | ID dell&#39;offerta proposta. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | Schema del contenuto associato all&#39;offerta proposta. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | ID dell&#39;offerta proposta. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | Formato del contenuto associato all&#39;offerta proposta. | `"format": "text/html"` |
| `language` | Un array di lingue associate al contenuto dell&#39;offerta proposta. | `"language": [ "en-US" ]` |
| `content` | Contenuto associato all&#39;offerta proposta nel formato di una stringa. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Contenuto immagine associato all’offerta proposta nel formato di un URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Caratteristiche associate all&#39;offerta proposta nel formato di un oggetto JSON. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

### Più valori `decisionScopes`

**Richiesta**

```json
{
  "events": [
    {
      "xdm": {
        "identityMap": {
          "ECID": [
            {
              "id": "91133425615229052182584359620783097099"
            }
          ]
        }
      },
      "query": {
        "personalization": {
          "decisionScopes": [
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ==",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyYzkxMzg1Mjc2MDE4YyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMzMxZjU2MTYyYWEyZjcifQ=="
          ]
        }
      }
    }
  ]
}
```

| Proprietà | Obbligatorio | Descrizione | Limiti | Esempio |
|---|---|---|---|---|
| `identityMap` | Sì | Fare riferimento a questa [documentazione del servizio identità](../../identity/overview.md). | Un&#39;identità per richiesta. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | Sì | Un array di stringhe codificate Base64 di JSON contenenti gli ID attività e posizionamento. | Massimo 30 `decisionScopes` per richiesta. | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

**Risposta**

```json
{
  "requestId": "94c4f2f1-9218-43ce-afd3-eb0d853c5174",
  "handle": [
    {
      "payload": [
        {
          "id": "a2804dfb-a0ec-4df9-8311-59d3ecdeb642",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MTEyMyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDExMjMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381123",
            "etag": "1"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b01123",
            "etag": "3"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:11e36d4a22954123",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-text",
              "etag": "2",
              "data": {
                "id": "xcore:personalized-offer:11e36d4a22954123",
                "format": "text/text",
                "language": [
                  "en"
                ],
                "content": "20% Off on shipping",
                "characteristics": {
                  "foo2": "bar2"
                }
              }
            }
          ]
        },
        {
          "id": "a2804dfb-a0ec-4df9-8311-59d3ecdeb642",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381aca",
            "etag": "2"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b0100c",
            "etag": "1"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:11e36d4a2295415d",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
              "etag": "1",
              "data": {
                "id": "xcore:personalized-offer:11e36d4a2295415d",
                "format": "image/png",
                "language": [
                  "en"
                ],
                "deliveryURL": "https://image.jpeg",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

| Proprietà | Descrizione | Esempio |
|---|---|---|
| `scope` | Il campo di applicazione della decisione che ha portato alle offerte proposte. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | ID univoco dell&#39;attività dell&#39;offerta. | `"id": "xcore:offer-activity:11cfb1fa93381123"` |
| `placement.id` | ID univoco del posizionamento dell&#39;offerta. | `"xcore:offer-placement:1175009612b01123"` |
| `items.id` | ID dell&#39;offerta proposta. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `schema` | Schema del contenuto associato all&#39;offerta proposta. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-text"` |
| `data.id` | ID dell&#39;offerta proposta. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `format` | Formato del contenuto associato all&#39;offerta proposta. | `"format": "text/text"` |
| `language` | Un array di lingue associate al contenuto dell&#39;offerta proposta. | `"language": [ "en-US" ]` |
| `content` | Contenuto associato all&#39;offerta proposta nel formato di una stringa. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Contenuto immagine associato all’offerta proposta nel formato di un URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Caratteristiche associate all&#39;offerta proposta nel formato di un oggetto JSON. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |
