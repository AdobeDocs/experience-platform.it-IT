---
solution: Experience Platform
title: Modificare le connessioni di destinazione utilizzando l’API del servizio Flusso
type: Tutorial
description: Scopri come modificare vari componenti di una connessione di destinazione utilizzando l’API del servizio Flusso.
exl-id: d6d27d5a-e50c-4170-bb3a-c4cbf2b46653
source-git-commit: 2a72f6886f7a100d0a1bf963eedaed8823a7b313
workflow-type: tm+mt
source-wordcount: '1605'
ht-degree: 5%

---

# Modificare le connessioni di destinazione utilizzando l’API del servizio Flusso

Questo tutorial illustra i passaggi necessari per modificare vari componenti di una connessione di destinazione. Scopri come aggiornare le credenziali di autenticazione, il percorso di esportazione e altro ancora utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
> Le operazioni di modifica descritte in questo tutorial sono attualmente supportate solo tramite l’API del servizio Flusso.

## Introduzione {#get-started}

Questo tutorial richiede un ID del flusso di dati valido. Se non disponi di un ID flusso di dati valido, seleziona la destinazione desiderata dal [catalogo destinazioni](../catalog/overview.md) e segui i passaggi descritti per [connettersi alla destinazione](../ui/connect-destination.md) e [attivare i dati](../ui/activation-overview.md) prima di provare questa esercitazione.

>[!NOTE]
>
> I termini *flusso* e *flusso di dati* vengono utilizzati in modo intercambiabile in questa esercitazione. Nel contesto di questa esercitazione, hanno lo stesso significato.

