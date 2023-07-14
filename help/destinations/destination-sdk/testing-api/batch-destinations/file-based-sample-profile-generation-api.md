---
description: Questa pagina spiega come utilizzare l’endpoint API /sample-profiles di Destination SDK per generare profili di esempio in base a uno schema di origine. Puoi utilizzare questi profili di esempio per testare la configurazione della destinazione basata su file.
title: Generare profili di esempio in base a uno schema di origine
exl-id: aea50d2e-e916-4ef0-8864-9333a4eafe80
source-git-commit: c1ba465a8a866bd8bdc9a2b294ec5d894db81e11
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 3%

---


# Generare profili di esempio in base a uno schema di origine

Il primo passaggio nel test della destinazione basata su file consiste nell&#39;utilizzare `/sample-profiles` per generare un profilo di esempio basato sullo schema di origine esistente.

I profili di esempio possono aiutarti a comprendere la struttura JSON di un profilo. Inoltre, ti forniscono un valore predefinito che puoi personalizzare con i tuoi dati di profilo, per ulteriori test di destinazione.

## Introduzione {#getting-started}

Prima di continuare, controlla [guida introduttiva](../../getting-started.md) per informazioni importanti che è necessario conoscere per effettuare correttamente chiamate all’API, tra cui come ottenere l’autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Prerequisiti {#prerequisites}

Prima di utilizzare il `/sample-profiles` endpoint, assicurati di soddisfare le seguenti condizioni:

* Hai già una destinazione basata su file creata tramite la Destination SDK e puoi visualizzarla nel tuo [catalogo delle destinazioni](../../../ui/destinations-workspace.md).
* Nell’interfaccia utente di Experience Platform è stato creato almeno un flusso di attivazione per la destinazione. Il `/sample-profiles` l’endpoint crea i profili in base allo schema di origine definito nel flusso di attivazione. Consulta la [tutorial di attivazione](../../../ui/activate-batch-profile-destinations.md) per scoprire come creare un flusso di attivazione.
* Per eseguire correttamente la richiesta API, è necessario disporre dell’ID dell’istanza di destinazione corrispondente all’istanza di destinazione da testare. Ottieni dall’URL l’ID dell’istanza di destinazione da utilizzare nella chiamata API per la navigazione di una connessione con la destinazione nell’interfaccia utente di Platform.

  ![Immagine dell’interfaccia utente che mostra come ottenere l’ID dell’istanza di destinazione dall’URL.](../../assets/testing-api/get-destination-instance-id.png)

## Generare profili di esempio per il test della destinazione {#generate-sample-profiles}

Puoi generare profili di esempio in base allo schema di origine effettuando una richiesta GET al `/sample-profiles` endpoint con l’ID dell’istanza di destinazione della destinazione da testare.

**Formato API**

```http
GET /authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={NUMBER_OF_GENERATED_PROFILES}
```

| Parametri query | Descrizione |
| -------- | ----------- |
| `destinationInstanceId` | ID dell’istanza di destinazione per la quale stai generando profili di esempio. Consulta la [prerequisiti](#prerequisites) per informazioni dettagliate su come ottenere questo ID. |
| `count` | *Facoltativo*. Il numero di profili di esempio che desideri generare. Il parametro può accettare valori compresi tra `1 - 1000`. Se questa proprietà non è definita, l’API genera un singolo profilo di esempio. |

**Richiesta**

La richiesta seguente genera un profilo di esempio basato sullo schema di origine definito nell’istanza di destinazione con il profilo corrispondente `destinationInstanceId`.

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con il numero specificato di profili di esempio, con l’appartenenza al pubblico, le identità e gli attributi di profilo che corrispondono allo schema XDM di origine.

>[!NOTE]
>
> La risposta restituisce solo l’appartenenza al pubblico, le identità e gli attributi di profilo utilizzati nell’istanza di destinazione. Anche se lo schema di origine contiene altri campi, questi vengono ignorati.

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

![Immagine che mostra la mappatura dall’interfaccia utente ai campi dalla risposta API.](../../assets/testing-api/batch-destinations/sample-api-response-mapping.png)

| Proprietà | Descrizione |
| -------- | ----------- |
| `segmentMembership` | Oggetto mappa che descrive le appartenenze del singolo pubblico. Per ulteriori informazioni su `segmentMembership`, leggi [Dettagli sull’iscrizione al pubblico](../../../../xdm/field-groups/profile/segmentation.md). |
| `lastQualificationTime` | Un timestamp dell’ultima volta che questo profilo si è qualificato per il segmento. |
| `status` | Campo stringa che indica se l’appartenenza al pubblico è stata realizzata come parte della richiesta corrente. Sono accettati i seguenti valori: <ul><li>`realized`: il profilo fa parte del segmento.</li><li>`exited`: il profilo sta uscendo dal pubblico come parte della richiesta corrente.</li></ul> |
| `identityMap` | Campo di tipo mappa che descrive i vari valori di identità di un individuo, insieme ai relativi spazi dei nomi associati. Per ulteriori informazioni su `identityMap`, vedi [base della composizione dello schema](../../../../xdm/schema/composition.md#identityMap). |

{style="table-layout:auto"}

## Gestione degli errori API {#api-error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai come generare profili di esempio in base allo schema di origine configurato nella destinazione [flusso di attivazione](../../../ui/activate-batch-profile-destinations.md).

Ora puoi personalizzare questi profili o utilizzarli man mano che vengono restituiti dall’API, per [verifica della configurazione della destinazione basata su file](file-based-destination-testing-api.md).
