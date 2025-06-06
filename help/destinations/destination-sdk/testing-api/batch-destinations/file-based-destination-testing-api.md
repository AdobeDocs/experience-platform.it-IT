---
description: Questa pagina spiega come utilizzare l’endpoint API /testing/destinationInstance per verificare se la destinazione basata su file è configurata correttamente e per verificare l’integrità dei flussi di dati alla destinazione configurata.
title: Test della destinazione basata su file con profili di esempio
exl-id: 75f76aec-245b-4f07-8871-c64a710db9f6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 2%

---

# Test della destinazione basata su file con profili di esempio

## Panoramica {#overview}

In questa pagina viene illustrato come utilizzare l&#39;endpoint API `/testing/destinationInstance` per verificare se la destinazione basata su file è configurata correttamente e per verificare l&#39;integrità dei flussi di dati nella destinazione configurata.

Puoi effettuare richieste all&#39;endpoint di test con o senza aggiungere [profili di esempio](file-based-sample-profile-generation-api.md) alla chiamata. Se non invii profili nella richiesta, l’API genera automaticamente un profilo di esempio e lo aggiunge alla richiesta.

I profili di esempio generati automaticamente contengono dati generici. Se desideri testare la destinazione con dati di profilo personalizzati e più intuitivi, utilizza l&#39;[API di generazione del profilo di esempio](file-based-sample-profile-generation-api.md) per generare un profilo di esempio, quindi personalizzane la risposta e includila nella richiesta all&#39;endpoint `/testing/destinationInstance`.

## Introduzione {#getting-started}

Prima di continuare, consulta la [guida introduttiva](../../getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API, tra cui come ottenere l&#39;autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Prerequisiti {#prerequisites}

Prima di poter utilizzare l&#39;endpoint `/testing/destinationInstance`, verificare di soddisfare le seguenti condizioni:

* Hai già una destinazione basata su file creata tramite Destination SDK e la puoi visualizzare nel [catalogo delle destinazioni](../../../ui/destinations-workspace.md).
* Hai creato almeno un flusso di attivazione per la tua destinazione nell’interfaccia utente di Experience Platform.
* Per eseguire correttamente la richiesta API, è necessario disporre dell’ID dell’istanza di destinazione corrispondente all’istanza di destinazione da testare. Ottieni dall’URL l’ID dell’istanza di destinazione da utilizzare nella chiamata API per la navigazione di una connessione con la destinazione nell’interfaccia utente di Experience Platform.

  ![Immagine dell&#39;interfaccia utente che mostra come ottenere l&#39;ID dell&#39;istanza di destinazione dall&#39;URL.](../../assets/testing-api/get-destination-instance-id.png)
* *Facoltativo*: se desideri testare la configurazione di destinazione con un profilo di esempio aggiunto alla chiamata API, utilizza l&#39;endpoint [/sample-profiles](file-based-sample-profile-generation-api.md) per generare un profilo di esempio in base allo schema di origine esistente. Se non fornisci un profilo di esempio, l’API ne genererà uno e lo restituirà nella risposta.

## Verifica la configurazione di destinazione senza aggiungere profili alla chiamata {#test-without-adding-profiles}

**Formato API**

```http
POST /authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

**Richiesta**

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

| Parametri del percorso | Descrizione |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | ID dell’istanza di destinazione per la quale stai generando profili di esempio. Consulta la sezione [prerequisiti](#prerequisites) per informazioni dettagliate su come ottenere questo ID. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 insieme al payload di risposta.

```json
{
   "activations":[
      {
         "segment":"6fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"81150d76-7909-46b6-83f4-fc855a92de07"
      },
      {
         "segment":"5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"4706780a-2ab3-4d33-8c76-7c87fd318cd8"
      }
   ],
   "results":"/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=4706780a-2ab3-4d33-8c76-7c87fd318cd8,81150d76-7909-46b6-83f4-fc855a92de07",
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
                  "status":"realized"
               },
               "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"john.smith@abc.com"
         },
         "identityMap":{
            "crmid":[
               {
                  "id":"crmid-P1A7l"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"string",
               "lastName":"string"
            }
         }
      }
   ]
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `activations` | Restituisce l’ID del pubblico e l’ID di esecuzione del flusso per ogni pubblico attivato. Il numero di voci di attivazione (e dei file generati associati) è uguale al numero di tipi di pubblico mappati sull’istanza di destinazione. <br><br> Esempio: se hai mappato due tipi di pubblico all&#39;istanza di destinazione, l&#39;array `activations` conterrà due voci. Ogni pubblico attivato corrisponderà a un file esportato. |
| `results` | Restituisce l&#39;ID dell&#39;istanza di destinazione e gli ID di esecuzione del flusso che è possibile utilizzare per chiamare l&#39;API [results](file-based-destination-results-api.md), per testare ulteriormente l&#39;integrazione. |
| `inputProfiles` | Restituisce i profili di esempio generati automaticamente dall’API. |

