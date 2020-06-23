---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Valutazione di un segmento
topic: tutorial
translation-type: tm+mt
source-git-commit: 822f43b139b68b96b02f9a5fe0549736b2524ab7
workflow-type: tm+mt
source-wordcount: '2841'
ht-degree: 1%

---


# Valutazione e accesso ai risultati dei segmenti

Questo documento fornisce un&#39;esercitazione per valutare i segmenti e accedere ai risultati dei segmenti utilizzando l&#39;API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)Segmentazione.

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei vari servizi di Adobe Experience Platform  coinvolti nella creazione di segmenti di pubblico. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [Profilo](../../profile/home.md)cliente in tempo reale: Fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
- [servizio](../home.md)di segmentazione Adobe Experience Platform: Consente di creare segmenti di pubblico dai dati del profilo cliente in tempo reale.
- [Experience Data Model (XDM)](../../xdm/home.md): Framework standard con cui Platform organizza i dati sull&#39;esperienza dei clienti.
- [Sandbox](../../sandboxes/home.md):  Experience Platform fornisce sandbox virtuali che dividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

### Intestazioni necessarie

Questa esercitazione richiede anche di aver completato l&#39;esercitazione [di](../../tutorials/authentication.md) autenticazione per effettuare correttamente le chiamate alle API Platform. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte  chiamate API Experience Platform, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in  Experience Platform sono isolate in sandbox virtuali specifiche. Le richieste alle API Platform richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Per ulteriori informazioni sulle sandbox in Platform, consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste POST, PUT e PATCH richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

## Valutazione di un segmento

Dopo aver sviluppato, testato e salvato la definizione del segmento, puoi valutare il segmento tramite una valutazione programmata o su richiesta.

[La valutazione](#scheduled-evaluation) pianificata (nota anche come &quot;segmentazione pianificata&quot;) consente di creare una pianificazione periodica per l’esecuzione di un processo di esportazione in un momento specifico, mentre la valutazione [](#on-demand-evaluation) su richiesta comporta la creazione di un processo segmento per creare immediatamente l’audience. Di seguito sono descritti i passaggi da seguire per ciascuno di essi.

Se non hai ancora completato l’esercitazione [Crea un segmento utilizzando l’esercitazione API](./create-a-segment.md) Profilo cliente in tempo reale o hai creato una definizione di segmento utilizzando [Segment Builder](../ui/overview.md), effettua questa operazione prima di continuare con questa esercitazione.

## Valutazione programmata {#scheduled-evaulation}

Mediante la valutazione pianificata, l’organizzazione IMS può creare una pianificazione periodica per eseguire automaticamente i processi di esportazione.

>[!NOTE] La valutazione pianificata può essere abilitata per le sandbox con un massimo di cinque (5) criteri di unione per il profilo individuale XDM. Se l&#39;organizzazione dispone di più di cinque criteri di unione per il profilo individuale XDM all&#39;interno di un unico ambiente sandbox, non sarà possibile utilizzare la valutazione pianificata.

### Creare una pianificazione

Effettuando una richiesta POST all&#39; `/config/schedules` endpoint, potete creare una pianificazione e includere l&#39;ora specifica in cui deve essere attivata la pianificazione.

**Formato API**

```http
POST /config/schedules
```

**Richiesta**

La richiesta seguente crea una nuova pianificazione in base alle specifiche fornite nel payload.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "{SCHEDULE_NAME}",
        "type": "batch_segmentation",
        "properties": {
            "segments": ["*"]
        },
        "schedule": "0 0 1 * * ?",
        "state": "inactive"
        }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `name` | **(Obbligatorio)** Nome della pianificazione. Deve essere una stringa. |
