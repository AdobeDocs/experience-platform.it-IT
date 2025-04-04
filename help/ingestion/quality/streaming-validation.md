---
keywords: Experience Platform;home;argomenti popolari;streaming;acquisizione streaming;convalida acquisizione streaming;convalida acquisizione streaming;convalida;convalida acquisizione streaming;convalida;convalida sincrona;convalida asincrona;convalida asincrona;;home;argomenti popolari;streaming;streaming ingestion;streaming ingestion validation;Streaming ingestion validation;Synchronous validation;Asynchronous validation;asynchronous validation;
solution: Experience Platform
title: Convalida acquisizione in streaming
type: Tutorial
description: L’acquisizione in streaming ti consente di caricare i dati in Adobe Experience Platform utilizzando endpoint di streaming in tempo reale. Le API di acquisizione in streaming supportano due modalità di convalida, sincrona e asincrona.
exl-id: 6e9ac943-6d73-44de-a13b-bef6041d3834
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 11%

---

# Convalida acquisizione in streaming

L’acquisizione in streaming ti consente di caricare i dati in Adobe Experience Platform utilizzando endpoint di streaming in tempo reale. Le API di acquisizione in streaming supportano due modalità di convalida, sincrona e asincrona.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
- [[!DNL Streaming Ingestion]](../streaming-ingestion/overview.md): uno dei metodi con cui i dati possono essere inviati a [!DNL Experience Platform].

### Lettura delle chiamate API di esempio

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogliere i valori per le intestazioni richieste

Per effettuare chiamate alle API [!DNL Experience Platform], devi prima completare l&#39;[esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Completando il tutorial sull’autenticazione si ottengono i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di [!DNL Experience Platform], come mostrato di seguito:

