---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Endpoint API per la proiezione Edge
topic: guida
type: Documentazione
description: Adobe Experience Platform ti consente di promuovere esperienze coordinate, coerenti e personalizzate per i tuoi clienti su più canali in tempo reale, rendendo i dati giusti immediatamente disponibili e costantemente aggiornati man mano che avvengono le modifiche. Questo avviene tramite l'uso di edge, un server collocato geograficamente che memorizza i dati e li rende facilmente accessibili alle applicazioni.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '1966'
ht-degree: 2%

---


# Endpoint di destinazioni e configurazioni di proiezione Edge

Al fine di promuovere in tempo reale esperienze coordinate, coerenti e personalizzate per i clienti su più canali, i dati giusti devono essere prontamente disponibili e costantemente aggiornati man mano che si verificano cambiamenti. Adobe Experience Platform consente l’accesso in tempo reale ai dati tramite l’utilizzo dei cosiddetti edge. Un server perimetrale è un server collocato geograficamente che memorizza i dati e li rende facilmente accessibili alle applicazioni. Ad esempio, le applicazioni Adobe come Adobe Target e Adobe Campaign utilizzano i bordi per fornire esperienze cliente personalizzate in tempo reale. I dati vengono indirizzati a un bordo da una proiezione, con una destinazione di proiezione che definisce il bordo a cui i dati saranno inviati, e una configurazione di proiezione che definisce le informazioni specifiche che saranno rese disponibili sul bordo. Questa guida fornisce istruzioni dettagliate sull’utilizzo dell’API [!DNL Real-time Customer Profile] per lavorare con le proiezioni edge, incluse destinazioni e configurazioni.

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte del [[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). Prima di continuare, controlla la [guida introduttiva](getting-started.md) per i collegamenti alla relativa documentazione, una guida per la lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API [!DNL Experience Platform].

>[!NOTE]
>
>Le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione `Content-Type`. In questo documento vengono utilizzati più `Content-Type`. Presta particolare attenzione alle intestazioni nelle chiamate di esempio per assicurarti di utilizzare la `Content-Type` corretta per ogni richiesta.

## Destinazioni di proiezione

Una proiezione può essere indirizzata a uno o più bordi specificando le posizioni in cui i dati devono essere inviati. Ogni destinazione di proiezione creata ha un ID univoco che viene quindi utilizzato per creare la configurazione di proiezione.

### Elenca tutte le destinazioni

Puoi elencare le destinazioni edge che sono già state create per la tua organizzazione effettuando una richiesta GET all’ endpoint `/config/destinations` .

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

La risposta include un array `projectionDestinations` con i dettagli di ogni destinazione mostrati come un singolo oggetto all&#39;interno dell&#39;array. Se non è stata configurata alcuna proiezione, l&#39;array `projectionDestinations` restituisce vuoto.

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
| `_links.self.href` | Al livello principale, corrisponde al percorso utilizzato per effettuare la richiesta GET. All&#39;interno di ogni singolo oggetto di destinazione, questo percorso può essere utilizzato in una richiesta GET per cercare direttamente i dettagli di una destinazione specifica. |
| `id` | All&#39;interno di ogni oggetto di destinazione, il `"id"` mostra l&#39;ID univoco generato dal sistema di sola lettura per la destinazione. Questo ID viene utilizzato quando si fa riferimento a una destinazione specifica e quando si creano configurazioni di proiezione. |

Per ulteriori informazioni sugli attributi di una singola destinazione, consulta la sezione sulla [creazione di una destinazione](#create-a-destination) che segue.

### Creare una destinazione {#create-a-destination}

Se la destinazione desiderata non esiste già, è possibile creare una nuova destinazione di proiezione effettuando una richiesta POST all&#39;endpoint `/config/destinations`.

**Formato API**

```http
POST /config/destinations
```

**Richiesta**

Nella richiesta seguente viene creata una nuova destinazione Edge.

>[!NOTE]
>
>La richiesta POST per creare una destinazione richiede un’intestazione `Content-Type` specifica, come illustrato di seguito. Se si utilizza un&#39;intestazione `Content-Type` errata, si verifica un errore di stato HTTP 415 (tipo di supporto non supportato).

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
| `self.href` | Questo percorso viene utilizzato per cercare direttamente la destinazione (GET) e può anche essere utilizzato per aggiornare (PUT) o eliminare (DELETE) la destinazione. |
| `id` | L&#39;ID univoco generato dal sistema di sola lettura per la destinazione. Questo ID viene utilizzato per fare riferimento direttamente alla destinazione e durante la creazione di configurazioni di proiezione. |
| `version` | Questo valore di sola lettura mostra la versione corrente della destinazione. Quando una destinazione viene aggiornata, il numero di versione viene incrementato automaticamente. |

### Visualizzare una destinazione

Se conosci l&#39;ID univoco di una destinazione di proiezione, puoi eseguire una richiesta di ricerca per visualizzarne i dettagli. A questo scopo, invia una richiesta GET all’ endpoint `/config/destinations` e include l’ID della destinazione nel percorso della richiesta.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

L&#39;oggetto response mostra i dettagli della destinazione di proiezione. L&#39;attributo `id` deve corrispondere all&#39;ID della destinazione di proiezione fornita nella richiesta.

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

Una destinazione esistente può essere aggiornata effettuando una richiesta PUT all’ endpoint `/config/destinations` e includendo l’ID della destinazione da aggiornare nel percorso della richiesta. Questa operazione sta essenzialmente riscrivendo la destinazione, pertanto gli stessi attributi devono essere forniti nel corpo della richiesta come vengono forniti durante la creazione di una nuova destinazione.

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

La richiesta seguente aggiorna la destinazione esistente in modo da includere una seconda posizione (`dataCenters`).

>[!IMPORTANT]
>
>La richiesta PUT richiede un&#39;intestazione `Content-Type` specifica, come illustrato di seguito. Se si utilizza un&#39;intestazione `Content-Type` errata, si verifica un errore di stato HTTP 415 (tipo di supporto non supportato).

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
| `currentVersion` | Versione corrente della destinazione esistente. Il valore dell&#39;attributo `version` quando si esegue una richiesta di ricerca per la destinazione. |

**Risposta**

La risposta include i dettagli aggiornati della destinazione, compreso il relativo ID e la nuova `version` della destinazione.

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

Se l&#39;organizzazione non richiede più una destinazione di proiezione, può essere eliminata effettuando una richiesta DELETE all&#39;endpoint `/config/destinations` e includendo l&#39;ID della destinazione che si desidera eliminare nel percorso della richiesta.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La richiesta di eliminazione restituisce lo stato HTTP 204 (nessun contenuto) e un corpo di risposta vuoto. Puoi confermare che l’eliminazione è avvenuta correttamente eseguendo una richiesta di ricerca per la destinazione in base al relativo ID. La ricerca deve restituire lo stato HTTP 404 (Non trovato).

## Configurazioni di proiezione

Le configurazioni di proiezione forniscono informazioni su quali dati dovrebbero essere disponibili su ciascun bordo. Invece di proiettare uno schema [!DNL Experience Data Model] completo (XDM) sul bordo, una proiezione fornisce solo dati specifici, o campi, dallo schema. La tua organizzazione può definire più di una configurazione di proiezione per ogni schema XDM.

### Elenca tutte le configurazioni di proiezione

È possibile elencare tutte le configurazioni di proiezione create per la propria organizzazione effettuando una richiesta GET all&#39;endpoint `/config/projections`. È inoltre possibile aggiungere parametri facoltativi al percorso della richiesta per accedere alle configurazioni di proiezione per uno schema specifico o cercare una proiezione singola in base al nome.

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
>`schemaName` è richiesto quando si utilizza il  `name` parametro , in quanto il nome di una configurazione di proiezione è univoco solo nel contesto di una classe di schema.

**Richiesta**

Nella richiesta seguente sono elencate tutte le configurazioni di proiezione associate alla classe di schema [!DNL Experience Data Model] [!DNL XDM Individual Profile]. Per ulteriori informazioni su XDM e sul suo ruolo all&#39;interno di [!DNL Platform], leggere la [Panoramica del sistema XDM](../../xdm/home.md).

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di configurazioni di proiezione all&#39;interno dell&#39;attributo radice `_embedded`, contenuto nell&#39;array `projectionConfigs`. Se non sono state apportate configurazioni di proiezione per la tua organizzazione, la matrice `projectionConfigs` sarà vuota.

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
>La richiesta POST per creare una configurazione richiede un&#39;intestazione `Content-Type` specifica, come mostrato di seguito. Se si utilizza un&#39;intestazione `Content-Type` errata, si verifica un errore di stato HTTP 415 (tipo di supporto non supportato).

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

Un selettore è un elenco separato da virgole di nomi di campi XDM. In una configurazione di proiezione, il selettore designa le proprietà da includere nelle proiezioni. Il formato del valore del parametro `selector` è liberamente basato sulla sintassi XPath. Di seguito è riportato un riepilogo della sintassi supportata, con ulteriori esempi di riferimento.

### Sintassi supportata

* Utilizzare le virgole per selezionare più campi. Non utilizzare spazi.
* Utilizzare la notazione del punto per selezionare i campi nidificati.
   * Ad esempio, per selezionare un campo denominato `field` nidificato all’interno di un campo denominato `foo`, utilizza il selettore `foo.field`.
* Se si include un campo contenente campi secondari, anche tutti i campi secondari vengono proiettati per impostazione predefinita. Tuttavia, puoi filtrare i campi secondari restituiti utilizzando le parentesi `"( )"`.
   * Ad esempio, `addresses(type,city.country)` restituisce solo il tipo di indirizzo e il paese in cui si trova la città dell&#39;indirizzo per ciascun elemento della matrice `addresses`.
   * L&#39;esempio precedente è equivalente a `addresses.type,addresses.city.country`.

>[!NOTE]
>
>Per fare riferimento ai campi secondari sono supportate sia la notazione del punto che la notazione tra parentesi. Tuttavia, è consigliabile utilizzare la notazione del punto perché è più concisa e fornisce una migliore illustrazione della gerarchia dei campi.

* Ogni campo di un selettore viene specificato relativo alla directory principale della risposta.
   * Se i dati sono una raccolta di risorse, la proiezione includerà una matrice di risorse.
   * Se i dati sono una singola risorsa, la proiezione includerà i campi relativi a tale risorsa.
   * Se il campo selezionato è (o fa parte) di una matrice, la proiezione includerà la parte selezionata di tutti gli elementi della matrice.

### Esempi del parametro del selettore

Gli esempi seguenti mostrano parametri di esempio `selector`, seguiti dai valori strutturati che rappresentano.

**person.lastName**

Restituisce il sottocampo `lastName` dell&#39;oggetto `person` nella risorsa richiesta.

```json
{
  "person": {
    "lastName": "Smith"
  }
}
```

**indirizzi**

Restituisce tutti gli elementi della matrice `addresses`, inclusi tutti i campi di ciascun elemento, ma nessun altro campo.

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

Restituisce il campo `person.lastName` e tutti gli elementi della matrice `addresses`.

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

Restituisce solo i valori dei campi `type` e `city` per ogni elemento della matrice `addresses`. Tutti gli altri campi secondari contenuti in ciascun elemento `addresses` vengono filtrati.

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

Questa guida illustra i passaggi necessari per configurare proiezioni e destinazioni, incluso come formattare correttamente il parametro `selector` . Ora puoi creare nuove destinazioni e configurazioni di proiezione specifiche per le esigenze della tua organizzazione.