| `type` | **(Obbligatorio)** Il tipo di processo in formato stringa. I tipi supportati sono `batch_segmentation` e `export`. |
| `properties` | **(Obbligatorio)** Un oggetto contenente proprietà aggiuntive correlate alla pianificazione. |
| `properties.segments` | **(Obbligatorio se`type`è uguale a`batch_segmentation`)** L&#39;utilizzo di `["*"]` assicura che tutti i segmenti siano inclusi. |
| `schedule` | **(Obbligatorio)** Una stringa contenente la pianificazione del processo. È possibile pianificare l’esecuzione dei processi solo una volta al giorno, pertanto non è possibile pianificare l’esecuzione di un processo più volte durante un periodo di 24 ore. L’esempio mostrato (`0 0 1 * * ?`) indica che il processo viene attivato ogni giorno alle 1:00:00 UTC. Per ulteriori informazioni, consulta la documentazione relativa al formato [delle espressioni](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron. |
| `state` | *(Facoltativo)* Stringa contenente lo stato di pianificazione. Valori disponibili: `active` e `inactive`. Il valore predefinito è `inactive`. Un&#39;organizzazione IMS può creare una sola pianificazione. I passaggi per aggiornare la pianificazione sono disponibili più avanti in questa esercitazione. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova pianificazione creata.

```json
{
    "id": "cd585edf-962d-420d-94ad-3be03e619ac2",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

### Attivare una pianificazione

Per impostazione predefinita, una pianificazione è inattiva quando viene creata, a meno che la `state` proprietà non sia impostata `active` nel corpo della richiesta di creazione (POST). Potete abilitare una pianificazione (impostate `state` su `active`) eseguendo una richiesta PATCH all&#39; `/config/schedules` endpoint e includendo l&#39;ID della pianificazione nel percorso.

**Formato API**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Richiesta**

La richiesta seguente utilizza la formattazione [](http://jsonpatch.com/) JSON Patch per aggiornare la `state` pianificazione a `active`.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "add",
          "path": "/state",
          "value": "active"
        }
      ]'
```

**Risposta**

Un aggiornamento riuscito restituisce un corpo di risposta vuoto e lo stato HTTP 204 (nessun contenuto).

La stessa operazione può essere utilizzata per disattivare una pianificazione sostituendo il &quot;valore&quot; nella richiesta precedente con &quot;inattivo&quot;.

### Aggiornamento dell&#39;ora di pianificazione

È possibile aggiornare i tempi di programmazione eseguendo una richiesta PATCH all&#39; `/config/schedules` endpoint e includendo l&#39;ID della pianificazione nel percorso.

**Formato API**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Richiesta**

Nella richiesta seguente viene utilizzata la formattazione [della patch](http://jsonpatch.com/) JSON per aggiornare l&#39;espressione [](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron per la pianificazione. In questo esempio, la pianificazione ora viene attivata alle 10:15:00 UTC.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "add",
          "path": "/schedule",
          "value": "0 15 10 * * ?"
        }
      ]'
