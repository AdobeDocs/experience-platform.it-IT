---
keywords: Experience Platform;home;argomenti comuni;streaming;acquisizione streaming;convalida streaming ingestion;convalida;convalida Streaming ingestion;convalida;convalida sincrona;convalida sincrona;convalida asincrona;convalida asincrona;
solution: Experience Platform
title: Convalida dell’acquisizione in streaming
topic-legacy: tutorial
type: Tutorial
description: L’acquisizione in streaming ti consente di caricare i dati in Adobe Experience Platform utilizzando gli endpoint di streaming in tempo reale. Le API Streaming Ingestion supportano due modalità di convalida, sincrone e asincrona.
exl-id: 6e9ac943-6d73-44de-a13b-bef6041d3834
source-git-commit: ec8eb0e805f7127dd8712fc3fe08057d1d8c10c1
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 4%

---

# Convalida dell’acquisizione in streaming

L’acquisizione in streaming ti consente di caricare i dati in Adobe Experience Platform utilizzando gli endpoint di streaming in tempo reale. Le API Streaming Ingestion supportano due modalità di convalida, sincrone e asincrona.

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
- [[!DNL Streaming Ingestion]](../streaming-ingestion/overview.md): Uno dei metodi con cui i dati possono essere inviati a [!DNL Experience Platform].

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate a [!DNL Platform] API, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform], compresi quelli appartenenti al [!DNL Schema Registry], sono isolate in sandbox virtuali specifiche. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedi [documentazione panoramica su sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Content-Type: `application/json`

### Copertura della convalida

[!DNL Streaming Validation Service] riguarda la convalida nei seguenti settori:
- Range
- Presenza
- Enum
- Pattern
- Tipo
- Formato

## Convalida sincrona

La convalida sincrona è un metodo di convalida che fornisce un feedback immediato sui motivi per cui un’acquisizione non è riuscita. Tuttavia, in caso di errore, i record con errore di convalida vengono eliminati e non possono essere inviati a valle. Di conseguenza, la convalida sincrona deve essere utilizzata solo durante il processo di sviluppo. Durante la convalida sincrona, i chiamanti vengono informati del risultato della convalida XDM e, in caso di errore, del motivo dell’errore.

Per impostazione predefinita, la convalida sincrona non è attivata. Per abilitarlo, devi trasmettere il parametro di query facoltativo. `syncValidation=true` quando effettui chiamate API. Inoltre, la convalida sincrona è attualmente disponibile solo se l&#39;endpoint del flusso si trova nel data center VA7.

>[!NOTE]
>
>La `syncValidation` il parametro query è disponibile solo per l&#39;endpoint con messaggio singolo e non può essere utilizzato per l&#39;endpoint batch.

Se un messaggio non riesce durante la convalida sincrona, non verrà scritto nella coda di output, che fornisce un feedback immediato agli utenti.

>[!NOTE]
>
>Le modifiche allo schema potrebbero non essere immediatamente disponibili in quanto le modifiche sono memorizzate nella cache. Consenti fino a quindici minuti per l&#39;aggiornamento della cache.

**Formato API**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | La `id` valore della connessione in streaming creata in precedenza. |

**Richiesta**

Invia la seguente richiesta per l’acquisizione di dati all’entrata dati con convalida sincrona:

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | Il corpo JSON di un dato che desideri acquisire. |

**Risposta**

Con la convalida sincrona abilitata, una risposta corretta include eventuali errori di convalida riscontrati nel payload:

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

La risposta di cui sopra elenca quante violazioni dello schema sono state trovate e quali sono state riscontrate. Ad esempio, questa risposta indica che le chiavi `workEmail` e `person` non sono stati definiti nello schema e pertanto non sono consentiti. Inoltre, contrassegna il valore per `_id` non corretto, poiché lo schema prevedeva un `string`, ma `long` è stato invece inserito. Una volta riscontrati cinque errori, il servizio di convalida **stop** elaborazione del messaggio. Tuttavia, altri messaggi continueranno ad essere analizzati.

## Convalida asincrona

La convalida asincrona è un metodo di convalida che non fornisce feedback immediato. I dati vengono invece inviati a un batch con errore in [!DNL Data Lake] per evitare la perdita di dati. Questi dati non riusciti possono essere recuperati in un secondo momento per un’ulteriore analisi e ripetizione. Questo metodo deve essere utilizzato nella produzione. Se non diversamente richiesto, l’acquisizione in streaming funziona in modalità di convalida asincrona.

**Formato API**

```http
POST /collection/{CONNECTION_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | La `id` valore della connessione in streaming creata in precedenza. |

**Richiesta**

Invia la seguente richiesta per inserire i dati nell’entrata dati con convalida asincrona:

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

Con la convalida asincrona abilitata, una risposta corretta restituisce quanto segue:

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
| 200 | Operazione riuscita. Per la convalida sincrona, significa che ha superato i controlli di convalida. Per la convalida asincrona, significa che ha ricevuto il messaggio solo correttamente. Gli utenti possono scoprire l’eventuale stato del messaggio osservando il set di dati. |
| 400 | Errore. C&#39;è qualcosa che non va nella tua richiesta. Un messaggio di errore con ulteriori dettagli viene ricevuto da Servizi di convalida in streaming. |
| 401 | Errore. La richiesta non è autorizzata. Sarà necessario richiedere un token portatore. Per ulteriori informazioni su come richiedere l’accesso, consulta questo [tutorial](https://www.adobe.com/go/platform-api-authentication-en) o [post di blog](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f). |
| 500 | Errore. Errore interno del sistema. |
| 501 | Errore. Ciò significa che la convalida sincrona è **not** supportato per questa posizione. |
| 503 | Errore. Il servizio non è al momento disponibile. I clienti devono riprovare almeno tre volte utilizzando una strategia di back-off esponenziale. |
