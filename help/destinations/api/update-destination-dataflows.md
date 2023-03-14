---
keywords: Experience Platform;home;argomenti popolari;servizio di flusso;aggiornare i flussi di dati di destinazione
solution: Experience Platform
title: Aggiornare i flussi di dati di destinazione utilizzando l’API del servizio Flusso
type: Tutorial
description: Questa esercitazione illustra i passaggi per aggiornare un flusso di dati di destinazione. Scopri come abilitare o disabilitare il flusso di dati, aggiornarne le informazioni di base o aggiungere e rimuovere segmenti e attributi utilizzando l’API del servizio Flusso.
exl-id: 3f69ad12-940a-4aa1-a1ae-5ceea997a9ba
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '2408'
ht-degree: 2%

---

# Aggiornare i flussi di dati di destinazione utilizzando l’API del servizio Flusso

Questa esercitazione illustra i passaggi per aggiornare un flusso di dati di destinazione. Scopri come abilitare o disabilitare il flusso di dati, aggiornarne le informazioni di base o aggiungere e rimuovere segmenti e attributi utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Per informazioni sulla modifica dei flussi di dati di destinazione tramite l’interfaccia utente di Experience Platform, leggi [Modifica flussi di attivazione](/help/destinations/ui/edit-activation.md).

## Introduzione {#get-started}

Questo tutorial richiede un ID di flusso valido. Se non disponi di un ID di flusso valido, seleziona la destinazione desiderata tra [catalogo delle destinazioni](../catalog/overview.md) e segui i passaggi descritti per [connettersi alla destinazione](../ui/connect-destination.md) e [attivare i dati](../ui/activation-overview.md) prima di provare questa esercitazione.

>[!NOTE]
>
> I termini *flusso* e *flusso di dati* sono utilizzati in modo intercambiabile in questa esercitazione. Nel contesto di questa esercitazione, hanno lo stesso significato.

