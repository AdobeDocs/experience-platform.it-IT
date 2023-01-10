---
keywords: Experience Platform;home;argomenti popolari; Notifiche
description: Iscrivendosi a Eventi di Adobe I/O, puoi utilizzare i webhook per ricevere notifiche relative agli stati di esecuzione del flusso delle connessioni di origine. Queste notifiche contengono informazioni sul successo dell'esecuzione del flusso o sugli errori che hanno contribuito al fallimento di un'esecuzione.
solution: Experience Platform
title: Notifiche di esecuzione del flusso
exl-id: 0f1cde97-3030-4b8e-be08-21f64e78b794
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 1%

---

# Notifiche di esecuzione del flusso

Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, database e molti altri.

[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti diverse all&#39;interno di [!DNL Platform]. Il servizio fornisce un’interfaccia utente e un’API RESTful da cui è possibile connettere tutte le sorgenti supportate.

Ad Adobe I/O, Eventi, puoi abbonarti agli eventi e utilizzare i webhook per ricevere notifiche sullo stato delle esecuzioni dei flussi. Queste notifiche contengono informazioni sul successo dell&#39;esecuzione del flusso o sugli errori che hanno contribuito al fallimento di un&#39;esecuzione.

Questo documento fornisce passaggi su come abbonarsi agli eventi, registrare i webhook e ricevere notifiche contenenti informazioni sullo stato delle esecuzioni dei flussi.

## Introduzione

Questa esercitazione presuppone che sia già stata creata almeno una connessione di origine il cui flusso viene eseguito da monitorare. Se non hai ancora configurato una connessione di origine, visita il [panoramica di origini](./home.md) per configurare l’origine scelta prima di tornare a questa guida.

Questo documento richiede anche una comprensione funzionante dei webhook e come collegare un webhook da un&#39;applicazione a un&#39;altra. Fai riferimento a [[!DNL I/O Events] documentazione](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) per un&#39;introduzione ai webhooks.

## Registra un webhook per le notifiche di esecuzione del flusso

Per ricevere le notifiche di esecuzione del flusso, devi utilizzare Adobe Developer Console per registrare un webhook nel tuo [!DNL Experience Platform] integrazione.

Segui l’esercitazione su [iscrizione alle notifiche di [!DNL I/O Event]](../observability/alerts/subscribe.md) per passaggi dettagliati su come eseguire questa operazione.

>[!IMPORTANT]
>
>Durante il processo di abbonamento, assicurati di selezionare **[!UICONTROL Notifiche di Platform]** come provider di eventi e seleziona le seguenti sottoscrizioni di eventi:
>
>* **[!UICONTROL Flusso dell&#39;origine di Experience Platform eseguito correttamente]**
>* **[!UICONTROL Impossibile eseguire il flusso dell&#39;origine di Experience Platform]**


## Ricevere notifiche di esecuzione del flusso

Con il tuo webhook collegato e l&#39;abbonamento all&#39;evento completato, puoi iniziare a ricevere notifiche di esecuzione del flusso attraverso il dashboard webhook.

Una notifica restituisce informazioni quali il numero di processi di acquisizione eseguiti, le dimensioni del file e gli errori. Una notifica restituisce anche un payload associato al flusso eseguito in formato JSON. Il payload di risposta può essere classificato come `sources_flow_run_success` o `sources_flow_run_failure`.

>[!IMPORTANT]
>
>Se durante il processo di creazione del flusso è abilitata l’acquisizione parziale, un flusso contenente sia l’acquisizione riuscita che quella non riuscita verrà contrassegnato come `sources_flow_run_success` solo se il numero di errori è inferiore alla soglia di errore impostata durante il processo di creazione del flusso. Se un&#39;esecuzione di flusso corretta contiene errori, questi verranno comunque inclusi come parte del payload restituito.

### Operazione riuscita

Una risposta corretta restituisce un set di `metrics` che definiscono le caratteristiche di un flusso specifico e `activities` che delineano il modo in cui i dati vengono trasformati.

```json
{
  "event_id": "aec55616-1715-487f-8044-ba648cc8ffee",
  "event": {
    "createdAt": 1597213529158,
    "updatedAt": 1597213530760,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "7127a4f0-def8-11e9-83ce-e79494b1c2a5",
    "sandboxName": "prod",
    "imsOrgId": "{ORG_ID}",
    "id": "933cf9f4-cf01-4d75-bcf9-f4cf010d750a",
    "flowId": "1c6f1047-dcaf-48fe-af10-47dcaf08feaf",
    "providerRefId": "test1234",
    "etag": "\"5100ec97-0000-0200-0000-5f338b5b0000\"",
    "metrics": {
      "durationSummary": {
        "startedAtUTC": 1590512053,
        "completedAtUTC": 1590512053
      },
      "sizeSummary": {
        "inputBytes": 2048,
        "outputBytes": 1024
      },
      "recordSummary": {
        "inputRecordCount": 100,
        "outputRecordCount": 70
      },
      "fileSummary": {
        "inputFileCount": 10,
        "outputFileCount": 10
      },
      "statusSummary": {
        "status": "success"
      }
    },
    "activities": [
      {
        "id": "copyActivity",
        "updatedAtUTC": 87473822,
        "durationSummary": {
          "startedAtUTC": 1590512053,
          "completedAtUTC": 1590512053
        },
        "sizeSummary": {
          "inputBytes": 2048,
          "outputBytes": 1098
        },
        "recordSummary": {
          "inputRecordCount": 100,
          "outputRecordCount": 100
        },
        "fileSummary": {
          "inputFileCount": 10,
          "outputFileCount": 10
        },
        "statusSummary": {
          "status": "success",
          "extensions": {
            "adf/pipeline/id": "abcd",
            "adf/run/id": "1234"
          }
        },
        "sourceInfo": [
          {
            "id": "sourceConnectionId1",
            "type": "SourceConnection",
            "reference": {
              "type": "AdfRunId"
            }
          }
        ]
      },
      {
        "id": "promotionActivity",
        "updatedAtUTC": 87473822,
        "durationSummary": {
          "completedAtUTC": 1590512053
        },
        "sizeSummary": {
          "inputBytes": 1098,
          "outputBytes": 1024
        },
        "recordSummary": {},
        "fileSummary": {
          "inputFileCount": 10,
          "outputFileCount": 10,
          "extensions": {
            "manifest": {
              "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01E4TSJNM2H5M74J0XB8MFWDHK/meta?path=input_files"
            }
          }
        },
        "statusSummary": {
          "status": "success",
          "extensions": {
            "batchId": "b1",
            "acp_request_id": "1234"
          }
        },
        "targetInfo": [
          {
            "id": "targetConnectionId1",
            "type": "TargetConnection",
            "reference": {
              "type": "batch"
            }
          }
        ]
      }
    ],
    "slaCreatedAt": 1597213531124,
    "processStartTime": 1597213531213,
    "header": {
      "_adobeio": {
        "imsOrgId": "{ORG_ID}",
        "providerMetadata": "platform_notifications",
        "eventCode": "sources_flow_run_success"
      }
    },
    "transformedTime": 1597213531214
  }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `metrics` | Definisce le caratteristiche dei dati nell&#39;esecuzione del flusso. |
| `activities` | Definisce i diversi passaggi e attività che vengono eseguiti per trasformare i dati. |
| `durationSummary` | Definisce l&#39;ora di inizio e di fine dell&#39;esecuzione del flusso. |
| `sizeSummary` | Definisce il volume dei dati in byte. |
| `recordSummary` | Definisce il conteggio dei record dei dati. |
| `fileSummary` | Definisce il conteggio dei file dei dati. |
| `fileInfo` | URL che consente di visualizzare una panoramica dei file acquisiti correttamente. |
| `statusSummary` | Definisce se l&#39;esecuzione del flusso è un successo o un errore. |

### Errore

La risposta seguente è un esempio di esecuzione non riuscita del flusso, con un errore che si verifica quando i dati copiati vengono elaborati. Gli errori possono inoltre verificarsi durante la copia dei dati dall’origine. Un&#39;esecuzione di flusso non riuscita include informazioni sugli errori che hanno contribuito al fallimento dell&#39;esecuzione, inclusi l&#39;errore e la descrizione.

```json
[
  {
    "messages": [
      {
        "msgType": "eventNotification",
        "version": "1.0",
        "timestamp": 1597434157622,
        "imsOrgId": "{ORG_ID}",
        "schema": {
          "name": "run-notification",
          "version": "1.0"
        },
        "provider": "FlowService",
        "_eventNotificationMeta": {
          "category": "Platform Notifications",
          "type": "sources_flow_run_failed"
        },
        "value": {
          "createdAt": 1597434147259,
          "updatedAt": 1597434157567,
          "createdBy": "{CREATED_BY}",
          "updatedBy": "{UPDATED_BY}",
          "createdClient": "{CREATED_CLIENT}",
          "updatedClient": "{UPDATED_CLIENT}",
          "sandboxId": "e49ebb00-d0fa-11e9-b164-ed6a398c8b35",
          "sandboxName": "prod",
          "imsOrgId": "{ORG_ID}",
          "id": "d9024c32-2174-4271-824c-322174627101",
          "flowId": "cf4fce79-8822-456d-8fce-798822556dc6",
          "etag": "\"0c003dbf-0000-0200-0000-5f36e92d0000\"",
          "metrics": {
            "durationSummary": {
              "startedAtUTC": 1597434147190
            },
            "sizeSummary": {
              "inputBytes": -1
            },
            "fileSummary": {
              "inputFileCount": -1
            },
            "statusSummary": {
              "status": "failed",
              "errors": [
                {
                  "code": "CONNECTOR-2001-500",
                  "message": "Error in processing (parsing, validation or transformation) the copied data."
                }
              ]
            }
          },
          "activities": [
            {
              "id": "promotionActivity",
              "updatedAtUTC": 1597434157529,
              "durationSummary": {
                "startedAtUTC": 1597434147190,
                "completedAtUTC": 1597434157212
              },
              "sizeSummary": {
                "inputBytes": -1
              },
              "recordSummary": {},
              "fileSummary": {
                "inputFileCount": -1,
                "extensions": {
                  "manifest": {
                    "fileInfo": "https://platform-stage.adobe.io/data/foundation/export/batches/6f6a900f-e40d-4f0e-9bb9-b614436c3465/meta?path=input_files"
                  }
                }
              },
              "statusSummary": {
                "status": "failed",
                "errors": [
                  {
                    "code": "CONNECTOR-2001-500",
                    "message": "Error in processing (parsing, validation or transformation) the copied data."
                  }
                ],
                "extensions": {
                  "errors": [
                    {
                      "code": "133",
                      "message": "We are unable to locate any files uploaded for this batch. Please upload files to ingest."
                    }
                  ]
                }
              },
              "targetInfo": [
                {
                  "id": "e88737aa-27b8-4795-8737-aa27b8f7959e",
                  "type": "TargetConnection",
                  "reference": {
                    "type": "Batch",
                    "ids": [
                      "6f6a900f-e40d-4f0e-9bb9-b614436c3465"
                    ]
                  }
                }
              ]
            }
          ]
        }
      }
    ]
  }
]
```

| Proprietà | Descrizione |
| ---------- | ----------- |
| `fileInfo` | URL che consente di visualizzare una panoramica dei file che sono stati acquisiti con successo e senza successo. |

>[!NOTE]
>
>Consulta la sezione [appendice](#errors) per ulteriori informazioni sui messaggi di errore.

## Passaggi successivi

Ora puoi abbonarti a eventi che ti consentono di ricevere notifiche in tempo reale sugli stati di esecuzione del flusso. Per ulteriori informazioni sulle esecuzioni di flusso e sulle origini, consulta la sezione [panoramica di origini](./home.md).

## Appendice

Le sezioni seguenti forniscono informazioni aggiuntive per l’utilizzo delle notifiche di esecuzione del flusso.

### Informazioni sui messaggi di errore {#errors}

Gli errori di acquisizione possono verificarsi quando i dati vengono copiati dall’origine o quando i dati copiati vengono elaborati in [!DNL Platform]. Per ulteriori informazioni su errori specifici, consulta la tabella seguente.

| Errore | Descrizione |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | Errore durante la copia dei dati da un&#39;origine. |
| `CONNECTOR-2001-500` | Errore durante l&#39;elaborazione dei dati copiati in [!DNL Platform]. Questo errore potrebbe riguardare l’analisi, la convalida o la trasformazione. |
