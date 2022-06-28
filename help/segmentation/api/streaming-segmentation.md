---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;segmentazione in streaming;Segmentazione in streaming;Valutazione continua;
solution: Experience Platform
title: 'Valutare gli eventi in tempo reale con Segmentazione in streaming '
topic-legacy: developer guide
description: Questo documento contiene esempi sull’utilizzo della segmentazione in streaming con l’API del servizio di segmentazione di Adobe Experience Platform.
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
source-git-commit: 81659da18d4fa8b733200998c27c25ec356ca264
workflow-type: tm+mt
source-wordcount: '1915'
ht-degree: 1%

---

# Valutare gli eventi in tempo quasi reale con la segmentazione in streaming

>[!NOTE]
>
>Il seguente documento spiega come utilizzare la segmentazione in streaming utilizzando l’API. Per informazioni sull’utilizzo della segmentazione in streaming tramite l’interfaccia utente, consulta la [guida all’interfaccia utente per la segmentazione in streaming](../ui/streaming-segmentation.md).

Segmentazione streaming su [!DNL Adobe Experience Platform] consente ai clienti di effettuare segmentazione in tempo quasi reale, concentrandosi sulla ricchezza dei dati. Con la segmentazione in streaming, la qualificazione dei segmenti ora avviene quando i dati in streaming arrivano in [!DNL Platform], per ridurre la necessità di pianificare ed eseguire processi di segmentazione. Con questa funzionalità, ora è possibile valutare la maggior parte delle regole di segmento quando i dati vengono trasmessi in [!DNL Platform], il che significa che l’appartenenza al segmento verrà mantenuta aggiornata senza eseguire processi di segmentazione pianificati.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>La segmentazione in streaming funziona su tutti i dati acquisiti tramite un’origine streaming. I segmenti acquisiti utilizzando un’origine basata su batch verranno valutati ogni notte, anche se idonei per la segmentazione in streaming.
>
>Inoltre, i segmenti valutati con la segmentazione in streaming possono variare tra l’appartenenza ideale e l’appartenenza effettiva se il segmento è basato su un altro segmento valutato utilizzando la segmentazione in batch. Ad esempio, se il segmento A è basato sul segmento B e il segmento B viene valutato utilizzando la segmentazione batch, poiché il segmento B viene aggiornato solo ogni 24 ore, il segmento A si allontanerà ulteriormente dai dati effettivi fino a quando non viene sincronizzato nuovamente con l’aggiornamento del segmento B.

## Introduzione

Questa guida per gli sviluppatori richiede una comprensione approfondita dei vari [!DNL Adobe Experience Platform] servizi coinvolti nella segmentazione in streaming. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumatore unificato in tempo reale, basato su dati aggregati provenienti da più origini.
- [[!DNL Segmentation]](../home.md): Consente di creare segmenti e tipi di pubblico dal [!DNL Real-time Customer Profile] dati.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il quadro standardizzato [!DNL Platform] organizza i dati sulla customer experience.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente le chiamate a [!DNL Platform] API.

### Lettura di chiamate API di esempio

