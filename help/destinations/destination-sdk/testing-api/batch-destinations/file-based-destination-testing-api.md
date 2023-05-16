---
description: Questa pagina spiega come utilizzare l'endpoint API /testing/destinationInstance per verificare se la destinazione basata su file è configurata correttamente e per verificare l'integrità dei dati scorre nella destinazione configurata.
title: Verifica la destinazione basata su file con profili di esempio
exl-id: 75f76aec-245b-4f07-8871-c64a710db9f6
source-git-commit: ffd87573b93d642202e51e5299250a05112b6058
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 2%

---

# Verifica la destinazione basata su file con profili di esempio

## Panoramica {#overview}

Questa pagina spiega come utilizzare il `/testing/destinationInstance` Endpoint API per verificare se la destinazione basata su file è configurata correttamente e l’integrità dei dati scorre nella destinazione configurata.

È possibile inviare richieste all’endpoint di test con o senza l’aggiunta di [profili di esempio](file-based-sample-profile-generation-api.md) alla chiamata. Se non invii profili sulla richiesta, l’API genera automaticamente un profilo di esempio e lo aggiunge alla richiesta.

I profili di esempio generati automaticamente contengono dati generici. Se desideri testare la destinazione con dati di profilo personalizzati e più intuitivi, utilizza la funzione [API di generazione di profili di esempio](file-based-sample-profile-generation-api.md) per generare un profilo di esempio, personalizzane la risposta e includilo nella richiesta al `/testing/destinationInstance` punto finale.

## Introduzione {#getting-started}

Prima di continuare, controlla la [guida introduttiva](../../getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all’API, tra cui come ottenere l’autorizzazione di authoring di destinazione richiesta e le intestazioni richieste.

## Prerequisiti {#prerequisites}

Prima di poter utilizzare il `/testing/destinationInstance` endpoint, assicurarsi di soddisfare le seguenti condizioni:

* Una destinazione basata su file esistente creata tramite la Destination SDK può essere visualizzata nella [catalogo delle destinazioni](../../../ui/destinations-workspace.md).
* Hai creato almeno un flusso di attivazione per la destinazione nell’interfaccia utente di Experience Platform.
* Per effettuare correttamente la richiesta API, devi disporre dell’ID dell’istanza di destinazione corrispondente all’istanza di destinazione che stai testando. Ottieni dall’URL l’ID dell’istanza di destinazione da utilizzare nella chiamata API quando esplori una connessione con la destinazione nell’interfaccia utente di Platform.

   ![Immagine dell’interfaccia utente che mostra come ottenere l’ID dell’istanza di destinazione dall’URL.](../../assets/testing-api/get-destination-instance-id.png)
* *Facoltativo*: Se desideri testare la configurazione di destinazione con un profilo di esempio aggiunto alla chiamata API, utilizza [/sample-profiles](file-based-sample-profile-generation-api.md) per generare un profilo di esempio basato sullo schema di origine esistente. Se non fornisci un profilo di esempio, l’API ne genererà uno e lo restituirà nella risposta.

## Verifica la configurazione di destinazione senza aggiungere profili alla chiamata . {#test-without-adding-profiles}

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

Una risposta corretta restituisce lo stato HTTP 200 insieme al payload di risposta.

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
| `activations` | Restituisce l’ID del segmento e l’ID dell’esecuzione di flusso per ciascun segmento attivato. Il numero di voci di attivazione (e dei file generati associati) è uguale al numero di segmenti mappati sull&#39;istanza di destinazione. <br><br> Esempio: Se hai mappato due segmenti all’istanza di destinazione, la variabile `activations` la matrice conterrà due voci. Ogni segmento attivato corrisponde a un file esportato. |
| `results` | Restituisce l&#39;ID dell&#39;istanza di destinazione e gli ID di esecuzione di flusso che puoi utilizzare per chiamare il [API dei risultati](file-based-destination-results-api.md), per testare ulteriormente l&#39;integrazione. |
| `inputProfiles` | Restituisce i profili di esempio generati automaticamente dall’API. |

{style="table-layout:auto"}

## Verifica la configurazione di destinazione con i profili aggiunti alla chiamata . {#test-with-added-profiles}

Per testare la destinazione con dati di profilo personalizzati e più intuitivi, puoi personalizzare la risposta ottenuta dalla [/sample-profiles](file-based-sample-profile-generation-api.md) endpoint con valori selezionati e includere il profilo personalizzato nella richiesta al `/testing/destinationInstance` punto finale.

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
| `{DESTINATION_INSTANCE_ID}` | L&#39;ID dell&#39;istanza di destinazione della destinazione che stai testando.  ID dell’istanza di destinazione per la quale stai generando profili di esempio. Consulta la sezione [prerequisiti](#prerequisites) per informazioni dettagliate su come ottenere questo ID. |
| `profiles` | Array che può includere uno o più profili. Utilizza la [endpoint API di profilo di esempio](file-based-sample-profile-generation-api.md) per generare profili da utilizzare in questa chiamata API. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 insieme al payload di risposta.

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
| `activations` | Restituisce l’ID del segmento e l’ID dell’esecuzione di flusso per ciascun segmento attivato. Il numero di voci di attivazione (e dei file generati associati) è uguale al numero di segmenti mappati sull&#39;istanza di destinazione. <br><br> Esempio: Se hai mappato due segmenti all’istanza di destinazione, la variabile `activations` la matrice conterrà due voci. Ogni segmento attivato corrisponde a un file esportato. |
| `results` | Restituisce l&#39;ID dell&#39;istanza di destinazione e gli ID di esecuzione di flusso che puoi utilizzare per chiamare il [API dei risultati](file-based-destination-results-api.md), per testare ulteriormente l&#39;integrazione. |
| `inputProfiles` | Restituisce i profili di esempio personalizzati passati nella richiesta API. |

## Gestione degli errori API {#api-error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai come verificare la configurazione di destinazione basata su file.

Se hai ricevuto una risposta API valida, la destinazione funziona correttamente. Per visualizzare informazioni più dettagliate sul flusso di attivazione, puoi utilizzare la funzione `results` dalla risposta a [visualizzare i risultati dettagliati dell’attivazione](file-based-destination-results-api.md).

Se stai costruendo una destinazione pubblica, ora puoi [invia la configurazione di destinazione](../../guides/submit-destination.md) all&#39;Adobe per la revisione.