Questo tutorial richiede anche una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Destinazioni](../home.md): [!DNL Destinations] sono integrazioni preconfigurate con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.
* [Sandbox](../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per aggiornare correttamente il flusso di dati utilizzando [!DNL Flow Service] API.

### Lettura delle chiamate API di esempio {#reading-sample-api-calls}

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito il codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

### Raccogli i valori per le intestazioni richieste {#gather-values-for-required-headers}

Per effettuare chiamate alle API di Platform, devi prima completare la sezione [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in Experience Platform, incluse quelle appartenenti a [!DNL Flow Service], sono isolate in specifiche sandbox virtuali. Tutte le richieste alle API di Platform richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Se il `x-sandbox-name` non è specificata, le richieste vengono risolte in `prod` sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* `Content-Type: application/json`

## Cerca dettagli flusso di dati {#look-up-dataflow-details}

Il primo passaggio nell’aggiornamento del flusso di dati di destinazione consiste nel recuperare i dettagli del flusso di dati utilizzando il tuo ID flusso. Per visualizzare i dettagli correnti di un flusso di dati esistente, effettua una richiesta GET al `/flows` endpoint.

**Formato API**

```http
GET /flows/{FLOW_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FLOW_ID}` | L&#39;unico `id` valore per il flusso di dati di destinazione che desideri recuperare. |

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

In caso di esito positivo, la risposta restituisce i dettagli correnti del flusso di dati, inclusa la versione, l’identificatore univoco (`id`) e altre informazioni pertinenti.

```json
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
            {
               "name":"GeneralTransform",
               "params":{
                  "profileSelectors":{
                     "selectors":[
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"Email",
                              "operator":"EXISTS",
                              "identity":{
                                 "namespace":"Email"
                              },
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"Email",
                                 "destination":"Email",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"Email",
                                 "destinationXdmPath":"Email"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"person.name.firstName",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"person.name.firstName",
                                 "destination":"person.name.firstName",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"person.name.firstName",
                                 "destinationXdmPath":"person.name.firstName"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"person.name.lastName",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"person.name.lastName",
                                 "destination":"person.name.lastName",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"person.name.lastName",
                                 "destinationXdmPath":"person.name.lastName"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"personalEmail.address",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"personalEmail.address",
                                 "destination":"personalEmail.address",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"personalEmail.address",
                                 "destinationXdmPath":"personalEmail.address"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"segmentMembership.status",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"segmentMembership.status",
                                 "destination":"segmentMembership.status",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"segmentMembership.status",
                                 "destinationXdmPath":"segmentMembership.status"
                              }
                           }
                        }
                     ],
                     "mandatoryFields":[
                        "Email",
                        "person.name.firstName",
                        "person.name.lastName"
                     ],
                     "primaryFields":[
                        {
                           "identityNamespace":"Email",
                           "fieldType":"IDENTITY"
                        }
                     ]
                  },
                  "segmentSelectors":{
                     "selectors":[
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"9f7d37fd-7039-4454-94ef-2b0cd6c3206a",
                              "name":"Interested in Mountain Biking",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"DAILY_FULL_EXPORT",
                              "schedule":{
                                 "frequency":"ONCE",
                                 "startDate":"2021-12-25",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"f52a3785-2e7c-40a7-8137-9be99af7794e",
                              "name":"Birth year 1970",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"DAILY_FULL_EXPORT",
                              "schedule":{
                                 "frequency":"DAILY",
                                 "startDate":"2021-12-23",
                                 "endDate":"2021-12-31",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"6caa79b9-39e0-4c37-892b-5061cdca2377",
                              "name":"Account Leads",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                              "schedule":{
                                 "frequency":"DAILY",
                                 "startDate":"2021-12-23",
                                 "endDate":"2021-12-31",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"4c41c318-9e8c-4a4f-b880-877cdd629fc7",
                              "name":"Batch export for autumn campaign",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                              "schedule":{
                                 "frequency":"EVERY_6_HOURS",
                                 "startDate":"2022-01-05",
                                 "endDate":"2022-12-30",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        }
                     ]
                  }
               }
            }
         ]
      }
   ]
```

## Aggiorna nome e descrizione del flusso di dati {#update-dataflow}

Per aggiornare il nome e la descrizione del flusso di dati, esegui una richiesta PATCH al [!DNL Flow Service] fornendo l’ID di flusso, la versione e i nuovi valori che desideri utilizzare.

>[!IMPORTANT]
>
>Il `If-Match` L’intestazione è obbligatoria quando si effettua una richiesta PATCH. Il valore di questa intestazione è la versione univoca del flusso di dati che desideri aggiornare. Il valore etag viene aggiornato a ogni aggiornamento riuscito di un flusso di dati.

**Formato API**

```http
PATCH /flows/{FLOW_ID}
```

**Richiesta**

La richiesta seguente aggiorna il nome e la descrizione del flusso di dati.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
            {
                "op": "replace",
                "path": "/name",
                "value": "2021/2022 winter campaign"
            },
            {
                "op": "replace",
                "path": "/description",
                "value": "ACME company holiday campaign for high fidelity customers and prospects"
            }
        ]'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `op` | Chiamata di operazione utilizzata per definire l’azione necessaria per aggiornare il flusso di dati. Le operazioni includono: `add`, `replace`, e `remove`. |
| `path` | Definisce la parte del flusso da aggiornare. |
| `value` | Il nuovo valore con cui desideri aggiornare il parametro. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID di flusso e un tag aggiornato. Per verificare l’aggiornamento, effettua una richiesta GET al [!DNL Flow Service] , fornendo al tempo stesso l&#39;ID di flusso.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Abilita o disabilita il flusso di dati {#enable-disable-dataflow}

Quando è abilitato, un flusso di dati esporta i profili nella destinazione. I flussi di dati sono abilitati per impostazione predefinita, ma possono essere disabilitati per mettere in pausa le esportazioni dei profili.

Per abilitare o disabilitare un flusso di dati di destinazione esistente, devi effettuare una richiesta POST al [!DNL Flow Service] e fornendo lo stato a cui desideri aggiornare il flusso.

**Formato API**

```http
POST /flows/{FLOW_ID}/action?op=enable or disable
```

**Richiesta**

La richiesta seguente aggiorna lo stato del flusso di dati su abilitato.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=enable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

La richiesta seguente aggiorna lo stato del flusso di dati su disabilitato.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=disable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID di flusso e un tag aggiornato. Per verificare l’aggiornamento, effettua una richiesta GET al [!DNL Flow Service] , fornendo al tempo stesso l&#39;ID di flusso.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Aggiungere un segmento a un flusso di dati {#add-segment}

Per aggiungere un segmento al flusso di dati di destinazione, esegui una richiesta PATCH al [!DNL Flow Service] fornendo il tuo ID di flusso, la versione e il segmento che desideri aggiungere.

**Formato API**

```http
PATCH /flows/{FLOW_ID}
```

**Richiesta**

La richiesta seguente aggiunge un nuovo segmento a un flusso di dati di destinazione esistente.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
   {
      "op":"add",
      "path":"/transformations/0/params/segmentSelectors/selectors/-",
      "value":{
         "type":"PLATFORM_SEGMENT",
         "value":{
            "id":"2d79d0d8-724f-49fc-a09d-d1dec338c93c",
            "name":"Winter 2021/2022 campaign",
            "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%SEGMENT_NAME%_%DATETIME(YYYYMMdd_HHmmss)%_custom-text",
            "exportMode":"DAILY_FULL_EXPORT",
            "schedule":{
               "startDate":"2022-01-05",
               "frequency":"DAILY",
               "triggerType": "AFTER_SEGMENT_EVAL",
               "endDate":"2022-03-10"
            }
         }
      }
   }
]'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `op` | Chiamata di operazione utilizzata per definire l’azione necessaria per aggiornare il flusso di dati. Le operazioni includono: `add`, `replace`, e `remove`. Per aggiungere un segmento a un flusso di dati, utilizza `add` operazione. |
| `path` | Definisce la parte del flusso da aggiornare. Quando aggiungi un segmento a un flusso di dati, utilizza il percorso specificato nell’esempio. |
| `value` | Il nuovo valore con cui desideri aggiornare il parametro. |
| `id` | Specifica l’ID del segmento che stai aggiungendo al flusso di dati di destinazione. |
| `name` | **(Facoltativo)**. Specifica il nome del segmento che stai aggiungendo al flusso di dati di destinazione. Tieni presente che questo campo non è obbligatorio e puoi aggiungere correttamente un segmento al flusso di dati di destinazione senza specificarne il nome. |
| `filenameTemplate` | Per *destinazioni batch* solo. Questo campo è necessario solo quando si aggiunge un segmento a un flusso di dati in destinazioni di esportazione di file batch come Amazon S3, SFTP o Azure Blob. <br> Questo campo determina il formato del nome file dei file esportati nella destinazione. <br> Sono disponibili le seguenti opzioni: <br> <ul><li>`%DESTINATION_NAME%`: Obbligatorio. I file esportati contengono il nome della destinazione.</li><li>`%SEGMENT_ID%`: Obbligatorio. I file esportati contengono l’ID del segmento esportato.</li><li>`%SEGMENT_NAME%`: **(Facoltativo)**. I file esportati contengono il nome del segmento esportato.</li><li>`DATETIME(YYYYMMdd_HHmmss)` o `%TIMESTAMP%`: **(Facoltativo)**. Seleziona una di queste due opzioni per includere l&#39;ora in cui vengono generati da Experience Platform.</li><li>`custom-text`: **(Facoltativo)**. Sostituire questo segnaposto con qualsiasi testo personalizzato che si desidera aggiungere alla fine dei nomi dei file.</li></ul> <br> Per ulteriori informazioni sulla configurazione dei nomi di file, consultare [configurare i nomi dei file](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) nell’esercitazione di attivazione delle destinazioni batch. |
| `exportMode` | Per *destinazioni batch* solo. Questo campo è necessario solo quando si aggiunge un segmento a un flusso di dati in destinazioni di esportazione di file batch come Amazon S3, SFTP o Azure Blob. <br> Obbligatorio. Seleziona `"DAILY_FULL_EXPORT"` (Mostra origine dati) o `"FIRST_FULL_THEN_INCREMENTAL"` (Blocca selezione). Per ulteriori informazioni sulle due opzioni, consulta [esporta file completi](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) e [esportare file incrementali](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) nell’esercitazione di attivazione delle destinazioni batch. |
| `startDate` | Seleziona la data in cui il segmento deve iniziare a esportare i profili nella destinazione. |
| `frequency` | Per *destinazioni batch* solo. Questo campo è necessario solo quando si aggiunge un segmento a un flusso di dati in destinazioni di esportazione di file batch come Amazon S3, SFTP o Azure Blob. <br> Obbligatorio. <br> <ul><li>Per `"DAILY_FULL_EXPORT"` modalità di esportazione, puoi selezionare `ONCE` o `DAILY`.</li><li>Per `"FIRST_FULL_THEN_INCREMENTAL"` modalità di esportazione, puoi selezionare `"DAILY"`, `"EVERY_3_HOURS"`, `"EVERY_6_HOURS"`, `"EVERY_8_HOURS"`, `"EVERY_12_HOURS"`.</li></ul> |
| `triggerType` | Per *destinazioni batch* solo. Questo campo è obbligatorio solo quando si seleziona `"DAILY_FULL_EXPORT"` modalità in `frequency` selettore. <br> Obbligatorio. <br> <ul><li>Seleziona `"AFTER_SEGMENT_EVAL"` far eseguire il processo di attivazione subito dopo il completamento del processo di segmentazione batch giornaliero di Platform. In questo modo, quando viene eseguito il processo di attivazione, i profili più aggiornati vengono esportati nella destinazione.</li><li>Seleziona `"SCHEDULED"` per fare in modo che il processo di attivazione venga eseguito a un orario fisso. In questo modo i dati del profilo di Experience Platform vengono esportati ogni giorno alla stessa ora, ma i profili esportati potrebbero non essere quelli più aggiornati, a seconda che il processo di segmentazione batch sia stato completato prima dell’avvio del processo di attivazione. Quando selezioni questa opzione, devi aggiungere anche una `startTime` per indicare in quale momento in UTC devono essere effettuate le esportazioni giornaliere.</li></ul> |
| `endDate` | Per *destinazioni batch* solo. Questo campo è necessario solo quando si aggiunge un segmento a un flusso di dati in destinazioni di esportazione di file batch come Amazon S3, SFTP o Azure Blob. <br> Non applicabile durante la selezione `"exportMode":"DAILY_FULL_EXPORT"` e `"frequency":"ONCE"`. <br> Imposta la data in cui i membri del segmento cessano di essere esportati nella destinazione. |
| `startTime` | Per *destinazioni batch* solo. Questo campo è necessario solo quando si aggiunge un segmento a un flusso di dati in destinazioni di esportazione di file batch come Amazon S3, SFTP o Azure Blob. <br> Obbligatorio. Seleziona il momento in cui generare ed esportare nella destinazione i file contenenti i membri del segmento. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID di flusso e un tag aggiornato. Per verificare l’aggiornamento, effettua una richiesta GET al [!DNL Flow Service] , fornendo al tempo stesso l&#39;ID di flusso.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Rimuovere un segmento da un flusso di dati {#remove-segment}

