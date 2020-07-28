---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Processi
topic: developer guide
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '1795'
ht-degree: 2%

---


# Lavori di privacy

Questo documento descrive come lavorare con i processi di privacy utilizzando le chiamate API. Nello specifico, copre l&#39;utilizzo dell&#39; `/job` endpoint nell&#39; [!DNL Privacy Service] API. Prima di leggere questa guida, fate riferimento alla sezione [](./getting-started.md#getting-started) introduttiva per informazioni importanti che è necessario conoscere per eseguire correttamente le chiamate all&#39;API, comprese le intestazioni richieste e come leggere le chiamate API di esempio.

## Elenca tutti i processi {#list}

Potete visualizzare un elenco di tutti i processi di privacy disponibili all’interno dell’organizzazione effettuando una richiesta di GET all’ `/jobs` endpoint.

**Formato API**

Questo formato di richiesta utilizza un parametro di `regulation` query sull’ `/jobs` endpoint, pertanto inizia con un punto interrogativo (`?`) come mostrato di seguito. La risposta è impaginata e consente di utilizzare altri parametri di query (`page` e `size`) per filtrare la risposta. Potete separare più parametri utilizzando le e commerciale (`&`).

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| Parametro | Descrizione |
| --- | --- |
| `{REGULATION}` | Il tipo di regolamento per cui eseguire la query. I valori accettati sono `gdpr`, `ccpa`, e `pdpa_tha`. |
| `{PAGE}` | Pagina di dati da visualizzare, con numerazione basata su 0. Il valore predefinito è `0`. |
| `{SIZE}` | Il numero di risultati da visualizzare su ogni pagina. Il valore predefinito è `1` e il valore massimo è `100`. Se si supera il limite massimo, l&#39;API restituisce un errore di 400 codice. |

**Richiesta**

La richiesta seguente recupera un elenco impaginato di tutti i processi all’interno di un’organizzazione IMS, a partire dalla terza pagina con una dimensione di pagina pari a 50.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Risposta**

Una risposta corretta restituisce un elenco di processi, con ogni processo contenente dettagli come il relativo `jobId`. In questo esempio, la risposta conterrebbe un elenco di 50 processi, a partire dalla terza pagina dei risultati.

### Accesso alle pagine successive

Per recuperare il set di risultati successivo in una risposta impaginata, dovete effettuare un&#39;altra chiamata API allo stesso endpoint aumentando il parametro della `page` query di 1.

## Creazione di un processo di privacy {#create-job}

Prima di creare una nuova richiesta di processo, è necessario innanzitutto raccogliere informazioni identificative sugli interessati di cui si desidera accedere, eliminare o rifiutare la vendita. Una volta ricevuti i dati richiesti, questi devono essere forniti nel payload di una richiesta POST all&#39; `/jobs` endpoint.

>[!NOTE]
>
>Le applicazioni Adobe Experience Cloud compatibili utilizzano valori diversi per identificare gli oggetti dei dati. Per ulteriori informazioni sugli identificatori richiesti per le applicazioni, consultate la guida sulle applicazioni [](../experience-cloud-apps.md) Privacy Service e  Experience Cloud. Per indicazioni più generali su come determinare a quali ID inviare [!DNL Privacy Service], consulta il documento sui dati di [identità nelle richieste](../identity-data.md)di privacy.

L&#39; [!DNL Privacy Service] API supporta due tipi di richieste di lavoro per i dati personali:

