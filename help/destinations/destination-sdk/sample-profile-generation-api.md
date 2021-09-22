---
description: Questa pagina elenca e descrive tutte le operazioni API che puoi eseguire utilizzando l’endpoint API `/authoring/sample-profiles`, per generare profili di esempio da utilizzare nel test di destinazione.
title: Operazioni API per la generazione di profili di esempio
exl-id: 5f1cd00a-8eee-4454-bcae-07b05afa54af
source-git-commit: 2ed132cd16db64b5921c5632445956f750fead56
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 3%

---

# Operazioni API per la generazione di profili di esempio {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**Endpoint** API:  `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

In questa pagina sono elencate e descritte tutte le operazioni API che puoi eseguire utilizzando l’endpoint API `/authoring/sample-profiles`.

Questo endpoint API ti consente di generare profili di esempio da utilizzare:
* Quando si esegue il test di un modello di trasformazione del messaggio. Per ulteriori informazioni, consulta [Creare e testare un modello di trasformazione dei messaggi](./create-template.md).
* Quando si verifica se la destinazione è configurata correttamente. Ulteriori informazioni in [Verifica la configurazione di destinazione](./test-destination.md).

Puoi generare profili di esempio in base allo schema di origine XDM di Adobe o allo schema di destinazione supportato dalla destinazione. Per comprendere la differenza tra lo schema di origine XDM di Adobe e lo schema di destinazione, leggi l&#39;articolo [Formato del messaggio](./message-format.md) .

## Guida introduttiva alle operazioni API di generazione dei profili di esempio {#get-started}

Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all&#39;API, tra cui come ottenere l&#39;autorizzazione di authoring di destinazione richiesta e le intestazioni richieste.

## Generare profili di esempio in base allo schema di origine {#generate-sample-profiles-source-schema}

>[!IMPORTANT]
>
>Aggiungi i profili di esempio generati qui alle chiamate HTTP durante il [test della destinazione](./test-destination.md).

Puoi generare profili di esempio basati sullo schema di origine effettuando una richiesta di GET all’ endpoint `authoring/sample-profiles/` e fornendo l’ID di un’istanza di destinazione creata in base alla configurazione di destinazione che desideri verificare.

>[!TIP]
>
>* Ottieni l’ID dell’istanza di destinazione da utilizzare qui dall’URL quando esplori una connessione con la tua destinazione.
   >![Immagine dell&#39;interfaccia utente come ottenere l&#39;ID dell&#39;istanza di destinazione](./assets/get-destination-instance-id.png)


**Formato API**


```http
GET authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={COUNT}
```

| Parametro query | Descrizione |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | L’ID dell’istanza di destinazione in base a cui stai generando profili di esempio. |
| `{COUNT}` | *Facoltativo*. Il numero di profili di esempio che stai generando. Il parametro può accettare valori compresi tra `1 - 1000`. <br> Se il parametro count non è specificato, il numero predefinito di profili generati è determinato dal  `maxUsersPerRequest` valore nella configurazione [ del server di ](./destination-server-api.md#create)destinazione. Se questa proprietà non è definita, Adobe genererà un profilo di esempio. |

{style=&quot;table-layout:auto&quot;}


**Richiesta**

La richiesta seguente genera profili di esempio configurati dai parametri di query `{DESTINATION_INSTANCE_ID}` e `{COUNT}` .

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con il numero specificato di profili di esempio, con appartenenza al segmento, identità e attributi di profilo corrispondenti allo schema XDM di origine.

>[!TIP]
>
> La risposta restituisce solo l’appartenenza al segmento, le identità e gli attributi di profilo utilizzati nell’istanza di destinazione. Anche se lo schema di origine dispone di altri campi, questi vengono ignorati.

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
| `segmentMembership` | Un oggetto map che descrive le appartenenze al segmento del singolo utente. Per ulteriori informazioni su `segmentMembership`, leggere [Dettagli di appartenenza al segmento](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html). |
| `lastQualificationTime` | Una marca temporale dell’ultima volta che il profilo è qualificato per il segmento. |
| `xdm:status` | Indica se l’appartenenza al segmento è stata realizzata come parte della richiesta corrente. Sono accettati i seguenti valori: <ul><li>`existing`: Il profilo faceva già parte del segmento prima della richiesta e continua a mantenere la sua appartenenza.</li><li>`realized`: Il profilo sta entrando nel segmento come parte della richiesta corrente.</li><li>`exited`: Il profilo sta uscendo dal segmento come parte della richiesta corrente.</li></ul> |
| `identityMap` | Campo di tipo mappa che descrive i vari valori di identità di un singolo utente, insieme ai relativi namespace associati. Per ulteriori informazioni su `identityMap`, leggere [Base della composizione dello schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#identityMap). |

{style=&quot;table-layout:auto&quot;}

## Generare profili di esempio in base allo schema di destinazione {#generate-sample-profiles-target-schema}

>[!IMPORTANT]
>
>Utilizza i profili di esempio generati qui durante la creazione del modello, nel [passaggio del modello di rendering](./render-template-api.md#multiple-profiles-with-body).

Puoi generare profili di esempio in base allo schema di destinazione effettuando una richiesta di GET all’ endpoint `authoring/sample-profiles/` e fornendo l’ID di destinazione della configurazione di destinazione in base alla quale stai creando il modello.

>[!TIP]
>
>* L&#39;ID di destinazione da utilizzare qui è il `instanceId` che corrisponde a una configurazione di destinazione, creata utilizzando l&#39;endpoint `/destinations`. Fai riferimento al [riferimento API per la configurazione di destinazione](./destination-configuration-api.md#retrieve-list).


**Formato API**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| Parametro query | Descrizione |
| -------- | ----------- |
| `{DESTINATION_ID}` | L’ID della configurazione di destinazione in base alla quale stai generando profili di esempio. |
| `{COUNT}` | *Facoltativo*. Il numero di profili di esempio che stai generando. Il parametro può accettare valori compresi tra `1 - 1000`. <br> Se il parametro count non è specificato, il numero predefinito di profili generati è determinato dal  `maxUsersPerRequest` valore nella configurazione [ del server di ](./destination-server-api.md#create)destinazione. Se questa proprietà non è definita, Adobe genererà un profilo di esempio. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La richiesta seguente genera profili di esempio configurati dai parametri di query `{DESTINATION_ID}` e `{COUNT}` .

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con il numero specificato di profili di esempio, con appartenenza al segmento, identità e attributi di profilo corrispondenti allo schema XDM di destinazione.

```json
[
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609326Z",
                    "status": "existing"
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
                    "status": "existing"
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
                    "status": "existing"
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

Gli endpoint API SDK di destinazione seguono i principi generali dei messaggi di errore API di Experience Platform. Consulta [Codici di stato API](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) e [richiedi errori di intestazione](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi

Dopo aver letto questo documento, ora sai come generare profili di esempio da utilizzare durante il [test di un modello di trasformazione del messaggio](./create-template.md) o quando [si verifica se la destinazione è configurata correttamente](./test-destination.md).