Per rimuovere un segmento da un flusso di dati di destinazione esistente, esegui una richiesta PATCH al [!DNL Flow Service] fornendo l’ID di flusso, la versione e il selettore di indice del segmento che desideri rimuovere. L’indicizzazione inizia da `0`. Ad esempio, la richiesta di esempio più avanti rimuove il primo e il secondo segmento dal flusso di dati.

**Formato API**

```http
PATCH /flows/{FLOW_ID}
```

**Richiesta**

La richiesta seguente rimuove due segmenti da un flusso di dati di destinazione esistente.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
{
   "op":"remove",
   "path":"transformations/0/params/segmentSelectors/selectors/0/",
   "value":{
      "type":"PLATFORM_SEGMENT",
      "value":{
      }
   }
},
{
   "op":"remove",
   "path":"transformations/0/params/segmentSelectors/selectors/1/",
   "value":{
      "type":"PLATFORM_SEGMENT",
      "value":{
      }
   }
}
]'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `op` | Chiamata di operazione utilizzata per definire l’azione necessaria per aggiornare il flusso di dati. Le operazioni includono: `add`, `replace`, e `remove`. Per rimuovere un segmento da un flusso di dati, utilizza `remove` operazione. |
| `path` | Specifica quale segmento esistente deve essere rimosso dal flusso di dati di destinazione, in base all’indice del selettore di segmenti. Per recuperare l’ordine dei segmenti in un flusso di dati, esegui una chiamata GET al `/flows` e ispezionare il `transformations.segmentSelectors` proprietà. Per eliminare il primo segmento nel flusso di dati, utilizza `"path":"transformations/0/params/segmentSelectors/selectors/0/"`. |


