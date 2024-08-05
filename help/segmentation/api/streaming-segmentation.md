---
solution: Experience Platform
title: Valutazione degli eventi in tempo quasi reale con segmentazione in streaming
description: Questo documento contiene esempi su come utilizzare la segmentazione in streaming con l’API del servizio di segmentazione di Adobe Experience Platform.
role: Developer
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
source-git-commit: 914174de797d7d5f6c47769d75380c0ce5685ee2
workflow-type: tm+mt
source-wordcount: '2050'
ht-degree: 4%

---

# Valutare gli eventi in tempo quasi reale con la segmentazione in streaming

>[!NOTE]
>
>Il documento seguente illustra come utilizzare la segmentazione in streaming utilizzando l’API. Per informazioni sull&#39;utilizzo della segmentazione in streaming tramite l&#39;interfaccia utente, leggere la [guida dell&#39;interfaccia utente per la segmentazione in streaming](../ui/streaming-segmentation.md).

La segmentazione in streaming su [!DNL Adobe Experience Platform] consente ai clienti di eseguire la segmentazione quasi in tempo reale concentrandosi sulla ricchezza dei dati. Con la segmentazione in streaming, la qualificazione dei segmenti ora avviene quando i dati in streaming arrivano in [!DNL Platform], riducendo la necessità di pianificare ed eseguire processi di segmentazione. Con questa funzionalità è ora possibile valutare la maggior parte delle regole del segmento quando i dati vengono passati in [!DNL Platform], il che significa che l&#39;appartenenza al segmento verrà mantenuta aggiornata senza eseguire processi di segmentazione pianificati.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>La segmentazione in streaming funziona su tutti i dati acquisiti utilizzando un’origine di streaming. I segmenti acquisiti utilizzando un’origine basata su batch vengono valutati di notte, anche se è idoneo per la segmentazione in streaming.
>
>Inoltre, le definizioni dei segmenti valutate con la segmentazione in streaming possono spostarsi tra l’appartenenza ideale e quella effettiva se la definizione del segmento è basata su un’altra definizione di segmento valutata utilizzando la segmentazione batch. Ad esempio, se il segmento A è basato sul segmento B e il segmento B viene valutato utilizzando la segmentazione batch, poiché il segmento B viene aggiornato solo ogni 24 ore, il segmento A si allontanerà ulteriormente dai dati effettivi fino a sincronizzarsi nuovamente con l’aggiornamento del segmento B.

## Introduzione

Questa guida per sviluppatori richiede una buona conoscenza dei vari servizi [!DNL Adobe Experience Platform] coinvolti nella segmentazione streaming. Prima di iniziare questo tutorial, consulta la documentazione dei seguenti servizi:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce un profilo consumer unificato in tempo reale, basato su dati aggregati provenienti da più origini.
- [[!DNL Segmentation]](../home.md): consente di creare tipi di pubblico utilizzando le definizioni dei segmenti e altre origini esterne dai dati di [!DNL Real-Time Customer Profile].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): framework standardizzato tramite il quale [!DNL Platform] organizza i dati sull&#39;esperienza del cliente.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per effettuare correttamente chiamate alle API [!DNL Platform].

### Lettura delle chiamate API di esempio

Questa guida per gli sviluppatori fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogliere i valori per le intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l&#39;[esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Completando il tutorial sull’autenticazione si ottengono i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di [!DNL Experience Platform], come mostrato di seguito:

