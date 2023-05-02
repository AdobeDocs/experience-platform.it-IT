---
solution: Experience Platform
title: Modificare le connessioni di destinazione utilizzando l’API del servizio di flusso
type: Tutorial
description: Scopri come modificare vari componenti di una connessione di destinazione utilizzando l’API del servizio di flusso.
source-git-commit: 956ac5d210d54526e886e57b8ea37ab4b3fbab8a
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 2%

---

# Modificare le connessioni di destinazione utilizzando l’API del servizio di flusso

Questa esercitazione descrive i passaggi per la modifica di vari componenti di una connessione di destinazione. Scopri come aggiornare le credenziali di autenticazione, il percorso di esportazione e altro ancora utilizzando il [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
> Le operazioni di modifica descritte in questa esercitazione sono attualmente supportate solo tramite l’API del servizio di flusso.

## Introduzione {#get-started}

Questa esercitazione richiede un ID di flusso di dati valido. Se non disponi di un ID flusso di dati valido, seleziona la destinazione scelta dalla [catalogo delle destinazioni](../catalog/overview.md) e seguire i passi descritti in [connettersi alla destinazione](../ui/connect-destination.md) e [attivare i dati](../ui/activation-overview.md) prima di provare questa esercitazione.

>[!NOTE]
>
> I termini *flusso* e *flusso dati* sono utilizzati in modo intercambiabile in questa esercitazione. Nel contesto di questa esercitazione, hanno lo stesso significato.

Questa esercitazione richiede anche di avere una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Destinazioni](../home.md): [!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione senza soluzione di continuità dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per le campagne di marketing cross-channel, le campagne e-mail, la pubblicità mirata e molti altri casi d’uso.
* [Sandbox](../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per aggiornare correttamente il flusso di dati utilizzando [!DNL Flow Service] API.

### Lettura di chiamate API di esempio {#reading-sample-api-calls}

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

### Raccogli i valori delle intestazioni richieste {#gather-values-for-required-headers}

Per effettuare chiamate alle API di Platform, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in Experience Platform, comprese quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API di Platform richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Se la `x-sandbox-name` intestazione non specificata, le richieste vengono risolte sotto `prod` sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* `Content-Type: application/json`

## Ricerca dei dettagli del flusso di dati {#look-up-dataflow-details}

Il primo passaggio nella modifica della connessione di destinazione consiste nel recuperare i dettagli del flusso di dati utilizzando il proprio ID di flusso. Puoi visualizzare i dettagli correnti di un flusso di dati esistente effettuando una richiesta di GET al `/flows` punto finale.

>[!TIP]
>
>Puoi utilizzare l’interfaccia utente di Experience Platform per ottenere l’ID del flusso di dati desiderato per una destinazione. Vai a **[!UICONTROL Destinazioni]** > **[!UICONTROL Sfoglia]**, seleziona il flusso di dati di destinazione desiderato e trova l’ID di destinazione nella barra a destra. L&#39;ID di destinazione è il valore che userai come ID di flusso nel passaggio successivo.
>
> ![Ottenere l’ID di destinazione tramite l’interfaccia utente di Experience Platform](/help/destinations/assets/api/edit-destination/get-destination-id.png)

>[!BEGINSHADEBOX]

**Formato API**

```http
GET /flows/{FLOW_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FLOW_ID}` | L&#39;unico `id` valore del flusso di dati di destinazione che si desidera recuperare. |

**Richiesta**

La seguente richiesta recupera informazioni relative all’ID di flusso.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli correnti del flusso di dati, inclusa la relativa versione, identificatore univoco (`id`) e altre informazioni pertinenti. Per questa esercitazione, gli ID di connessione di destinazione e di base evidenziati nella risposta riportata di seguito. Puoi utilizzare questi ID nelle sezioni successive per aggiornare vari componenti della connessione di destinazione.

```json {line-numbers="true" start-line="1" highlight="27,38"}
{
   "items":[
      {
         "id":"226fb2e1-db69-4760-b67e-9e671e05abfc",
         "createdAt":"{CREATED_AT}",
         "updatedAt":"{UPDATED_BY}",
         "createdBy":"{CREATED_BY}",
         "updatedBy":"{UPDATED_BY}",
         "createdClient":"{CREATED_CLIENT}",
         "updatedClient":"{UPDATED_CLIENT}",
         "sandboxId":"{SANDBOX_ID}",
         "sandboxName":"prod",
         "imsOrgId":"{ORG_ID}",
         "name":"2021 winter campaign",
         "description":"ACME company holiday campaign for high fidelity customers",
         "flowSpec":{
            "id":"71471eba-b620-49e4-90fd-23f1fa0174d8",
            "version":"1.0"
         },
         "state":"enabled",
         "version":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "etag":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "sourceConnectionIds":[
            "5e45582a-5336-4ea1-9ec9-d0004a9f344a"
         ],
         "targetConnectionIds":[
            "8ce3dc63-3766-4220-9f61-51d2f8f14618"
         ],
         "inheritedAttributes":{
            "sourceConnections":[
               {
                  "id":"5e45582a-5336-4ea1-9ec9-d0004a9f344a",
                  "connectionSpec":{
                     "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"0a82f29f-b457-47f7-bb30-33856e2ae5aa",
                     "connectionSpec":{
                        "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                        "version":"1.0"
                     }
                  },
                  "typeInfo":{
                     "type":"ProfileFragments",
                     "id":"ups"
                  }
               }
            ],
            "targetConnections":[
               {
                  "id":"8ce3dc63-3766-4220-9f61-51d2f8f14618",
                  "connectionSpec":{
                     "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"7fbf542b-83ed-498f-8838-8fde0c4d4d69",
                     "connectionSpec":{
                        "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                        "version":"1.0"
                     }
                  }
               }
            ]
         },
         "transformations":[
            "shortened for brevity"
         ]
      }
   ]
```

>[!ENDSHADEBOX]

## Modifica dei componenti di connessione di destinazione (posizione di archiviazione e altri componenti) {#patch-target-connection}

I componenti di una connessione di destinazione variano a seconda della destinazione. Ad esempio, [!DNL Amazon S3] destinazioni , puoi aggiornare il bucket e il percorso in cui vengono esportati i file. Per [!DNL Pinterest] destinazioni, puoi aggiornare le [!DNL Pinterest Advertiser ID] e [!DNL Google Customer Match] è possibile aggiornare [!DNL Pinterest Account ID].

Per aggiornare i componenti di una connessione di destinazione, esegui una richiesta PATCH al `/targetConnections/{TARGET_CONNECTION_ID}` durante la fornitura dell&#39;ID di connessione di destinazione, della versione e dei nuovi valori che si desidera utilizzare. Ricorda che hai ottenuto l’ID di connessione di destinazione nel passaggio precedente, quando hai ispezionato un flusso di dati esistente nella destinazione desiderata.

>[!IMPORTANT]
>
>La `If-Match` l’intestazione è necessaria quando si effettua una richiesta PATCH. Il valore di questa intestazione è la versione univoca della connessione di destinazione che si desidera aggiornare. Il valore etag viene aggiornato con ogni aggiornamento riuscito di un’entità di flusso come flusso di dati, connessione di destinazione e altri.
>
> Per ottenere la versione più recente del valore etag, esegui una richiesta GET al `/targetConnections/{TARGET_CONNECTION_ID}` punto finale, dove `{TARGET_CONNECTION_ID}` è l&#39;ID di connessione di destinazione che desideri aggiornare.

Di seguito sono riportati alcuni esempi di aggiornamento dei parametri nelle specifiche di connessione di destinazione per diversi tipi di destinazioni. Ma la regola generale per aggiornare i parametri per qualsiasi destinazione è la seguente:

Ottieni l’ID del flusso di dati della connessione > ottieni l’ID della connessione di destinazione > PATCH la connessione di destinazione con i valori aggiornati per i parametri desiderati.

>[!BEGINSHADEBOX]

**Formato API**

```http
PATCH /targetConnections/{TARGET_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**Richiesta**

La seguente richiesta aggiorna il `bucketName` e `path` parametri di un [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) connessione di destinazione.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "replace",
    "path": "/params",
    "value": {
      "bucketName": "newBucketName",
      "path": "updatedPath"
    }
  }
]'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `op` | La chiamata dell’operazione utilizzata per definire l’azione necessaria per aggiornare il flusso di dati. Le operazioni includono: `add`, `replace`e `remove`. |
| `path` | Definisce la parte del flusso da aggiornare. |
| `value` | Il nuovo valore con cui si desidera aggiornare il parametro. |

**Risposta**

Una risposta corretta restituisce l&#39;ID di connessione di destinazione e un tag Etag aggiornato. Puoi verificare l’aggiornamento effettuando una richiesta GET al [!DNL Flow Service] , fornendo al contempo l&#39;ID di connessione di destinazione.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Google Ad Manager e Google Ad Manager 360]

**Richiesta**

La seguente richiesta aggiorna i parametri di un [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md) o [[!DNL Google Ad Manager 360] destinazione](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) connessione per aggiungere la nuova [**[!UICONTROL Aggiungi ID segmento al nome del segmento]**](/help/release-notes/2023/april-2023.md#destinations) campo .

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/params/appendSegmentId",
    "value": true
  }
]'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `op` | La chiamata dell’operazione utilizzata per definire l’azione necessaria per aggiornare il flusso di dati. Le operazioni includono: `add`, `replace`e `remove`. |
| `path` | Definisce la parte del flusso da aggiornare. |
| `value` | Il nuovo valore con cui si desidera aggiornare il parametro. |

**Risposta**

Una risposta corretta restituisce l’ID di connessione di destinazione e un tag aggiornato. Puoi verificare l’aggiornamento effettuando una richiesta GET al [!DNL Flow Service] , fornendo al contempo l&#39;ID di connessione di destinazione.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Pinterest]

**Richiesta**

La seguente richiesta aggiorna il `advertiserId` parametro di un [[!DNL Pinterest] connessione di destinazione](/help/destinations/catalog/advertising/pinterest.md#parameters).

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "replace",
    "path": "/params",
    "value": {
      "advertiser_id": "1234567890"
    }
  }
]'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `op` | La chiamata dell’operazione utilizzata per definire l’azione necessaria per aggiornare il flusso di dati. Le operazioni includono: `add`, `replace`e `remove`. |
| `path` | Definisce la parte del flusso da aggiornare. |
| `value` | Il nuovo valore con cui si desidera aggiornare il parametro. |

**Risposta**

Una risposta corretta restituisce l’ID di connessione di destinazione e un tag aggiornato. Puoi verificare l’aggiornamento effettuando una richiesta GET al [!DNL Flow Service] , fornendo al contempo l&#39;ID di connessione di destinazione.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## Modifica dei componenti di connessione di base (parametri di autenticazione e altri componenti) {#patch-base-connection}

I componenti di una connessione di base variano a seconda della destinazione. Ad esempio, [!DNL Amazon S3] destinazioni, puoi aggiornare la chiave di accesso e la chiave segreta al tuo [!DNL Amazon S3] posizione.

Per aggiornare i componenti di una connessione di base, esegui una richiesta PATCH al `/connections` durante la fornitura dell&#39;ID di connessione di base, della versione e dei nuovi valori che si desidera utilizzare.

Ricorda che hai ottenuto l&#39;ID di connessione di base in un passaggio precedente, quando hai ispezionato un flusso di dati esistente nella destinazione desiderata.

>[!IMPORTANT]
>
>La `If-Match` l’intestazione è necessaria quando si effettua una richiesta PATCH. Il valore di questa intestazione è la versione univoca della connessione di base che si desidera aggiornare. Il valore etag viene aggiornato con ogni aggiornamento riuscito di un’entità di flusso come flusso di dati, connessione di base e altri.
>
> Per ottenere la versione più recente del valore Etag , esegui una richiesta di GET al `/connections/{BASE_CONNECTION_ID}` punto finale, dove `{BASE_CONNECTION_ID}` è l&#39;ID di connessione di base che si desidera aggiornare.

Di seguito sono riportati alcuni esempi di aggiornamento dei parametri nelle specifiche di connessione di base per diversi tipi di destinazioni. Ma la regola generale per aggiornare i parametri per qualsiasi destinazione è la seguente:

Ottieni l’ID del flusso di dati della connessione > ottieni l’ID della connessione di base > PATCH la connessione di base con i valori aggiornati per i parametri desiderati.

>[!BEGINSHADEBOX]

**Formato API**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**Richiesta**

La seguente richiesta aggiorna il `accessId` e `secretKey` parametri di un [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) connessione di destinazione.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/auth/params",
    "value": {
      "accessId": "exampleAccessId",
      "secretKey": "exampleSecretKey"
    }
  }
]'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `op` | La chiamata dell’operazione utilizzata per definire l’azione necessaria per aggiornare il flusso di dati. Le operazioni includono: `add`, `replace`e `remove`. |
| `path` | Definisce la parte del flusso da aggiornare. |
| `value` | Il nuovo valore con cui si desidera aggiornare il parametro. |

**Risposta**

Una risposta corretta restituisce l&#39;ID di connessione di base e un tag aggiornato. Puoi verificare l’aggiornamento effettuando una richiesta GET al [!DNL Flow Service] API, fornendo al contempo l&#39;ID di connessione di base.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB BLOB di Azure]

**Richiesta**

La seguente richiesta aggiorna i parametri di un [[!DNL Azure Blob] destinazione](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) connessione per aggiornare la stringa di connessione necessaria per la connessione a un&#39;istanza BLOB di Azure.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/auth/params",
    "value": {
      "connectionString": "updatedString"
    }
  }
]'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `op` | La chiamata dell’operazione utilizzata per definire l’azione necessaria per aggiornare il flusso di dati. Le operazioni includono: `add`, `replace`e `remove`. |
| `path` | Definisce la parte del flusso da aggiornare. |
| `value` | Il nuovo valore con cui si desidera aggiornare il parametro. |

**Risposta**

Una risposta corretta restituisce l&#39;ID di connessione di base e un tag aggiornato. Puoi verificare l’aggiornamento effettuando una richiesta GET al [!DNL Flow Service] API, fornendo al contempo l&#39;ID di connessione di base.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## Gestione degli errori API {#api-error-handling}

Gli endpoint API in questa esercitazione seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](/help/landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](/help/landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform per ulteriori informazioni sull’interpretazione delle risposte agli errori.

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai imparato ad aggiornare vari componenti di una connessione di destinazione utilizzando [!DNL Flow Service] API. Per ulteriori informazioni sulle destinazioni, consulta la sezione [panoramica sulle destinazioni](../home.md).
