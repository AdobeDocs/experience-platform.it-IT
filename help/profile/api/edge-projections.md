---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Endpoint API di proiezione Edge
type: Documentation
description: Adobe Experience Platform ti consente di promuovere esperienze coordinate, coerenti e personalizzate per i clienti su più canali in tempo reale, rendendo i dati giusti prontamente disponibili e continuamente aggiornati in caso di cambiamenti. Ciò avviene tramite l’utilizzo di edge, un server posizionato geograficamente che memorizza i dati e li rende facilmente accessibili alle applicazioni.
exl-id: ce429164-8e87-412d-9a9d-e0d4738c7815
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1959'
ht-degree: 2%

---

# Endpoint di destinazioni e configurazioni di proiezione Edge

Per fornire ai clienti esperienze coordinate, coerenti e personalizzate in tempo reale su più canali, i dati giusti devono essere prontamente disponibili e continuamente aggiornati in base alle modifiche apportate. Adobe Experience Platform consente questo accesso in tempo reale ai dati tramite l’utilizzo dei cosiddetti edge. Un server perimetrale è un server posizionato geograficamente che memorizza i dati e li rende facilmente accessibili alle applicazioni. Ad Adobe, applicazioni come Adobe Target e Adobe Campaign utilizzano Edge per fornire ai clienti esperienze personalizzate in tempo reale. I dati vengono instradati a uno spigolo da una proiezione, con una destinazione di proiezione che definisce lo spigolo a cui verranno inviati i dati e una configurazione di proiezione che definisce le informazioni specifiche che saranno rese disponibili sullo spigolo. Questa guida fornisce istruzioni dettagliate per l&#39;utilizzo di [!DNL Real-Time Customer Profile] API per lavorare con le proiezioni Edge di, incluse le destinazioni e le configurazioni.

## Introduzione

