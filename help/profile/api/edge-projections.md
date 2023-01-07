---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Endpoint API per la proiezione Edge
type: Documentation
description: Adobe Experience Platform consente di gestire in tempo reale esperienze coordinate, coerenti e personalizzate per i clienti su più canali, rendendo i dati giusti immediatamente disponibili e costantemente aggiornati man mano che avvengono le modifiche. Questo avviene tramite l'uso di edge, un server collocato geograficamente che memorizza i dati e li rende facilmente accessibili alle applicazioni.
exl-id: ce429164-8e87-412d-9a9d-e0d4738c7815
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1959'
ht-degree: 2%

---

# Endpoint di destinazioni e configurazioni di proiezione Edge

Al fine di promuovere in tempo reale esperienze coordinate, coerenti e personalizzate per i clienti su più canali, i dati giusti devono essere prontamente disponibili e costantemente aggiornati man mano che si verificano cambiamenti. Adobe Experience Platform consente l’accesso in tempo reale ai dati tramite l’utilizzo dei cosiddetti edge. Un server perimetrale è un server collocato geograficamente che memorizza i dati e li rende facilmente accessibili alle applicazioni. Ad Adobe, applicazioni come Adobe Target e Adobe Campaign utilizzano i bordi per offrire esperienze cliente personalizzate in tempo reale. I dati vengono indirizzati a un bordo da una proiezione, con una destinazione di proiezione che definisce il bordo a cui i dati saranno inviati, e una configurazione di proiezione che definisce le informazioni specifiche che saranno rese disponibili sul bordo. Questa guida fornisce istruzioni dettagliate sull’utilizzo di [!DNL Real-Time Customer Profile] API per lavorare con proiezioni edge, incluse destinazioni e configurazioni.

## Introduzione