- Autorizzazione: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform], incluse quelle appartenenti a [!DNL Schema Registry], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Experience Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Experience Platform], consulta la [documentazione di panoramica sulle sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Tipo di contenuto: `application/json`

### Copertura di convalida

[!DNL Streaming Validation Service] riguarda la convalida nelle seguenti aree:
- Intervallo
- Presenza
- Enumerazione
- Pattern
- Tipo
- Formato

## Convalida sincrona

La convalida sincrona è un metodo di convalida che fornisce un feedback immediato sul motivo per cui un’acquisizione non è riuscita. Tuttavia, in caso di errore, i record che non superano la convalida vengono eliminati e non possono essere inviati a valle. Di conseguenza, la convalida sincrona deve essere utilizzata solo durante il processo di sviluppo. Durante la convalida sincrona, i chiamanti vengono informati sia del risultato della convalida XDM che, se questa non è riuscita, del motivo dell’errore.

Per impostazione predefinita, la convalida sincrona non è attivata. Per abilitarlo, è necessario passare il parametro di query opzionale `syncValidation=true` quando si eseguono chiamate API. Inoltre, la convalida sincrona è attualmente disponibile solo se l&#39;endpoint di flusso si trova nel data center VA7.

>[!NOTE]
>
>Il parametro di query `syncValidation` è disponibile solo per il singolo endpoint di messaggio e non può essere utilizzato per l&#39;endpoint batch.

Se un messaggio non riesce durante la convalida sincrona, non verrà scritto nella coda di output, che fornisce un feedback immediato agli utenti.

>[!NOTE]
>
>Le modifiche allo schema potrebbero non essere immediatamente disponibili, poiché sono memorizzate nella cache. Attendere fino a quindici minuti per l&#39;aggiornamento della cache.

**Formato API**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | Il valore `id` della connessione streaming creata in precedenza. |

**Richiesta**

Invia la seguente richiesta per acquisire i dati all’ingresso dei dati con convalida sincrona:

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | Il corpo JSON di un dato che desideri acquisire. |

**Risposta**

Con la convalida sincrona abilitata, una risposta corretta include eventuali errori di convalida riscontrati nel relativo payload:

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [6aca7aa2d87ebd6b2780ca5724d94324a14475f140a2b69373dd5c714430dfd4] imsOrgId: [7BF122A65C5B3FE40A494026@AdobeOrg] Message is invalid",
        "cause": {
            "_streamingValidation": [
                {
                    "schemaLocation": "#",
                    "pointerToViolation": "#",
                    "causingExceptions": [
                        {
                            "schemaLocation": "#",
                            "pointerToViolation": "#",
                            "causingExceptions": [],
                            "keyword": "additionalProperties",
                            "message": "extraneous key [workEmail] is not permitted"
                        },
                        {
                            "schemaLocation": "#",
                            "pointerToViolation": "#",
                            "causingExceptions": [],
                            "keyword": "additionalProperties",
                            "message": "extraneous key [person] is not permitted"
                        },
                        {
                            "schemaLocation": "#/properties/_id",
                            "pointerToViolation": "#/_id",
                            "causingExceptions": [],
                            "keyword": "type",
                            "message": "expected type: String, found: Long"
                        }
                    ],
                    "message": "3 schema violations found"
                }
            ]
        }
    }
}
```

La risposta precedente elenca quante violazioni dello schema sono state trovate e quali sono state. Ad esempio, questa risposta indica che le chiavi `workEmail` e `person` non sono state definite nello schema e pertanto non sono consentite. Inoltre, contrassegna il valore per `_id` come errato, poiché lo schema prevedeva un `string`, ma è stato inserito invece un `long`. Tieni presente che una volta riscontrati cinque errori, il servizio di convalida **interrompe** l&#39;elaborazione del messaggio. Tuttavia, altri messaggi continueranno a essere analizzati.

## Convalida asincrona

La convalida asincrona è un metodo di convalida che non fornisce feedback immediati. I dati vengono invece inviati a un batch non riuscito in [!DNL Data Lake] per evitare la perdita di dati. Questi dati non riusciti possono essere recuperati in seguito per ulteriori analisi e ripetizioni. Questo metodo deve essere utilizzato nella produzione. Se non diversamente richiesto, l’acquisizione in streaming funziona in modalità di convalida asincrona.

**Formato API**

```http
POST /collection/{CONNECTION_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | Il valore `id` della connessione streaming creata in precedenza. |

**Richiesta**

Invia la seguente richiesta per acquisire i dati all’ingresso dei dati con convalida asincrona:

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | Il corpo JSON di un dato che desideri acquisire. |

>[!NOTE]
>
>Non è richiesto alcun parametro di query aggiuntivo, in quanto la convalida asincrona è abilitata per impostazione predefinita.

**Risposta**

Se la convalida asincrona è abilitata, una risposta corretta restituisce quanto segue:

```json
{
    "inletId": "f6ca9706d61de3b78be69e2673ad68ab9fb2cece0c1e1afc071718a0033e6877",
    "xactionId": "1555445493896:8600:8",
    "receivedTimeMs": 1555445493932,
    "syncValidation": {
        "skipped": true
    }
}
```

La risposta indica che la convalida sincrona è stata ignorata, in quanto non è stata esplicitamente richiesta.

## Appendice

Questa sezione contiene informazioni sul significato dei vari codici di stato per le risposte per l’acquisizione dei dati.

### Codici di stato

| Codice di stato | Che cosa significa |
| ----------- | ------------- |
| 200 | Operazione completata. Per la convalida sincrona, significa che ha superato i controlli di convalida. Per la convalida asincrona, significa che ha ricevuto correttamente solo il messaggio. Gli utenti possono scoprire l’eventuale stato del messaggio osservando il set di dati. |
| 400 | Errore. Si è verificato un errore nella richiesta. Un messaggio di errore con ulteriori dettagli viene ricevuto da Streaming Validation Services. |
| 401 | Errore. La richiesta non è autorizzata: dovrai richiedere con un token Bearer. Per ulteriori informazioni su come richiedere l&#39;accesso, vedi questa [esercitazione](https://www.adobe.com/go/platform-api-authentication-en) o questo [post di blog](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f). |
| 500 | Errore. Si è verificato un errore interno del sistema. |
| 501 | Errore. Ciò significa che la convalida sincrona è **non** supportata per questa posizione. |
| 503 | Errore. Il servizio non è al momento disponibile. I clienti devono riprovare almeno tre volte utilizzando una strategia di back-off esponenziale. |