Questo tutorial richiede anche una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Destinazioni](../home.md): [!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l&#39;attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.
* [Sandbox](../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per aggiornare correttamente il flusso di dati utilizzando l&#39;API [!DNL Flow Service].

### Lettura delle chiamate API di esempio {#reading-sample-api-calls}

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

### Raccogliere i valori per le intestazioni richieste {#gather-values-for-required-headers}

Per effettuare chiamate alle API di Platform, devi prima completare l&#39;[esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in Experience Platform, incluse quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API di Platform richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Se l&#39;intestazione `x-sandbox-name` non è specificata, le richieste vengono risolte nella sandbox `prod`.

Tutte le richieste che contengono un payload (`POST`, `PUT`, `PATCH`) richiedono un&#39;intestazione del tipo di supporto aggiuntiva:

* `Content-Type: application/json`

## Cerca dettagli flusso di dati {#look-up-dataflow-details}

Il primo passaggio nella modifica della connessione di destinazione consiste nel recuperare i dettagli del flusso di dati utilizzando il tuo ID flusso. È possibile visualizzare i dettagli correnti di un flusso di dati esistente effettuando una richiesta GET all&#39;endpoint `/flows`.

>[!TIP]
>
>Puoi utilizzare l’interfaccia utente di Experience Platform per ottenere l’ID del flusso di dati desiderato per una destinazione. Vai a **[!UICONTROL Destinazioni]** > **[!UICONTROL Sfoglia]**, seleziona il flusso di dati di destinazione desiderato e individua l&#39;ID di destinazione nella barra a destra. L’ID di destinazione è il valore che utilizzerai come ID di flusso nel passaggio successivo.
>
> ![Ottieni l&#39;ID di destinazione tramite l&#39;interfaccia utente Experience Platform](/help/destinations/assets/api/edit-destination/get-destination-id.png)

>[!BEGINSHADEBOX]

**Formato API**

```http
GET /flows/{FLOW_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FLOW_ID}` | Il valore `id` univoco per il flusso di dati di destinazione che desideri recuperare. |

**Richiesta**

La richiesta seguente recupera informazioni relative all’ID di flusso.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli correnti del flusso di dati, inclusa la versione, l&#39;identificatore univoco (`id`) e altre informazioni rilevanti. I più rilevanti per questa esercitazione sono gli ID connessione di destinazione e connessione di base evidenziati nella risposta seguente. Questi ID verranno utilizzati nelle sezioni successive per aggiornare vari componenti della connessione di destinazione.

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

## Modifica dei componenti di connessione di destinazione (percorso di archiviazione e altri componenti) {#patch-target-connection}

I componenti di una connessione di destinazione differiscono a seconda della destinazione. Ad esempio, per [!DNL Amazon S3] destinazioni, puoi aggiornare il bucket e il percorso in cui vengono esportati i file. Per [!DNL Pinterest] destinazioni, puoi aggiornare [!DNL Pinterest Advertiser ID] e per [!DNL Google Customer Match] puoi aggiornare [!DNL Pinterest Account ID].

Per aggiornare i componenti di una connessione di destinazione, eseguire una richiesta `PATCH` all&#39;endpoint `/targetConnections/{TARGET_CONNECTION_ID}` fornendo l&#39;ID della connessione di destinazione, la versione e i nuovi valori che si desidera utilizzare. Ricorda che hai ottenuto l’ID di connessione di destinazione nel passaggio precedente, quando hai ispezionato un flusso di dati esistente nella destinazione desiderata.

>[!IMPORTANT]
>
>L&#39;intestazione `If-Match` è obbligatoria quando si effettua una richiesta `PATCH`. Il valore di questa intestazione è la versione univoca della connessione di destinazione che desideri aggiornare. Il valore etag viene aggiornato a ogni aggiornamento riuscito di un’entità di flusso come flusso di dati, connessione di destinazione e altre.
>
> Per ottenere la versione più recente del valore etag, eseguire una richiesta di GET all&#39;endpoint `/targetConnections/{TARGET_CONNECTION_ID}`, dove `{TARGET_CONNECTION_ID}` è l&#39;ID di connessione di destinazione che si desidera aggiornare.
>
> Assicurarsi di racchiudere il valore dell&#39;intestazione `If-Match` tra virgolette doppie, come negli esempi seguenti, quando si eseguono `PATCH` richieste.

Di seguito sono riportati alcuni esempi di aggiornamento dei parametri nella specifica di connessione di destinazione per diversi tipi di destinazioni. Tuttavia, la regola generale per aggiornare i parametri per qualsiasi destinazione è la seguente:

Ottieni l’ID del flusso di dati della connessione > ottieni l’ID della connessione di destinazione > `PATCH` la connessione di destinazione con valori aggiornati per i parametri desiderati.

>[!BEGINSHADEBOX]

**Formato API**

```http
PATCH /targetConnections/{TARGET_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**Richiesta**

La richiesta seguente aggiorna i parametri `bucketName` e `path` di una connessione di destinazione [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details).

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
| `op` | Chiamata di operazione utilizzata per definire l’azione necessaria per aggiornare il flusso di dati. Le operazioni includono: `add`, `replace` e `remove`. |
| `path` | Definisce la parte del flusso da aggiornare. |
| `value` | Il nuovo valore con cui desideri aggiornare il parametro. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID connessione di destinazione e un Etag aggiornato. È possibile verificare l&#39;aggiornamento effettuando una richiesta di GET all&#39;API [!DNL Flow Service] e fornendo l&#39;ID di connessione di destinazione.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Google Ad Manager e Google Ad Manager 360]

**Richiesta**

La richiesta seguente aggiorna i parametri di una connessione [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md) o [[!DNL Google Ad Manager 360] destinazione](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) per aggiungere il nuovo campo [**[!UICONTROL Aggiungi ID pubblico al nome pubblico]**](/help/release-notes/2023/april-2023.md#destinations).

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
| `op` | Chiamata di operazione utilizzata per definire l’azione necessaria per aggiornare il flusso di dati. Le operazioni includono: `add`, `replace` e `remove`. |
| `path` | Definisce la parte del flusso da aggiornare. |
| `value` | Il nuovo valore con cui desideri aggiornare il parametro. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID connessione di destinazione e un tag aggiornato. È possibile verificare l&#39;aggiornamento effettuando una richiesta di GET all&#39;API [!DNL Flow Service] e fornendo l&#39;ID di connessione di destinazione.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Pinterest]

**Richiesta**

La richiesta seguente aggiorna il parametro `advertiserId` di una [[!DNL Pinterest] connessione di destinazione](/help/destinations/catalog/advertising/pinterest.md#parameters).

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
| `op` | Chiamata di operazione utilizzata per definire l’azione necessaria per aggiornare il flusso di dati. Le operazioni includono: `add`, `replace` e `remove`. |
| `path` | Definisce la parte del flusso da aggiornare. |
| `value` | Il nuovo valore con cui desideri aggiornare il parametro. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID connessione di destinazione e un tag aggiornato. È possibile verificare l&#39;aggiornamento effettuando una richiesta di GET all&#39;API [!DNL Flow Service] e fornendo l&#39;ID di connessione di destinazione.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## Modifica dei componenti di connessione di base (parametri di autenticazione e altri componenti) {#patch-base-connection}

Modificare la connessione di base per aggiornare le credenziali di una destinazione. I componenti di una connessione di base differiscono a seconda della destinazione. Ad esempio, per le destinazioni [!DNL Amazon S3], è possibile aggiornare la chiave di accesso e la chiave segreta nella posizione [!DNL Amazon S3].

Per aggiornare i componenti di una connessione di base, eseguire una richiesta `PATCH` all&#39;endpoint `/connections` fornendo l&#39;ID della connessione di base, la versione e i nuovi valori che si desidera utilizzare.

Ricorda che hai ottenuto l&#39;ID di connessione di base in un [passaggio precedente](#look-up-dataflow-details), quando hai esaminato un flusso di dati esistente nella destinazione desiderata per il parametro `baseConnection`.

>[!IMPORTANT]
>
>L&#39;intestazione `If-Match` è obbligatoria quando si effettua una richiesta `PATCH`. Il valore di questa intestazione corrisponde alla versione univoca della connessione di base che si desidera aggiornare. Il valore etag viene aggiornato a ogni aggiornamento riuscito di un’entità di flusso come flusso di dati, connessione di base e altre.
>
> Per ottenere la versione più recente del valore Etag, eseguire una richiesta di GET all&#39;endpoint `/connections/{BASE_CONNECTION_ID}`, dove `{BASE_CONNECTION_ID}` è l&#39;ID connessione di base che si desidera aggiornare.
>
> Assicurarsi di racchiudere il valore dell&#39;intestazione `If-Match` tra virgolette doppie, come negli esempi seguenti, quando si eseguono `PATCH` richieste.

Di seguito sono riportati alcuni esempi di aggiornamento dei parametri nella specifica di connessione di base per diversi tipi di destinazioni. Tuttavia, la regola generale per aggiornare i parametri per qualsiasi destinazione è la seguente:

Ottieni l’ID del flusso di dati della connessione > ottieni l’ID della connessione di base > `PATCH` la connessione di base con valori aggiornati per i parametri desiderati.

>[!BEGINSHADEBOX]

**Formato API**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**Richiesta**

La richiesta seguente aggiorna i parametri `accessId` e `secretKey` di una connessione di destinazione [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details).

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
| `op` | Chiamata di operazione utilizzata per definire l’azione necessaria per aggiornare il flusso di dati. Le operazioni includono: `add`, `replace` e `remove`. |
| `path` | Definisce la parte del flusso da aggiornare. |
| `value` | Il nuovo valore con cui desideri aggiornare il parametro. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID della connessione di base e un tag aggiornato. È possibile verificare l&#39;aggiornamento effettuando una richiesta di GET all&#39;API [!DNL Flow Service] e fornendo l&#39;ID connessione di base.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB BLOB di Azure]

**Richiesta**

La richiesta seguente aggiorna i parametri di una connessione [[!DNL Azure Blob] destination](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) per aggiornare la stringa di connessione necessaria per connettersi a un&#39;istanza BLOB di Azure.

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
| `op` | Chiamata di operazione utilizzata per definire l’azione necessaria per aggiornare il flusso di dati. Le operazioni includono: `add`, `replace` e `remove`. |
| `path` | Definisce la parte del flusso da aggiornare. |
| `value` | Il nuovo valore con cui desideri aggiornare il parametro. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID della connessione di base e un tag aggiornato. È possibile verificare l&#39;aggiornamento effettuando una richiesta di GET all&#39;API [!DNL Flow Service] e fornendo l&#39;ID connessione di base.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## Gestione degli errori API {#api-error-handling}

Gli endpoint API in questa esercitazione seguono i principi generali dei messaggi di errore API di Experience Platform. Per ulteriori informazioni sull&#39;interpretazione delle risposte di errore, consultare [codici di stato API](/help/landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](/help/landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai imparato ad aggiornare vari componenti di una connessione di destinazione utilizzando l&#39;API [!DNL Flow Service]. Per ulteriori informazioni sulle destinazioni, consulta la [panoramica sulle destinazioni](../home.md).
