---
title: Gestione degli errori
description: Scopri i possibili errori che potresti riscontrare durante l’esecuzione di richieste API all’API di Adobe Experience Platform Edge Network Server.
seo-description: Learn about the possible errors you might encounter when performing API requests to the Adobe Experience Platform Edge Network Server API.
keywords: errore;codice;gestione;edge;rete;gateway;api
exl-id: f6b8435c-b163-4046-b5fb-50a13a897637
source-git-commit: 422f859bef8faf292fd7e5fd8b6a8d31967421c1
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 3%

---

# Gestione degli errori

## Panoramica {#overview}

Gli errori API in Adobe Experience Platform Edge Network Server API possono avere diverse cause, interne (Edge Network) o esterne (input, configurazione o correlate a monte).

## Tipi di errore {#error-types}

| Errore | Tipo | Descrizione | Codice di stato |
| --- | --- | --- | --- |
| `RequestProcessingError` | Interno | Errore di scopo generale emesso da Adobe Experience Platform Edge Network in circostanze impreviste. | `500` |
| `InputError` | Esterno | Include gli errori causati da un input non corretto e gli errori di convalida delle entità. | `4xx` |
| `ConfigurationError` | Esterno | Errori di configurazione lato server. | `422` |
| `UpstreamError` | Esterno | Errori di comunicazione con i servizi a monte. | `207 Multi-Status` |

## Gravità

Gli errori API del server possono essere suddivisi anche per gravità:

* **Errori irreversibili** interrompe la pipeline di spedizione.
* **Errori non irreversibili** potrebbe segnalare un’elaborazione parziale, consentendo al contempo il proseguimento dell’elaborazione della richiesta.
   * Se presente, il codice di stato globale della richiesta verrà modificato in `207 Multi-Status`.

| Errore | Tipo | Osservazioni |
| --- | --- | --- |
| `RequestProcessingError` | Fatale | Può accadere in qualsiasi momento durante l’elaborazione della richiesta. |
| `InputError` | Fatale | Si verifica quando si accetta la richiesta, prima di inviarla a monte. |
| `ConfigurationError` | Fatale | Si verifica quando si accetta la richiesta, prima di inviarla a monte. |
| `UpstreamError` | Non Fatale | Errori di comunicazione con i servizi a monte. |

### Errori irreversibili {#fatal-errors}

Errori irreversibili bloccano l&#39;elaborazione della richiesta e causano la restituzione di uno stato di risposta non 2xx. Consulta la sezione [tipi di errore](#error-types) per visualizzare il codice di stato previsto, corrispondente a ciascun tipo di errore.