```

**Risposta**

Un aggiornamento riuscito restituisce un corpo di risposta vuoto e lo stato HTTP 204 (nessun contenuto).

## Valutazione su richiesta

La valutazione su richiesta consente di creare un processo di segmento per generare un segmento di pubblico ogni volta che lo desiderate. A differenza della valutazione pianificata, ciò si verificherà solo se richiesto e non ricorrente.

### Creazione di un processo di segmento

Un processo di segmento è un processo asincrono che crea un nuovo segmento di pubblico. Fa riferimento a una definizione di segmento, nonché a qualsiasi criterio di unione che controlla in che modo il profilo cliente in tempo reale unisce gli attributi sovrapposti nei frammenti di profilo. Quando un processo del segmento viene completato correttamente, potete raccogliere varie informazioni sul segmento, ad esempio eventuali errori che si sono verificati durante l&#39;elaborazione e le dimensioni finali del pubblico.

Puoi creare un nuovo processo per segmenti effettuando una richiesta POST all’ `/segment/jobs` endpoint nell’API del profilo cliente in tempo reale.

**Formato API**

```http
POST /segment/jobs
```

**Richiesta**

La richiesta seguente crea un nuovo processo segmento in base alle definizioni dei due segmenti fornite nel payload.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "segmentId" : "42f49f2d-edb0-474f-b29d-2799d89cd5a6"
        },
        {
          "segmentId" : "54a20f19-9a0w-293a-9b82-409b1p3v0192"
        }
    ]'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `segmentId` | Identificatore di una definizione di segmento da cui generare l&#39;audience. È necessario fornire almeno un ID segmento nell&#39;array payload. |

**Risposta**

Una risposta di successo restituisce i dettagli del processo del segmento appena creato, incluso il relativo valore di sola lettura generato dal sistema `id`che è univoco per questo processo del segmento.

```json
{
    "profileInstanceId": "ups",
    "computeJobId": 1,
    "id": "b0f99dde-6d3b-4d92-aa92-28072ded71a0",
    "status": "PROCESSING",
    "segments": [
        {
            "segmentId": "42f49f2d-edb0-474f-b29d-2799d89cd5a6",
            "segment": {
                "id": "42f49f2d-edb0-474f-b29d-2799d89cd5a6",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "mpid1",
                    "version": 1
                }
            }
        },
        {
            "segmentId": "54a20f19-9a0w-293a-9b82-409b1p3v0192",
            "segment": {
                "id": "54a20f19-9a0w-293a-9b82-409b1p3v0192",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "mpid1",
                    "version": 1
                }
            }
        }
    ],
    "updateTime": 1533581808162,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1533581808162,
    "_links": {
        "cancel": {
            "href": "/segment/jobs/b0f99dde-6d3b-4d92-aa92-28072ded71a0",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/b0f99dde-6d3b-4d92-aa92-28072ded71a0",
            "method": "GET"
        }
    }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | Identificatore del nuovo processo del segmento, utilizzato a scopo di ricerca. |
| `status` | Lo stato corrente del processo del segmento. Sarà &quot;PROCESSING&quot; fino al completamento dell&#39;elaborazione, al punto in cui diventa &quot;SUCCEEDED&quot; o &quot;FAILED&quot;. |

### Cerca stato processo segmento

È possibile utilizzare l&#39; `id` per un processo segmento specifico per eseguire una richiesta di ricerca (GET) al fine di visualizzare lo stato corrente del processo.

**Formato API**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SEGMENT_JOB_ID}` | Indica `id` il processo del segmento a cui si desidera accedere. |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

Una risposta corretta restituisce i dettagli del processo di segmentazione e fornisce informazioni diverse a seconda dello stato corrente del processo. Puoi ripetere la richiesta di ricerca fino a `status` raggiungere &quot;SUCCEEDED&quot;, al momento in cui puoi esportare il segmento in un dataset.


```json
{
    "profileInstanceId": "ups",
    "errors": [],
    "computeJobId": 13377,
    "modelName": "_xdm.context.profile",
    "id": "80388706-29fa-40d3-81cf-a297d0224ad9",
    "status": "SUCCEEDED",
    "segments": [
        {
            "segmentId": "b560a09a-de85-4a1c-8477-2f3da1d9e86b",
            "segment": {
                "id": "b560a09a-de85-4a1c-8477-2f3da1d9e86b",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
                    "version": 1
                }
            }
        }
    ],
    "requestId": "prgu92v4VNvsGuuXticcsqX96UXGjXtS",
    "computeGatewayJobId": "a7c33b77-3aeb-497f-bc88-807915c57b5f",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1547063631503,
            "endTimeInMs": 1547063731181,
            "totalTimeInMs": 99678
        },
        "profileSegmentationTime": {
            "startTimeInMs": 1547063669001,
            "endTimeInMs": 1547063720887,
            "totalTimeInMs": 51886
        },
        "segmentedProfileCounter": {
            "ca763983-5572-4ea4-809c-b7dff7e0d79b": 4195,
            "251e3a1f-645c-4444-836b-18e6b668bdf8": 0,
            "3da8bad9-29fb-40e0-b39e-f80322e964de": 0,
            "30230300-ccf1-48ad-8012-c5563a007069": 0
        },
        "segmentedProfileByNamespaceCounter": {
            "ca763983-5572-4ea4-809c-b7dff7e0d79b": {
                "email": 4195
            },
            "251e3a1f-645c-4444-836b-18e6b668bdf8": {},
            "3da8bad9-29fb-40e0-b39e-f80322e964de": {},
            "30230300-ccf1-48ad-8012-c5563a007069": {}
        }     
    },
    "updateTime": 1547063731181,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1547063631503,
    "_links": {
        "cancel": {
            "href": "/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9",
            "method": "GET"
        }
    }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `segmentedProfileCounter` | Numero totale di profili uniti idonei per il segmento. |