**Risposta**

In caso di esito positivo, la risposta restituisce l’ID di flusso e un tag aggiornato. Per verificare l’aggiornamento, effettua una richiesta GET al [!DNL Flow Service] , fornendo al tempo stesso l&#39;ID di flusso.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Aggiornare i componenti di un segmento in un flusso di dati {#update-segment}

Puoi aggiornare i componenti di un segmento in un flusso di dati di destinazione esistente. È ad esempio possibile modificare la frequenza di esportazione oppure il modello di nome file. A questo scopo, esegui una richiesta PATCH a [!DNL Flow Service] fornendo l’ID di flusso, la versione e il selettore di indice del segmento che desideri aggiornare. L’indicizzazione inizia da `0`. Ad esempio, la richiesta seguente aggiorna il nono segmento di un flusso di dati.

**Formato API**

```http
PATCH /flows/{FLOW_ID}
```

**Richiesta**

Quando aggiorni un segmento in un flusso di dati di destinazione esistente, devi prima eseguire un’operazione di GET per recuperare i dettagli del segmento da aggiornare. Quindi, fornisci tutte le informazioni sul segmento nel payload, non solo i campi che desideri aggiornare. Nell’esempio seguente, viene aggiunto testo personalizzato alla fine del modello di nome file e la frequenza della pianificazione di esportazione viene aggiornata da 6 ore a 12 ore.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
   {
      "op":"replace",
      "path":"/transformations/0/params/segmentSelectors/selectors/8",
      "value":{
         "type":"PLATFORM_SEGMENT",
         "value":{
            "id":"4c41c318-9e8c-4a4f-b880-877cdd629fc7",
            "name":"Batch export for autumn campaign",
            "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%_custom-text",
            "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
            "schedule":{
               "frequency":"EVERY_12_HOURS",
               "startDate":"2022-01-05",
               "endDate":"2022-01-30",
               "startTime":"20:00"
            },
            "createTime":"1640289901",
            "updateTime":"1640289901"
         }
      }
   }
]'
```

Per le descrizioni delle proprietà nel payload, consulta la sezione [Aggiungere un segmento a un flusso di dati](#add-segment).


**Risposta**

In caso di esito positivo, la risposta restituisce l’ID di flusso e un tag aggiornato. Per verificare l’aggiornamento, effettua una richiesta GET al [!DNL Flow Service] , fornendo al tempo stesso l&#39;ID di flusso.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

Per ulteriori esempi dei componenti del segmento che è possibile aggiornare in un flusso di dati, vedi gli esempi riportati di seguito.

## Aggiornare la modalità di esportazione di un segmento da programmato a dopo la valutazione del segmento {#update-export-mode}

+++ Fai clic su per visualizzare un esempio in cui un’esportazione di segmenti viene aggiornata dall’attivazione giornaliera a un orario specificato all’attivazione giornaliera al completamento del processo di segmentazione batch di Platform.

Il segmento viene esportato ogni giorno alle 16:00 UTC.

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

Il segmento viene esportato ogni giorno dopo il completamento del processo di segmentazione batch giornaliero.

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "AFTER_SEGMENT_EVAL",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

+++

## Aggiorna il modello del nome file per includere campi aggiuntivi nel nome file {#update-filename-template}

+++ Fare clic per visualizzare un esempio in cui il modello di nome file viene aggiornato per includere campi aggiuntivi nel nome file

I file esportati contengono il nome di destinazione e l’ID del segmento di Experience Platform

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

I file esportati contengono il nome di destinazione, l&#39;ID del segmento di Experience Platform, la data e l&#39;ora in cui il file è stato generato da Experience Platform e il testo personalizzato aggiunto alla fine dei file.


```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%_%this is custom text%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

