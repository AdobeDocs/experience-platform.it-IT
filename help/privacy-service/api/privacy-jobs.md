---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Endpoint API per i processi di privacy
topic-legacy: developer guide
description: Scopri come gestire i processi relativi alla privacy per le applicazioni di Experience Cloud utilizzando l’API di Privacy Service.
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1344'
ht-degree: 1%

---

# Endpoint per i processi di privacy

Questo documento illustra come lavorare con i processi relativi alla privacy utilizzando le chiamate API. In particolare, tratta l’utilizzo dell’endpoint `/job` nell’ API [!DNL Privacy Service]. Prima di leggere questa guida, consulta la sezione [guida introduttiva](./getting-started.md#getting-started) per informazioni importanti da conoscere per effettuare correttamente le chiamate all&#39;API, incluse le intestazioni richieste e come leggere le chiamate API di esempio.

>[!NOTE]
>
>Se stai cercando di gestire le richieste di consenso o rinuncia dei clienti, fai riferimento alla [guida all&#39;endpoint del consenso](./consent.md).

## Elenca tutti i processi {#list}

Puoi visualizzare un elenco di tutti i processi di privacy disponibili all’interno dell’organizzazione effettuando una richiesta di GET all’endpoint `/jobs` .

**Formato API**

Questo formato di richiesta utilizza un parametro di query `regulation` sull&#39;endpoint `/jobs`, quindi inizia con un punto interrogativo (`?`) come mostrato di seguito. La risposta è impaginata e consente di utilizzare altri parametri di query (`page` e `size`) per filtrare la risposta. È possibile separare più parametri utilizzando il simbolo commerciale (`&`).

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| Parametro | Descrizione |
| --- | --- |
| `{REGULATION}` | Il tipo di regolamento per cui eseguire la query. I valori accettati includono: <ul><li>`gdpr` (Unione europea)</li><li>`ccpa` (California)</li><li>`lgpd_bra` (Brasile)</li><li>`nzpa_nzl` (Nuova Zelanda)</li><li>`pdpa_tha` (Thailandia)</li></ul> |
| `{PAGE}` | Pagina di dati da visualizzare, utilizzando la numerazione basata su 0. Il valore predefinito è `0`. |
| `{SIZE}` | Il numero di risultati da visualizzare su ogni pagina. Il valore predefinito è `1` e il valore massimo è `100`. Se si supera il valore massimo, l&#39;API restituisce un errore di codice 400. |

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

Una risposta corretta restituisce un elenco di processi, con ogni processo contenente dettagli come `jobId`. In questo esempio, la risposta conterrebbe un elenco di 50 lavori, a partire dalla terza pagina dei risultati.

### Accesso alle pagine successive

Per recuperare il successivo set di risultati in una risposta impaginata, devi effettuare un’altra chiamata API allo stesso endpoint aumentando di 1 il parametro di query `page`.

## Crea un processo per la privacy {#create-job}

Prima di creare una nuova richiesta di lavoro, è necessario innanzitutto raccogliere informazioni identificative sulle persone interessate i cui dati si desidera accedere, eliminare o rinunciare alla vendita. Una volta ottenuti i dati richiesti, questi devono essere forniti nel payload di una richiesta POST all’endpoint `/jobs` .

>[!NOTE]
>
>Le applicazioni Adobe Experience Cloud compatibili utilizzano valori diversi per identificare le persone interessate. Per ulteriori informazioni sugli identificatori richiesti per le applicazioni, consulta la guida sulle [applicazioni Privacy Service e Experience Cloud](../experience-cloud-apps.md) . Per indicazioni più generali su come determinare gli ID da inviare a [!DNL Privacy Service], consulta il documento relativo ai [dati di identità nelle richieste di privacy](../identity-data.md).

L’ API [!DNL Privacy Service] supporta due tipi di richieste di lavoro per i dati personali:

* [Accedere e/o eliminare](#access-delete): Accedere (leggere) o cancellare dati personali.
* [Rinuncia alla vendita](#opt-out): Contrassegna i dati personali come non da vendere.

>[!IMPORTANT]
>
>Mentre le richieste di accesso e cancellazione possono essere combinate come una singola chiamata API, le richieste di rinuncia devono essere effettuate separatamente.

### Crea un processo di accesso/eliminazione {#access-delete}

Questa sezione illustra come effettuare una richiesta di processo di accesso/eliminazione utilizzando l’API.

**Formato API**

```http
POST /jobs
```

**Richiesta**

La seguente richiesta crea una nuova richiesta di lavoro, configurata dagli attributi forniti nel payload come descritto di seguito.

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
| `companyContexts` **(Obbligatorio)** | Matrice contenente informazioni di autenticazione per la tua organizzazione. Ogni identificatore elencato include i seguenti attributi: <ul><li>`namespace`: Spazio dei nomi di un identificatore.</li><li>`value`: Il valore dell&#39;identificatore.</li></ul>È **obbligatorio** che uno degli identificatori utilizza `imsOrgId` come `namespace`, con il relativo `value` contenente l&#39;ID univoco per la tua organizzazione IMS. <br/><br/>Gli identificatori aggiuntivi possono essere qualificatori aziendali specifici per prodotto (ad esempio,  `Campaign`), che identificano un’integrazione con un’applicazione di Adobe appartenente alla tua organizzazione. I valori potenziali includono nomi account, codici client, ID tenant o altri identificatori di applicazione. |
| `users` **(Obbligatorio)** | Matrice contenente una raccolta di almeno un utente le cui informazioni si desidera accedere o eliminare. È possibile fornire un massimo di 1000 ID utente in un’unica richiesta. Ogni oggetto utente contiene le informazioni seguenti: <ul><li>`key`: Identificatore per un utente utilizzato per qualificare gli ID processo separati nei dati di risposta. È consigliabile scegliere una stringa univoca e facilmente identificabile per questo valore in modo che possa essere facilmente referenziata o cercata in un secondo momento.</li><li>`action`: Array che elenca le azioni desiderate da eseguire sui dati dell’utente. A seconda delle azioni che si desidera eseguire, questa matrice deve includere `access`, `delete` o entrambi.</li><li>`userIDs`: Una raccolta di identità per l&#39;utente. Il numero di identità che un singolo utente può avere è limitato a nove. Ciascuna identità è costituita da un `namespace`, un `value` e un qualificatore dello spazio dei nomi (`type`). Per ulteriori informazioni sulle proprietà richieste, vedere l&#39; [appendice](appendix.md) .</li></ul> Per una spiegazione più dettagliata di `users` e `userIDs`, consulta la [guida alla risoluzione dei problemi](../troubleshooting-guide.md#user-ids). |
| `include` **(Obbligatorio)** | Matrice di prodotti Adobe da includere nell’elaborazione. Se questo valore è mancante o altrimenti vuoto, la richiesta verrà rifiutata. Includere solo i prodotti con cui l’organizzazione dispone di un’integrazione. Per ulteriori informazioni, consulta la sezione sui [valori dei prodotti accettati](appendix.md) nell&#39;appendice. |
| `expandIDs` | Proprietà opzionale che, se impostata su `true`, rappresenta un&#39;ottimizzazione per l&#39;elaborazione degli ID nelle applicazioni (attualmente supportata solo da [!DNL Analytics]). Se omesso, il valore predefinito sarà `false`. |
| `priority` | Proprietà facoltativa utilizzata da Adobe Analytics che imposta la priorità per l’elaborazione delle richieste. I valori accettati sono `normal` e `low`. Se `priority` viene omesso, il comportamento predefinito è `normal`. |
| `analyticsDeleteMethod` | Proprietà facoltativa che specifica come Adobe Analytics deve gestire i dati personali. Per questo attributo sono accettati due possibili valori: <ul><li>`anonymize`: Tutti i dati a cui fa riferimento la raccolta di ID utente specificata vengono resi anonimi. Se `analyticsDeleteMethod` viene omesso, si tratta del comportamento predefinito.</li><li>`purge`: Tutti i dati vengono rimossi completamente.</li></ul> |
| `regulation` **(Obbligatorio)** | Il regolamento per il lavoro sulla privacy. Sono accettati i seguenti valori: <ul><li>`gdpr` (Unione europea)</li><li>`ccpa` (California)</li><li>`lgpd_bra` (Brasile)</li><li>`nzpa_nzl` (Nuova Zelanda)</li><li>`pdpa_tha` (Thailandia)</li></ul> |

**Risposta**

Una risposta corretta restituisce i dettagli dei nuovi processi creati.

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
| `jobId` | ID univoco e di sola lettura generato dal sistema per un processo. Questo valore viene utilizzato nel passaggio successivo per cercare un lavoro specifico. |

Dopo aver inviato correttamente la richiesta di lavoro, puoi procedere al passaggio successivo di [controllare lo stato del processo](#check-status).

## Controllare lo stato di un processo {#check-status}

È possibile recuperare informazioni su un processo specifico, ad esempio lo stato di elaborazione corrente, includendo il processo `jobId` nel percorso di una richiesta di GET all&#39;endpoint `/jobs`.

>[!IMPORTANT]
>
>I dati per i processi creati in precedenza sono disponibili per il recupero solo entro 30 giorni dalla data di completamento del processo.

**Formato API**

```http
GET /jobs/{JOB_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{JOB_ID}` | ID del processo da cercare. Questo ID viene restituito in `jobId` nelle risposte API per [creazione di un processo](#create-job) e [elencazione di tutti i processi](#list). |

**Richiesta**

La richiesta seguente recupera i dettagli del processo di cui viene fornito `jobId` nel percorso della richiesta.

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
| `productStatusResponse` | Ogni oggetto all&#39;interno della matrice `productResponses` contiene informazioni sullo stato corrente del processo rispetto a un&#39;applicazione [!DNL Experience Cloud] specifica. |
| `productStatusResponse.status` | La categoria di stato corrente del processo. Vedi la tabella seguente per un elenco delle [categorie di stato disponibili](#status-categories) e i loro significati corrispondenti. |
| `productStatusResponse.message` | Lo stato specifico del processo, corrispondente alla categoria di stato. |
| `productStatusResponse.responseMsgCode` | Un codice standard per i messaggi di risposta prodotto ricevuti da [!DNL Privacy Service]. I dettagli del messaggio sono forniti in `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | Una spiegazione più dettagliata dello stato del processo. I messaggi per stati simili possono variare tra i prodotti. |
| `productStatusResponse.results` | Per alcuni stati, alcuni prodotti possono restituire un oggetto `results` che fornisce informazioni aggiuntive non coperte da `responseMsgDetail`. |
| `downloadURL` | Se lo stato del processo è `complete`, questo attributo fornisce un URL per scaricare i risultati del processo come file ZIP. Questo file è disponibile per il download per 60 giorni al termine del processo. |

### Categorie di stato del processo {#status-categories}

Nella tabella seguente sono elencate le diverse possibili categorie di stato del processo e il relativo significato:

| Categoria di stato | Significato |
| -------------- | -------- |
| `complete` | Il processo è completo e (se necessario) i file vengono caricati da ogni applicazione. |
| `processing` | Le applicazioni hanno riconosciuto il processo e sono in fase di elaborazione. |
| `submitted` | Il processo viene inviato a ogni applicazione applicabile. |
| `error` | Errore durante l&#39;elaborazione del processo. È possibile ottenere informazioni più specifiche recuperando i dettagli dei singoli processi. |

>[!NOTE]
>
>Un processo inviato potrebbe rimanere in uno stato `processing` se presenta un processo figlio dipendente ancora in elaborazione.

## Passaggi successivi

Ora sai come creare e monitorare i processi relativi alla privacy utilizzando l’ API [!DNL Privacy Service] . Per informazioni su come eseguire le stesse attività utilizzando l&#39;interfaccia utente, consulta la [panoramica dell&#39;interfaccia utente di Privacy Service](../ui/overview.md).