- Autorizzazione: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in specifiche sandbox virtuali. Tutte le richieste alle API [!DNL Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la [documentazione di panoramica sulle sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Content-Type: application/json

Per completare richieste specifiche possono essere necessarie intestazioni aggiuntive. Le intestazioni corrette vengono visualizzate in ciascuno degli esempi all&#39;interno di questo documento. Presta particolare attenzione alle richieste di esempio per assicurarti che siano incluse tutte le intestazioni richieste.

### Tipi di query abilitati per la segmentazione in streaming {#query-types}

>[!NOTE]
>
>Affinché la segmentazione in streaming funzioni, devi abilitare la segmentazione pianificata per l’organizzazione. Le informazioni sull&#39;abilitazione della segmentazione pianificata sono disponibili nella sezione [abilita segmentazione pianificata](#enable-scheduled-segmentation)

Affinché una definizione di segmento possa essere valutata utilizzando la segmentazione in streaming, la query deve essere conforme alle seguenti linee guida.

| Tipo di query | Dettagli |
| ---------- | ------- |
| Evento singolo | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo senza restrizioni temporali. |
| Singolo evento entro una finestra temporale relativa | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo. |
| Evento singolo con finestra temporale | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo con una finestra temporale. |
| Solo profilo | Qualsiasi definizione di segmento che fa riferimento solo a un attributo di profilo. |
| Singolo evento con un attributo di profilo entro un intervallo di tempo relativo inferiore a 24 ore | Qualsiasi definizione di segmento che si riferisce a un singolo evento in arrivo, con uno o più attributi di profilo, e si verifica entro un intervallo di tempo relativo inferiore a 24 ore. |
| Segmento di segmenti | Qualsiasi definizione di segmento che contiene uno o più segmenti batch o in streaming. **Nota:** se si utilizza un segmento di segmenti, l&#39;annullamento del profilo avverrà **ogni 24 ore**. |
| Più eventi con un attributo di profilo | Qualsiasi definizione di segmento che fa riferimento a più eventi **nelle ultime 24 ore** e (facoltativamente) ha uno o più attributi di profilo. |

Una definizione di segmento **non** verrà abilitata per la segmentazione in streaming nei seguenti scenari:

- La definizione del segmento include segmenti o caratteristiche di Adobe Audience Manager (AAM).
- La definizione del segmento include più entità (query con più entità).
- La definizione del segmento include una combinazione di un singolo evento e un evento `inSegment`.
   - Tuttavia, se il segmento contenuto nell&#39;evento `inSegment` è solo di profilo, la definizione del segmento **sarà** abilitata per la segmentazione in streaming.
- La definizione del segmento utilizza &quot;Ignora anno&quot; come parte dei vincoli di tempo.

Tieni presente che le seguenti linee guida sono applicabili quando esegui la segmentazione in streaming:

| Tipo di query | Linea guida |
| ---------- | -------- |
| Query evento singolo | Non ci sono limiti all’intervallo di lookback. |
| Query con cronologia eventi | <ul><li>L&#39;intervallo di lookback è limitato a **un giorno**.</li><li>Tra gli eventi è presente una condizione di ordinamento temporale **must**.</li><li>Sono supportate le query con almeno un evento negato. L&#39;intero evento **non può** essere una negazione.</li></ul> |

Se una definizione di segmento viene modificata in modo da non soddisfare più i criteri per la segmentazione in streaming, la definizione del segmento passerà automaticamente da &quot;Streaming&quot; a &quot;Batch&quot;.

Inoltre, l’annullamento del riconoscimento del segmento, in modo simile alla qualificazione del segmento, avviene in tempo reale. Di conseguenza, se un profilo non è più idoneo per la definizione di un segmento, non potrà più essere qualificato immediatamente. Ad esempio, se la definizione del segmento richiede &quot;Tutti gli utenti che hanno acquistato scarpe rosse nelle ultime tre ore&quot;, dopo tre ore tutti i profili che si sono inizialmente qualificati per la definizione del segmento non saranno qualificati.

## Recupera tutte le definizioni di segmento abilitate per la segmentazione in streaming

Per recuperare un elenco di tutte le definizioni di segmenti abilitate per la segmentazione in streaming all&#39;interno dell&#39;organizzazione, effettua una richiesta di GET all&#39;endpoint `/segment/definitions`.

**Formato API**

Per recuperare le definizioni dei segmenti abilitati per lo streaming, è necessario includere il parametro di query `evaluationInfo.continuous.enabled=true` nel percorso della richiesta.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un array di definizioni di segmenti nell’organizzazione abilitate per la segmentazione in streaming.

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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

## Creare una definizione di segmento abilitata per lo streaming

Una definizione di segmento sarà automaticamente abilitata per lo streaming se corrisponde a uno dei [tipi di segmentazione streaming elencati sopra](#query-types).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.profile"
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
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    }
}'
```

>[!NOTE]
>
>Si tratta di una richiesta standard di &quot;creazione di una definizione di segmento&quot;. Per ulteriori informazioni sulla creazione di una definizione di segmento, consulta l&#39;esercitazione su [creazione di una definizione di segmento](../tutorials/create-a-segment.md).

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della nuova definizione di segmento abilitata per lo streaming.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{ORG_ID}",
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

Una volta abilitata la valutazione in streaming, è necessario creare una linea di base (dopo di che la definizione del segmento sarà sempre aggiornata). La valutazione pianificata (nota anche come segmentazione pianificata) deve prima essere abilitata affinché il sistema esegua automaticamente la baseline. Con la segmentazione pianificata, la tua organizzazione può rispettare una pianificazione ricorrente per eseguire automaticamente processi di esportazione per valutare le definizioni dei segmenti.

>[!NOTE]
>
>È possibile abilitare la valutazione pianificata per le sandbox con un massimo di cinque (5) criteri di unione per [!DNL XDM Individual Profile]. Se nell&#39;organizzazione sono presenti più di cinque criteri di unione per [!DNL XDM Individual Profile] in un singolo ambiente sandbox, non sarà possibile utilizzare la valutazione pianificata.

### Creare una pianificazione

Effettuando una richiesta POST all&#39;endpoint `/config/schedules`, è possibile creare una pianificazione e includere l&#39;ora specifica in cui attivare la pianificazione.

**Formato API**

```http
POST /config/schedules
```

**Richiesta**

La seguente richiesta crea una nuova pianificazione basata sulle specifiche fornite nel payload.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `properties` | **(Obbligatorio)** Oggetto contenente proprietà aggiuntive relative alla pianificazione. |
| `properties.segments` | **(Obbligatorio quando `type` è uguale a `batch_segmentation`)** L&#39;utilizzo di `["*"]` garantisce l&#39;inclusione di tutte le definizioni dei segmenti. |
| `schedule` | **(Obbligatorio)** Stringa contenente la pianificazione del processo. È possibile programmare l&#39;esecuzione dei job solo una volta al giorno, pertanto non è possibile programmare l&#39;esecuzione di un job più di una volta in un periodo di 24 ore. L&#39;esempio mostrato (`0 0 1 * * ?`) indica che il processo viene attivato ogni giorno alle 1:00:00 UTC. Per ulteriori informazioni, consulta l&#39;appendice sul formato di espressione [cron](./schedules.md#appendix) all&#39;interno della documentazione sulle pianificazioni all&#39;interno della segmentazione. |
| `state` | *(Facoltativo)* Stringa contenente lo stato della pianificazione. Valori disponibili: `active` e `inactive`. Il valore predefinito è `inactive`. Un’organizzazione può creare una sola pianificazione. I passaggi per aggiornare la pianificazione sono disponibili più avanti in questa esercitazione. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della pianificazione appena creata.

```json
{
    "id": "cd585edf-962d-420d-94ad-3be03e619ac2",
    "imsOrgId": "{ORG_ID}",
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

### Abilitare una pianificazione

Per impostazione predefinita, una pianificazione non è attiva al momento della creazione, a meno che la proprietà `state` non sia impostata su `active` nel corpo della richiesta di creazione (POST). È possibile abilitare una pianificazione (impostare `state` su `active`) effettuando una richiesta PATCH all&#39;endpoint `/config/schedules` e includendo l&#39;ID della pianificazione nel percorso.

**Formato API**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Richiesta**

La richiesta seguente utilizza la formattazione [JSON Patch](https://datatracker.ietf.org/doc/html/rfc6902) per aggiornare `state` della pianificazione a `active`.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

In caso di esito positivo, l’aggiornamento restituisce un corpo di risposta vuoto e lo stato HTTP 204 (nessun contenuto).

La stessa operazione può essere utilizzata per disabilitare una pianificazione sostituendo il &quot;valore&quot; nella richiesta precedente con &quot;inattivo&quot;.

## Passaggi successivi

Ora che hai abilitato sia le definizioni di segmenti nuove che quelle esistenti per la segmentazione in streaming, sia la segmentazione pianificata per sviluppare una linea di base ed eseguire valutazioni ricorrenti, puoi iniziare a creare definizioni di segmenti abilitati per lo streaming per la tua organizzazione.

Per informazioni su come eseguire azioni simili e lavorare con le definizioni dei segmenti utilizzando l&#39;interfaccia utente di Adobe Experience Platform, visita la [guida utente di Segment Builder](../ui/segment-builder.md).

## Appendice

Nella sezione seguente sono elencate le domande frequenti sulla segmentazione in streaming:

### La segmentazione in streaming &quot;unqualification&quot; (non qualificazione) si verifica anche in tempo reale?

Nella maggior parte dei casi, l’annullamento della qualifica per segmentazione in streaming avviene in tempo reale. Tuttavia, le definizioni dei segmenti in streaming che utilizzano segmenti di segmenti **not** non sono idonee in tempo reale, ma vengono annullate dopo 24 ore.

### Su quali dati funziona la segmentazione in streaming?

La segmentazione in streaming funziona su tutti i dati acquisiti utilizzando un’origine di streaming. I segmenti acquisiti utilizzando un’origine basata su batch vengono valutati di notte, anche se è idoneo per la segmentazione in streaming. Gli eventi inviati in streaming al sistema con una marca temporale precedente alle 24 ore verranno elaborati nel processo batch successivo.

### Come vengono definite le definizioni dei segmenti come segmentazione in batch o in streaming?

Una definizione di segmento è definita come segmentazione in batch o in streaming in base a una combinazione di tipo di query e durata della cronologia degli eventi. Nella sezione [tipi di query di segmentazione in streaming](#query-types) è disponibile un elenco delle definizioni dei segmenti che verranno valutate come segmenti in streaming.

Tieni presente che se un segmento contiene **both** un&#39;espressione `inSegment` e una catena di eventi singola diretta, non può essere qualificato per la segmentazione in streaming. Se desideri che questa definizione di segmento sia idonea per la segmentazione in streaming, devi rendere la catena di eventi singoli diretta la propria definizione di segmento.

### Perché il numero di definizioni di segmenti &quot;qualificati totali&quot; continua a crescere mentre il numero in &quot;Ultimi X giorni&quot; rimane pari a zero nella sezione dei dettagli di definizione del segmento?

Il numero totale di definizioni di segmenti qualificati viene ricavato dal processo di segmentazione giornaliero, che include i tipi di pubblico idonei per le definizioni di segmenti in batch e in streaming. Questo valore viene visualizzato sia per le definizioni dei segmenti batch che per quelle dei segmenti in streaming.

Il numero in &quot;Ultimi X giorni&quot; **solo** include tipi di pubblico qualificati nella segmentazione in streaming e **solo** aumenta se i dati sono stati inviati in streaming al sistema e conta per tale definizione di streaming. Questo valore è **only** visualizzato per le definizioni dei segmenti di streaming. Di conseguenza, questo valore **maggio** viene visualizzato come 0 per le definizioni dei segmenti batch.

Di conseguenza, se noti che il numero in &quot;Ultimi X giorni&quot; è zero e anche il grafico a linee riporta zero, hai **non** inviato in streaming nel sistema tutti i profili che sarebbero idonei per la definizione del segmento.

### Quanto tempo ci vuole affinché una definizione di segmento sia disponibile?

È necessaria fino a un’ora perché la definizione di un segmento sia disponibile.

### Ci sono limiti ai dati inviati in streaming?

Affinché i dati in streaming possano essere utilizzati nella segmentazione in streaming, **deve** essere presente una spaziatura tra gli eventi in streaming. Se un numero eccessivo di eventi viene inviato in streaming nello stesso secondo, Platform tratterà tali eventi come dati generati da bot, che verranno eliminati. Come best practice, è necessario disporre di **almeno** cinque secondi tra i dati dell&#39;evento per garantire che vengano utilizzati correttamente.