Gli errori saranno accompagnati da un corpo della risposta contenente un oggetto errore. In questo caso, il corpo della risposta contiene un dettaglio del problema, come definito da [RFC 7807 - Dettagli del problema per le API HTTP](https://tools.ietf.org/html/rfc7807).

Il tipo di contenuto restituito è il `application/problem+json` tipo di supporto. Se presente, questa risposta contiene dettagli leggibili da computer relativi all’errore. I dettagli del problema includono un tipo URI.

Tutti gli oggetti di errore hanno un `type`, `status`, `title`, `detail` e `report` proprietà del messaggio in modo che il client API possa individuare il problema.

| Proprietà | Tipo | Descrizione |
| -------- | ------ | ----------- |
| `type` | Stringa | Un riferimento URI (RFC3986) che identifica il tipo di problema, seguendo il formato `https://ns.adobe.com/aep/errors/<ERROR-CODE>`. |
| `status` | Numero | Codice di stato HTTP generato dal server per questa occorrenza del problema. |
| `title` | Stringa | Breve riassunto del tipo di problema leggibile dall&#39;uomo. |
| `detail` | Stringa | Una breve descrizione del tipo di problema leggibile dall&#39;uomo. |
| `report` | Oggetto | Mappa di proprietà aggiuntive che consentono il debug, ad esempio l’ID richiesta o l’ID organizzazione. In alcuni casi potrebbe contenere dati specifici dell’errore in corso, ad esempio un elenco di errori di convalida. |

```json
{
   "type":"https://ns.adobe.com/aep/errors/EXEG-0104-422",
   "status":422,
   "title":"Unprocessable entity",
   "detail":"Invalid request (report attached). Please check your input and try again.",
   "report":{
      "errors":[
         "Allowed Adobe version is 1.0 for standard 'Adobe' at index 0",
         "Allowed IAB version is 2.0 for standard 'IAB TCF' at index 1",
         "IAB consent string value must not be empty for standard 'IAB TCF' at index 1"
      ],
      "requestId":"0f8821e5-ed1a-4301-b445-5f336fb50ee8",
      "orgId":"53A16ACB5CC1D3760A495C99@AdobeOrg"
   }
}
```

### Errori non irreversibili {#non-fatal-errors}

Gli errori non fatali possono essere ulteriormente suddivisi in:

* Errori: Problemi che si sono verificati durante l’elaborazione della richiesta, ma che non hanno causato il rifiuto dell’intera richiesta (ad esempio un errore non critico a monte).
* Avvisi: Messaggi da servizi a monte che potrebbero segnalare un’elaborazione parziale della richiesta.

In caso di errori non fatali (esclusi gli avvisi), la [!DNL Server API] cambia lo stato della risposta in `207 Multi-Status`.

Le avvertenze, d&#39;altra parte, sono per lo più informative, in quanto rappresentano generalmente una condizione potenzialmente transitoria, che non ha avuto alcun impatto sulla richiesta in tutta la sua portata. Un esempio qui è un profilo parziale letto nel motore di segmentazione, nel qual caso la precisione è influenzata in un certo grado, ma la funzionalità viene ancora distribuita.

Gli errori non fatali sono rappresentati nel _Dettagli del problema_ sono incorporati direttamente nella risposta standard del gateway Edge, di tipo `application/json`.

```json
{
  "requestId": "72eaa048-207e-4dde-bf16-0cb2b21336d5",
  "handle": [
  ],
  "errors": [
    {
      "type": "https://ns.adobe.com/aep/errors/EXEG-0201-503",
      "status": 503,
      "title": "The 'com.adobe.experience.platform.ode' service is temporarily unable to serve this request. Please try again later."
    }
  ],
  "warnings": [
    {
      "type": "https://ns.adobe.com/aep/errors/EXEG-0204-200",
      "status": 200,
      "title": "A warning occurred while calling the 'com.adobe.audiencemanager' service for this request.",
      "report": {
        "cause": {
          "message": "Cannot read related customer for device id: ...",
          "code": 202
        }
      }
    }
  ]
}
```

## Trattamento `4xx` e `5xx` Risposte


| Codice di errore | Descrizione |
|---|---|
| `4xx Bad Request` | Più `4xx` Gli errori, come 400, 403, 404, non devono essere riprovati per conto del cliente, tranne che per `429`. Si tratta di errori client che non avranno esito positivo. Il client deve risolvere l&#39;errore prima di riprovare la richiesta. |
| `429 Too Many Requests` | `429` Il codice di risposta HTTP indica che Adobe Experience Platform Edge Network o un servizio upstream limita le richieste. In questo caso, il chiamante deve rispettare il `Retry-After` intestazione di risposta. Tutte le risposte che ritornano devono contenere il codice di risposta HTTP con un codice di errore specifico per il dominio. |
| `500 Internal Server Error` | `500` Gli errori sono generici, errori catch-all. `500` gli errori non devono essere ritentati, tranne che per `502` e `503`. Gli intermediari devono rispondere con un `500` errore e può rispondere con un codice/messaggio di errore generico o un codice/messaggio di errore specifico del dominio. |
| `502 Bad Gateway` | Indica che Adobe Experience Platform Edge Network ha ricevuto una risposta non valida dai server upstream. Questo può accadere a causa di problemi di rete tra i server. Il problema di rete temporaneo può essere risolto e quindi un nuovo tentativo può risolvere il problema, in modo che i destinatari di `502` dopo un certo periodo di tempo, la richiesta potrebbe essere nuovamente ripetuta. |
| `503 Service Unavailable` | Questo codice di errore indica che il servizio è temporaneamente non disponibile. Questo può accadere durante i periodi di manutenzione. Destinatari di `503` gli errori possono riprovare la richiesta, ma devono rispettare `Retry-After` intestazione. |
| `504 Gateway Timeout` | Indica che la richiesta di Adobe Experience Platform Edge Network ai server a monte è scaduta. Ciò può verificarsi a causa di problemi di rete tra server, problemi DNS o altri problemi di rete. I problemi temporanei di rete possono essere risolti dopo un certo periodo di tempo e un nuovo tentativo potrebbe risolvere il problema. |
