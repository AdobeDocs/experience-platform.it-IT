---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guida per lo sviluppatore di API profilo cliente in tempo reale
topic: guide
translation-type: tm+mt
source-git-commit: d464a6b4abd843f5f8545bc3aa8000f379a86c6d
workflow-type: tm+mt
source-wordcount: '1919'
ht-degree: 2%

---


# Configurazioni di proiezione Edge e endpoint di destinazioni

Al fine di promuovere esperienze coordinate, coerenti e personalizzate per i clienti attraverso più canali in tempo reale, i dati giusti devono essere prontamente disponibili e costantemente aggiornati man mano che si verificano le modifiche.  Adobe Experience Platform consente l&#39;accesso in tempo reale ai dati attraverso l&#39;uso di ciò che sono noti come edge. Un server periferico è un server collocato geograficamente che memorizza i dati e li rende facilmente accessibili alle applicazioni. Ad esempio, applicazioni Adobe come  Adobe Target e  Adobe Campaign utilizzano i bordi per fornire esperienze personalizzate ai clienti in tempo reale. I dati vengono indirizzati a un bordo da una proiezione, con una destinazione di proiezione che definisce il bordo a cui verranno inviati i dati, e una configurazione di proiezione che definisce le informazioni specifiche che verranno rese disponibili sul bordo. Questa guida fornisce istruzioni dettagliate per l’utilizzo dell’API Profilo cliente in tempo reale per lavorare con proiezioni Edge, incluse destinazioni e configurazioni.

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte dell&#39;API [Profilo cliente in tempo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)reale. Prima di continuare, consultate la guida [](getting-started.md) introduttiva per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente chiamate a qualsiasi API Experience Platform .

>[!NOTE]
>Le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39; `Content-Type` intestazione. Nel documento `Content-Type` vengono utilizzati più di uno. Prestate particolare attenzione alle intestazioni delle chiamate di esempio per verificare di utilizzare la versione corretta `Content-Type` per ogni richiesta.

## Destinazioni di proiezione

Una proiezione può essere instradata a uno o più bordi specificando le posizioni in cui inviare i dati. Ogni destinazione di proiezione creata ha un ID univoco che viene quindi utilizzato per creare la configurazione di proiezione.

### Elenca tutte le destinazioni

Potete elencare le destinazioni periferiche già create per la vostra organizzazione eseguendo una richiesta GET all&#39; `/config/destinations` endpoint.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta include un `projectionDestinations` &#39;array con i dettagli per ogni destinazione visualizzati come singolo oggetto all&#39;interno dell&#39;array. Se non è stata configurata alcuna proiezione, l&#39; `projectionDestinations` array restituisce empty.

>[!NOTE]
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
| `_links.self.href` | Al livello principale corrisponde al percorso utilizzato per effettuare la richiesta GET. All&#39;interno di ciascun oggetto di destinazione, questo percorso può essere utilizzato in una richiesta GET per cercare direttamente i dettagli di una destinazione specifica. |
| `id` | All&#39;interno di ciascun oggetto di destinazione, `"id"` viene visualizzato l&#39;ID univoco generato dal sistema di sola lettura per la destinazione. Questo ID viene utilizzato quando si fa riferimento a una destinazione specifica e quando si creano configurazioni di proiezione. |

