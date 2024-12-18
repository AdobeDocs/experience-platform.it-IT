---
title: Gestione degli errori
description: Scopri i possibili errori che potresti riscontrare durante l’esecuzione di richieste API all’API Adobe Experience Platform Edge Network Server.
exl-id: f6b8435c-b163-4046-b5fb-50a13a897637
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 2%

---

# Gestione degli errori

## Panoramica {#overview}

Gli errori API nell’API Adobe Experience Platform Edge Network Server possono avere diverse cause, interne (Edge Network stesso) o esterne (correlate all’input, alla configurazione o a monte).

## Tipi di errore {#error-types}

| Errore | Tipo | Descrizione | Codice di stato |
| --- | --- | --- | --- |
| `RequestProcessingError` | Interno | Errore generico emesso dall’Edge Network di Adobe Experience Platform in circostanze impreviste. | `500` |
| `InputError` | Esterno | Include gli errori causati da input non validi, nonché gli errori di convalida delle entità. | `4xx` |
| `ConfigurationError` | Esterno | Errori di configurazione lato server. | `422` |
| `UpstreamError` | Esterno | Errori di comunicazione con i servizi a monte. | `207 Multi-Status` |

## Gravità

Gli errori API server possono essere suddivisi anche in base alla gravità:

* **Errori irreversibili** causeranno l&#39;arresto della pipeline di invio.
* **Errori non irreversibili** potrebbero segnalare un&#39;elaborazione parziale, consentendo al contempo la continuazione dell&#39;elaborazione delle richieste.
   * Se presente, il codice di stato complessivo della richiesta verrà modificato in `207 Multi-Status`.

| Errore | Tipo | Osservazioni |
| --- | --- | --- |
| `RequestProcessingError` | Fatale | Può verificarsi in qualsiasi momento durante l’elaborazione della richiesta. |
| `InputError` | Fatale | Si verifica quando si accetta la richiesta, prima di inviarla a monte. |
| `ConfigurationError` | Fatale | Si verifica quando si accetta la richiesta, prima di inviarla a monte. |
| `UpstreamError` | Non fatale | Errori di comunicazione con i servizi a monte. |

### Errori irreversibili {#fatal-errors}

Errori irreversibili interrompono l’elaborazione della richiesta e causano la restituzione di uno stato di risposta non 2xx. Consulta la sezione [tipi di errore](#error-types) per visualizzare il codice di stato previsto, corrispondente a ciascun tipo di errore.

Gli errori saranno accompagnati da un corpo della risposta contenente un oggetto di errore. In questo caso, il corpo della risposta contiene un dettaglio del problema, come definito da [RFC 7807 Problem Details for HTTP APIs](https://tools.ietf.org/html/rfc7807).

Il tipo di contenuto restituito è il tipo di supporto `application/problem+json`. Se presente, questa risposta contiene dettagli leggibili dal computer relativi all’errore. I dettagli del problema includono un tipo URI.

Tutti gli oggetti errore hanno proprietà di messaggio `type`, `status`, `title`, `detail` e `report` in modo che il client API possa individuare il problema.

| Proprietà | Tipo | Descrizione |
| -------- | ------ | ----------- |
| `type` | Stringa | Riferimento URI (RFC3986) che identifica il tipo di problema, nel formato `https://ns.adobe.com/aep/errors/<ERROR-CODE>`. |
| `status` | Numero | Il codice di stato HTTP generato dal server per questa occorrenza del problema. |
| `title` | Stringa | Riepilogo breve e leggibile del tipo di problema. |
| `detail` | Stringa | Breve descrizione leggibile del tipo di problema. |
| `report` | Oggetto | Mappa di proprietà aggiuntive utili per il debug, ad esempio l’ID richiesta o l’ID organizzazione. In alcuni casi, potrebbe contenere dati specifici per l’errore in questione, ad esempio un elenco di errori di convalida. |

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

Gli errori non irreversibili possono essere ulteriormente suddivisi in:

* Errori: problemi che si sono verificati durante l’elaborazione della richiesta, ma che non hanno causato il rifiuto dell’intera richiesta (ad esempio un errore upstream non critico).
* Avvisi: messaggi provenienti dai servizi upstream che potrebbero segnalare che si è verificata un’elaborazione parziale della richiesta.

Quando si verificano errori non irreversibili (esclusi gli avvisi), [!DNL Server API] cambierà lo stato della risposta in `207 Multi-Status`.

Le avvertenze, d’altro canto, sono per lo più informative, in quanto in genere rappresentano una condizione potenzialmente transitoria che non ha avuto un impatto completo sulla richiesta. Un esempio di questo è un profilo parziale letto nel motore di segmentazione, nel qual caso la precisione è influenzata in qualche misura, ma la funzionalità è ancora disponibile.

Gli errori non irreversibili sono rappresentati nel formato _Dettagli problema_, ma sono incorporati direttamente nella risposta standard del gateway Edge, che è di tipo `application/json`.

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

## Gestione di `4xx` e `5xx` risposte

| Codice errore | Descrizione |
|---|---|
| `4xx Bad Request` | La maggior parte degli errori `4xx`, come 400, 403, 404, non deve essere ritentata per conto del client, ad eccezione di `429`. Si tratta di errori client che non verranno eseguiti correttamente. Il client deve risolvere l’errore prima di ritentare la richiesta. |
| `429 Too Many Requests` | `429` il codice di risposta HTTP indica che l&#39;Edge Network di Adobe Experience Platform o un servizio a monte limita la frequenza delle richieste. In questo caso, il chiamante deve rispettare l&#39;intestazione di risposta `Retry-After` in uno scenario simile. Tutte le risposte che tornano devono contenere il codice di risposta HTTP con un codice di errore specifico del dominio. |
| `500 Internal Server Error` | `500` errori sono generici e includono tutti gli errori. `500` errori non devono essere ritentati, tranne `502` e `503`. Gli intermediari devono rispondere con un errore `500` e possono rispondere con un codice/messaggio di errore generico o con un codice/messaggio di errore più specifico del dominio. |
| `502 Bad Gateway` | Indica che l’Edge Network di Adobe Experience Platform ha ricevuto una risposta non valida dai server upstream. Ciò può verificarsi a causa di problemi di rete tra i server. Il problema di rete temporaneo potrebbe risolversi e quindi un nuovo tentativo potrebbe risolvere il problema. I destinatari di `502` errori potrebbero riprovare la richiesta dopo un certo periodo di tempo. |
| `503 Service Unavailable` | Questo codice di errore indica che il servizio non è al momento disponibile. Ciò può verificarsi durante i periodi di manutenzione. I destinatari di `503` errori possono ritentare la richiesta, ma devono rispettare l&#39;intestazione `Retry-After`. |
| `504 Gateway Timeout` | Indica che la richiesta di Edge Network di Adobe Experience Platform ai server upstream è scaduta. Ciò può verificarsi a causa di problemi di rete tra server, problemi DNS o altri problemi di rete. I problemi di rete temporanei possono essere risolti dopo un certo periodo di tempo e un nuovo tentativo potrebbe risolvere il problema. |