* [Accesso e/o eliminazione](#access-delete): Accesso (lettura) o eliminazione di dati personali.
* [Rifiuto della vendita](#opt-out): Contrassegnare i dati personali come non da vendere.

>[!IMPORTANT]
>
>Mentre le richieste di accesso ed eliminazione possono essere combinate come una singola chiamata API, le richieste di rifiuto devono essere effettuate separatamente.

### Creazione di un processo di accesso/eliminazione {#access-delete}

Questa sezione illustra come effettuare una richiesta di accesso/eliminazione tramite l’API.

**Formato API**

```http
POST /jobs
```

**Richiesta**

La richiesta seguente crea una nuova richiesta di processo, configurata dagli attributi forniti nel payload come descritto di seguito.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "DavidSmith",
        "action": ["access"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "443636576799758681021090721276",
            "isDeletedClientSide": false
          }
        ]
      },
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "loyaltyAccount",
            "value": "12AD45FE30R29",
            "type": "integrationCode"
          }
        ]
      }
    ],
    "include": ["Analytics", "AudienceManager"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

| Proprietà | Descrizione |
| --- | --- |
| `companyContexts` **(Obbligatorio)** | Un array contenente informazioni di autenticazione per l&#39;organizzazione. Ogni identificatore elencato include i seguenti attributi: <ul><li>`namespace`: Spazio dei nomi di un identificatore.</li><li>`value`: Il valore dell’identificatore.</li></ul>È **necessario** che uno degli identificatori venga utilizzato `imsOrgId` come `namespace`, con `value` l’ID univoco per l’organizzazione IMS. <br/><br/>Gli identificatori aggiuntivi possono essere qualificatori aziendali specifici per il prodotto (ad esempio, `Campaign`), che identificano un&#39;integrazione con un&#39;applicazione di Adobe  appartenente all&#39;organizzazione. I potenziali valori includono nomi account, codici cliente, ID tenant o altri identificatori dell&#39;applicazione. |
| `users` **(Obbligatorio)** | Array contenente una raccolta di almeno un utente le cui informazioni si desidera accedere o eliminare. In un&#39;unica richiesta è possibile fornire un massimo di 1000 ID utente. Ciascun oggetto utente contiene le informazioni seguenti: <ul><li>`key`: Identificatore per un utente utilizzato per qualificare gli ID processo separati nei dati della risposta. È consigliabile scegliere una stringa univoca e facilmente identificabile per questo valore in modo che possa essere facilmente reperibile o ricercato in un secondo momento.</li><li>`action`: Un array che elenca le azioni desiderate da eseguire sui dati dell&#39;utente. A seconda delle azioni che si desidera eseguire, l&#39;array deve includere `access`, `delete`o entrambi.</li><li>`userIDs`: Raccolta di identità per l&#39;utente. Il numero di identità che un singolo utente può avere è limitato a nove. Ogni identità è costituita da un `namespace`, un `value`e un qualificatore dello spazio dei nomi (`type`). Per ulteriori dettagli su queste proprietà richieste, vedere l&#39; [appendice](appendix.md) .</li></ul> Per una spiegazione più dettagliata di `users` e `userIDs`, consultate la guida alla [risoluzione dei problemi](../troubleshooting-guide.md#user-ids). |
| `include` **(Obbligatorio)** | Un array di prodotti  Adobe da includere nell&#39;elaborazione. Se questo valore risulta mancante o vuoto, la richiesta verrà rifiutata. Includete solo i prodotti con cui l&#39;organizzazione dispone di un&#39;integrazione. Per ulteriori informazioni, consulta la sezione sui valori [di prodotto](appendix.md) accettati nell’appendice. |
| `expandIDs` | Una proprietà opzionale che, se impostata su `true`, rappresenta un&#39;ottimizzazione per l&#39;elaborazione degli ID nelle applicazioni (attualmente supportata solo da [!DNL Analytics]). Se omesso, il valore predefinito sarà `false`. |
| `priority` | Proprietà opzionale utilizzata da  Adobe Analytics che imposta la priorità per l&#39;elaborazione delle richieste. I valori accettati sono `normal` e `low`. Se `priority` viene omesso, il comportamento predefinito è `normal`. |
| `analyticsDeleteMethod` | Proprietà facoltativa che specifica come  Adobe Analytics deve gestire i dati personali. Per questo attributo sono accettati due possibili valori: <ul><li>`anonymize`: Tutti i dati a cui fa riferimento la raccolta di ID utente specificata vengono resi anonimi. Se `analyticsDeleteMethod` viene omesso, questo è il comportamento predefinito.</li><li>`purge`: Tutti i dati vengono rimossi completamente.</li></ul> |
| `regulation` **(Obbligatorio)** | Il regolamento per la richiesta. Deve essere uno dei tre valori seguenti: <ul><li>gdpr</li><li>ccpa</li><li>pdpa_tha</li></ul> |

**Risposta**

Una risposta corretta restituisce i dettagli dei processi appena creati.

```json
{
    "jobs": [
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076b0842b6",
            "customer": {
                "user": {
                    "key": "DavidSmith",
                    "action": [
                        "access"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076be029f3",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "access"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bd023j1",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "delete"
                    ]
                }
            }
        }
    ],
    "requestStatus": 1,
    "totalRecords": 3
}
```

| Proprietà | Descrizione |
| --- | --- |
| `jobId` | ID univoco generato dal sistema di sola lettura per un processo. Questo valore viene utilizzato nel passaggio successivo per cercare un processo specifico. |

Dopo aver inviato correttamente la richiesta di processo, potete procedere alla fase successiva del [controllo dello stato](#check-status)del processo.

### Creare un processo di rinuncia alla vendita {#opt-out}

In questa sezione viene illustrato come effettuare una richiesta di OdL per la rinuncia alla vendita tramite l&#39;API.

**Formato API**

```http
POST /jobs
```

**Richiesta**

La richiesta seguente crea una nuova richiesta di processo, configurata dagli attributi forniti nel payload come descritto di seguito.

```shell
curl -X POST \
  https://platform.adobe.io/data/privacy/gdpr/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "DavidSmith",
        "action": ["opt-out-of-sale"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "443636576799758681021090721276",
            "isDeletedClientSide": false
          }
        ]
      },
      {
        "key": "user12345",
        "action": ["opt-out-of-sale"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "loyaltyAccount",
            "value": "12AD45FE30R29",
            "type": "integrationCode"
          }
        ]
      }
    ],
    "include": ["Analytics", "AudienceManager"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

| Proprietà | Descrizione |
| --- | --- |
| `companyContexts` **(Obbligatorio)** | Un array contenente informazioni di autenticazione per l&#39;organizzazione. Ogni identificatore elencato include i seguenti attributi: <ul><li>`namespace`: Spazio dei nomi di un identificatore.</li><li>`value`: Il valore dell’identificatore.</li></ul>È **necessario** che uno degli identificatori venga utilizzato `imsOrgId` come `namespace`, con `value` l’ID univoco per l’organizzazione IMS. <br/><br/>Gli identificatori aggiuntivi possono essere qualificatori aziendali specifici per il prodotto (ad esempio, `Campaign`), che identificano un&#39;integrazione con un&#39;applicazione di Adobe  appartenente all&#39;organizzazione. I potenziali valori includono nomi account, codici cliente, ID tenant o altri identificatori dell&#39;applicazione. |
| `users` **(Obbligatorio)** | Array contenente una raccolta di almeno un utente le cui informazioni si desidera accedere o eliminare. In un&#39;unica richiesta è possibile fornire un massimo di 1000 ID utente. Ciascun oggetto utente contiene le informazioni seguenti: <ul><li>`key`: Identificatore per un utente utilizzato per qualificare gli ID processo separati nei dati della risposta. È consigliabile scegliere una stringa univoca e facilmente identificabile per questo valore in modo che possa essere facilmente reperibile o ricercato in un secondo momento.</li><li>`action`: Un array che elenca le azioni da eseguire sui dati. Per le richieste di rinuncia alla vendita, l&#39;array deve contenere solo il valore `opt-out-of-sale`.</li><li>`userIDs`: Raccolta di identità per l&#39;utente. Il numero di identità che un singolo utente può avere è limitato a nove. Ogni identità è costituita da un `namespace`, un `value`e un qualificatore dello spazio dei nomi (`type`). Per ulteriori dettagli su queste proprietà richieste, vedere l&#39; [appendice](appendix.md) .</li></ul> Per una spiegazione più dettagliata di `users` e `userIDs`, consultate la guida alla [risoluzione dei problemi](../troubleshooting-guide.md#user-ids). |
| `include` **(Obbligatorio)** | Un array di prodotti  Adobe da includere nell&#39;elaborazione. Se questo valore risulta mancante o vuoto, la richiesta verrà rifiutata. Includete solo i prodotti con cui l&#39;organizzazione dispone di un&#39;integrazione. Per ulteriori informazioni, consulta la sezione sui valori [di prodotto](appendix.md) accettati nell’appendice. |
| `expandIDs` | Una proprietà opzionale che, se impostata su `true`, rappresenta un&#39;ottimizzazione per l&#39;elaborazione degli ID nelle applicazioni (attualmente supportata solo da [!DNL Analytics]). Se omesso, il valore predefinito sarà `false`. |
| `priority` | Proprietà opzionale utilizzata da  Adobe Analytics che imposta la priorità per l&#39;elaborazione delle richieste. I valori accettati sono `normal` e `low`. Se `priority` viene omesso, il comportamento predefinito è `normal`. |
| `analyticsDeleteMethod` | Proprietà facoltativa che specifica come  Adobe Analytics deve gestire i dati personali. Per questo attributo sono accettati due possibili valori: <ul><li>`anonymize`: Tutti i dati a cui fa riferimento la raccolta di ID utente specificata vengono resi anonimi. Se `analyticsDeleteMethod` viene omesso, questo è il comportamento predefinito.</li><li>`purge`: Tutti i dati vengono rimossi completamente.</li></ul> |
| `regulation` **(Obbligatorio)** | Il regolamento per la richiesta. Deve essere uno dei tre valori seguenti: <ul><li>gdpr</li><li>ccpa</li><li>pdpa_tha</li></ul> |

**Risposta**

Una risposta corretta restituisce i dettagli dei processi appena creati.

```json
{
    "jobs": [
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bd9vjs0",
            "customer": {
                "user": {
                    "key": "DavidSmith",
                    "action": [
                        "opt-out-of-sale"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bes0ewj2",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "opt-out-of-sale"
                    ]
                }
            }
        }
    ],
    "requestStatus": 1,
    "totalRecords": 2
}
```

| Proprietà | Descrizione |
| --- | --- |
| `jobId` | ID univoco generato dal sistema di sola lettura per un processo. Questo valore viene utilizzato per cercare un processo specifico nel passaggio successivo. |

Dopo aver inviato correttamente la richiesta di processo, potete procedere al passaggio successivo per controllare lo stato del processo.

## Verificare lo stato di un processo {#check-status}

È possibile recuperare informazioni su un processo specifico, ad esempio lo stato di elaborazione corrente, includendo tale processo nel percorso di una richiesta di GET `jobId` all&#39; `/jobs` endpoint.

>[!IMPORTANT]
>
>I dati per i processi creati in precedenza sono disponibili solo per il recupero entro 30 giorni dalla data di completamento del processo.

**Formato API**

```http
GET /jobs/{JOB_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{JOB_ID}` | ID del processo da cercare. Questo ID viene restituito in `jobId` nelle risposte API corrette per la [creazione di un processo](#create-job) e l’ [elencazione di tutti i processi](#list). |

**Richiesta**

La richiesta seguente recupera i dettagli del processo `jobId` fornito nel percorso della richiesta.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Risposta**

Una risposta corretta restituisce i dettagli del processo specificato.

```json
{
    "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076b0842b6",
    "requestId": "15700479082313109RX-899",
    "userKey": "David Smith",
    "action": "access",
    "status": "complete",
    "submittedBy": "{ACCOUNT_ID}",
    "createdDate": "10/02/2019 08:25 PM GMT",
    "lastModifiedDate": "10/02/2019 08:25 PM GMT",
    "userIds": [
        {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard",
            "namespaceId": 6,
            "isDeletedClientSide": false
        },
        {
            "namespace": "ECID",
            "value": "1123A4D5690B32A",
            "type": "standard",
            "namespaceId": 4,
            "isDeletedClientSide": false
        }
    ],
    "productResponses": [
        {
            "product": "Analytics",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6000-200",
                "responseMsgDetail": "Finished successfully."
            }
        },
        {
            "product": "Profile",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6000-200",
                "responseMsgDetail": "Success dataSetIds = [5dbb87aad37beb18a96feb61], Failed dataSetIds = []"
            }
        },
        {
            "product": "AudienceManager",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6054-200",
                "responseMsgDetail": "PARTIALLY COMPLETED- Data not found for some requests, check results for more info.",
                "results": {
                  "processed": ["1123A4D5690B32A"],
                  "ignored": ["dsmith@acme.com"]
                }
            }
        }
    ],
    "downloadURL": "http://...",
    "regulation": "ccpa"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `productStatusResponse` | Ogni oggetto all&#39;interno dell&#39; `productResponses` array contiene informazioni sullo stato corrente del processo rispetto a una specifica [!DNL Experience Cloud] applicazione. |
