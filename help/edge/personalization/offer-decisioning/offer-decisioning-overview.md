---
title: Utilizzo di Offer Decisioning con Platform Web SDK
description: Adobe Experience Platform Web SDK può distribuire ed eseguire il rendering di offerte personalizzate gestite in Offer Decisioning. Puoi creare le offerte e altri oggetti correlati utilizzando l’interfaccia utente o l’API di Offer Decisioning.
keywords: offer decisioning;decisione;SDK web;Platform Web SDK;offerte personalizzate;distribuire offerte;consegna offerte;personalizzazione offerte;
exl-id: 4ab51f9d-3c44-4855-b900-aa2cde673a9a
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 5%

---

# Utilizzo di Offer Decisioning con Platform Web SDK

>[!NOTE]
>
>L’utilizzo di Offer Decisioning in Adobe Experience Platform Web SDK è disponibile in modalità di accesso anticipato a determinati utenti. Questa funzionalità non è disponibile per tutte le organizzazioni IMS.

Adobe Experience Platform [!DNL Web SDK] può fornire ed eseguire il rendering di offerte personalizzate gestite in Offer Decisioning. Puoi creare le offerte e altri oggetti correlati utilizzando l’interfaccia utente (UI) o le API di Offer Decisioning.

## Prerequisiti

* L’organizzazione IMS è abilitata per le decisioni edge
* Offerte, Attività create
* Datastream pubblicato

## Terminologia

È importante comprendere la seguente terminologia quando si lavora con Offer Decisioning. Per ulteriori informazioni e per visualizzare i termini aggiuntivi, visita il [offer decisioning glossario](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html).

* **Contenitore:** Un contenitore è un meccanismo di isolamento per tenere separate le diverse preoccupazioni. L’ID contenitore è il primo elemento del percorso per tutte le API dell’archivio. Tutti gli oggetti decisionali risiedono all&#39;interno di un contenitore.

* **Ambiti decisionali:** Ad Offer decisioning, gli ambiti decisionali sono stringhe JSON codificate Base64 contenenti gli ID di attività e posizionamento che desideri che il servizio offer decisioning utilizzi per proporre offerte.

   *Ambito della decisione JSON:*

   ```json
   {
     "activityId":"xcore:offer-activity:11cfb1fa93381aca",
     "placementId":"xcore:offer-placement:1175009612b0100c"
   }
   ```

   *Stringa codificata Base64 dell&#39;ambito decisionale:*

   ```json
   "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
   ```

   >[!TIP]
   >
   >Puoi copiare il valore dell’ambito decisionale dalla **Panoramica dell’attività** nell’interfaccia utente di .

   ![](assets/decision-scope-copy.png)

* **Datastreams:** Per ulteriori informazioni, leggere il [datastreams](../../datastreams/overview.md) documentazione.

* **Identità**: Per ulteriori informazioni, consulta questa documentazione che illustra come [L’SDK per web di Platform utilizza il servizio Identity](../../identity/overview.md).

## Abilitazione dell’Offer decisioning

Per abilitare l’Offer decisioning, esegui le seguenti operazioni:

1. Abilitazione di Adobe Experience Platform nel [datastream](../../datastreams/overview.md) e selezionare la casella &quot;Offer decisioning&quot;

   ![offer-decisioning-edge-config](./assets/offer-decisioning-edge-config.png)

1. Segui le istruzioni per [installare l&#39;SDK](../../fundamentals/installing-the-sdk.md) (L&#39;SDK può essere installato autonomamente o tramite l&#39;interfaccia utente. Consulta la sezione [guida rapida tag](../../../tags/quick-start/quick-start.md)) per ulteriori informazioni.
1. [Configurare l&#39;SDK](../../fundamentals/configuring-the-sdk.md) ad Offer decisioning. Di seguito sono riportati ulteriori passaggi specifici per Offer decisioning.

   * Installare l’SDK indipendente

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
   * Installare l’SDK tramite tag

      1. [Creare una proprietà tag](../../../tags/ui/administration/companies-and-properties.md)
      1. [Aggiungere il codice di incorporamento ](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html)
      1. Installa e configura l’estensione Platform Web SDK con il Datastream creato selezionando la configurazione dal menu a discesa &quot;Datastream&quot;. Consulta la documentazione su [estensioni](../../../tags/ui/managing-resources/extensions/overview.md).

         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)

      1. Crea il necessario [Elementi dati](../../../tags/ui/managing-resources/data-elements.md). Come minimo, devi creare una mappa di identità web SDK per Platform e un elemento dati di oggetto XDM per l’SDK per web per Platform.

         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)

      1. Crea il tuo [Regole](../../../tags/ui/managing-resources/rules.md).

         * Aggiungi un’azione Invia evento SDK per web Platform e aggiungi il pertinente `decisionScopes` alla configurazione di tale azione

            ![send-event-action-decisionScopes](./assets/send-event-action-decisionScopes.png)
      1. [Creare e pubblicare una libreria](../../../tags/ui/publishing/libraries.md) contenente tutte le regole, gli elementi dati e le estensioni pertinenti che hai configurato



