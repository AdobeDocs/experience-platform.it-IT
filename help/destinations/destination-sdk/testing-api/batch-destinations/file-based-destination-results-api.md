---
description: Questa pagina spiega come utilizzare l’endpoint API /testing/destinationInstance per visualizzare i dettagli completi dei risultati del test. Questo endpoint API restituisce lo stesso risultato che si otterrebbe quando si utilizza l’API del servizio Flusso per monitorare i flussi di dati.
title: Visualizza risultati di attivazione dettagliati
exl-id: a7b27beb-825e-47fd-8939-f499c3298f68
source-git-commit: 9ac6b075af3805da4dad0dd6442d026ae96ab5c7
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 2%

---

# Visualizza risultati di attivazione dettagliati {#view-test-results}

## Panoramica {#overview}

Questa pagina spiega come utilizzare il `/testing/destinationInstance` Endpoint API per visualizzare i dettagli completi dei risultati del test di destinazione basato su file.

Se hai già [ha testato la tua destinazione](file-based-destination-testing-api.md) e ha ricevuto una risposta API valida, la destinazione funziona correttamente.

Se desideri visualizzare informazioni più dettagliate sul flusso di attivazione, puoi utilizzare `results` proprietà dal [test di destinazione](file-based-destination-testing-api.md) risposta dell’endpoint, come descritto di seguito.

>[!NOTE]
>
>Questo endpoint API restituisce lo stesso risultato che si otterrebbe utilizzando [API del servizio Flusso](../../../api/update-destination-dataflows.md) per monitorare i flussi di dati.

## Introduzione {#getting-started}