+++

## Aggiungere un attributo di profilo a un flusso di dati {#add-profile-attribute}

Per aggiungere un attributo di profilo al flusso di dati di destinazione, esegui una richiesta PATCH al [!DNL Flow Service] fornendo l’ID di flusso, la versione e l’attributo di profilo che desideri aggiungere.

**Formato API**

```http
PATCH /flows/{FLOW_ID}
```

**Richiesta**

La richiesta seguente aggiunge un nuovo attributo di profilo a un flusso di dati di destinazione esistente.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
    {
    "op":"add",
    "path":"/transformations/0/params/profileSelectors/selectors/-",
    "value":{
        "type":"JSON_PATH",
        "value":{
            "path":"mobilePhone.status"
        }
    }
    }
]'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `op` | Chiamata di operazione utilizzata per definire l’azione necessaria per aggiornare il flusso di dati. Le operazioni includono: `add`, `replace`, e `remove`. Per aggiungere un attributo di profilo a un flusso di dati, utilizza `add` operazione. |
| `path` | Definisce la parte del flusso da aggiornare. Quando aggiungi un attributo di profilo a un flusso di dati, utilizza il percorso specificato nell’esempio. |
| `value.path` | Valore dell’attributo di profilo che stai aggiungendo al flusso di dati. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID di flusso e un tag aggiornato. Per verificare l’aggiornamento, effettua una richiesta GET al [!DNL Flow Service] , fornendo al tempo stesso l&#39;ID di flusso.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Rimuovere un attributo di profilo da un flusso di dati {#remove-profile-attribute}