| `productStatusResponse.status` | La categoria di stato corrente del processo. Per un elenco delle categorie [di stato](#status-categories) disponibili e i significati corrispondenti, vedere la tabella seguente. |
| `productStatusResponse.message` | Stato specifico del processo, corrispondente alla categoria di stato. |
| `productStatusResponse.responseMsgCode` | Un codice standard per i messaggi di risposta ai prodotti ricevuti da [!DNL Privacy Service]. I dettagli del messaggio sono forniti in `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | Una spiegazione più dettagliata dello stato del processo. I messaggi per stati simili possono variare tra i prodotti. |
| `productStatusResponse.results` | Per alcuni stati, alcuni prodotti possono restituire un `results` oggetto che fornisce informazioni aggiuntive non coperte da `responseMsgDetail`. |
| `downloadURL` | Se lo stato del processo è `complete`, questo attributo fornisce un URL per scaricare i risultati del processo come file ZIP. Questo file può essere scaricato per 60 giorni al termine del processo. |

### Categorie stato processo {#status-categories}

Nella tabella seguente sono elencate le diverse possibili categorie di stato del processo e il relativo significato:

| Categoria stato | Significato |
| -------------- | -------- |
| Complete | Il processo è completo e (se necessario) i file vengono caricati da ogni applicazione. |
| Elaborazione | Le applicazioni hanno riconosciuto il processo e stanno elaborando il processo. |
| Inviato | Il processo viene inviato a tutte le applicazioni applicabili. |
| Errore | Si è verificato un errore durante l’elaborazione del processo. È possibile ottenere informazioni più specifiche recuperando i dettagli dei singoli processi. |

>[!NOTE]
>
>Un processo inviato potrebbe rimanere in stato di elaborazione se presenta un processo figlio dipendente in fase di elaborazione.

## Passaggi successivi

Ora sai come creare e monitorare i processi relativi alla privacy utilizzando l&#39; [!DNL Privacy Service] API. Per informazioni su come eseguire le stesse attività mediante l’interfaccia utente, consultate la panoramica [dell’interfaccia utente](../ui/overview.md)Privacy Service.