| `segmentedProfileByNamespaceCounter` | Una suddivisione dei profili idonei per il segmento in base al codice dello spazio dei nomi dell&#39;identità. Nella panoramica [](../../identity-service/namespaces.md)dello spazio nomi identità è possibile trovare un elenco di codici dello spazio nomi identità. |

## Interpreta i risultati del segmento

Quando i processi del segmento vengono eseguiti correttamente, la `segmentMembership` mappa viene aggiornata per ogni profilo incluso nel segmento. `segmentMembership` memorizza inoltre tutti i segmenti di pubblico già valutati che vengono trasferiti in Platform, consentendo l&#39;integrazione con altre soluzioni come  Adobe Audience Manager.

L&#39;esempio seguente mostra l&#39;aspetto `segmentMembership` dell&#39;attributo per ciascun record di profilo:

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "existing"
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "status": "exited"
      }
    }
  }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `lastQualificationTime` | La marca temporale in cui è stata rilasciata l&#39;asserzione dell&#39;appartenenza al segmento e il profilo è entrato o uscito dal segmento. |
| `status` | Stato della partecipazione al segmento come parte della richiesta corrente. Deve essere uguale a uno dei seguenti valori noti: <ul><li>`existing`: L&#39;entità continua a trovarsi nel segmento.</li><li>`realized`: L&#39;entità sta entrando nel segmento.</li><li>`exited`: L&#39;entità sta uscendo dal segmento.</li></ul> |

## Accesso ai risultati del segmento

È possibile accedere ai risultati di un processo segmento in uno dei due modi seguenti: puoi accedere a singoli profili o esportare un&#39;intera audience in un dataset.

Le sezioni seguenti descrivono queste opzioni in modo più dettagliato.

## Cercare un profilo

Se conosci il profilo specifico a cui vuoi accedere, puoi farlo utilizzando l&#39;API Profilo cliente in tempo reale. I passaggi completi per accedere ai singoli profili sono disponibili nei dati [Access Real-time Customer Profile (Profilo cliente in tempo reale) tramite l&#39;esercitazione Profile API](../../profile/api/entities.md) (API profilo).

## Esportare un segmento {#export}

