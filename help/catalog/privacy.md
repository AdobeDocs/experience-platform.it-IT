---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Elaborazione delle richieste di privacy nel Data Lake
topic: overview
translation-type: tm+mt
source-git-commit: 409d98818888f2758258441ea2d993ced48caf9a

---


# Elaborazione delle richieste di privacy nel Data Lake

Il servizio Adobe Experience Platform Privacy Service elabora le richieste dei clienti di accedere, rifiutare la vendita o cancellare i loro dati personali, come delineato dalle normative sulla privacy come il General Data Protection Regulation (GDPR) e il California Consumer Privacy Act (CCPA).

Questo documento tratta i concetti essenziali relativi all&#39;elaborazione delle richieste di privacy per i dati dei clienti memorizzati nel Data Lake.

## Introduzione

Prima di leggere questa guida, è consigliabile avere una conoscenza approfondita dei seguenti servizi della piattaforma Experience:

* [Servizio](../privacy-service/home.md)Privacy: Gestisce le richieste dei clienti relative all&#39;accesso, al rifiuto della vendita o all&#39;eliminazione dei loro dati personali tra le applicazioni Adobe Experience Cloud.
* [Servizio](home.md)catalogo: Il sistema di record per la posizione dei dati e la linea all&#39;interno di Experience Platform. Fornisce un&#39;API che può essere utilizzata per aggiornare i metadati del set di dati.
* [Sistema](../xdm/home.md)XDM (Experience Data Model): Il framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza dei clienti.

## Aggiunta di etichette di privacy ai set di dati {#privacy-labels}

Affinché un set di dati possa essere elaborato in una richiesta di privacy per il Data Lake, è necessario che al set di dati siano assegnate etichette sulla privacy. Le etichette per la privacy indicano quali campi all&#39;interno dello schema associato a un dataset si applicano agli spazi dei nomi che si prevede verranno inviati nelle richieste di privacy.

Questa sezione illustra come aggiungere etichette sulla privacy a un set di dati da utilizzare nelle richieste sulla privacy di Data Lake. Per iniziare, prendere in considerazione il seguente set di dati:

```json
{
    "5d8e9cf5872f18164763f971": {
        "name": "Loyalty Members",
        "description": "Dataset for the Loyalty Members schema",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "loyalty_members"
            ]
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "id": "5d8e9cf5872f18164763f971",
        "dule": {
            "identity": [],
            "contract": [
                "C2",
                "C5"
            ],
            "sensitive": [],
            "contracts": [
                "C2",
                "C5"
            ],
            "identifiability": [],
            "specialTypes": []
        },
        "version": "1.0.2",
        "created": 1569627381749,
        "updated": 1569880723282,
        "createdClient": "acp_ui_platform",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "viewId": "5d8e9cf5872f18164763f972",
        "status": "enabled",
        "fileDescription": {
            "persisted": true,
            "containerFormat": "parquet",
            "format": "parquet"
        },
        "files": "@/dataSets/5d8e9cf5872f18164763f971/views/5d8e9cf5872f18164763f972/files",
        "schemaMetadata": {
            "primaryKey": [],
            "delta": [],
            "dule": [
                {
                    "path": "/properties/personalEmail/properties/address",
                    "identity": [
                        "I1"
                    ],
                    "contract": [],
                    "sensitive": [],
                    "contracts": [],
                    "identifiability": [
                        "I1"
                    ],
                    "specialTypes": []
                }
            ],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    }
}
```

La `schemaMetadata` proprietà del dataset contiene una `gdpr` matrice, attualmente vuota. Per aggiungere etichette sulla privacy al set di dati, questo array deve essere aggiornato utilizzando una richiesta PATCH all’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)Catalog Service.

>[!NOTE] Anche se l&#39;array è denominato `gdpr`, l&#39;aggiunta di etichette consentirà la richiesta di processi per la privacy sia per le norme GDPR che per le norme CCPA.

**Formato API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | Il `id` valore del set di dati da aggiornare. |

**Richiesta**

In questo esempio, un dataset include un indirizzo e-mail nel `personalEmail.address` campo. Affinché questo campo funga da identificatore per le richieste di privacy di Data Lake, è necessario aggiungere all&#39; `gdpr` array un&#39;etichetta che utilizza uno spazio dei nomi non registrato.

Nella richiesta seguente viene aggiunta un&#39;etichetta per la privacy che assegna lo spazio dei nomi &quot;email_label&quot; al `personalEmail.address` campo.

>[!IMPORTANT] Quando si esegue un&#39;operazione PATCH sulla `schemaMetadata` proprietà di un dataset, assicurarsi di copiare eventuali proprietà secondarie esistenti all&#39;interno del payload della richiesta. Escludendo eventuali valori esistenti dal payload, questi verranno rimossi dal dataset.