{style="table-layout:auto"}

## Verifica la configurazione di destinazione con i profili aggiunti alla chiamata {#test-with-added-profiles}

Per testare la destinazione con dati di profilo personalizzati e più intuitivi, puoi personalizzare la risposta ottenuta dall&#39;endpoint [/sample-profiles](file-based-sample-profile-generation-api.md) con i valori desiderati e includere il profilo personalizzato nella richiesta all&#39;endpoint `/testing/destinationInstance`.

**Formato API**

```http
POST  /testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

**Richiesta**

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}' 
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
                  "status":"realized"
               },
               "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"michaelsmith@example.com"
         },
         "identityMap":{
            "crmid":[
               {
                  "id":"Custom CRM ID"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"Michael",
               "lastName":"Smith"
            }
         }
      }
   ]
}'
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | ID dell’istanza di destinazione della destinazione da testare.  ID dell’istanza di destinazione per la quale stai generando profili di esempio. Consulta la sezione [prerequisiti](#prerequisites) per informazioni dettagliate su come ottenere questo ID. |
| `profiles` | Array che può includere uno o più profili. Utilizza l&#39;endpoint [sample profile API](file-based-sample-profile-generation-api.md) per generare i profili da utilizzare in questa chiamata API. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 insieme al payload di risposta.

```json
{
   "activations":[
      {
         "segment":"6fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"81150d76-7909-46b6-83f4-fc855a92de07"
      },
      {
         "segment":"5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"4706780a-2ab3-4d33-8c76-7c87fd318cd8"
      }
   ],
   "results":"/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=4706780a-2ab3-4d33-8c76-7c87fd318cd8,81150d76-7909-46b6-83f4-fc855a92de07",
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
                  "status":"realized"
               },
               "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"michaelsmith@example.com"
         },
         "identityMap":{
            "crmid":[
               {
                  "id":"Custom CRM ID"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"Michael",
               "lastName":"Smith"
            }
         }
      }
   ]
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `activations` | Restituisce l’ID del pubblico e l’ID di esecuzione del flusso per ogni pubblico attivato. Il numero di voci di attivazione (e dei file generati associati) è uguale al numero di tipi di pubblico mappati sull’istanza di destinazione. <br><br> Esempio: se hai mappato due tipi di pubblico all&#39;istanza di destinazione, l&#39;array `activations` conterrà due voci. Ogni pubblico attivato corrisponderà a un file esportato. |
| `results` | Restituisce l&#39;ID dell&#39;istanza di destinazione e gli ID di esecuzione del flusso che è possibile utilizzare per chiamare l&#39;API [results](file-based-destination-results-api.md), per testare ulteriormente l&#39;integrazione. |
| `inputProfiles` | Restituisce i profili di esempio personalizzati passati nella richiesta API. |

## Gestione degli errori API {#api-error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Consulta [Codici di stato API](../../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Experience Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai come verificare la configurazione della destinazione basata su file.

Se hai ricevuto una risposta API valida, la destinazione funziona correttamente. Se desideri visualizzare informazioni più dettagliate sul flusso di attivazione, puoi utilizzare la proprietà `results` dalla risposta a [visualizza risultati dettagliati dell&#39;attivazione](file-based-destination-results-api.md).

Se stai creando una destinazione pubblica, ora puoi [inviare la configurazione di destinazione](../../guides/submit-destination.md) ad Adobe per la revisione.