L’endpoint API utilizzato in questa guida fa parte del [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Prima di continuare, controlla [guida introduttiva](getting-started.md) per collegamenti alla documentazione correlata, una guida per la lettura delle chiamate API di esempio di questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a [!DNL Experience Platform] API.

>[!NOTE]
>
>Le richieste che contengono un payload (POST, PUT, PATCH) richiedono un `Content-Type` intestazione. Più di uno `Content-Type` viene utilizzato in questo documento. Presta particolare attenzione alle intestazioni nelle chiamate di esempio per assicurarti di utilizzare correttamente `Content-Type` per ogni richiesta.

## Destinazioni di proiezione

Una proiezione può essere indirizzata a uno o più spigoli specificando le posizioni in cui i dati devono essere inviati. Ogni destinazione di proiezione creata ha un ID univoco che viene quindi utilizzato per creare la configurazione di proiezione.

### Elenca tutte le destinazioni

Puoi elencare le destinazioni Edge che sono già state create per la tua organizzazione effettuando una richiesta GET al `/config/destinations` endpoint.

**Formato API**

```http
GET /config/destinations
```

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta include una `projectionDestinations` con i dettagli di ogni destinazione mostrata come singolo oggetto all&#39;interno dell&#39;array. Se non è stata configurata alcuna proiezione, il `projectionDestinations` l’array restituisce un valore vuoto.

>[!NOTE]
>
>Questa risposta è stata ridotta per motivi di spazio e mostra solo due destinazioni.

```json
{
    "_links": {
        "self": {
            "href": "/data/core/ups/config/destinations",
            "templated": false
        }
    },
    "_embedded": {
        "projectionDestinations": [
            {
                "_links": {
                    "self": {
                        "href": "/data/core/ups/config/destinations/cef0e2ef-5249-4e25-be90-94f5797a2841",
                        "templated": false
                    }
                },
                "id": "cef0e2ef-5249-4e25-be90-94f5797a2841",
                "type": "EDGE",
                "ttl": 3600,
                "dataCenters": [
                    "VA5"
                ],
                "version": 1
            },
            {
                "_links": {
                    "self": {
                        "href": "/data/core/ups/config/destinations/7d26263f-a5df-43ce-b088-7f70e187f549",
                        "templated": false
                    }
                },
                "id": "7d26263f-a5df-43ce-b088-7f70e187f549",
                "type": "EDGE",
                "ttl": 3600,
                "dataCenters": [
                    "OR1"
                ],
                "version": 1
            }
        ]
    }
}
```

| Proprietà | Descrizione |
|---|---|
| `_links.self.href` | Al livello principale, corrisponde al percorso utilizzato per effettuare la richiesta di GET. All’interno di ogni singolo oggetto di destinazione, questo percorso può essere utilizzato in una richiesta GET per ricercare direttamente i dettagli di una destinazione specifica. |
| `id` | All&#39;interno di ogni oggetto di destinazione, il `"id"` mostra l’ID univoco di sola lettura generato dal sistema per la destinazione. Questo ID viene utilizzato quando si fa riferimento a una destinazione specifica e durante la creazione di configurazioni di proiezione. |

Per ulteriori informazioni sugli attributi di una singola destinazione, consulta la sezione su [creazione di una destinazione](#create-a-destination) questo è quanto segue.

### Creare una destinazione {#create-a-destination}

Se la destinazione desiderata non esiste già, potete creare una nuova destinazione di proiezione effettuando una richiesta POST al `/config/destinations` endpoint.

**Formato API**

```http
POST /config/destinations
```

**Richiesta**

La richiesta seguente crea una nuova destinazione Edge.

>[!NOTE]
>
>La richiesta POST di creazione di una destinazione richiede un `Content-Type` come mostrato di seguito. Utilizzo di un `Content-Type` L’intestazione restituisce un errore HTTP Status 415 (Tipo di file multimediale non supportato).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionDestination+json; version=1' \
  -d '{
        "type": "EDGE",
        "dataCenters": [ 
          "OR1" 
        ],
        "ttl": 3600,
        "replicationPolicy": REACTIVE
      }'
```

| Proprietà | Descrizione |
|---|---|
| `type` **(Obbligatorio)** | Tipo di destinazione da creare. L’unico valore accettato, &quot;EDGE&quot;, crea una destinazione edge. |
| `dataCenters` **(Obbligatorio)** | Matrice di stringhe che elenca gli spigoli verso cui instradare le proiezioni. Può contenere uno o più dei seguenti valori: &quot;OR1&quot; - Stati Uniti occidentali, &quot;VA5&quot; - Stati Uniti orientali, &quot;NLD1&quot; - EMEA. |
| `ttl` **(Obbligatorio)** | Specifica la scadenza della proiezione. Intervallo di valori accettati: da 600 a 604800. Valore predefinito: 3600. |
| `replicationPolicy` **(Obbligatorio)** | Definisce il comportamento della replica dei dati dall&#39;hub ai bordi.  Valori supportati: PROACTIVE, REACTIVE. Valore predefinito: REACTIVE. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della nuova destinazione Edge creata, incluso l’ID univoco generato dal sistema e di sola lettura (`id`).

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
        "templated": false
    },
    "id": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
    "type": "EDGE",
    "dataCenters": [
       "OR1"
    ],
    "ttl": 3600,
    "version": 1
}
```

| Proprietà | Descrizione |
|---|---|
| `self.href` | Questo percorso viene utilizzato per cercare (GET) direttamente la destinazione e può anche essere utilizzato per aggiornare (PUT) o eliminare (DELETE) la destinazione. |
| `id` | ID univoco di sola lettura generato dal sistema per la destinazione. Questo ID viene utilizzato per fare riferimento direttamente alla destinazione e durante la creazione di configurazioni di proiezione. |
| `version` | Questo valore di sola lettura mostra la versione corrente della destinazione. Quando una destinazione viene aggiornata, il numero di versione viene incrementato automaticamente. |

### Visualizzare una destinazione

Se si conosce l&#39;ID univoco di una destinazione di proiezione, è possibile eseguire una richiesta di ricerca per visualizzarne i dettagli. A tale scopo, invia una richiesta GET al `/config/destinations` e includendo l’ID della destinazione nel percorso della richiesta.

**Formato API**

```http
GET /config/destinations/{DESTINATION_ID}
```

| Parametro | Descrizione |
|---|---|
| `{DESTINATION_ID}` | ID univoco della destinazione di proiezione che desideri visualizzare. |

**Richiesta**

La richiesta seguente esegue una ricerca (GET) per visualizzare la destinazione dell’ID fornito nel percorso della richiesta.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations/9d66c06e-c745-480c-b64c-1d5234d25f4b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

L&#39;oggetto di risposta mostra i dettagli della destinazione della proiezione. Il `id` deve corrispondere all’ID della destinazione di proiezione fornito nella richiesta.

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/cef0e2ef-5249-4e25-be90-94f5797a2841",
        "templated": false
    },
    "id": "cef0e2ef-5249-4e25-be90-94f5797a2841",
    "type": "EDGE",
    "ttl": 3600,
    "dataCenters": [
        "OR1"
    ],
    "version": 1
}
```

### Aggiornare una destinazione

È possibile aggiornare una destinazione esistente effettuando una richiesta PUT al `/config/destinations` e che include l’ID della destinazione da aggiornare nel percorso della richiesta. Questa operazione consiste essenzialmente nella riscrittura della destinazione, pertanto nel corpo della richiesta devono essere forniti gli stessi attributi forniti durante la creazione di una nuova destinazione.

>[!CAUTION]
>
>La risposta API alla richiesta di aggiornamento è immediata, tuttavia le modifiche alle proiezioni vengono applicate in modo asincrono. In altre parole, esiste una differenza di tempo tra il momento in cui viene effettuato l’aggiornamento alla definizione della destinazione e quello in cui viene applicato.

**Formato API**

```http
PUT /config/destinations/{DESTINATION_ID}
```

| Parametro | Descrizione |
|---|---|
| `{DESTINATION_ID}` | ID univoco della destinazione della proiezione che desideri aggiornare. |

**Richiesta**

La richiesta seguente aggiorna la destinazione esistente includendovi una seconda posizione (`dataCenters`).

>[!IMPORTANT]
>
>La richiesta PUT richiede un `Content-Type` come mostrato di seguito. Utilizzo di un `Content-Type` L’intestazione restituisce un errore HTTP Status 415 (Tipo di file multimediale non supportato).

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionDestination+json' \
  -d '{
        "type": "EDGE",
        "dataCenters": [ 
          "OR1",
          "VA5" 
        ],
        "replicationPolicy": REACTIVE,
        "currentVersion": 1
      }'
```

