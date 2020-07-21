---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Convalida dell'assimilazione in streaming
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 3%

---


# Convalida dell&#39;assimilazione in streaming

L’assimilazione dello streaming consente di caricare i dati  Adobe Experience Platform utilizzando gli endpoint di streaming in tempo reale. Le API di assimilazione in streaming supportano due modalità di convalida: sincrona e asincrona.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti del  Adobe Experience Platform:

- [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
- [!DNL Streaming Ingestion](../streaming-ingestion/overview.md): Uno dei metodi tramite i quali è possibile inviare i dati [!DNL Experience Platform].

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti al gruppo [!DNL Schema Registry], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

- Content-Type: `application/json`

### Copertura convalida

[!DNL Streaming Validation Service] copre la convalida nei seguenti settori:
- Intervallo
- Presenza
- Enum
- Pattern
- Tipo
- Formato

## Convalida sincrona

La convalida sincrona è un metodo di convalida che fornisce un feedback immediato sui motivi per cui un&#39;assimilazione non è riuscita. Tuttavia, in caso di errore, i record con errore di convalida vengono ignorati e non possono essere inviati a valle. Di conseguenza, la convalida sincrona deve essere utilizzata solo durante il processo di sviluppo. Durante la convalida sincrona, i chiamanti vengono informati del risultato della convalida XDM e, in caso di errore, del motivo dell&#39;errore.

Per impostazione predefinita, la convalida sincrona non è attivata. Per attivarla, è necessario passare il parametro di query facoltativo `synchronousValidation=true` quando si effettuano chiamate API. Inoltre, la convalida sincrona è attualmente disponibile solo se l&#39;endpoint del flusso si trova nel centro dati VA7.

Se un messaggio ha esito negativo durante la convalida sincrona, il messaggio non verrà scritto nella coda di output, che fornisce agli utenti un feedback immediato.

**Formato API**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | Il `id` valore della connessione di streaming creata in precedenza. |

**Richiesta**

Invia la seguente richiesta per l’inserimento di dati all’ingresso dati con convalida sincrona:

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | Il corpo JSON di un dato che desideri acquisire. |

**Risposta**

Quando la convalida sincrona è attivata, una risposta corretta include eventuali errori di convalida nel payload:

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

La risposta riportata sopra elenca quante violazioni dello schema sono state trovate e quali sono state riscontrate. Ad esempio, questa risposta indica che le chiavi `workEmail` e `person` non sono state definite nello schema, pertanto non sono consentite. Inoltre, contrassegna il valore per `_id` come errato, poiché lo schema prevedeva un `string`, ma `long` è stato inserito un valore. Si noti che, una volta riscontrati cinque errori, il servizio di convalida **interrompe** l&#39;elaborazione del messaggio. Tuttavia, altri messaggi continueranno ad essere analizzati.

## Convalida asincrona

La convalida asincrona è un metodo di convalida che non fornisce feedback immediato. Al contrario, i dati vengono inviati a un batch con errore per [!DNL Data Lake] evitare la perdita di dati. Questi dati con errore possono essere successivamente recuperati per ulteriore analisi e ripetizione. Questo metodo deve essere utilizzato nella produzione. Se non diversamente richiesto, l&#39;assimilazione in streaming viene eseguita in modalità di convalida asincrona.

**Formato API**

```http
POST /collection/{CONNECTION_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | Il `id` valore della connessione di streaming creata in precedenza. |

**Richiesta**

Invia la seguente richiesta per l’inserimento di dati all’ingresso dati con convalida asincrona:

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

Se la convalida asincrona è attivata, una risposta corretta restituisce quanto segue:

```json
{
    "inletId": "f6ca9706d61de3b78be69e2673ad68ab9fb2cece0c1e1afc071718a0033e6877",
    "xactionId": "1555445493896:8600:8",
    "receivedTimeMs": 1555445493932,
    "synchronousValidation": {
        "skipped": true
    }
}
```

Tenere presente che la risposta indica che la convalida sincrona è stata saltata, in quanto non è stata esplicitamente richiesta.

## Appendice

Questa sezione contiene informazioni sul significato dei vari codici di stato per le risposte per l’assimilazione dei dati.

### Codici di stato

| Codice di stato | Significato |
| ----------- | ------------- |
| 200 | Operazione riuscita. Per la convalida sincrona, significa che ha superato i controlli di convalida. Per la convalida asincrona, significa che ha ricevuto correttamente solo il messaggio. Gli utenti possono scoprire lo stato finale del messaggio osservando il dataset. |
| 400 | Errore. C&#39;è qualcosa che non va con la tua richiesta. Un messaggio di errore con ulteriori dettagli viene ricevuto dai servizi di convalida in streaming. |
| 401 | Errore. La tua richiesta non è autorizzata. Dovrai richiedere un token per il portatore. Per ulteriori informazioni su come richiedere l&#39;accesso, consultate questa [esercitazione](../../tutorials/authentication.md) o questo post [di](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)blog. |
| 500 | Errore. Errore interno del sistema. |
| 501 | Errore. Ciò significa che la convalida sincrona **non** è supportata per questa posizione. |
| 503 | Errore. Il servizio non è al momento disponibile. I client devono riprovare almeno tre volte utilizzando una strategia di back-off esponenziale. |