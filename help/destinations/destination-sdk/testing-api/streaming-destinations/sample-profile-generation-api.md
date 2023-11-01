---
description: Scopri come utilizzare l’API di test di destinazione per generare profili di esempio per la destinazione di streaming, che puoi utilizzare nel test di destinazione.
title: Generare profili di esempio in base a uno schema di origine
exl-id: 5f1cd00a-8eee-4454-bcae-07b05afa54af
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 2%

---


# Generare profili di esempio in base a uno schema di origine {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**Endpoint API**: `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

Questa pagina elenca e descrive tutte le operazioni API che è possibile eseguire utilizzando `/authoring/sample-profiles` Endpoint API

## Generare diversi tipi di profilo per API diverse {#different-profiles-different-apis}

>[!IMPORTANT]
>
>Utilizza questo endpoint API per generare profili di esempio per due casi d’uso separati. Puoi effettuare le seguenti operazioni:
>* generare profili da utilizzare quando [creazione e test di un modello di trasformazione dei messaggi](create-template.md) - utilizzando *ID destinazione* come parametro di query.
>* generare profili da utilizzare quando si effettuano chiamate a [verifica se la destinazione è configurata correttamente](streaming-destination-testing-overview.md) - utilizzando *ID istanza di destinazione* come parametro di query.

Puoi generare profili di esempio in base allo schema di origine XDM di Adobe (da utilizzare durante il test della destinazione) o allo schema di destinazione supportato dalla destinazione (da utilizzare per la creazione del modello). Per comprendere la differenza tra lo schema di origine XDM di Adobe e lo schema di destinazione, leggi la sezione panoramica della sezione [Formato del messaggio](../../functionality/destination-server/message-format.md) articolo.

Si noti che gli scopi per i quali è possibile utilizzare i profili di esempio non sono intercambiabili. Profili generati in base al *ID destinazione* può essere utilizzato solo per creare modelli di trasformazione dei messaggi e profili generati in base al *ID istanza di destinazione* può essere utilizzato solo per testare l’endpoint di destinazione.

## Guida introduttiva alle operazioni API di generazione dei profili di esempio {#get-started}

