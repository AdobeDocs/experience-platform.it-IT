---
keywords: ' Experience Platform;home;argomenti più diffusi;segmentazione;segmentazione;Segmentazione segmentazione in streaming;Segmentazione in streaming;Segmentazione in streaming;Valutazione continua;'
solution: Experience Platform
title: Segmentazione in streaming
topic: developer guide
description: Questo documento contiene esempi sull’utilizzo della segmentazione in streaming con l’API di segmentazione in streaming.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 1%

---


# Valutazione degli eventi in tempo quasi reale con segmentazione in streaming

>[!NOTE]
>
>Il seguente documento spiega come utilizzare la segmentazione in streaming mediante l&#39;API. Per informazioni sull&#39;utilizzo della segmentazione in streaming tramite l&#39;interfaccia utente, consultate la [guida all&#39;interfaccia utente per la segmentazione in streaming](../ui/streaming-segmentation.md).

La segmentazione in streaming su [!DNL Adobe Experience Platform] consente ai clienti di eseguire la segmentazione in tempo quasi reale, concentrandosi sulla ricchezza dei dati. Con la segmentazione in streaming, la qualifica del segmento ora avviene quando i dati in streaming arrivano in [!DNL Platform], riducendo la necessità di pianificare ed eseguire processi di segmentazione. Grazie a questa funzionalità, ora è possibile valutare la maggior parte delle regole del segmento in quanto i dati vengono passati in [!DNL Platform], il che significa che l&#39;appartenenza al segmento verrà mantenuta aggiornata senza eseguire processi di segmentazione pianificati.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>La segmentazione in streaming può essere utilizzata solo per valutare i dati in streaming in Piattaforma. In altre parole, i dati acquisiti tramite l’assimilazione batch non verranno valutati tramite la segmentazione in streaming e verranno valutati insieme al processo segmentato pianificato ogni sera.

## Introduzione

Questa guida per gli sviluppatori richiede una buona conoscenza dei vari servizi [!DNL Adobe Experience Platform] coinvolti nella segmentazione in streaming. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo del consumatore unificato in tempo reale, basato su dati aggregati provenienti da più origini.
- [[!DNL Segmentation]](../home.md): Consente di creare segmenti e audience dai  [!DNL Real-time Customer Profile] dati.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standard con cui  [!DNL Platform] organizzare i dati relativi all&#39;esperienza dei clienti.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per eseguire correttamente le chiamate alle [!DNL Platform] API.

### Lettura di chiamate API di esempio

Questa guida per gli sviluppatori fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è innanzitutto necessario completare l&#39;esercitazione sull&#39;autenticazione [a2/>. ](https://www.adobe.com/go/platform-api-authentication-en) Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui verrà eseguita l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione di [panoramica sulla sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

Possono essere necessarie intestazioni aggiuntive per completare richieste specifiche. Le intestazioni corrette vengono visualizzate in ciascuno degli esempi contenuti in questo documento. Prestate particolare attenzione alle richieste di esempio al fine di garantire che tutte le intestazioni richieste siano incluse.

### Tipi di query abilitate alla segmentazione in streaming {#streaming-segmentation-query-types}

>[!NOTE]
>
>Per consentire il funzionamento della segmentazione in streaming, è necessario abilitare la segmentazione pianificata per l&#39;organizzazione. Informazioni sull&#39;abilitazione della segmentazione pianificata sono disponibili nella sezione [abilita segmentazione pianificata](#enable-scheduled-segmentation)

Affinché un segmento possa essere valutato utilizzando la segmentazione in streaming, la query deve essere conforme alle seguenti linee guida.

| Tipo di query | Dettagli |
| ---------- | ------- |
| hit in ingresso | Definizione di segmento che fa riferimento a un singolo evento in arrivo senza limitazioni temporali. |
| Hit in arrivo all’interno di una finestra temporale relativa | Definizione di segmento che fa riferimento a un singolo evento in arrivo. |
| Solo profilo | Definizione di segmento che fa riferimento solo a un attributo di profilo. |
| Hit in arrivo che fa riferimento a un profilo | Definizione di segmento che fa riferimento a un singolo evento in arrivo, senza limitazioni temporali, e uno o più attributi di profilo. |
| Hit in arrivo che fa riferimento a un profilo all’interno di una finestra temporale relativa | Definizione di segmento che fa riferimento a un singolo evento in arrivo e a uno o più attributi di profilo. |
| Più eventi che fanno riferimento a un profilo | Qualsiasi definizione di segmento che fa riferimento a più eventi **nelle ultime 24 ore** e (facoltativamente) ha uno o più attributi di profilo. |

