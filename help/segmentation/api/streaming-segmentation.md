---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;segmentazione in streaming;Segmentazione in streaming;Valutazione continua;
solution: Experience Platform
title: 'Valutare gli eventi in tempo reale con Segmentazione in streaming '
topic: guida per sviluppatori
description: Questo documento contiene esempi sull’utilizzo della segmentazione in streaming con l’API di Adobe Experience Platform Segmentation Service.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '1341'
ht-degree: 1%

---


# Valutare gli eventi in tempo quasi reale con la segmentazione in streaming

>[!NOTE]
>
>Il seguente documento spiega come utilizzare la segmentazione in streaming utilizzando l’API. Per informazioni sull&#39;utilizzo della segmentazione in streaming tramite l&#39;interfaccia utente, leggere la [guida all&#39;interfaccia utente per la segmentazione in streaming](../ui/streaming-segmentation.md).

La segmentazione in streaming su [!DNL Adobe Experience Platform] consente ai clienti di eseguire la segmentazione in tempo quasi reale, concentrandosi sulla ricchezza dei dati. Con la segmentazione in streaming, la qualificazione dei segmenti ora avviene quando i dati in streaming arrivano in [!DNL Platform], alleviando la necessità di pianificare ed eseguire processi di segmentazione. Con questa funzionalità, la maggior parte delle regole del segmento può ora essere valutata in quanto i dati vengono trasmessi in [!DNL Platform], il che significa che l’appartenenza al segmento verrà mantenuta aggiornata senza eseguire processi di segmentazione pianificati.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>La segmentazione in streaming può essere utilizzata solo per valutare i dati trasmessi in streaming in Platform. In altre parole, i dati acquisiti tramite l’acquisizione batch non verranno valutati tramite la segmentazione in streaming e verranno valutati insieme al lavoro segmentato pianificato ogni sera.

## Introduzione

Questa guida per gli sviluppatori richiede una buona comprensione dei vari servizi [!DNL Adobe Experience Platform] coinvolti nella segmentazione in streaming. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumatore unificato in tempo reale, basato su dati aggregati provenienti da più origini.
- [[!DNL Segmentation]](../home.md): Consente di creare segmenti e tipi di pubblico dai  [!DNL Real-time Customer Profile] dati.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Platform] vengono organizzati i dati sulla customer experience.

Le sezioni seguenti forniscono informazioni aggiuntive che dovrai conoscere per effettuare correttamente le chiamate alle API [!DNL Platform] .

### Lettura di chiamate API di esempio

