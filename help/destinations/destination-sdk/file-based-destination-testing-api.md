---
description: Questa pagina spiega come utilizzare l’endpoint API /testing/destinationInstance per verificare se la destinazione basata su file è configurata correttamente e per verificare l’integrità dei flussi di dati alla destinazione configurata.
title: Test della destinazione basata su file con profili di esempio
exl-id: 75f76aec-245b-4f07-8871-c64a710db9f6
source-git-commit: 44e056407f5089c927752f00cc6bf173d7640b83
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 2%

---

# Test della destinazione basata su file con profili di esempio

## Panoramica {#overview}

Questa pagina spiega come utilizzare il `/testing/destinationInstance` Endpoint API per verificare se la destinazione basata su file è configurata correttamente e per verificare l’integrità dei flussi di dati alla destinazione configurata.

Puoi effettuare richieste all’endpoint di test con o senza aggiunta di [profili di esempio](file-based-sample-profile-generation-api.md) alla chiamata. Se non invii profili nella richiesta, l’API genera automaticamente un profilo di esempio e lo aggiunge alla richiesta.

I profili di esempio generati automaticamente contengono dati generici. Se desideri testare la destinazione con dati di profilo personalizzati e più intuitivi, utilizza [API di generazione del profilo di esempio](file-based-sample-profile-generation-api.md) per generare un profilo di esempio, personalizzane la risposta e includila nella richiesta al `/testing/destinationInstance` endpoint.

## Introduzione {#getting-started}

Prima di continuare, controlla [guida introduttiva](./getting-started.md) per informazioni importanti che è necessario conoscere per effettuare correttamente chiamate all’API, tra cui come ottenere l’autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Prerequisiti {#prerequisites}

Prima di utilizzare il `/testing/destinationInstance` endpoint, assicurati di soddisfare le seguenti condizioni:

* Hai già una destinazione basata su file creata tramite la Destination SDK e puoi visualizzarla nel tuo [catalogo delle destinazioni](../ui/destinations-workspace.md).
* Nell’interfaccia utente di Experience Platform è stato creato almeno un flusso di attivazione per la destinazione.
* Per eseguire correttamente la richiesta API, è necessario disporre dell’ID dell’istanza di destinazione corrispondente all’istanza di destinazione da testare. Ottieni dall’URL l’ID dell’istanza di destinazione da utilizzare nella chiamata API per la navigazione di una connessione con la destinazione nell’interfaccia utente di Platform.

   ![Immagine dell’interfaccia utente che mostra come ottenere l’ID dell’istanza di destinazione dall’URL.](assets/get-destination-instance-id.png)
* *Facoltativo*: se desideri testare la configurazione di destinazione con un profilo di esempio aggiunto alla chiamata API, utilizza [/sample-profiles](file-based-sample-profile-generation-api.md) per generare un profilo di esempio basato sullo schema di origine esistente. Se non fornisci un profilo di esempio, l’API ne genererà uno e lo restituirà nella risposta.

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
| `{DESTINATION_INSTANCE_ID}` | ID dell’istanza di destinazione per la quale stai generando profili di esempio. Consulta la [prerequisiti](#prerequisites) per informazioni dettagliate su come ottenere questo ID. |

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
| `activations` | Restituisce l’ID del segmento e l’ID dell’esecuzione del flusso per ciascun segmento attivato. Il numero di voci di attivazione (e dei file generati associati) è uguale al numero di segmenti mappati sull’istanza di destinazione. <br><br> Esempio: se hai mappato due segmenti all’istanza di destinazione, il `activations` l’array conterrà due voci. Ogni segmento attivato corrisponderà a un file esportato. |
| `results` | Restituisce l’ID dell’istanza di destinazione e gli ID di esecuzione del flusso che è possibile utilizzare per chiamare [API dei risultati](file-based-destination-results-api.md), per testare ulteriormente l’integrazione. |
| `inputProfiles` | Restituisce i profili di esempio generati automaticamente dall’API. |

{style="table-layout:auto"}

## Verifica la configurazione di destinazione con i profili aggiunti alla chiamata {#test-with-added-profiles}

Per testare la destinazione con dati di profilo personalizzati e più intuitivi, puoi personalizzare la risposta ottenuta da [/sample-profiles](file-based-sample-profile-generation-api.md) con i valori desiderati e includere il profilo personalizzato nella richiesta al `/testing/destinationInstance` endpoint.

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
| `{DESTINATION_INSTANCE_ID}` | ID dell’istanza di destinazione della destinazione da testare.  ID dell’istanza di destinazione per la quale stai generando profili di esempio. Consulta la [prerequisiti](#prerequisites) per informazioni dettagliate su come ottenere questo ID. |
| `profiles` | Array che può includere uno o più profili. Utilizza il [endpoint API del profilo di esempio](file-based-sample-profile-generation-api.md) per generare profili da utilizzare in questa chiamata API. |

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
| `activations` | Restituisce l’ID del segmento e l’ID dell’esecuzione del flusso per ciascun segmento attivato. Il numero di voci di attivazione (e dei file generati associati) è uguale al numero di segmenti mappati sull’istanza di destinazione. <br><br> Esempio: se hai mappato due segmenti all’istanza di destinazione, il `activations` l’array conterrà due voci. Ogni segmento attivato corrisponderà a un file esportato. |
| `results` | Restituisce l’ID dell’istanza di destinazione e gli ID di esecuzione del flusso che è possibile utilizzare per chiamare [API dei risultati](file-based-destination-results-api.md), per testare ulteriormente l’integrazione. |
| `inputProfiles` | Restituisce i profili di esempio personalizzati passati nella richiesta API. |

## Gestione degli errori API {#api-error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai come verificare la configurazione della destinazione basata su file.

Se hai ricevuto una risposta API valida, la destinazione funziona correttamente. Se desideri visualizzare informazioni più dettagliate sul flusso di attivazione, puoi utilizzare `results` proprietà dalla risposta a [visualizzare i risultati dettagliati dell’attivazione](file-based-destination-results-api.md).

Se stai creando una destinazione pubblica, ora puoi [invia la configurazione di destinazione](../destination-sdk/submit-destination.md) all&#39;Adobe per la revisione.
