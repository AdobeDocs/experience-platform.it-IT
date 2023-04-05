---
description: Questa pagina spiega come utilizzare l’endpoint API /sample-profiles da Destination SDK per generare profili di esempio basati su uno schema di origine. Puoi utilizzare questi profili di esempio per testare la configurazione di destinazione basata su file.
title: Generare profili di esempio in base a uno schema di origine
exl-id: aea50d2e-e916-4ef0-8864-9333a4eafe80
source-git-commit: 229dd08bc5d5dfab068db3be84ad20d10992fd31
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 3%

---

# Generare profili di esempio in base a uno schema di origine

## Panoramica {#overview}

Il primo passo per testare la destinazione basata su file è quello di utilizzare il `/sample-profiles` per generare un profilo di esempio basato sullo schema di origine esistente.

I profili di esempio possono aiutarti a comprendere la struttura JSON di un profilo. Inoltre, ti forniscono un valore predefinito che puoi personalizzare con i tuoi dati di profilo, per ulteriori test di destinazione.

## Introduzione {#getting-started}

Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all’API, tra cui come ottenere l’autorizzazione di authoring di destinazione richiesta e le intestazioni richieste.

## Prerequisiti {#prerequisites}

Prima di poter utilizzare il `/sample-profiles` endpoint, assicurarsi di soddisfare le seguenti condizioni:

* Una destinazione basata su file esistente creata tramite la Destination SDK può essere visualizzata nella [catalogo delle destinazioni](../ui/destinations-workspace.md).
* Hai creato almeno un flusso di attivazione per la destinazione nell’interfaccia utente di Experience Platform. La `/sample-profiles` l’endpoint crea i profili in base allo schema di origine definito nel flusso di attivazione. Consulta la sezione [esercitazione sull&#39;attivazione](../ui/activate-batch-profile-destinations.md) per scoprire come creare un flusso di attivazione.
* Per effettuare correttamente la richiesta API, devi disporre dell’ID dell’istanza di destinazione corrispondente all’istanza di destinazione che stai testando. Ottieni dall’URL l’ID dell’istanza di destinazione da utilizzare nella chiamata API quando esplori una connessione con la destinazione nell’interfaccia utente di Platform.

   ![Immagine dell’interfaccia utente che mostra come ottenere l’ID dell’istanza di destinazione dall’URL.](assets/get-destination-instance-id.png)

## Genera profili di esempio per il test di destinazione {#generate-sample-profiles}

Puoi generare profili di esempio basati sullo schema di origine effettuando una richiesta di GET al `/sample-profiles` endpoint con l&#39;ID di istanza di destinazione della destinazione che desideri verificare.

**Formato API**

```http
GET /authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={NUMBER_OF_GENERATED_PROFILES}
```

| Parametri query | Descrizione |
| -------- | ----------- |
| `destinationInstanceId` | ID dell’istanza di destinazione per la quale stai generando profili di esempio. Consulta la sezione [prerequisiti](#prerequisites) per informazioni dettagliate su come ottenere questo ID. |
| `count` | *Facoltativo*. Il numero di profili di esempio da generare. Il parametro può accettare valori compresi tra `1 - 1000`. Se questa proprietà non è definita, l’API genera un singolo profilo di esempio. |

**Richiesta**

La richiesta seguente genera un profilo di esempio basato sullo schema di origine definito nell’istanza di destinazione con il `destinationInstanceId`.

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con il numero specificato di profili di esempio, con appartenenza al segmento, identità e attributi di profilo corrispondenti allo schema XDM di origine.

>[!NOTE]
>
> La risposta restituisce solo l’appartenenza al segmento, le identità e gli attributi di profilo utilizzati nell’istanza di destinazione. Anche se lo schema di origine dispone di altri campi, questi vengono ignorati.

```json
[
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
```

![Immagine che mostra la mappatura dall’interfaccia utente ai campi dalla risposta API.](assets/sample-api-response-mapping.png)

| Proprietà | Descrizione |
| -------- | ----------- |
| `segmentMembership` | Un oggetto map che descrive le appartenenze al segmento del singolo utente. Per ulteriori informazioni su `segmentMembership`, leggi [Dettagli di appartenenza al segmento](../../xdm/field-groups/profile/segmentation.md). |
| `lastQualificationTime` | Una marca temporale dell’ultima volta che il profilo è qualificato per il segmento. |
| `status` | Campo stringa che indica se l’appartenenza al segmento è stata realizzata come parte della richiesta corrente. Sono accettati i seguenti valori: <ul><li>`realized`: Il profilo fa parte del segmento.</li><li>`exited`: Il profilo sta uscendo dal segmento come parte della richiesta corrente.</li></ul> |
| `identityMap` | Campo di tipo mappa che descrive i vari valori di identità di un singolo utente, insieme ai relativi namespace associati. Per ulteriori informazioni su `identityMap`, vedi [base della composizione dello schema](../../xdm/schema/composition.md#identityMap). |

{style="table-layout:auto"}

## Gestione degli errori API {#api-error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai come generare profili di esempio in base allo schema di origine configurato nella destinazione [flusso di attivazione](../ui/activate-batch-profile-destinations.md).

Ora puoi personalizzare questi profili o utilizzarli quando vengono restituiti dall’API, per [verifica la configurazione di destinazione basata su file](file-based-destination-testing-api.md).