Una definizione di segmento **non** sarà abilitata per la segmentazione in streaming nei seguenti scenari:

- La definizione del segmento include segmenti o caratteristiche Adobe Audience Manager (AAM).
- La definizione del segmento include più entità (query con più entità).

Inoltre, durante la segmentazione in streaming si applicano alcune linee guida:

| Tipo di query | Indirizzo |
| ---------- | -------- |
| Query evento singolo | Non ci sono limiti alla finestra di lookback. |
| Query con cronologia eventi | <ul><li>La finestra di lookback è limitata a **un giorno**.</li><li>Tra gli eventi è presente una condizione di ordine di tempo rigoroso **must**.</li><li>Sono supportate le query con almeno un evento negativo. Tuttavia, l&#39;intero evento **non può essere una negazione**.</li></ul> |

## Recupera tutti i segmenti abilitati per la segmentazione in streaming

Puoi ottenere un elenco di tutti i segmenti abilitati per la segmentazione in streaming all&#39;interno dell&#39;organizzazione IMS effettuando una richiesta di GET all&#39;endpoint `/segment/definitions`.

**Formato API**

Per recuperare i segmenti abilitati per lo streaming, è necessario includere il parametro di query `evaluationInfo.continuous.enabled=true` nel percorso della richiesta.

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
  -H 'x-sandbox-name: {SANDBOX_NAME}'
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

Un segmento sarà automaticamente abilitato per lo streaming se corrisponde a uno dei [tipi di segmentazione dello streaming elencati sopra](#streaming-segmentation-query-types).

**Formato API**

```http
POST /segment/definitions
```

**Richiesta**

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
    }
}'
```

>[!NOTE]
>
>Si tratta di una richiesta standard di creazione di un segmento. Per ulteriori informazioni sulla creazione di una definizione di segmento, leggete l&#39;esercitazione su [creazione di un segmento](../tutorials/create-a-segment.md).

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

## Abilita valutazione pianificata {#enable-scheduled-segmentation}

Una volta abilitata la valutazione dello streaming, è necessario creare una baseline (dopodiché il segmento sarà sempre aggiornato). La valutazione pianificata (nota anche come segmentazione pianificata) deve essere attivata prima di tutto per consentire al sistema di eseguire automaticamente le attività di base. Con la segmentazione pianificata, l’organizzazione IMS può aderire a una pianificazione periodica per eseguire automaticamente i processi di esportazione per valutare i segmenti.

>[!NOTE]
>
>La valutazione pianificata può essere abilitata per le sandbox con un massimo di cinque (5) criteri di unione per [!DNL XDM Individual Profile]. Se l&#39;organizzazione dispone di più di cinque criteri di unione per [!DNL XDM Individual Profile] all&#39;interno di un unico ambiente sandbox, non sarà possibile utilizzare la valutazione pianificata.

### Creare una pianificazione

Eseguendo una richiesta POST all&#39;endpoint `/config/schedules`, potete creare una pianificazione e includere l&#39;ora specifica in cui avviare la pianificazione.

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
| `properties.segments` | **(Obbligatorio quando  `type` è uguale a  `batch_segmentation`)** L&#39;utilizzo di  `["*"]` assicura che tutti i segmenti siano inclusi. |
| `schedule` | **(Obbligatorio)** Una stringa contenente la pianificazione del processo. È possibile pianificare l’esecuzione dei processi solo una volta al giorno, pertanto non è possibile pianificare l’esecuzione di un processo più volte durante un periodo di 24 ore. L&#39;esempio mostrato (`0 0 1 * * ?`) indica che il processo viene attivato ogni giorno alle 1:00:00 UTC. Per ulteriori informazioni, consultare la documentazione relativa al formato di espressione cron [cron](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html). |
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

Per impostazione predefinita, una pianificazione è inattiva quando viene creata, a meno che la proprietà `state` sia impostata su `active` nel corpo della richiesta di creazione (POST). Puoi abilitare una pianificazione (impostare `state` su `active`) effettuando una richiesta di PATCH all&#39;endpoint `/config/schedules` e includendo l&#39;ID della pianificazione nel percorso.

**Formato API**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Richiesta**

La richiesta seguente utilizza la formattazione [JSON Patch](http://jsonpatch.com/) per aggiornare la `state` della pianificazione a `active`.

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

Per informazioni su come eseguire azioni simili e lavorare con segmenti utilizzando l&#39;interfaccia utente di Adobe Experience Platform, visita la [Guida utente di Segment Builder](../ui/segment-builder.md).