Questa guida per gli sviluppatori fornisce esempi di chiamate API per mostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come mostrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- nome x-sandbox: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la documentazione di panoramica [sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Tipo di contenuto: application/json

Per completare richieste specifiche possono essere necessarie intestazioni aggiuntive. Le intestazioni corrette vengono visualizzate in ciascuno degli esempi contenuti in questo documento. Presta particolare attenzione alle richieste di esempio per garantire che tutte le intestazioni richieste siano incluse.

### Tipi di query abilitate per la segmentazione in streaming {#streaming-segmentation-query-types}

>[!NOTE]
>
>Per il corretto funzionamento della segmentazione in streaming, devi abilitare la segmentazione pianificata per l’organizzazione. Le informazioni sull&#39;abilitazione della segmentazione pianificata si trovano nella sezione [abilita segmentazione pianificata](#enable-scheduled-segmentation)

Affinché un segmento possa essere valutato utilizzando la segmentazione in streaming, la query deve essere conforme alle seguenti linee guida.

| Tipo di query | Dettagli |
| ---------- | ------- |
| Hit in entrata | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo senza restrizioni temporali. |
| Hit in arrivo in una finestra temporale relativa | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo. |
| Solo profilo | Qualsiasi definizione di segmento che fa riferimento solo a un attributo di profilo. |
| Hit in entrata che fa riferimento a un profilo | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo, senza restrizioni di tempo, e a uno o più attributi di profilo. |
| Hit in arrivo che fa riferimento a un profilo all’interno di una finestra temporale relativa | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo e a uno o più attributi di profilo. |
| Eventi multipli che fanno riferimento a un profilo | Qualsiasi definizione di segmento che fa riferimento a più eventi **nelle ultime 24 ore** e (facoltativamente) ha uno o più attributi di profilo. |

La definizione di un segmento **non** sarà abilitata per la segmentazione in streaming nei seguenti scenari:

- La definizione del segmento include segmenti o caratteristiche di Adobe Audience Manager (AAM).
- La definizione del segmento include più entità (query con più entità).

Inoltre, durante la segmentazione in streaming si applicano alcune linee guida:

| Tipo di query | Indirizzo |
| ---------- | -------- |
| Query a evento singolo | Non ci sono limiti all’intervallo di lookback. |
| Query con cronologia eventi | <ul><li>L&#39;intervallo di lookback è limitato a **un giorno**.</li><li>Tra gli eventi è presente una condizione di ordine temporale rigida **deve** .</li><li>Sono supportate le query con almeno un evento negato. Tuttavia, l&#39;intero evento **non può** essere una negazione.</li></ul> |

## Recupera tutti i segmenti abilitati per la segmentazione in streaming

Puoi recuperare un elenco di tutti i segmenti abilitati per la segmentazione in streaming all’interno dell’organizzazione IMS effettuando una richiesta GET all’endpoint `/segment/definitions` .

**Formato API**

Per recuperare i segmenti abilitati per lo streaming, devi includere il parametro di query `evaluationInfo.continuous.enabled=true` nel percorso della richiesta.

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

Una risposta corretta restituisce un array di segmenti nell’organizzazione IMS abilitati per la segmentazione in streaming.

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

Un segmento sarà automaticamente abilitato per lo streaming se corrisponde a uno dei [tipi di segmentazione in streaming elencati sopra](#streaming-segmentation-query-types).

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
>Questa è una richiesta standard &quot;crea un segmento&quot;. Per ulteriori informazioni sulla creazione di una definizione di segmento, consulta l’esercitazione su [creazione di un segmento](../tutorials/create-a-segment.md).

**Risposta**

Una risposta corretta restituisce i dettagli della nuova definizione del segmento abilitato per lo streaming.

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

Una volta abilitata la valutazione dello streaming, devi creare una baseline (dopodiché il segmento sarà sempre aggiornato). La valutazione pianificata (nota anche come segmentazione pianificata) deve prima essere abilitata affinché il sistema esegua automaticamente la valutazione. Con la segmentazione pianificata, l’organizzazione IMS può aderire a una pianificazione periodica per eseguire automaticamente i processi di esportazione per valutare i segmenti.

>[!NOTE]
>
>La valutazione pianificata può essere abilitata per le sandbox con un massimo di cinque (5) criteri di unione per [!DNL XDM Individual Profile]. Se la tua organizzazione dispone di più di cinque criteri di unione per [!DNL XDM Individual Profile] all’interno di un singolo ambiente sandbox, non potrai utilizzare la valutazione pianificata.

### Creare una pianificazione

Effettuando una richiesta POST all&#39;endpoint `/config/schedules`, puoi creare una pianificazione e includere l&#39;ora specifica in cui deve essere attivata la pianificazione.

**Formato API**

```http
POST /config/schedules
```

**Richiesta**

Nella richiesta seguente viene creata una nuova pianificazione in base alle specifiche fornite nel payload.

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
| `name` | **(Obbligatorio)** Il nome della pianificazione. Deve essere una stringa. |
| `type` | **(Obbligatorio)** Il tipo di processo in formato stringa. I tipi supportati sono `batch_segmentation` e `export`. |
| `properties` | **(Obbligatorio)** Un oggetto contenente proprietà aggiuntive correlate alla pianificazione. |
| `properties.segments` | **(Obbligatorio quando  `type` è uguale a  `batch_segmentation`)** L’utilizzo  `["*"]` assicura che tutti i segmenti siano inclusi. |
| `schedule` | **(Obbligatorio)** Una stringa contenente la pianificazione del processo. L&#39;esecuzione dei processi può essere pianificata solo una volta al giorno, il che significa che non è possibile pianificare l&#39;esecuzione di un processo più di una volta durante un periodo di 24 ore. L&#39;esempio mostrato (`0 0 1 * * ?`) indica che il processo viene attivato ogni giorno alle 1:00:00 UTC. Per ulteriori informazioni, consulta la documentazione [formato espressione cron](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) . |
| `state` | *(Facoltativo)* Stringa contenente lo stato della pianificazione. Valori disponibili: `active` e `inactive`. Il valore predefinito è `inactive`. Un’organizzazione IMS può creare una sola pianificazione. I passaggi per aggiornare la pianificazione sono disponibili più avanti in questa esercitazione. |

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

### Abilita pianificazione

Per impostazione predefinita, una pianificazione è inattiva quando viene creata a meno che la proprietà `state` non sia impostata su `active` nel corpo della richiesta di creazione (POST). Puoi abilitare una pianificazione (imposta `state` su `active`) effettuando una richiesta PATCH all&#39;endpoint `/config/schedules` e includendo l&#39;ID della pianificazione nel percorso.

**Formato API**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Richiesta**

La richiesta seguente utilizza [JSON Patch formatted](http://jsonpatch.com/) per aggiornare `state` della pianificazione a `active`.

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

Un aggiornamento corretto restituisce un corpo di risposta vuoto e lo stato HTTP 204 (nessun contenuto).

La stessa operazione può essere utilizzata per disabilitare una pianificazione sostituendo il &quot;valore&quot; nella richiesta precedente con &quot;inattivo&quot;.

## Passaggi successivi

Ora che hai abilitato segmenti nuovi ed esistenti per la segmentazione in streaming e hai abilitato la segmentazione pianificata per sviluppare una linea di base ed eseguire valutazioni ricorrenti, puoi iniziare a creare segmenti per la tua organizzazione.

Per informazioni su come eseguire azioni simili e lavorare con segmenti utilizzando l’interfaccia utente di Adobe Experience Platform, visita la [guida utente del Generatore di segmenti](../ui/segment-builder.md).