| Proprietà | Descrizione |
|---|---|
| `currentVersion` | La versione corrente della destinazione esistente. Il valore della proprietà `version` quando si esegue una richiesta di ricerca per la destinazione. |

**Risposta**

La risposta include i dettagli aggiornati per la destinazione, incluso il suo ID e il nuovo `version` della destinazione.

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7",
        "templated": false
    },
    "id": "8b90ce19-e7dd-403a-ae24-69683a6674e7",
    "type": "EDGE",
    "ttl": 8000,
    "dataCenters": [
        "OR1",
        "VA5"
    ],
    "version": 2
}
```

### Eliminare una destinazione

Se la tua organizzazione non richiede più una destinazione di proiezione, puoi eliminarla effettuando una richiesta DELETE al `/config/destinations` e includendo l’ID della destinazione da eliminare nel percorso della richiesta.

>[!CAUTION]
>
>La risposta API alla richiesta di eliminazione è immediata, tuttavia le modifiche effettive ai dati sui bordi si verificano in modo asincrono. In altre parole, i dati del profilo verranno rimossi da tutti i bordi (il `dataCenters` specificato nella destinazione di proiezione), ma il completamento del processo richiederà del tempo.

**Formato API**

```http
DELETE /config/destinations/{DESTINATION_ID}
```

| Parametro | Descrizione |
|---|---|
| `{DESTINATION_ID}` | ID univoco della destinazione di proiezione che desideri eliminare. |


**Richiesta**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La richiesta di eliminazione restituisce lo stato HTTP 204 (nessun contenuto) e un corpo di risposta vuoto. Puoi confermare che l’eliminazione è avvenuta correttamente eseguendo una richiesta di ricerca per la destinazione in base al relativo ID. La ricerca deve restituire lo stato HTTP 404 (non trovato).

## Configurazioni di proiezione

Le configurazioni di proiezione forniscono informazioni sui dati che dovrebbero essere disponibili su ogni lato. invece di proiettare un [!DNL Experience Data Model] (XDM) al server Edge di, una proiezione fornisce solo dati specifici, o campi, dallo schema. La tua organizzazione può definire più configurazioni di proiezione per ogni schema XDM.

### Elenca tutte le configurazioni di proiezione

È possibile elencare tutte le configurazioni di proiezione create per l&#39;organizzazione effettuando una richiesta di GET al `/config/projections` endpoint. Puoi anche aggiungere parametri facoltativi al percorso della richiesta per accedere alle configurazioni di proiezione per un particolare schema o cercare una singola proiezione in base al suo nome.

**Formato API**

```http
GET /config/projections
GET /config/projections?schemaName={SCHEMA_NAME}
GET /config/projections?schemaName={SCHEMA_NAME}&name={PROJECTION_NAME}
```

| Parametro | Descrizione |
|---|---|
| `{SCHEMA_NAME}` | Il nome della classe dello schema associata alla configurazione della proiezione a cui desideri accedere. |
| `{PROJECTION_NAME}` | Nome della configurazione di proiezione a cui si desidera accedere. |

>[!NOTE]
>
>`schemaName` è richiesto quando si utilizza `name` come nome della configurazione di una proiezione è univoco solo nel contesto di una classe di schema.

**Richiesta**

La richiesta seguente elenca tutte le configurazioni di proiezione associate alla [!DNL Experience Data Model] classe di schema, [!DNL XDM Individual Profile]. Per ulteriori informazioni su XDM e il suo ruolo in [!DNL Platform], iniziare leggendo il [Panoramica del sistema XDM](../../xdm/home.md).

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di configurazioni di proiezione all’interno della radice `_embedded` , contenuto all&#39;interno del `projectionConfigs` array. Se non sono state effettuate configurazioni di proiezione per la tua organizzazione, il `projectionConfigs` l’array sarà vuoto.

```json
{
    "_links": {
        "self": {
            "href": "/data/core/ups/config/projections",
            "templated": false
        }
    },
    "_embedded": {
        "projectionConfigs": [
            {
                "_links": {
                    "destination": {
                        "href": "/data/core/ups/config/destinations/a689248a-5d2b-44af-bb70-c8f17f97011b",
                        "templated": false
                    },
                    "self": {
                        "href": "/data/core/ups/config/projections/99aed0bc-c183-4997-ada7-7843642e08f6",
                        "templated": false
                    }
                },
                "_embedded": {
                    "destination": {
                        "self": {
                            "href": "/data/core/ups/config/destinations/a689248a-5d2b-44af-bb70-c8f17f97011b",
                            "templated": false
                        },
                        "id": "a689248a-5d2b-44af-bb70-c8f17f97011b",
                        "type": "EDGE",
                        "ttl": 1000,
                        "dataCenters": [
                            "OR1"
                        ],
                        "version": 1
                    }
                },
                "selector": "strategy",
                "version": 2,
                "id": "99aed0bc-c183-4997-ada7-7843642e08f6",
                "schemaName": "_xdm.context.profile",
                "name": "adcloud_rlsa",
                "destinationId": "a689248a-5d2b-44af-bb70-c8f17f97011b"
            },
        ]
    }
}
```

### Creare una configurazione di proiezione

Puoi creare (POST) una nuova configurazione di proiezione che determinerà quali campi XDM saranno disponibili sui bordi.

**Formato API**

```http
POST /config/projections?schemaName={SCHEMA_NAME}
```

| Parametro | Descrizione |
|---|---|
| `{SCHEMA_NAME}` | Il nome della classe dello schema associata alla configurazione della proiezione a cui desideri accedere. |

**Richiesta**

>[!NOTE]
>
>La richiesta POST di creazione di una configurazione richiede un `Content-Type` come mostrato di seguito. Utilizzo di un `Content-Type` L’intestazione restituisce un errore HTTP Status 415 (Tipo di file multimediale non supportato).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionConfig+json; version=1' \
  -d '{
        "selector": "emails,person(firstName)",
        "name": "my_test_projection",
        "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
      }'
```