Prima di continuare, controlla [guida introduttiva](../../getting-started.md) per informazioni importanti che è necessario conoscere per effettuare correttamente chiamate all’API, tra cui come ottenere l’autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Genera profili di esempio in base allo schema di origine da utilizzare durante il test della destinazione {#generate-sample-profiles-source-schema}

>[!IMPORTANT]
>
>Aggiungi i profili di esempio generati qui alle chiamate HTTP quando [verifica della destinazione](streaming-destination-testing-overview.md).

Puoi generare profili di esempio in base allo schema di origine effettuando una richiesta GET al `authoring/sample-profiles/` e fornendo l’ID di un’istanza di destinazione creata in base alla configurazione di destinazione da testare.

Per ottenere l’ID di un’istanza di destinazione, devi innanzitutto creare una connessione nell’interfaccia utente di Experienci Platform con la destinazione prima di tentare di testare la destinazione. Leggi le [esercitazione attivazione destinazione](../../../ui/activation-overview.md) e consulta il suggerimento seguente per ottenere l’ID istanza delle destinazioni da utilizzare per questa API.

>[!IMPORTANT]
>
>* Per utilizzare questa API, è necessario disporre di una connessione esistente alla destinazione nell’interfaccia utente di Experienci Platform. Letto [connetti alla destinazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) e [attivare profili e pubblico in una destinazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html) per ulteriori informazioni.
> * Dopo aver stabilito la connessione alla destinazione, ottieni l’ID istanza di destinazione da utilizzare nelle chiamate API a questo endpoint quando [esplorazione di una connessione con la destinazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html).
>![Immagine dell’interfaccia utente per ottenere l’ID dell’istanza di destinazione](../../assets/testing-api/get-destination-instance-id.png)

**Formato API**

```http
GET authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={COUNT}
```

| Parametro query | Descrizione |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | ID dell’istanza di destinazione in base alla quale stai generando profili di esempio. |
| `{COUNT}` | *Facoltativo*. Il numero di profili di esempio che stai generando. Il parametro può accettare valori compresi tra `1 - 1000`. <br> Se il parametro count non è specificato, il numero predefinito di profili generati è determinato da `maxUsersPerRequest` valore in [configurazione del server di destinazione](../../authoring-api/destination-server/create-destination-server.md). Se questa proprietà non è definita, Adobe genera un profilo di esempio. |

{style="table-layout:auto"}


**Richiesta**

La richiesta seguente genera profili di esempio, configurati dalla `{DESTINATION_INSTANCE_ID}` e `{COUNT}` parametri di query.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con il numero specificato di profili di esempio, con l’appartenenza al pubblico, le identità e gli attributi di profilo che corrispondono allo schema XDM di origine.

>[!TIP]
>
> La risposta restituisce solo l’appartenenza al pubblico, le identità e gli attributi di profilo utilizzati nell’istanza di destinazione. Anche se lo schema di origine contiene altri campi, questi vengono ignorati.

```json
[
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-7VEsJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Y55JJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Nd9GK"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    }
]
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `segmentMembership` | Oggetto mappa che descrive le appartenenze del singolo pubblico. Per ulteriori informazioni su `segmentMembership`, leggi [Dettagli sull’iscrizione al pubblico](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html). |
| `lastQualificationTime` | Un timestamp dell’ultima volta che questo profilo si è qualificato per il segmento. |
| `xdm:status` | Campo stringa che indica se l’appartenenza al pubblico è stata realizzata come parte della richiesta corrente. Sono accettati i seguenti valori: <ul><li>`realized`: il profilo fa parte del segmento.</li><li>`exited`: il profilo sta uscendo dal pubblico come parte della richiesta corrente.</li></ul> |
| `identityMap` | Campo di tipo mappa che descrive i vari valori di identità di un individuo, insieme ai relativi spazi dei nomi associati. Per ulteriori informazioni su `identityMap`, leggi [Base della composizione dello schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html#identityMap). |

{style="table-layout:auto"}

## Generare profili di esempio in base allo schema di destinazione da utilizzare per la creazione di un modello di trasformazione dei messaggi {#generate-sample-profiles-target-schema}

>[!IMPORTANT]
>
>Utilizza i profili di esempio generati qui durante la creazione del modello, nel [passaggio modello di rendering](render-template-api.md#multiple-profiles-with-body).

Puoi generare profili di esempio in base allo schema di destinazione effettuando una richiesta GET al `authoring/sample-profiles/` e fornendo l’ID di destinazione della configurazione di destinazione in base alla quale stai creando il modello.

>[!TIP]
>
>* L’ID di destinazione da utilizzare qui è il `instanceId` che corrisponde a una configurazione di destinazione, creata utilizzando `/destinations` endpoint. Fai riferimento a [recuperare una configurazione di destinazione](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) per ulteriori dettagli.

**Formato API**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| Parametro query | Descrizione |
| -------- | ----------- |
| `{DESTINATION_ID}` | ID della configurazione di destinazione in base alla quale stai generando profili di esempio. |
| `{COUNT}` | *Facoltativo*. Il numero di profili di esempio che stai generando. Il parametro può accettare valori compresi tra `1 - 1000`. <br> Se il parametro count non è specificato, il numero predefinito di profili generati è determinato da `maxUsersPerRequest` valore in [configurazione del server di destinazione](../../authoring-api/destination-server/create-destination-server.md). Se questa proprietà non è definita, Adobe genera un profilo di esempio. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente genera profili di esempio, configurati dalla `{DESTINATION_ID}` e `{COUNT}` parametri di query.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con il numero specificato di profili di esempio, con l’appartenenza al pubblico, le identità e gli attributi di profilo che corrispondono allo schema XDM di destinazione.

```json
[
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609326Z",
                    "status": "realized"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-vizii"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-adKYs"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-t4sKv"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-C3enB"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-bfnbs"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609626Z",
                    "status": "realized"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-6YjGc"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-SfJ21"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-eQMWS"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-d3WzP"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-eWfFn"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609823Z",
                    "status": "realized"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-2PMjZ"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-3aLez"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-D2H1J"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-i6PsF"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-VPUtZ"
                }
            ]
        }
    }
]
```

## Gestione degli errori API {#api-error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai come generare profili di esempio da utilizzare quando [verifica di un modello di trasformazione dei messaggi](create-template.md) o quando [verifica della corretta configurazione della destinazione](streaming-destination-testing-overview.md).