Per rimuovere un attributo di profilo da un flusso di dati di destinazione esistente, esegui una richiesta PATCH al [!DNL Flow Service] fornendo l’ID di flusso, la versione e il selettore di indice dell’attributo di profilo che desideri rimuovere. L’indicizzazione inizia da `0`. Ad esempio, la richiesta di esempio più avanti rimuove il quinto attributo di profilo dal flusso di dati.


**Formato API**

```http
PATCH /flows/{FLOW_ID}
```

**Richiesta**

La richiesta seguente rimuove un attributo di profilo da un flusso di dati di destinazione esistente.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
    {
    "op":"remove",
    "path":"/transformations/0/params/profileSelectors/selectors/4",
    "value":{
        "type":"JSON_PATH",
        "value":{
            "path":"mobilePhone.status"
        }
    }
    }
]'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `op` | Chiamata di operazione utilizzata per definire l’azione necessaria per aggiornare il flusso di dati. Le operazioni includono: `add`, `replace`, e `remove`. Per rimuovere un segmento da un flusso di dati, utilizza `remove` operazione. |
| `path` | Specifica l’attributo di profilo esistente da rimuovere dal flusso di dati di destinazione, in base all’indice del selettore di segmenti. Per recuperare l’ordine degli attributi di profilo in un flusso di dati, esegui una chiamata di GET al `/flows` e ispezionare il `transformations.profileSelectors` proprietà. Per eliminare il primo segmento nel flusso di dati, utilizza `"path":"transformations/0/params/segmentSelectors/selectors/0/"`. |


**Risposta**

In caso di esito positivo, la risposta restituisce l’ID di flusso e un tag aggiornato. Per verificare l’aggiornamento, effettua una richiesta GET al [!DNL Flow Service] , fornendo al tempo stesso l&#39;ID di flusso.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Gestione degli errori API {#api-error-handling}

Gli endpoint API in questa esercitazione seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](/help/landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](/help/landing/troubleshooting.md#request-header-errors) per ulteriori informazioni sull’interpretazione delle risposte di errore, consulta la guida alla risoluzione dei problemi di Platform.

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai imparato ad aggiornare vari componenti di un flusso di dati di destinazione, come l’aggiunta o la rimozione di segmenti o attributi di profilo utilizzando [!DNL Flow Service] API. Per ulteriori informazioni sulle destinazioni, vedi [panoramica sulle destinazioni](../home.md).
