---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentazione in streaming
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# Valutazione degli eventi in tempo reale con segmentazione in streaming (versione beta)

>[!NOTE] La segmentazione in streaming è una funzione beta e sarà disponibile su richiesta.

La segmentazione in streaming (nota anche come valutazione continua delle query) consente di valutare istantaneamente un cliente non appena un evento entra in un particolare gruppo di segmenti. Grazie a questa funzionalità, ora è possibile valutare la maggior parte delle regole del segmento in quanto i dati vengono passati in Adobe Experience Platform, il che significa che l&#39;appartenenza al segmento verrà mantenuta aggiornata senza eseguire processi di segmentazione pianificati.

![](../images/api/streaming-segment-evaluation.png)

## Introduzione

Questa guida per gli sviluppatori richiede una buona conoscenza dei diversi servizi Adobe Experience Platform coinvolti nella segmentazione dei flussi. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [Profilo](../../profile/home.md)cliente in tempo reale: Fornisce un profilo del consumatore unificato in tempo reale, basato su dati aggregati provenienti da più origini.
- [Segmentazione](../home.md): Consente di creare segmenti e audience dai dati del profilo cliente in tempo reale.
- [Experience Data Model (XDM)](../../xdm/home.md): Il framework standardizzato tramite il quale la piattaforma organizza i dati sull&#39;esperienza cliente.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente chiamate alle API della piattaforma.

### Lettura di chiamate API di esempio

Questa guida per gli sviluppatori fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione [come leggere le chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi della piattaforma Experience.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle API della piattaforma, dovete prima completare l&#39;esercitazione [di](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in Experience Platform sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API della piattaforma richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Per ulteriori informazioni sulle sandbox in Piattaforma, consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

Possono essere necessarie intestazioni aggiuntive per completare richieste specifiche. Le intestazioni corrette vengono visualizzate in ciascuno degli esempi contenuti in questo documento. Prestate particolare attenzione alle richieste di esempio al fine di garantire che tutte le intestazioni richieste siano incluse.

### Tipi di query abilitate alla segmentazione in streaming

Nella tabella seguente sono elencati i diversi tipi di query di segmentazione e se supportano o meno la segmentazione in streaming.

| Tipo di query | Query di esempio | Segmentazione in streaming supportata |
| ---------- | ------------ | --------------------------------- |
| Semplicità demografica | &quot;Datemi tutte le persone il cui indirizzo è in Canada.&quot; | Supportato |
| Eventi serie temporali | &quot;Dammi tutte le persone che hanno scaricato Lightroom.&quot; | Supportato |
| Serie temporali e demografiche | &quot;Datemi tutte le persone che vivono in Canada e che hanno fatto un ordine negli ultimi 30 giorni.&quot; | Supportato |
| Assenza di eventi | &quot;Datemi tutte le persone che hanno abbandonato due carrelli separati in due giorni l&#39;una dall&#39;altra&quot;. | Supportato |
| Più entità | &quot;Dammi tutte le persone il cui tipo di adesione è &#39;Esperienza&#39;.&quot; | Non supportato |
| Funzioni PQL avanzate | &quot;Datemi tutti i profili che hanno effettuato un ordine nell&#39;ultima settimana, e includete SKU e Nome per tutti i prodotti acquistati.&quot; | Non supportato |

## Recupera tutti i segmenti abilitati per la segmentazione in streaming

Prima di creare un nuovo segmento abilitato per lo streaming o di aggiornare un segmento esistente per l’attivazione dello streaming, accertatevi di non duplicare le informazioni recuperando un elenco di tutti i segmenti abilitati per lo streaming.

**Formato API**

Per recuperare i segmenti abilitati per lo streaming, è necessario includere il parametro query `evaluationInfo.continuous.enabled=true` nel percorso della richiesta.

```http
GET /segment/definitions?evaluationInfo.continuous.enabled=true
```

**Richiesta**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.continuous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME'
```

**Risposta**

Una risposta corretta restituisce un array di segmenti nell’organizzazione IMS che sono abilitati per la segmentazione in streaming.

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": " People who are NOT on their homepage ",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = false"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572029711000,
            "updateEpoch": 1572029712000,
            "updateTime": 1572029712000
        },
        {
            "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "Homepage_continuous",
            "description": "People who are on their homepage - continuous",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572021085000,
            "updateEpoch": 1572021086000,
            "updateTime": 1572021086000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

## Creare un segmento abilitato per lo streaming

Dopo aver confermato che il segmento da creare non esiste già, potete creare un nuovo segmento abilitato per la segmentazione in streaming.

**Formato API**

```http
POST /segment/definitions
```

**Richiesta**

La richiesta seguente crea un nuovo segmento abilitato per la segmentazione in streaming. Note that the `continuous` section is set to `enabled: true`.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'  \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    }
}'
```

>[!NOTE] Si tratta di una richiesta standard &quot;create a segment&quot;, con il parametro aggiunto della `continuous` sezione impostato su `enabled: true`. Per ulteriori informazioni sulla creazione di una definizione di segmento, consulta la documentazione sulla creazione [di](../tutorials/create-a-segment.md)segmenti.

**Risposta**

Una risposta corretta restituisce i dettagli della definizione del segmento abilitata per lo streaming appena creata.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true,
                   },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1572021085000,
    "updateEpoch": 1572021086000,
    "updateTime": 1572021086000
}
```

## Abilita un segmento esistente per la segmentazione in streaming

Puoi abilitare un segmento esistente per la segmentazione in streaming fornendo l’ID della definizione del segmento nel percorso di una richiesta PATCH. Inoltre, il payload di questa richiesta PATCH deve includere tutti i dettagli della definizione del segmento esistente, a cui è possibile accedere eseguendo una richiesta GET alla definizione del segmento in questione.

### Cerca una definizione di segmento esistente

Per cercare una definizione di segmento esistente, devi fornire il relativo ID nel percorso di una richiesta GET.

**Formato API**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | ID della definizione del segmento da cercare. |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/15063cb-2da8-4851-a2e2-bf59ddd2f004\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituirà i dettagli della definizione del segmento richiesta.

```json
{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "sandbox": {
        "sandboxId": "",
        "sandboxName": "",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "mergePolicyId": "50de2f9c-990c-4b96-945f-9570337ffe6d",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    }
}
```

>[!NOTE] Per la richiesta successiva, saranno necessari i dettagli completi della definizione del segmento che sono stati restituiti in questa risposta. Copiate i dettagli di questa risposta da utilizzare nel corpo della richiesta successiva.

### Abilita il segmento esistente per la segmentazione in streaming

Ora che conoscete i dettagli del segmento da aggiornare, potete eseguire una richiesta PATCH per aggiornare il segmento per abilitare la segmentazione in streaming.

**Formato API**

```http
PATCH /segment/definitions/{SEGMENT_DEFINITION_ID}
```

**Richiesta**

Il payload della richiesta seguente fornisce i dettagli della definizione del segmento (ottenuta nel passaggio [](#look-up-an-existing-segment-definition)precedente), e lo aggiorna modificandone `continuous.enabled` la proprietà in `true`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/segment/definitions/15063cb-2da8-4851-a2e2-bf59ddd2f004 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -d '{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "mergePolicyId": "50de2f9c-990c-4b96-945f-9570337ffe6d",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    }
}'
```