| Proprietà | Descrizione |
|---|---|
| `selector` | Stringa contenente un elenco di proprietà all’interno dello schema che devono essere replicate ai bordi. Le best practice per l’utilizzo dei selettori sono disponibili nella sezione [Selettori](#selectors) sezione del presente documento. |
| `name` | Nome descrittivo per la nuova configurazione della proiezione. |
| `destinationId` | Identificatore della destinazione Edge alla quale verranno proiettati i dati. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della configurazione di proiezione appena creata.

```json
{
    "_links": {
        "destination": {
            "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
            "templated": false
        },
        "self": {
            "href": "/data/core/ups/config/projections/87fcd0bc-c183-4997-daf9-7843642g95a1",
            "templated": false
        }
    },
    "_embedded": {
        "destination": {
            "self": {
                "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
                "templated": false
            },
            "id": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
            "type": "EDGE",
            "ttl": 1000,
            "dataCenters": [
                "OR1"
            ],
            "version": 1
        }
    },
    "selector": "emails,person(firstName)",
    "version": 2,
    "id": "87fcd0bc-c183-4997-daf9-7843642g95a1",
    "schemaName": "_xdm.context.profile",
    "name": "my_test_projection",
    "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
}
```

## Selettori {#selectors}

Un selettore è un elenco separato da virgole di nomi di campi XDM. In una configurazione di proiezione, il selettore indica le proprietà da includere nelle proiezioni. Il formato del `selector` Il valore del parametro è liberamente basato sulla sintassi XPath. La sintassi supportata è riepilogata di seguito, con esempi aggiuntivi forniti come riferimento.

### Sintassi supportata

* Utilizza le virgole per selezionare più campi. Non utilizzare spazi.
* Utilizza la notazione con punto per selezionare i campi nidificati.
   * Ad esempio, per selezionare un campo denominato `field` nidificato all’interno di un campo denominato `foo`, utilizza il selettore `foo.field`.
* Quando si include un campo contenente campi secondari, per impostazione predefinita vengono proiettati anche tutti i campi secondari. Tuttavia, puoi filtrare i sottocampi restituiti utilizzando le parentesi `"( )"`.
   * Ad esempio: `addresses(type,city.country)` restituisce solo il tipo di indirizzo e il paese in cui si trova la città dell&#39;indirizzo per ogni `addresses` elemento di matrice.
   * L’esempio precedente equivale a `addresses.type,addresses.city.country`.

>[!NOTE]
>
>Per i sottocampi di riferimento sono supportate sia la notazione del punto che la notazione parentetica. Tuttavia, è consigliabile utilizzare la notazione del punto, in quanto è più concisa e fornisce una migliore illustrazione della gerarchia dei campi.

* Ogni campo in un selettore viene specificato rispetto alla radice della risposta.
   * Se i dati sono una raccolta di risorse, la proiezione includerà una matrice di risorse.
   * Se i dati sono una singola risorsa, la proiezione includerà i campi relativi a tale risorsa.
   * Se il campo selezionato è (o fa parte di) un array, la proiezione includerà la porzione selezionata di tutti gli elementi dell&#39;array.

### Esempi del parametro del selettore

Gli esempi seguenti mostrano un esempio `selector` , seguiti dai valori strutturati che rappresentano.

**person.lastName**

Restituisce il valore `lastName` sottocampo del `person` nella risorsa richiesta.

```json
{
  "person": {
    "lastName": "Smith"
  }
}
```

**indirizzi**

Restituisce tutti gli elementi nel `addresses` , inclusi tutti i campi di ciascun elemento, ma nessun altro campo.

```json
{
  "addresses": [
    {
      "type": "home",
      "street1": "100 Great Mall Parkway",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "street1": "1 Main Street",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

**person.lastName,indirizzi**

Restituisce il valore `person.lastName` e tutti gli elementi nel `addresses` array.

```json
{
  "person": {
    "lastName": "Smith"
  },
  "addresses": [
    {
      "type": "home",
      "street1": "100 Great Mall Parkway",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "street1": "1 Main Street",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

**addresses.city**

Restituisce solo il campo città per tutti gli elementi nella matrice indirizzi.

```json
{
  "addresses": [
    {
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

>[!NOTE]
>
>Ogni volta che viene restituito un campo nidificato, la proiezione include gli oggetti padre che lo contengono. I campi padre non includono altri campi figlio a meno che non siano selezionati esplicitamente.

**indirizzi(tipo,città)**

Restituisce solo i valori del `type` e `city` campi per ogni elemento nel `addresses` array. Tutti gli altri sottocampi contenuti in ciascuno `addresses` sono esclusi.

```json
{
  "addresses": [
    {
      "type": "home",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

## Passaggi successivi

Questa guida illustra i passaggi necessari per configurare proiezioni e destinazioni, e le modalità di formattazione del `selector` parametro. Ora puoi creare nuove destinazioni di proiezione e configurazioni specifiche per le esigenze della tua organizzazione.