L’endpoint API utilizzato in questa guida fa parte del [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Prima di continuare, controlla la [guida introduttiva](getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio presenti in questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi [!DNL Experience Platform] API.

>[!NOTE]
>
>Le richieste che contengono un payload (POST, PUT, PATCH) richiedono un `Content-Type` intestazione. Più di uno `Content-Type` viene utilizzato in questo documento. Presta particolare attenzione alle intestazioni nelle chiamate di esempio per assicurarti di utilizzare la `Content-Type` per ogni richiesta.

## Destinazioni di proiezione

Una proiezione può essere indirizzata a uno o più bordi specificando le posizioni in cui i dati devono essere inviati. Ogni destinazione di proiezione creata ha un ID univoco che viene quindi utilizzato per creare la configurazione di proiezione.

### Elenca tutte le destinazioni

Puoi elencare le destinazioni edge già create per la tua organizzazione effettuando una richiesta di GET al `/config/destinations` punto finale.

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

La risposta include un `projectionDestinations` array con i dettagli di ogni destinazione mostrati come un singolo oggetto all&#39;interno dell&#39;array. Se non è stata configurata alcuna proiezione, la `projectionDestinations` restituisce empty.

>[!NOTE]
>
>Questa risposta è stata ridotta per lo spazio e mostra solo due destinazioni.

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
| `_links.self.href` | Al livello principale, corrisponde al percorso utilizzato per effettuare la richiesta GET. All&#39;interno di ogni singolo oggetto di destinazione, questo percorso può essere utilizzato in una richiesta di GET per cercare direttamente i dettagli di una destinazione specifica. |
| `id` | All&#39;interno di ogni oggetto di destinazione, il `"id"` mostra l’ID univoco generato dal sistema di sola lettura per la destinazione. Questo ID viene utilizzato quando si fa riferimento a una destinazione specifica e quando si creano configurazioni di proiezione. |

Per ulteriori informazioni sugli attributi di una singola destinazione, consulta la sezione [creazione di una destinazione](#create-a-destination) segue.

### Creare una destinazione {#create-a-destination}

Se la destinazione desiderata non esiste già, è possibile creare una nuova destinazione di proiezione effettuando una richiesta POST al `/config/destinations` punto finale.

**Formato API**

```http
POST /config/destinations
```

**Richiesta**

Nella richiesta seguente viene creata una nuova destinazione Edge.

>[!NOTE]
>
>La richiesta di POST per creare una destinazione richiede un `Content-Type` , come illustrato di seguito. Utilizzo di un errore `Content-Type` l’intestazione restituisce un errore di stato HTTP 415 (tipo di supporto non supportato).

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
| `type` **(Obbligatorio)** | Il tipo di destinazione da creare. L’unico valore accettato, &quot;EDGE&quot;, crea una destinazione Edge. |
| `dataCenters` **(Obbligatorio)** | Matrice di stringhe che elenca i bordi verso i quali le proiezioni devono essere instradate. Può contenere uno o più dei seguenti valori: &quot;OR1&quot; - Stati Uniti occidentali, &quot;VA5&quot; - Stati Uniti orientali, &quot;NLD1&quot; - EMEA. |
| `ttl` **(Obbligatorio)** | Specifica la scadenza della proiezione. Intervallo di valori accettati: Da 600 a 604800. Valore predefinito: 3600. |
| `replicationPolicy` **(Obbligatorio)** | Definisce il comportamento della replica dei dati dall&#39;hub ai bordi.  Valori supportati: PROATTIVO E REATTIVO. Valore predefinito: REATTIVO. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova destinazione Edge creata, incluso l’ID univoco generato dal sistema di sola lettura (`id`).

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
| `self.href` | Questo percorso viene utilizzato per cercare direttamente (GET) la destinazione e può anche essere utilizzato per aggiornare (PUT) o eliminare (DELETE) la destinazione. |
| `id` | L&#39;ID univoco generato dal sistema di sola lettura per la destinazione. Questo ID viene utilizzato per fare riferimento direttamente alla destinazione e durante la creazione di configurazioni di proiezione. |
| `version` | Questo valore di sola lettura mostra la versione corrente della destinazione. Quando una destinazione viene aggiornata, il numero di versione viene incrementato automaticamente. |

### Visualizzare una destinazione

Se conosci l&#39;ID univoco di una destinazione di proiezione, puoi eseguire una richiesta di ricerca per visualizzarne i dettagli. A tal fine, invia una richiesta GET al `/config/destinations` e include l&#39;ID della destinazione nel percorso della richiesta.

**Formato API**

```http
GET /config/destinations/{DESTINATION_ID}
```

| Parametro | Descrizione |
|---|---|
| `{DESTINATION_ID}` | ID univoco della destinazione di proiezione che si desidera visualizzare. |

**Richiesta**

La seguente richiesta esegue una ricerca (GET) per visualizzare la destinazione dell’ID fornito nel percorso della richiesta.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations/9d66c06e-c745-480c-b64c-1d5234d25f4b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

L&#39;oggetto response mostra i dettagli della destinazione di proiezione. La `id` L&#39;attributo deve corrispondere all&#39;ID della destinazione di proiezione fornita nella richiesta.

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

È possibile aggiornare una destinazione esistente effettuando una richiesta di PUT al `/config/destinations` e l’ID della destinazione da aggiornare nel percorso della richiesta. Questa operazione sta essenzialmente riscrivendo la destinazione, pertanto gli stessi attributi devono essere forniti nel corpo della richiesta come vengono forniti durante la creazione di una nuova destinazione.

>[!CAUTION]
>
>La risposta API alla richiesta di aggiornamento è immediata, ma le modifiche alle proiezioni vengono applicate in modo asincrono. In altre parole, esiste una differenza di tempo tra quando viene effettuato l’aggiornamento alla definizione della destinazione e quando viene applicato.

**Formato API**

```http
PUT /config/destinations/{DESTINATION_ID}
```

| Parametro | Descrizione |
|---|---|
| `{DESTINATION_ID}` | ID univoco della destinazione di proiezione che si desidera aggiornare. |

**Richiesta**

La richiesta seguente aggiorna la destinazione esistente in modo che includa una seconda posizione (`dataCenters`).

>[!IMPORTANT]
>
>La richiesta PUT richiede uno specifico `Content-Type` , come illustrato di seguito. Utilizzo di un errore `Content-Type` l’intestazione restituisce un errore di stato HTTP 415 (tipo di supporto non supportato).

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
| `currentVersion` | Versione corrente della destinazione esistente. Il valore del `version` quando si esegue una richiesta di ricerca per la destinazione. |

**Risposta**

La risposta include i dettagli aggiornati della destinazione, compreso il relativo ID e il nuovo `version` della destinazione.

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

Se l’organizzazione non richiede più una destinazione di proiezione, può essere eliminata effettuando una richiesta DELETE al `/config/destinations` e l’ID della destinazione che desideri eliminare nel percorso della richiesta.

>[!CAUTION]
>
>La risposta API alla richiesta di eliminazione è immediata, ma le modifiche effettive ai dati sui bordi avvengono in modo asincrono. In altre parole, i dati del profilo verranno rimossi da tutti i bordi (il `dataCenters` specificato nella destinazione di proiezione), ma il processo richiederà del tempo per essere completato.

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

La richiesta di eliminazione restituisce lo stato HTTP 204 (nessun contenuto) e un corpo di risposta vuoto. Puoi confermare che l’eliminazione è avvenuta correttamente eseguendo una richiesta di ricerca per la destinazione in base al relativo ID. La ricerca deve restituire lo stato HTTP 404 (Non trovato).

## Configurazioni di proiezione

Le configurazioni di proiezione forniscono informazioni su quali dati dovrebbero essere disponibili su ciascun bordo. Piuttosto che proiettare un [!DNL Experience Data Model] (XDM) schema al bordo, una proiezione fornisce solo dati specifici, o campi, dallo schema. La tua organizzazione può definire più di una configurazione di proiezione per ogni schema XDM.

### Elenca tutte le configurazioni di proiezione

Puoi elencare tutte le configurazioni di proiezione create per la tua organizzazione effettuando una richiesta di GET al `/config/projections` punto finale. È inoltre possibile aggiungere parametri facoltativi al percorso della richiesta per accedere alle configurazioni di proiezione per uno schema specifico o cercare una proiezione singola in base al nome.

**Formato API**

```http
GET /config/projections
GET /config/projections?schemaName={SCHEMA_NAME}
GET /config/projections?schemaName={SCHEMA_NAME}&name={PROJECTION_NAME}
```

| Parametro | Descrizione |
|---|---|
| `{SCHEMA_NAME}` | Nome della classe dello schema associata alla configurazione di proiezione a cui si desidera accedere. |
| `{PROJECTION_NAME}` | Nome della configurazione di proiezione a cui si desidera accedere. |

>[!NOTE]
>
>`schemaName` è necessario quando si utilizza il `name` come nome della configurazione di proiezione è univoco solo nel contesto di una classe di schema.

**Richiesta**

Nella richiesta seguente sono elencate tutte le configurazioni di proiezione associate al [!DNL Experience Data Model] classe schema, [!DNL XDM Individual Profile]. Per ulteriori informazioni su XDM e sul suo ruolo in [!DNL Platform], per favore inizia leggendo il [Panoramica del sistema XDM](../../xdm/home.md).

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di configurazioni di proiezione all&#39;interno della radice `_embedded` attributo contenuto nel `projectionConfigs` array. Se non è stata effettuata alcuna configurazione di proiezione per la tua organizzazione, la `projectionConfigs` array vuoto.

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

È possibile creare (POST) una nuova configurazione di proiezione che determina quali campi XDM sono resi disponibili sui bordi.

**Formato API**

```http
POST /config/projections?schemaName={SCHEMA_NAME}
```

| Parametro | Descrizione |
|---|---|
| `{SCHEMA_NAME}` | Nome della classe dello schema associata alla configurazione di proiezione a cui si desidera accedere. |

**Richiesta**

>[!NOTE]
>
>La richiesta di POST per creare una configurazione richiede un `Content-Type` , come illustrato di seguito. Utilizzo di un errore `Content-Type` l’intestazione restituisce un errore di stato HTTP 415 (tipo di supporto non supportato).

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
| `selector` | Una stringa contenente un elenco di proprietà all&#39;interno dello schema da replicare ai bordi. Le best practice per lavorare con i selettori sono disponibili nella sezione [Selettori](#selectors) sezione di questo documento. |
| `name` | Un nome descrittivo per la nuova configurazione di proiezione. |
| `destinationId` | Identificatore della destinazione perimetrale a cui verranno proiettati i dati. |

**Risposta**

Una risposta corretta restituisce i dettagli della configurazione di proiezione appena creata.

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

Un selettore è un elenco separato da virgole di nomi di campi XDM. In una configurazione di proiezione, il selettore designa le proprietà da includere nelle proiezioni. Il formato del `selector` Il valore del parametro è liberamente basato sulla sintassi XPath. Di seguito è riportato un riepilogo della sintassi supportata, con ulteriori esempi di riferimento.

### Sintassi supportata

* Utilizzare le virgole per selezionare più campi. Non utilizzare spazi.
* Utilizzare la notazione del punto per selezionare i campi nidificati.
   * Ad esempio, per selezionare un campo denominato `field` nidificato all’interno di un campo denominato `foo`, utilizza il selettore `foo.field`.
* Se si include un campo contenente campi secondari, anche tutti i campi secondari vengono proiettati per impostazione predefinita. Tuttavia, è possibile filtrare i campi secondari restituiti utilizzando le parentesi `"( )"`.
   * Ad esempio: `addresses(type,city.country)` restituisce solo il tipo di indirizzo e il paese in cui si trova la città dell&#39;indirizzo per ogni `addresses` elemento array.
   * L&#39;esempio precedente è equivalente a `addresses.type,addresses.city.country`.

>[!NOTE]
>
>Per fare riferimento ai campi secondari sono supportate sia la notazione del punto che la notazione tra parentesi. Tuttavia, è consigliabile utilizzare la notazione del punto perché è più concisa e fornisce una migliore illustrazione della gerarchia dei campi.

* Ogni campo di un selettore viene specificato relativo alla directory principale della risposta.
   * Se i dati sono una raccolta di risorse, la proiezione includerà una matrice di risorse.
   * Se i dati sono una singola risorsa, la proiezione includerà i campi relativi a tale risorsa.
   * Se il campo selezionato è (o fa parte) di una matrice, la proiezione includerà la parte selezionata di tutti gli elementi della matrice.

### Esempi del parametro del selettore

Gli esempi seguenti mostrano un esempio `selector` , seguiti dai valori strutturati che rappresentano.

**person.lastName**

Restituisce il `lastName` sottocampo della `person` nella risorsa richiesta.

```json
{
  "person": {
    "lastName": "Smith"
  }
}
```

**indirizzi**

Restituisce tutti gli elementi nel `addresses` array, inclusi tutti i campi in ciascun elemento, ma nessun altro campo.

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

**person.lastName,addresses**

Restituisce il `person.lastName` e tutti gli elementi nel `addresses` array.

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

Restituisce solo il campo city per tutti gli elementi della matrice indirizzi.

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
>Ogni volta che viene restituito un campo nidificato, la proiezione include gli oggetti principali che lo contengono. I campi principali non includono altri campi secondari, a meno che non siano anche selezionati esplicitamente.

**indirizzi(tipo, città)**

Restituisce solo i valori del `type` e `city` campi per ogni elemento nel `addresses` array. Tutti gli altri sottocampi contenuti in ciascuno `addresses` gli elementi vengono filtrati.

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

Questa guida illustra i passaggi necessari per configurare proiezioni e destinazioni, tra cui come formattare correttamente il `selector` parametro . Ora puoi creare nuove destinazioni e configurazioni di proiezione specifiche per le esigenze della tua organizzazione.