Prima di continuare, controlla [guida introduttiva](../../getting-started.md) per informazioni importanti che è necessario conoscere per effettuare correttamente chiamate all’API, tra cui come ottenere l’autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Prerequisiti {#prerequisites}

Prima di utilizzare il `/testing/destinationInstance` endpoint, assicurati di soddisfare le seguenti condizioni:

* Hai già una destinazione basata su file creata tramite la Destination SDK e puoi visualizzarla nel tuo [catalogo delle destinazioni](../../../ui/destinations-workspace.md).
* Nell’interfaccia utente di Experience Platform è stato creato almeno un flusso di attivazione per la destinazione.
* Per eseguire correttamente la richiesta API, è necessario disporre dell’ID dell’istanza di destinazione corrispondente all’istanza di destinazione da testare. Ottieni dall’URL l’ID dell’istanza di destinazione da utilizzare nella chiamata API per la navigazione di una connessione con la destinazione nell’interfaccia utente di Platform.

  ![Immagine dell’interfaccia utente che mostra come ottenere l’ID dell’istanza di destinazione dall’URL.](../../assets/testing-api/get-destination-instance-id.png)
* Hai precedentemente [ha testato la configurazione di destinazione](file-based-destination-testing-api.md), e ha ricevuto una risposta API valida, che include una `results` proprietà. Utilizzerai questo `results` per testare ulteriormente la destinazione.

## Visualizzare i risultati dettagliati dei test di destinazione {#test-activation-results}

Una volta che [ha convalidato la configurazione di destinazione](file-based-destination-testing-api.md), è possibile visualizzare i risultati dettagliati dell’attivazione effettuando una richiesta GET al `authoring/testing/destinationInstance/` e fornendo l’ID dell’istanza di destinazione della destinazione da testare e gli ID di esecuzione del flusso dei tipi di pubblico attivati.

Puoi trovare l’URL API completo da utilizzare nella sezione `results` proprietà restituita nel [risposta della chiamata di test di destinazione](file-based-destination-testing-api.md).

**Formato API**

```http
GET /authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}/results?flowRunIds=id1,id2
```

| Parametri del percorso | Descrizione |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | ID dell’istanza di destinazione per la quale stai generando profili di esempio. Consulta la [prerequisiti](#prerequisites) per informazioni dettagliate su come ottenere questo ID. |

| Parametri stringa di query | Descrizione |
| -------- | ----------- |
| `flowRunIds` | Gli ID esecuzione flusso corrispondenti ai tipi di pubblico attivati. Puoi trovare gli ID esecuzione del flusso in `results` proprietà restituita nel [risposta della chiamata di test di destinazione](file-based-destination-testing-api.md). |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=30d34875-e7ba-4520-ab6e-5705e01dfb16,86c00ad7-443c-459a-855d-0e8cbee43c4f,12305c58-42a9-4230-8fad-1661ee49cb70' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

La risposta contiene i dettagli completi del flusso di attivazione. Puoi ottenere la stessa risposta chiamando il [API del servizio Flusso](../../../api/update-destination-dataflows.md) per monitorare i flussi di dati.

```json
{
   "items":[
      {
         "id":"18efd5d2-40ae-4f5c-afd1-37a39a45183a",
         "flowId":"a02071ad-f3a4-496c-a2b1-468812301d5d",
         "flowSpec":{
            "id":"25473b67-0801-418a-ab49-ed74ebf88137",
            "version":"1.0"
         },
         "metrics":{
            "durationSummary":{
               "startedAtUTC":1646652235124,
               "completedAtUTC":1646652270439
            },
            "latencySummary":null,
            "sizeSummary":{
               "inputBytes":122,
               "outputBytes":122
            },
            "recordSummary":{
               "inputRecordCount":1,
               "outputRecordCount":1,
               "createdRecordCount":1,
               "skippedRecordCount":0,
               "sourceSummaries":[
                  {
                     "id":"76e4b969-9700-4557-8330-0a8390afbdde",
                     "entitySummaries":[
                        {
                           "inputRecordCount":1,
                           "skippedRecordCount":0,
                           "id":"segment:4326c566-f81c-4ab0-8a80-9e741a5d0b1f"
                        }
                     ]
                  }
               ],
               "targetSummaries":[
                  {
                     "id":"b43607b6-0dca-43b3-a0bc-ecdea4fa6aa9",
                     "entitySummaries":[
                        {
                           "outputRecordCount":1,
                           "createdRecordCount":1,
                           "id":"segment:4326c566-f81c-4ab0-8a80-9e741a5d0b1f"
                        }
                     ]
                  }
               ]
            },
            "fileSummary":{
               "inputFileCount":1,
               "outputFileCount":1
            },
            "statusSummary":{
               "status":"success"
            }
         },
         "activities":[
            {
               "id":"c4f238e3-7334-4933-8b56-64d7ea43ea54",
               "name":"Activation Batch XdmProcessor Activity",
               "updatedAtUTC":0,
               "durationSummary":{
                  "startedAtUTC":1646652235124,
                  "completedAtUTC":1646652255157
               },
               "latencySummary":{
                  
               },
               "sizeSummary":{
                  "inputBytes":122,
                  "outputBytes":122
               },
               "recordSummary":{
                  "inputRecordCount":1,
                  "outputRecordCount":1,
                  "createdRecordCount":1,
                  "skippedRecordCount":0
               },
               "fileSummary":{
                  "inputFileCount":1,
                  "outputFileCount":1
               },
               "statusSummary":{
                  "status":"success",
                  "extensions":{
                     "incremental.batchId":"",
                     "snapshot.batchId":"",
                     "snapshot.datasetId":"",
                     "incremental.datasetId":""
                  }
               },
               "sourceInfo":null,
               "targetInfo":null
            },
            {
               "id":"51d82b36-6b8f-11eb-9439-0242ac130002",
               "name":"Activation Batch Publisher Activity",
               "updatedAtUTC":0,
               "durationSummary":{
                  "startedAtUTC":1646652270326,
                  "completedAtUTC":1646652270439
               },
               "latencySummary":{
                  
               },
               "sizeSummary":{
                  "outputBytes":122
               },
               "recordSummary":{
                  "inputRecordCount":1,
                  "outputRecordCount":1,
                  "createdRecordCount":1,
                  "skippedRecordCount":0
               },
               "fileSummary":{
                  "outputFileCount":1
               },
               "statusSummary":{
                  "status":"success",
                  "extensions":{
                     
                  }
               },
               "sourceInfo":null,
               "targetInfo":null
            }
         ],
         "predecessors":null
      }
   ],
   "_links":{
      
   }
}
```

## Gestione degli errori API {#api-error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, sai come verificare la configurazione di destinazione basata su file e visualizzare tutti i dettagli dei risultati dell’attivazione.

Se stai creando una destinazione pubblica, ora puoi [invia la configurazione di destinazione](../../guides/submit-destination.md) all&#39;Adobe per la revisione.