```shell
curl -X PATCH 'https://platform.adobe.io/data/foundation/catalog/dataSets/5d8e9cf5872f18164763f971' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{ 
    "schemaMetadata": { 
      "primaryKey": [],
      "delta": [],
      "dule": [
        {
          "path": "/properties/personalEmail/properties/address",
          "identity": [
              "I1"
          ],
          "contract": [],
          "sensitive": [],
          "contracts": [],
          "identifiability": [
              "I1"
          ],
          "specialTypes": []
        }
      ],
      "gdpr": [
          {
              "namespace": ["email_label"],
              "path": "/properties/personalEmail/properties/address"
          }
      ]
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `namespace` | Array che elenca gli spazi dei nomi da associare al campo specificato in `path`. Gli spazi dei nomi vengono utilizzati per identificare i campi relativi alla privacy al momento dell&#39; [invio delle richieste](#submit) di accesso o eliminazione nell&#39;API del servizio sulla privacy. |
| `path` | Percorso del campo all&#39;interno dello schema associato del dataset che si applica al `namespace`. Idealmente, le etichette sulla privacy dovrebbero essere applicate solo ai campi &quot;foglia&quot; (campi senza sottocampi). |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 (OK) con l&#39;ID del set di dati fornito nel payload. Se si utilizza l’ID per cercare di nuovo il set di dati, vengono visualizzate le etichette relative alla privacy.

```json
[
    "@/dataSets/5d8e9cf5872f18164763f971"
]
```

### Etichettare i campi del tipo di mappa nidificati

È importante notare che esistono due tipi di campi di tipo mappa nidificati che non supportano l&#39;etichettatura della privacy:

* Campo di tipo mapping all&#39;interno di un campo di tipo matrice
* Campo di tipo mappa all’interno di un altro campo di tipo mappa

L&#39;elaborazione del lavoro sulla privacy per uno dei due esempi di cui sopra avrà un esito negativo. Per questo motivo, si consiglia di evitare di utilizzare campi di tipo mappa nidificati per memorizzare i dati privati dei clienti. Gli ID del consumatore pertinenti devono essere memorizzati come tipo di dati non mappato all&#39;interno del `identityMap` campo (stesso campo del tipo di mappa) per i set di dati basati su record, oppure come `endUserID` campo per i set di dati basati su serie temporali.

## Invio di richieste {#submit}

>[!NOTE] Questa sezione descrive come formattare le richieste di privacy per il Data Lake. È vivamente consigliato di consultare la documentazione API [del servizio](../privacy-service/api/getting-started.md) Privacy o dell&#39;interfaccia utente [del servizio](../privacy-service/ui/overview.md) Privacy per i passaggi completi su come inviare un processo di privacy, incluso come formattare correttamente i dati di identità dell&#39;utente inviati nei payload della richiesta.

La sezione seguente illustra come effettuare richieste di privacy per il Data Lake utilizzando l&#39;API o l&#39;interfaccia utente del servizio per la privacy.

### Utilizzo dell&#39;API

Quando si creano richieste di processo nell&#39;API, tutte le `userIDs` richieste fornite devono utilizzare un archivio dati specifico `namespace` e `type` a seconda dell&#39;archivio dati a cui si riferiscono. Gli ID per il Data Lake devono utilizzare &quot;non registrato&quot; per il loro `type` valore e un `namespace` valore che corrisponda a una delle etichette [di](#privacy-labels) privacy aggiunte ai set di dati applicabili.

Inoltre, l&#39; `include` array del payload della richiesta deve includere i valori prodotto per i diversi data store a cui viene effettuata la richiesta. Quando si effettuano richieste al Data Lake, l&#39;array deve includere il valore &quot;aepDataLake&quot;.

La richiesta seguente crea un nuovo processo di privacy per il Data Lake, utilizzando lo spazio dei nomi &quot;email_label&quot; non registrato. Include inoltre il valore prodotto per il Data Lake nell&#39; `include` array:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          },
          {
            "namespace": "email_label",
            "value": "jdoe@example.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

### Utilizzo dell’interfaccia

Durante la creazione di richieste di lavoro nell’interfaccia utente, accertatevi di selezionare **AEP Data Lake** e/o **Profile** in _Products_ , rispettivamente, per elaborare i processi per i dati memorizzati nel Data Lake o nel Real-time Customer Profile.

<img src="images/privacy/product-value.png" width="450"><br>

## Elimina elaborazione richiesta

Quando Experience Platform riceve una richiesta di eliminazione dal servizio per la privacy, la piattaforma invia al servizio per la privacy la conferma che la richiesta è stata ricevuta e che i dati interessati sono stati contrassegnati per l&#39;eliminazione. I record vengono quindi rimossi dal Data Lake entro sette giorni. Durante quella finestra di sette giorni, i dati vengono eliminati in modo morbido e pertanto non sono accessibili da alcun servizio Piattaforma.

Nelle release future, Platform invierà una conferma al Servizio Privacy dopo che i dati saranno stati fisicamente eliminati.

## Passaggi successivi

Leggendo questo documento, ti sono stati introdotti i concetti importanti relativi all&#39;elaborazione delle richieste di privacy per il Data Lake. Si consiglia di continuare a leggere la documentazione fornita in questa guida per approfondire la conoscenza su come gestire i dati di identità e creare processi di privacy.

Consulta il documento sull’elaborazione delle richieste di [privacy per il profilo](../profile/privacy.md) cliente in tempo reale per i passaggi relativi all’elaborazione delle richieste di privacy per l’archivio profili.