## Richieste e risposte di esempio

### Uno `decisionScopes` value

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
| `identityMap` | Sì | Fai riferimento a questo [Documentazione del servizio Identity](../../identity/overview.md). | Un&#39;identità per richiesta. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`. <br><br> Nota: Gli utenti non devono includere `ECID` nella chiamata API. Se necessario, questo parametro viene aggiunto automaticamente alla chiamata . |
| `decisionScopes` | Sì | Array di stringhe JSON codificate Base64 contenenti gli ID attività e di posizionamento. | Massimo 30 `decisionScopes` su richiesta. | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

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
| `scope` | Il campo di applicazione della decisione che ha dato luogo alle offerte proposte. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | ID univoco dell’attività di offerta. | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | ID univoco del posizionamento dell’offerta. | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | ID dell’offerta proposta. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | Schema del contenuto associato all’offerta proposta. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | ID dell’offerta proposta. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | Formato del contenuto associato all’offerta proposta. | `"format": "text/html"` |
| `language` | Matrice di lingue associate al contenuto dell’offerta proposta. | `"language": [ "en-US" ]` |
| `content` | Contenuto associato all’offerta proposta nel formato di una stringa. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Contenuto immagine associato all’offerta proposta sotto forma di URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Caratteristiche associate all’offerta proposta nel formato di un oggetto JSON. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

### Multipli `decisionScopes` values

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
| `identityMap` | Sì | Fai riferimento a questo [Documentazione del servizio Identity](../../identity/overview.md). | Un&#39;identità per richiesta. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`. <br><br> Nota: Gli utenti non devono includere `ECID` nella chiamata API. Se necessario, questo parametro viene aggiunto automaticamente alla chiamata . |
| `decisionScopes` | Sì | Array di stringhe JSON codificate Base64 contenenti gli ID attività e di posizionamento. | Massimo 30 `decisionScopes` su richiesta. | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

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
| `scope` | Il campo di applicazione della decisione che ha dato luogo alle offerte proposte. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | ID univoco dell’attività di offerta. | `"id": "xcore:offer-activity:11cfb1fa93381123"` |
| `placement.id` | ID univoco del posizionamento dell’offerta. | `"xcore:offer-placement:1175009612b01123"` |
| `items.id` | ID dell’offerta proposta. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `schema` | Schema del contenuto associato all’offerta proposta. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-text"` |
| `data.id` | ID dell’offerta proposta. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `format` | Formato del contenuto associato all’offerta proposta. | `"format": "text/text"` |
| `language` | Matrice di lingue associate al contenuto dell’offerta proposta. | `"language": [ "en-US" ]` |
| `content` | Contenuto associato all’offerta proposta nel formato di una stringa. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Contenuto immagine associato all’offerta proposta sotto forma di URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Caratteristiche associate all’offerta proposta nel formato di un oggetto JSON. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

## Limitazioni 

Alcuni vincoli di offerta non sono attualmente supportati con i flussi di lavoro Experience Edge per dispositivi mobili, ad esempio Limitazione di utilizzo. Il valore del campo Limitazione di utilizzo specifica il numero di volte in cui un’offerta può essere presentata a tutti gli utenti. Per ulteriori dettagli, consulta [Documentazione sulle regole di idoneità e sui vincoli delle offerte](https://experienceleague.adobe.com/docs/offer-decisioning/using/managing-offers-in-the-offer-library/creating-personalized-offers.html#eligibility).