Dopo che un processo di segmentazione è stato completato correttamente (il valore dell&#39; `status` attributo è &quot;SUCCEEDED&quot;), potete esportare il pubblico in un set di dati in cui è possibile accedervi e agire.

Per esportare il pubblico sono necessari i seguenti passaggi:

- [Crea un set di dati](#create-a-target-dataset) di destinazione: crea il set di dati per contenere i membri del pubblico.
- [Genera profili di pubblico nel set di dati](#generate-profiles-for-audience-members) - Compilare il set di dati con i singoli profili XDM in base ai risultati di un processo di segmento.
- [Monitorare l&#39;avanzamento](#monitor-export-progress) dell&#39;esportazione - Verificare l&#39;avanzamento corrente del processo di esportazione.
- [Leggi i dati](#next-steps) sul pubblico - Recupera i singoli profili XDM risultanti che rappresentano i membri del pubblico.

### Creare un dataset di destinazione

Quando si esporta un&#39;audience, è necessario creare prima un set di dati di destinazione. È importante che il set di dati sia configurato correttamente per garantire il successo dell&#39;esportazione.

Una delle considerazioni chiave è lo schema su cui si basa il dataset (`schemaRef.id` nella richiesta di esempio API di seguito). Per esportare un segmento, il set di dati deve essere basato sullo schema unionale profilo singolo XDM (`https://ns.adobe.com/xdm/context/profile__union`). Uno schema unione è uno schema di sola lettura generato dal sistema che aggrega i campi degli schemi che condividono la stessa classe, in questo caso si tratta della classe XDM Singolo profilo. Per ulteriori informazioni sugli schemi di visualizzazione dell&#39;unione, vedere la sezione Profilo cliente in tempo [reale della guida](../../xdm/api/getting-started.md)per gli sviluppatori del Registro di sistema dello schema.

Esistono due modi per creare il set di dati necessario:

- **Utilizzo delle API:** I passaggi che seguono in questa esercitazione descrivono come creare un dataset che faccia riferimento allo schema dell&#39;unione dei profili XDM utilizzando l&#39;API Catalog.
- **Utilizzo dell’interfaccia utente:** Per utilizzare l&#39;interfaccia utente del Adobe Experience Platform  per creare un dataset che faccia riferimento allo schema dell&#39;unione, seguire i passaggi dell&#39;esercitazione [](../ui/overview.md) dell&#39;interfaccia utente, quindi tornare a questa esercitazione per procedere con i passaggi necessari per [generare i profili](#generate-xdm-profiles-for-audience-members)dell&#39;audience.

Se disponete già di un set di dati compatibile e ne conoscete l’ID, potete procedere direttamente alla fase di [generazione dei profili](#generate-xdm-profiles-for-audience-members)di audience.

**Formato API**

```http
POST /dataSets
```

**Richiesta**

La richiesta seguente crea un nuovo dataset, fornendo i parametri di configurazione nel payload.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `name` | Un nome descrittivo per il set di dati. |
| `schemaRef.id` | ID della visualizzazione unione (schema) a cui sarà associato il set di dati. |
| `fileDescription.persisted` | Un valore booleano che, se impostato su `true`, consente al dataset di persistere nella visualizzazione unione. |

**Risposta**

Una risposta corretta restituisce un array contenente l&#39;ID univoco generato dal sistema di sola lettura del set di dati appena creato. Per esportare correttamente i membri dell&#39;audience è necessario un ID dataset configurato correttamente.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Generazione di profili per i membri dell&#39;audience

Una volta ottenuto un dataset persistente nell&#39;unione, potete creare un processo di esportazione per mantenere i membri dell&#39;audience nel dataset effettuando una richiesta POST all&#39; `/export/jobs` endpoint nell&#39;API del profilo cliente in tempo reale e fornendo l&#39;ID del set di dati e le informazioni del segmento per i segmenti che desiderate esportare.

**Formato API**

```http
POST /export/jobs
```

**Richiesta**

La richiesta seguente crea un nuovo processo di esportazione, fornendo i parametri di configurazione nel payload.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ],
      "segmentQualificationTime": {
            "startTime": "2019-09-01T00:00:00Z",
            "endTime": "2019-09-02T00:00:00Z"
        },
      "fromIngestTimestamp": "2018-10-25T13:22:04-07:00",
      "emptyProfiles": false
    },
    "additionalFields" : {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": true
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `fields` | *(Facoltativo)* Limita i campi di dati da includere nell’esportazione solo a quelli forniti in questo parametro. Lo stesso parametro è disponibile anche quando si crea un segmento, pertanto i campi nel segmento potrebbero essere già stati filtrati. Se si omette questo valore, tutti i campi verranno inclusi nei dati esportati |
| `mergePolicy` | *(Facoltativo)* Specifica il criterio di unione da applicare ai dati esportati. Includete questo parametro quando vi sono più segmenti da esportare. Se si omette questo valore, il servizio di esportazione utilizzerà il criterio di unione fornito dal segmento. |
| `mergePolicy.id` | ID del criterio di unione |
| `mergePolicy.version` | Versione specifica del criterio di unione da utilizzare. Se si omette questo valore, per impostazione predefinita verrà utilizzata la versione più recente. |
| `filter` | *(Facoltativo)* Specifica uno o più dei seguenti filtri da applicare al segmento prima dell&#39;esportazione: |
| `filter.segments` | *(Facoltativo)* Specifica i segmenti da esportare. Se si omette questo valore, verranno esportati tutti i dati di tutti i profili. Accetta un array di oggetti segmento, ciascuno dei quali contiene i campi seguenti: |
| `filter.segments.segmentId` | **(Obbligatorio se si utilizza`segments`)** ID segmento per i profili da esportare. |
| `filter.segments.segmentNs` | *(Facoltativo)* Spazio dei nomi del segmento per il dato `segmentID`. |
| `filter.segments.status` | *(Facoltativo)* Un array di stringhe che fornisce un filtro di stato per l&#39;oggetto `segmentID`. Per impostazione predefinita, `status` il valore `["realized", "existing"]` rappresenta tutti i profili che rientrano nel segmento al momento corrente. I valori possibili sono: `"realized"`, `"existing"`e `"exited"`. |
| `filter.segmentQualificationTime` | *(Facoltativo)* Filtra in base al tempo di qualificazione del segmento. È possibile specificare l&#39;ora di inizio e/o di fine. |
| `filter.segmentQualificationTime.startTime` | *(Facoltativo)* Ora di inizio qualifica segmento per un ID segmento per un dato stato. Non viene fornito, non verrà applicato alcun filtro all&#39;ora di inizio per la qualifica ID segmento. La marca temporale deve essere fornita in formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.segmentQualificationTime.endTime` | *(Facoltativo)* Tempo di fine qualifica segmento per un ID segmento per un dato stato. Non viene fornito, non verrà applicato alcun filtro all&#39;ora di fine per la qualifica di ID segmento. La marca temporale deve essere fornita in formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.fromIngestTimestamp` | *(Facoltativo)* Limita i profili esportati a includere solo quelli che sono stati aggiornati dopo questa marca temporale. La marca temporale deve essere fornita in formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.fromIngestTimestamp` per **i profili**, se forniti | Include tutti i profili uniti in cui la marca temporale aggiornata unita è maggiore della marca temporale specificata. Supporta `greater_than` l&#39;operando. |
| `filter.fromTimestamp` per gli eventi | Tutti gli eventi acquisiti dopo questa marca temporale verranno esportati in base al risultato del profilo risultante. Questo non è il momento dell’evento stesso ma il momento dell’inserimento degli eventi. |
| `filter.emptyProfiles` | *(Facoltativo)* Valore Boolean. I profili possono contenere record Profilo, record ExperienceEvent o entrambi. I profili senza record Profilo e solo i record ExperienceEvent sono denominati &quot;emptyProfiles&quot;. Per esportare tutti i profili nell’archivio profili, inclusi i &quot;emptyProfiles&quot;, imposta il valore di `emptyProfiles` su `true`. Se `emptyProfiles` è impostato su `false`, vengono esportati solo i profili con record Profilo nello store. Per impostazione predefinita, se `emptyProfiles` l’attributo non è incluso, vengono esportati solo i profili contenenti i record Profilo. |
| `additionalFields.eventList` | *(Facoltativo)* Controlla i campi evento delle serie temporali esportati per oggetti secondari o associati fornendo una o più delle seguenti impostazioni: |
| `additionalFields.eventList.fields` | Controllare i campi da esportare. |
| `additionalFields.eventList.filter` | Specifica i criteri che limitano i risultati inclusi dagli oggetti associati. Si attende un valore minimo richiesto per l&#39;esportazione, in genere una data. |
| `additionalFields.eventList.filter.fromIngestTimestamp` | Filtra gli eventi delle serie temporali a quelli che sono stati acquisiti dopo la marca temporale fornita. Questo non è il momento dell’evento stesso ma il momento dell’inserimento degli eventi. |
| `destination` | **(Obbligatorio)** Informazioni sulla destinazione per i dati esportati |
| `destination.datasetId` | **(Obbligatorio)** L&#39;ID del set di dati in cui devono essere esportati i dati. |
| `destination.segmentPerBatch` | *(Facoltativo)* Un valore booleano che, se non viene fornito, utilizza per impostazione predefinita `false`. Un valore di `false` esporta tutti gli ID segmento in un unico ID batch. Un valore di `true` esportazione consente di esportare un ID segmento in un ID batch. Tenete presente che l’impostazione del valore da assegnare `true` può influire sulle prestazioni di esportazione batch. |
| `schema.name` | **(Obbligatorio)** Il nome dello schema associato al dataset in cui devono essere esportati i dati. |

**Risposta**

Una risposta corretta restituisce un set di dati compilato con profili idonei per l’ultima esecuzione completata del processo del segmento. Sono stati rimossi tutti i profili che possono essere esistiti in precedenza nel set di dati ma che non erano idonei per il segmento durante l’ultima esecuzione completata del processo del segmento.

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "NEW",
    "requestId": "IwkVcD4RupdSmX376OBVORvcvTdA4ypN",
    "computeGatewayJobId": {},
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1559674261657
        }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

Se non `destination.segmentPerBatch` fosse stato incluso nella richiesta (se non presente, è `false`il valore predefinito) o se il valore fosse stato impostato su `false`, l&#39; `destination` oggetto nella risposta precedente non avrebbe una `batches` matrice e ne avrebbe invece inclusa solo una `batchId`, come mostrato di seguito. Tale batch singolo includerebbe tutti gli ID del segmento, mentre la risposta precedente mostra un ID segmento singolo per ID batch.

```json
  "destination": {
    "datasetId": "5cf6bcf79ecc7c14530fe436",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
  }
```

### Elenca tutti i processi di esportazione

Potete restituire un elenco di tutti i processi di esportazione per una particolare organizzazione IMS eseguendo una richiesta GET all&#39; `export/jobs` endpoint. La richiesta supporta anche i parametri di query `limit` e `offset`, come mostrato di seguito.

**Formato API**

```http
GET /export/jobs
GET /export/jobs?limit=4
GET /export/jobs?offset=2
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `limit` | Specificare il numero di record da restituire. |
| `offset` | Consente di scostare la pagina dei risultati da restituire in base al numero fornito. |


**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

La risposta include un `records` oggetto contenente i processi di esportazione creati dall&#39;organizzazione IMS.

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
      "filter": {
          "segments": [
              {
                  "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff"
              }
          ]
      },
      "id": 726,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "timestampOrdered-none-mp",
          "version": 1
      },
      "status": "SUCCEEDED",
      "requestId": "d995479c-8a08-4240-903b-af469c67be1f",
      "computeGatewayJobId": {
          "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
          "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538615973895,
              "endTimeInMs": 1538616233239,
              "totalTimeInMs": 259344
          },
          "profileExportTime": {
              "startTimeInMs": 1538616067445,
              "endTimeInMs": 1538616139576,
              "totalTimeInMs": 72131
          },
          "aCPDatasetWriteTime": {
              "startTimeInMs": 1538616195172,
              "endTimeInMs": 1538616195715,
              "totalTimeInMs": 543
          }
      },
      "destination": {
          "datasetId": "5b7c86968f7b6501e21ba9df",
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
      },
      "updateTime": 1538616233239,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538615973895
    },
    {
      "profileInstanceId": "test_xdm_latest_profile_20_e2e_1538573005395",
      "errors": [
        {
          "code": "0090000009",
          "msg": "Error writing profiles to output path 'adl://va7devprofilesnapshot.azuredatalakestore.net/snapshot/722'",
          "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger" 
        },
        {
          "code": "unknown",
          "msg": "Job aborted.",
          "callStack": "org.apache.spark.SparkException: Job aborted."
        }
      ],
      "jobType": "BATCH",
      "filter": {
        "segments": [
            {
                "segmentId": "7a93d2ff-a220-4bae-9a4e-5f3c35032be3"
            }
        ]
      },
      "id": 722,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "7972e3d6-96ea-4ece-9627-cbfd62709c5d",
          "version": 1
      },
      "status": "FAILED",
      "requestId": "KbOAsV7HXmdg262lc4yZZhoml27UWXPZ",
      "computeGatewayJobId": {
          "exportJob": "15971e0f-317c-4390-9038-1a0498eb356f"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538573416687,
              "endTimeInMs": 1538573922551,
              "totalTimeInMs": 505864
          },
          "profileExportTime": {
              "startTimeInMs": 1538573872211,
              "endTimeInMs": 1538573918809,
              "totalTimeInMs": 46598
          }
      },
      "destination": {
          "datasetId": "5bb4c46757920712f924a3eb",
          "batchId": ""
      },
      "updateTime": 1538573922551,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538573416687
    }
  ],
  "page": {
      "sortField": "createdTime",
      "sort": "desc",
      "pageOffset": "1538573416687_722",
      "pageSize": 2
  },
  "link": {
      "next": "/export/jobs/?limit=2&offset=1538573416687_722"
  }
}
```

### Monitorare l&#39;avanzamento dell&#39;esportazione

Come processo di esportazione, potete controllarne lo stato eseguendo una richiesta GET all&#39; `/export/jobs` endpoint e includendo nel percorso `id` il processo di esportazione. Il processo di esportazione viene completato una volta che il `status` campo restituisce il valore &quot;SUCCEEDED&quot;.

**Formato API**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | Indica `id` il processo di esportazione a cui si desidera accedere. |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "SUCCEEDED",
    "requestId": "YwMt1H8QbVlGT2pzyxgwFHTwzpMbHrTq",
    "computeGatewayJobId": {
      "exportJob": "305a2e5c-2cf3-4746-9b3d-3c5af0437754",
      "pushJob": "963f275e-91a3-4fa1-8417-d2ca00b16a8a"
    },
    "metrics": {
      "totalTime": {
        "startTimeInMs": 1547053539564,
        "endTimeInMs": 1547054743929,
        "totalTimeInMs": 1204365
      },
      "profileExportTime": {
        "startTimeInMs": 1547053667591,
        "endTimeInMs": 1547053778195,
        "totalTimeInMs": 110604
      },
      "aCPDatasetWriteTime": {
        "startTimeInMs": 1547054660416,
        "endTimeInMs": 1547054698918,
        "totalTimeInMs": 38502
      }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `batchId` | Identificatore dei batch creati da un&#39;esportazione riuscita, da utilizzare a scopo di ricerca durante la lettura dei dati dell&#39;audience. |

## Passaggi successivi

Una volta completata l&#39;esportazione, i dati sono disponibili all&#39;interno del Data Lake in  Experience Platform. Potete quindi utilizzare l&#39;API [di accesso ai](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) dati per accedere ai dati utilizzando l&#39; `batchId` API associata all&#39;esportazione. A seconda della dimensione del segmento, i dati possono essere in blocchi e il batch può essere composto da diversi file.

Per istruzioni dettagliate su come utilizzare l&#39;API di accesso ai dati per accedere e scaricare file batch, segui l&#39;esercitazione [sull&#39;accesso ai](../../data-access/tutorials/dataset-data.md)dati.

È inoltre possibile accedere ai dati del segmento esportati correttamente utilizzando  Adobe Experience Platform Query Service. Utilizzando l&#39;interfaccia utente o l&#39;API RESTful, Query Service consente di scrivere, convalidare ed eseguire query sui dati all&#39;interno del Data Lake.

Per ulteriori informazioni su come eseguire query sui dati del pubblico, consulta la documentazione [del servizio](../../query-service/home.md)Query.