Per ulteriori informazioni sugli attributi di una singola destinazione, consulta la sezione sulla [creazione di una destinazione](#create-a-destination) che segue.

### Creare una destinazione {#create-a-destination}

Se la destinazione desiderata non esiste già, potete creare una nuova destinazione di proiezione effettuando una richiesta POST all&#39; `/config/destinations` endpoint.

**Formato API**

```http
POST /config/destinations
```

**Richiesta**

La richiesta seguente crea una nuova destinazione edge.

>[!NOTE]
>La richiesta POST per creare una destinazione richiede un&#39; `Content-Type` intestazione specifica, come illustrato di seguito. Se si utilizza un&#39; `Content-Type` intestazione non corretta, si verifica un errore HTTP Status 415 (Tipo di supporto non supportato).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `type` **(Obbligatorio)** | Il tipo di destinazione da creare. L’unico valore accettato, &quot;EDGE&quot;, crea una destinazione edge. |
| `dataCenters` **(Obbligatorio)** | Un array di stringhe che elenca i bordi verso i quali le proiezioni devono essere instradate. Può contenere uno o più dei seguenti valori: &quot;OR1&quot; - Stati Uniti occidentali, &quot;VA5&quot; - Stati Uniti orientali, &quot;NLD1&quot; - EMEA. |
| `ttl` **(Obbligatorio)** | Specifica la scadenza della proiezione. Intervallo valori accettato: Da 600 a 604800. Valore predefinito: 3600. |
| `replicationPolicy` **(Obbligatorio)** | Definisce il comportamento della replica dei dati dall&#39;hub ai bordi.  Valori supportati: PROATTIVO, REATTIVO. Valore predefinito: REATTIVO. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova destinazione Edge creata, incluso l&#39;ID univoco generato dal sistema (`id`) di sola lettura.

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
| `self.href` | Questo percorso viene utilizzato per cercare (GET) direttamente la destinazione e può essere utilizzato anche per aggiornare (PUT) o eliminare (DELETE) la destinazione. |
| `id` | L&#39;ID univoco generato dal sistema di sola lettura per la destinazione. Questo ID viene utilizzato per fare riferimento direttamente alla destinazione e durante la creazione di configurazioni di proiezione. |
| `version` | Questo valore di sola lettura mostra la versione corrente della destinazione. Quando una destinazione viene aggiornata, il numero di versione aumenta automaticamente. |

### Visualizzare una destinazione

Se conoscete l&#39;ID univoco di una destinazione di proiezione, potete eseguire una richiesta di ricerca per visualizzarne i dettagli. A tal fine, viene effettuata una richiesta GET all&#39; `/config/destinations` endpoint e viene incluso l&#39;ID della destinazione nel percorso della richiesta.

**Formato API**

```http
GET /config/destinations/{DESTINATION_ID}
```

| Parametro | Descrizione |
|---|---|
| `{DESTINATION_ID}` | L&#39;ID univoco della destinazione di proiezione che si desidera visualizzare. |

**Richiesta**

La seguente richiesta esegue una ricerca (GET) per visualizzare la destinazione dell&#39;ID fornito nel percorso della richiesta.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations/9d66c06e-c745-480c-b64c-1d5234d25f4b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

L&#39;oggetto response mostra i dettagli della destinazione di proiezione. L&#39; `id` attributo deve corrispondere all&#39;ID della destinazione di proiezione fornita nella richiesta.

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

Una destinazione esistente può essere aggiornata effettuando una richiesta PUT all&#39; `/config/destinations` endpoint e includendo l&#39;ID della destinazione da aggiornare nel percorso della richiesta. Questa operazione _riscrive_ la destinazione, pertanto nel corpo della richiesta devono essere forniti gli stessi attributi forniti al momento della creazione di una nuova destinazione.

>[!CAUTION]
>La risposta API alla richiesta di aggiornamento è immediata, ma le modifiche alle proiezioni vengono applicate in modo asincrono. In altre parole, esiste una differenza di tempo tra quando viene effettuato l&#39;aggiornamento alla definizione della destinazione e quando viene applicato.

**Formato API**

```
PUT /config/destinations/{DESTINATION_ID}
```

| Parametro | Descrizione |
|---|---|
| `{DESTINATION_ID}` | L&#39;ID univoco della destinazione di proiezione che si desidera aggiornare. |

**Richiesta**

La seguente richiesta aggiorna la destinazione esistente per includere una seconda posizione (`dataCenters`).

>[!IMPORTANT]
>La richiesta PUT richiede un&#39; `Content-Type` intestazione specifica, come illustrato di seguito. Se si utilizza un&#39; `Content-Type` intestazione non corretta, si verifica un errore HTTP Status 415 (Tipo di supporto non supportato).

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `currentVersion` | La versione corrente della destinazione esistente. Il valore dell&#39; `version` attributo quando si esegue una richiesta di ricerca per la destinazione. |

**Risposta**

La risposta include i dettagli aggiornati per la destinazione, incluso il relativo ID e il nuovo `version` della destinazione.

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

Se l&#39;organizzazione non richiede più una destinazione di proiezione, può essere eliminata effettuando una richiesta di DELETE all&#39; `/config/destinations` endpoint e includendo l&#39;ID della destinazione che si desidera eliminare nel percorso della richiesta.

>[!CAUTION]
>La risposta API alla richiesta di eliminazione è immediata, ma le modifiche effettive ai dati sui bordi avvengono in modo asincrono. In altre parole, i dati del profilo verranno rimossi da tutti i bordi ( `dataCenters` specificati nella destinazione di proiezione), ma il processo richiederà del tempo per essere completato.

**Formato API**

```
DELETE /config/destinations/{DESTINATION_ID}
```

| Parametro | Descrizione |
|---|---|
| `{DESTINATION_ID}` | L&#39;ID univoco della destinazione di proiezione che si desidera eliminare. |


**Richiesta**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La richiesta di eliminazione restituisce lo stato HTTP 204 (Nessun contenuto) e un corpo di risposta vuoto. È possibile confermare che l&#39;eliminazione è avvenuta correttamente eseguendo una richiesta di ricerca per la destinazione tramite il relativo ID. La ricerca deve restituire lo stato HTTP 404 (Non trovato).

## Configurazioni di proiezione

Le configurazioni di proiezione forniscono informazioni su quali dati devono essere disponibili su ciascun bordo. Anziché proiettare uno schema XDM (Experience Data Model) completo sul margine, una proiezione fornisce solo dati o campi specifici dallo schema. L&#39;organizzazione può definire più di una configurazione di proiezione per ogni schema XDM.

### Elenca tutte le configurazioni di proiezione

Potete elencare tutte le configurazioni di proiezione che sono state create per la vostra organizzazione effettuando una richiesta GET all&#39; `/config/projections` endpoint. È inoltre possibile aggiungere parametri facoltativi al percorso della richiesta per accedere alle configurazioni di proiezione per uno schema specifico o per cercare una proiezione singola in base al nome.

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
>`schemaName` è richiesto quando si utilizza il `name` parametro, come nome di configurazione di proiezione è univoco solo nel contesto di una classe di schema.

**Richiesta**

Nella richiesta seguente sono elencate tutte le configurazioni di proiezione associate alla classe dello schema Experience Data Model, XDM Individuale Profile. Per ulteriori informazioni su XDM e sul suo ruolo all&#39;interno di Platform, consultare la panoramica [del sistema](../../xdm/home.md)XDM.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di configurazioni di proiezione all&#39;interno dell&#39; `_embedded` attributo principale, contenuto nell&#39; `projectionConfigs` array. Se non sono state eseguite configurazioni di proiezione per la vostra organizzazione, l&#39; `projectionConfigs` array sarà vuoto.

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

È possibile creare (POST) una nuova configurazione di proiezione che determinerà quali campi XDM rendere disponibili sui bordi.

**Formato API**

```http
POST /config/projections?schemaName={SCHEMA_NAME}
```

| Parametro | Descrizione |
|---|---|
| `{SCHEMA_NAME}` | Nome della classe dello schema associata alla configurazione di proiezione a cui si desidera accedere. |

**Richiesta**

>[!NOTE]
>La richiesta POST per creare una configurazione richiede un&#39; `Content-Type` intestazione specifica, come illustrato di seguito. Se si utilizza un&#39; `Content-Type` intestazione non corretta, si verifica un errore HTTP Status 415 (Tipo di supporto non supportato).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `selector` | Una stringa contenente un elenco di proprietà all&#39;interno dello schema da replicare ai bordi. Le best practice per lavorare con i selettori sono disponibili nella sezione [Selettori](#selectors) di questo documento. |
| `name` | Un nome descrittivo per la nuova configurazione di proiezione. |
| `destinationId` | Identificatore per la destinazione del bordo a cui verranno proiettati i dati. |

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

## Selectors {#selectors}

Un selettore è un elenco separato da virgole di nomi di campi XDM. In una configurazione di proiezione, il selettore indica le proprietà da includere nelle proiezioni. Il formato del valore del `selector` parametro è vagamente basato sulla sintassi XPath. Di seguito viene riepilogata la sintassi supportata, con ulteriori esempi di riferimento.

### Sintassi supportata

* Utilizzate le virgole per selezionare più campi. Non utilizzate gli spazi.
* Utilizzare la notazione dei punti per selezionare i campi nidificati.
   * Ad esempio, per selezionare un campo denominato `field` nidificato all&#39;interno di un campo denominato `foo`, utilizzare il selettore `foo.field`.
* Se si inserisce un campo contenente campi secondari, anche tutti i campi secondari vengono proiettati per impostazione predefinita. Tuttavia, è possibile filtrare i campi secondari restituiti utilizzando le parentesi `"( )"`.
   * Ad esempio, `addresses(type,city.country)` restituisce solo il tipo di indirizzo e il paese in cui si trova la città dell&#39;indirizzo per ciascun elemento `addresses` array.
   * L&#39;esempio precedente è equivalente a `addresses.type,addresses.city.country`.

>[!NOTE]
>La notazione dei punti e la notazione parentetica sono supportate per fare riferimento ai campi secondari. Tuttavia, è consigliabile utilizzare la notazione dei punti in quanto è più concisa e fornisce una migliore illustrazione della gerarchia dei campi.

* Ciascun campo di un selettore viene specificato rispetto al livello principale della risposta.
   * Se i dati sono una raccolta di risorse, la proiezione includerà un array di risorse.
   * Se i dati sono una singola risorsa, la proiezione includerà i campi relativi a tale risorsa.
   * Se il campo selezionato è (o fa parte di) un array, la proiezione includerà la parte selezionata di tutti gli elementi dell&#39;array.

### Esempi del parametro del selettore

Gli esempi seguenti mostrano parametri di esempio `selector` , seguiti dai valori strutturati che rappresentano.

**Persona.lastName**

Restituisce il `lastName` sottocampo dell&#39; `person` oggetto nella risorsa richiesta.

```json
{
  "person": {
    "lastName": "Smith"
  }
}
```

**address**

Restituisce tutti gli elementi dell&#39; `addresses` array, inclusi tutti i campi di ciascun elemento, ma nessun altro campo.

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

**Persona.lastName,indirizzi**

Restituisce il `person.lastName` campo e tutti gli elementi dell&#39; `addresses` array.

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

**address.city**

Restituisce solo il campo city per tutti gli elementi dell&#39;array address.

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
>Ogni volta che viene restituito un campo nidificato, la proiezione include gli oggetti principali che lo contengono. I campi principali non includono altri campi secondari, a meno che non siano selezionati in modo esplicito.

**address(type,city)**

Restituisce solo i valori dei campi `type` e `city` per ogni elemento dell&#39; `addresses` array. Tutti gli altri sottocampi contenuti in ciascun `addresses` elemento vengono filtrati.

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

Questa guida illustra i passaggi necessari per configurare le proiezioni e le destinazioni, incluso come formattare correttamente il `selector` parametro. Ora puoi creare nuove destinazioni di proiezione e configurazioni specifiche per le esigenze della tua organizzazione.