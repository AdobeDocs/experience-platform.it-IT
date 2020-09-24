---
keywords: Experience Platform;home;popular topics;authenticated streaming connection;streaming connection;create streaming connection;create authenticated streaming connection;streaming ingestion;ingestion;
solution: Experience Platform
title: Creare una connessione in streaming autenticata
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 2%

---


# Creazione di una connessione in streaming autenticata

La raccolta dati autenticata consente ai servizi Adobe Experience Platform, ad esempio [!DNL Real-time Customer Profile] e [!DNL Identity], di distinguere tra record provenienti da fonti attendibili e fonti non attendibili. I clienti che desiderano inviare informazioni personali (PII) possono farlo inviando token di accesso come parte della richiesta POST.

## Introduzione

Per avviare lo streaming dei dati su Adobe Experience Platform è necessaria la registrazione della connessione. Quando registrate una connessione in streaming, dovete fornire alcuni dettagli chiave come l&#39;origine dei dati in streaming.

Dopo la registrazione di una connessione di streaming, l&#39;utente, in qualità di produttore di dati, avrà un URL univoco che può essere utilizzato per lo streaming dei dati [!DNL Platform].

Questa esercitazione richiede anche una buona conoscenza dei diversi servizi Adobe Experience Platform. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standard con cui [!DNL Platform] organizzare i dati relativi all&#39;esperienza.
- [[!DNL Profilo cliente in tempo reale]](../../profile/home.md): Fornisce un profilo di consumo unificato in tempo reale basato su dati aggregati provenienti da più origini.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente chiamate alle API di assimilazione in streaming.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

## Creare una connessione

Una connessione specifica l&#39;origine e contiene le informazioni necessarie per rendere il flusso compatibile con le API di assimilazione in streaming.

**Formato API**

```http
POST /flowservice/connections
```

**Richiesta**

>[!NOTE]
>
>I valori per l&#39;elenco `providerId` e per l&#39;evento `connectionSpec` devono **** essere utilizzati come mostrato nell&#39;esempio, in quanto sono ciò che specifica all&#39;API che si sta creando una connessione di streaming per l&#39;assimilazione in streaming.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample name",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection",
             "authenticationRequired": true
         }
     }
 }
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 con i dettagli della nuova connessione creata.

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | La `id` nuova connessione appena creata. In questo caso si farà riferimento a `{CONNECTION_ID}`. |
| `etag` | Identificatore assegnato alla connessione, che specifica la revisione della connessione. |

## Ottieni URL raccolta dati

Con la connessione creata, ora puoi recuperare l&#39;URL di raccolta dati.

**Formato API**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | Il `id` valore della connessione precedentemente creata. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con informazioni dettagliate sulla connessione richiesta. L&#39;URL di raccolta dati viene creato automaticamente con la connessione e può essere recuperato utilizzando il `inletUrl` valore.

```json
{
    "items": [
        {
            "createdAt": 1583971856947,
            "updatedAt": 1583971856947,
            "createdBy": "{API_KEY}",
            "updatedBy": "{API_KEY}",
            "createdClient": "{USER_ID}",
            "updatedClient": "{USER_ID}",
            "id": "77a05521-91d6-451c-a055-2191d6851c34",
            "name": "Another new sample connection (Experience Event)",
            "description": "Sample description",
            "connectionSpec": {
                "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Streaming Connection",
                "params": {
                    "sourceId": "Sample connection (ExperienceEvent)",
                    "inletUrl": "https://dcs.adobedc.net/collection/a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "inletId": "a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "dataType": "xdm",
                    "name": "Sample connection (ExperienceEvent)"
                }
            },
            "version": "\"56008aee-0000-0200-0000-5e697e150000\"",
            "etag": "\"56008aee-0000-0200-0000-5e697e150000\""
        }
    ]
}
```

## Passaggi successivi

Dopo aver creato una connessione di streaming autenticata, è possibile trasmettere in streaming le serie temporali o registrare i dati, in modo da acquisire i dati all&#39;interno [!DNL Platform]. Per informazioni su come eseguire lo streaming dei dati delle serie temporali [!DNL Platform], consulta l’esercitazione [sui dati delle serie temporali in](./streaming-time-series-data.md)streaming. Per informazioni su come eseguire lo streaming dei dati dei record, [!DNL Platform]passare all&#39;esercitazione [sui dati dei record in](./streaming-record-data.md)streaming.

## Appendice

Questa sezione fornisce informazioni supplementari sulle connessioni in streaming autenticate.

### Invio di messaggi a una connessione in streaming autenticata

Se l’autenticazione di una connessione in streaming è abilitata, il client dovrà aggiungere l’ `Authorization` intestazione alla propria richiesta.

Se l’ `Authorization` intestazione non è presente o viene inviato un token di accesso non valido/scaduto, viene restituita una risposta non autorizzata HTTP 401 con una risposta simile come segue:

**Risposta**

```json
{
    "type": "https://ns.adobe.com/adobecloud/problem/data-collection-service-authorization",
    "status": "401",
    "title": "Authorization",
    "report": {
        "message": "[id] Ims service token is empty"
    }
}
```