**Risposta**

Una risposta corretta restituisce i dettagli della nuova definizione di segmento aggiornata.

```json
{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "4A21D36B544916100A4C98A7@AdobeOrg",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1572029711000,
    "updateEpoch": 1572029712000,
    "updateTime": 1572029712000
}
```

## Abilita valutazione pianificata

Una volta abilitata la valutazione dello streaming, è necessario creare una baseline (dopodiché il segmento sarà sempre aggiornato). Questa operazione viene eseguita automaticamente dal sistema, tuttavia la valutazione programmata (nota anche come segmentazione pianificata) deve essere attivata prima di poter eseguire la valutazione.

Con la segmentazione pianificata, l’organizzazione IMS può creare una pianificazione periodica per eseguire automaticamente i processi di esportazione per valutare i segmenti.

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
| `properties.segments` | **(Obbligatorio quando`type`è uguale`batch_segmentation`)** L&#39;utilizzo di `["*"]` assicura che tutti i segmenti siano inclusi. |
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

## Passaggi successivi

Ora che hai attivato sia i segmenti nuovi che quelli esistenti per la segmentazione in streaming e hai abilitato la segmentazione pianificata per sviluppare una linea di base ed eseguire valutazioni ricorrenti, puoi iniziare a creare segmenti per la tua organizzazione.

Per informazioni su come eseguire azioni simili e lavorare con segmenti utilizzando l’interfaccia utente di Adobe Experience Platform, consulta la guida [utente di](../ui/overview.md)Segment Builder.