Questa guida per gli sviluppatori fornisce esempi di chiamate API per mostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate a [!DNL Platform] API, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedi [documentazione panoramica su sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Tipo di contenuto: application/json

Per completare richieste specifiche possono essere necessarie intestazioni aggiuntive. Le intestazioni corrette vengono visualizzate in ciascuno degli esempi contenuti in questo documento. Presta particolare attenzione alle richieste di esempio per garantire che tutte le intestazioni richieste siano incluse.

### Tipi di query abilitate per la segmentazione in streaming {#query-types}

>[!NOTE]
>
>Per il corretto funzionamento della segmentazione in streaming, devi abilitare la segmentazione pianificata per l’organizzazione. Informazioni sull’abilitazione della segmentazione pianificata sono disponibili nella sezione [attiva sezione segmentazione pianificata](#enable-scheduled-segmentation)

Affinché un segmento possa essere valutato utilizzando la segmentazione in streaming, la query deve essere conforme alle seguenti linee guida.

| Tipo di query | Dettagli |
| ---------- | ------- |
| Evento singolo | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo senza restrizioni temporali. |
| Singolo evento all’interno di una finestra temporale relativa | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo. |
| Singolo evento con una finestra temporale | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo con una finestra temporale. |
| Solo profilo | Qualsiasi definizione di segmento che fa riferimento solo a un attributo di profilo. |
| Singolo evento con un attributo di profilo | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo, senza restrizioni di tempo, e a uno o più attributi di profilo. **Nota:** La query viene valutata immediatamente quando viene generato l’evento. Nel caso di un evento di profilo, tuttavia, deve attendere 24 ore per essere incorporato. |
| Singolo evento con un attributo di profilo in una finestra temporale relativa | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo e a uno o più attributi di profilo. |
| Segmento di segmenti | Qualsiasi definizione di segmento che contiene uno o più segmenti in batch o in streaming. **Nota:** Se utilizzi un segmento, si verificherà l’annullamento della qualifica del profilo **ogni 24 ore**. |
| Eventi multipli con un attributo di profilo | Qualsiasi definizione di segmento che fa riferimento a più eventi **nelle ultime 24 ore** e (facoltativamente) ha uno o più attributi di profilo. |

Una definizione di segmento **not** è abilitata per la segmentazione in streaming nei seguenti scenari:

- La definizione del segmento include segmenti o caratteristiche Adobe Audience Manager (AAM).
- La definizione del segmento include più entità (query con più entità).

Durante la segmentazione in streaming si applicano le seguenti linee guida:

| Tipo di query | Indirizzo |
| ---------- | -------- |
| Query a evento singolo | Non ci sono limiti all’intervallo di lookback. |
| Query con cronologia eventi | <ul><li>L’intervallo di lookback è limitato a **un giorno**.</li><li>Una rigorosa condizione di ordinamento dei tempi **deve** esistono tra gli eventi.</li><li>Sono supportate le query con almeno un evento negato. Tuttavia, l&#39;intero evento **impossibile** sia una negazione.</li></ul> |

Se la definizione di un segmento viene modificata in modo da non soddisfare più i criteri per la segmentazione in streaming, la definizione del segmento passa automaticamente da &quot;Streaming&quot; a &quot;Batch&quot;.

Inoltre, l’annullamento della qualificazione dei segmenti, analogamente alla qualificazione dei segmenti, avviene in tempo reale. Di conseguenza, se un pubblico non è più idoneo per un segmento, verrà immediatamente non qualificato. Ad esempio, se la definizione del segmento richiede &quot;Tutti gli utenti che hanno acquistato scarpe rosse nelle ultime tre ore&quot;, dopo tre ore, tutti i profili inizialmente qualificati per la definizione del segmento non saranno qualificati.

## Recupera tutti i segmenti abilitati per la segmentazione in streaming

Puoi recuperare un elenco di tutti i segmenti abilitati per la segmentazione in streaming all’interno della tua organizzazione IMS effettuando una richiesta di GET al `/segment/definitions` punto finale.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            "ttlInDays": 30,
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

## Creare un segmento abilitato per lo streaming

Un segmento viene abilitato automaticamente in streaming se corrisponde a uno dei [tipi di segmentazione in streaming elencati sopra](#query-types).

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

Una volta abilitata la valutazione dello streaming, devi creare una baseline (dopodiché il segmento sarà sempre aggiornato). La valutazione pianificata (nota anche come segmentazione pianificata) deve prima essere abilitata affinché il sistema esegua automaticamente la valutazione. Con la segmentazione pianificata, l’organizzazione IMS può aderire a una pianificazione periodica per eseguire automaticamente i processi di esportazione per valutare i segmenti.

>[!NOTE]
>
>La valutazione pianificata può essere abilitata per le sandbox con un massimo di cinque (5) criteri di unione per [!DNL XDM Individual Profile]. Se l&#39;organizzazione dispone di più di cinque criteri di unione per [!DNL XDM Individual Profile] in un unico ambiente sandbox, non potrai utilizzare valutazioni pianificate.

### Creare una pianificazione

Effettuando una richiesta POST al `/config/schedules` endpoint, puoi creare una pianificazione e includere l’ora specifica in cui deve essere attivata la pianificazione.

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
| `name` | **(Obbligatorio)** Nome della pianificazione. Deve essere una stringa. |
| `type` | **(Obbligatorio)** Tipo di processo in formato stringa. I tipi supportati sono `batch_segmentation` e `export`. |
| `properties` | **(Obbligatorio)** Un oggetto contenente proprietà aggiuntive correlate alla pianificazione. |
| `properties.segments` | **(Obbligatorio quando `type` è `batch_segmentation`)** Utilizzo `["*"]` assicura che tutti i segmenti siano inclusi. |
| `schedule` | **(Obbligatorio)** Una stringa contenente la pianificazione del processo. L&#39;esecuzione dei processi può essere pianificata solo una volta al giorno, il che significa che non è possibile pianificare l&#39;esecuzione di un processo più di una volta durante un periodo di 24 ore. L’esempio mostrato (`0 0 1 * * ?`) indica che il processo viene attivato ogni giorno a 1:00:00 UTC. Per ulteriori informazioni, consulta l’appendice [formato di espressione cron](./schedules.md#appendix) all’interno della documentazione sulle pianificazioni all’interno della segmentazione. |
| `state` | *(Facoltativo)* Stringa contenente lo stato della pianificazione. Valori disponibili: `active` e `inactive`. Il valore predefinito è `inactive`. Un’organizzazione IMS può creare una sola pianificazione. I passaggi per aggiornare la pianificazione sono disponibili più avanti in questa esercitazione. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova pianificazione creata.

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

### Abilita pianificazione

Per impostazione predefinita, una pianificazione è inattiva quando viene creata a meno che il `state` è impostata su `active` nel corpo della richiesta create (POST). Puoi abilitare una pianificazione (imposta la `state` a `active`) effettuando una richiesta PATCH al `/config/schedules` e l’ID della pianificazione nel percorso.

**Formato API**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Richiesta**

La richiesta seguente utilizza [Formattazione patch JSON](https://datatracker.ietf.org/doc/html/rfc6902) per aggiornare `state` del programma `active`.

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

Un aggiornamento corretto restituisce un corpo di risposta vuoto e lo stato HTTP 204 (nessun contenuto).

La stessa operazione può essere utilizzata per disabilitare una pianificazione sostituendo il &quot;valore&quot; nella richiesta precedente con &quot;inattivo&quot;.

## Passaggi successivi

Ora che hai abilitato segmenti nuovi ed esistenti per la segmentazione in streaming e hai abilitato la segmentazione pianificata per sviluppare una linea di base ed eseguire valutazioni ricorrenti, puoi iniziare a creare segmenti abilitati per lo streaming per la tua organizzazione.

Per informazioni su come eseguire azioni simili e lavorare con i segmenti utilizzando l’interfaccia utente di Adobe Experience Platform, visita il [Guida utente di Segment Builder](../ui/segment-builder.md).

## Appendice

Nella sezione seguente sono elencate le domande frequenti sulla segmentazione in streaming:

### La segmentazione in streaming avviene anche in tempo reale?

Per la maggior parte delle istanze, l’annullamento della segmentazione in streaming avviene in tempo reale. Tuttavia, i segmenti in streaming che utilizzano segmenti **not** non sono qualificati in tempo reale, ma non possono essere qualificati dopo 24 ore.

### Su quali dati funziona la segmentazione in streaming?

La segmentazione in streaming funziona su tutti i dati acquisiti tramite un’origine streaming. I segmenti acquisiti utilizzando un’origine basata su batch verranno valutati ogni notte, anche se idonei per la segmentazione in streaming. Gli eventi inviati in streaming nel sistema con una marca temporale superiore a 24 ore verranno elaborati nel successivo processo batch.

### Come vengono definiti i segmenti come segmentazione in batch o in streaming?

Un segmento è definito come segmentazione in batch o in streaming in base a una combinazione di tipo di query e durata della cronologia degli eventi. Un elenco dei segmenti che verranno valutati come segmento in streaming si trova nella sezione [sezione tipi di query per segmentazione in streaming](#query-types).

### Un utente può definire un segmento come segmentazione in batch o in streaming?

Al momento, l’utente non può definire se un segmento viene valutato utilizzando l’acquisizione in batch o in streaming, in quanto il sistema determinerà automaticamente con quale metodo verrà valutato il segmento.

### Perché il numero di segmenti &quot;qualificati totali&quot; continua ad aumentare mentre il numero sotto &quot;Ultimi X giorni&quot; rimane a zero all’interno della sezione dei dettagli del segmento?

Il numero di segmenti qualificati totali viene ricavato dal processo di segmentazione giornaliera, che include i tipi di pubblico idonei per i segmenti batch e in streaming. Questo valore viene visualizzato sia per i segmenti batch che per quelli in streaming.

Il numero sotto &quot;Ultimi X giorni&quot; **only** include i tipi di pubblico qualificati nella segmentazione in streaming, e **only** aumenta se hai inviato dati in streaming nel sistema e conta verso tale definizione di streaming. Questo valore è **only** mostrata per i segmenti in streaming. Di conseguenza, questo valore **possono** viene visualizzato come 0 per i segmenti batch.

Di conseguenza, se vedi che il numero sotto &quot;Ultimi X giorni&quot; è zero, e il grafico a linee è anche pari a zero, hai **not** ha inviato in streaming nel sistema tutti i profili idonei per quel segmento.