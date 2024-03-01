---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Endpoint API per processi di privacy
description: Scopri come gestire i processi sulla privacy per le applicazioni Experience Cloud utilizzando l’API Privacy Service.
role: Developer
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
source-git-commit: 0ffc9648fbc6e6aa3c43a7125f25a98452e8af9a
workflow-type: tm+mt
source-wordcount: '1857'
ht-degree: 1%

---

# Endpoint &quot;privacy jobs&quot;

Questo documento illustra come lavorare con i processi relativi alla privacy utilizzando le chiamate API. In particolare, riguarda l&#39;uso del `/job` endpoint nella [!DNL Privacy Service] API. Prima di leggere questa guida, consulta [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all’API, incluse le intestazioni richieste e la lettura di esempi di chiamate API.

>[!NOTE]
>
>Se stai tentando di gestire le richieste di consenso o rinuncia dei clienti, consulta [guida dell’endpoint di consenso](./consent.md).

## Elenca tutti i processi {#list}

Puoi visualizzare un elenco di tutti i processi di privacy disponibili all’interno della tua organizzazione effettuando una richiesta GET al `/jobs` endpoint.

**Formato API**

Questo formato di richiesta utilizza un `regulation` parametro di query sul `/jobs` punto finale, quindi inizia con un punto interrogativo (`?`) come illustrato di seguito. Quando vengono elencate le risorse, l’API Privacy Service restituisce fino a 1000 processi e impagina la risposta. Usa altri parametri di query (`page`, `size`e filtri di data) per filtrare la risposta. È possibile separare più parametri utilizzando il simbolo commerciale (`&`).

>[!TIP]
>
>Utilizza parametri di query aggiuntivi per filtrare ulteriormente i risultati per query specifiche. Ad esempio, puoi scoprire quanti processi relativi alla privacy sono stati inviati in un determinato periodo di tempo e il loro stato utilizzando `status`, `fromDate`, e `toDate` parametri di query.

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
GET /jobs?regulation={REGULATION}&fromDate={FROMDATE}&toDate={TODATE}&status={STATUS}
```

| Parametro | Descrizione |
| --- | --- |
| `{REGULATION}` | Tipo di regolamento per cui eseguire la query. I valori accettati includono: <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpa`</li><li>`cpra_usa`</li><li>`ctdpa`</li><li>`ctdpa_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`mhmda`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`ucpa_usa`</li><li>`vcdpa_usa`</li></ul><br>Consulta la panoramica su [normative supportate](../regulations/overview.md) per ulteriori informazioni sulle normative sulla privacy rappresentate dai valori di cui sopra. |
| `{PAGE}` | Pagina di dati da visualizzare, utilizzando la numerazione basata su 0. Il valore predefinito è `0`. |
| `{SIZE}` | Il numero di risultati da visualizzare su ogni pagina. Il valore predefinito è `100` e il massimo è `1000`. Se si supera il valore massimo, l’API restituisce un errore 400 codici. |
| `{status}` | Il comportamento predefinito consiste nell’includere tutti gli stati. Se si specifica un tipo di stato, la richiesta restituisce solo i processi di privacy che corrispondono a tale tipo di stato. I valori accettati includono: <ul><li>`processing`</li><li>`complete`</li><li>`error`</li></ul> |
| `{toDate}` | Questo parametro limita i risultati a quelli elaborati prima di una data specificata. Dalla data della richiesta, il sistema può tornare indietro di 45 giorni. Tuttavia, l’intervallo non può essere superiore a 30 giorni.<br>Accetta il formato AAAA-MM-GG. La data fornita viene interpretata come data di cessazione espressa in ora di Greenwich (GMT).<br>Se non fornisci questo parametro (e un corrispondente `fromDate`), il comportamento predefinito restituisce i processi che risalgono agli ultimi sette giorni. Se usa `toDate`, è inoltre necessario utilizzare `fromDate` parametro di query. Se non utilizzi entrambi, la chiamata restituisce un errore 400. |
| `{fromDate}` | Questo parametro limita i risultati a quelli elaborati dopo una data specificata. Dalla data della richiesta, il sistema può tornare indietro di 45 giorni. Tuttavia, l’intervallo non può essere superiore a 30 giorni.<br>Accetta il formato AAAA-MM-GG. La data fornita viene interpretata come la data di origine della richiesta espressa in ora di Greenwich (GMT).<br>Se non fornisci questo parametro (e un corrispondente `toDate`), il comportamento predefinito restituisce i processi che risalgono agli ultimi sette giorni. Se usa `fromDate`, è inoltre necessario utilizzare `toDate` parametro di query. Se non utilizzi entrambi, la chiamata restituisce un errore 400. |
| `{filterDate}` | Questo parametro limita i risultati a quelli elaborati in una data specificata. Accetta il formato AAAA-MM-GG. Il sistema può tornare indietro negli ultimi 45 giorni. |

{style="table-layout:auto"}

<!-- Not released yet:
<li>`pdpd_vnm`</li> 
 -->

**Richiesta**

La richiesta seguente recupera un elenco impaginato di tutti i processi all’interno di un’organizzazione, a partire dalla terza pagina con dimensioni di pagina pari a 50.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di processi, ciascuno dei quali contiene dettagli quali `jobId`. In questo esempio, la risposta conterrà un elenco di 50 processi, a partire dalla terza pagina dei risultati.

### Accesso alle pagine successive

Per recuperare il successivo set di risultati in una risposta impaginata, devi effettuare un’altra chiamata API allo stesso endpoint durante l’aumento del `page` parametro di query per 1.

## Creare un processo di privacy {#create-job}

>[!IMPORTANT]
>
>Privacy Service è destinato solo alle richieste degli interessati e dei diritti dei consumatori. Qualsiasi altro utilizzo di Privacy Service per la pulizia o la manutenzione dei dati non è supportato o consentito. L&#39;Adobe ha l&#39;obbligo giuridico di adempiere tali obblighi in modo tempestivo. Di conseguenza, il test di carico su Privacy Service non è consentito in quanto si tratta di un ambiente di sola produzione e crea un backlog inutile di richieste di privacy valide.
>
>È ora disponibile un limite massimo di caricamento giornaliero per evitare abusi del servizio. Se gli utenti rilevano un abuso del sistema, l’accesso al servizio verrà disattivato. Successivamente si terrà una riunione con i Privacy Service per discutere le loro azioni e l&#39;uso accettabile di tali strumenti.

Prima di creare una nuova richiesta di lavoro, devi raccogliere informazioni di identificazione sulle persone interessate a cui desideri accedere, eliminare o rinunciare alla vendita dei dati. Una volta che disponi dei dati richiesti, questi devono essere forniti nel payload di una richiesta POST al `/jobs` endpoint.

>[!NOTE]
>
>Le applicazioni Adobe Experience Cloud compatibili utilizzano valori diversi per identificare le persone interessate. Consulta la guida su [Applicazioni Privacy Service e Experience Cloud](../experience-cloud-apps.md) per ulteriori informazioni sugli identificatori richiesti per le applicazioni. Per informazioni più generali su come determinare gli ID da inviare a [!DNL Privacy Service], consulta il documento su [dati di identità nelle richieste di privacy](../identity-data.md).

Il [!DNL Privacy Service] L’API supporta due tipi di richieste di lavoro per i dati personali:

* [Accesso e/o eliminazione](#access-delete): accedere (leggere) o eliminare dati personali.
* [Rinuncia alla vendita](#opt-out): contrassegna i dati personali come non venduti.

>[!IMPORTANT]
>
>Mentre le richieste di accesso ed eliminazione possono essere combinate come una singola chiamata API, le richieste di rinuncia devono essere effettuate separatamente.

### Creare un processo di accesso/eliminazione {#access-delete}

In questa sezione viene illustrato come effettuare una richiesta di processo di accesso/eliminazione utilizzando l’API.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
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
    "include": ["Analytics", "AudienceManager","profileService"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "mergePolicyId": 124,
    "regulation": "ccpa"
}'
```

| Proprietà | Descrizione |
| --- | --- |
| `companyContexts` **(Obbligatorio)** | Array contenente le informazioni di autenticazione per l’organizzazione. Ogni identificatore elencato include i seguenti attributi: <ul><li>`namespace`: spazio dei nomi di un identificatore.</li><li>`value`: valore dell’identificatore.</li></ul>È **obbligatorio** che uno degli identificatori utilizza `imsOrgId` come `namespace`, con i relativi `value` contenente l’ID univoco della tua organizzazione. <br/><br/>Identificatori aggiuntivi possono essere qualificatori aziendali specifici per prodotto (ad esempio, `Campaign`), che identificano un’integrazione con un’applicazione di Adobe appartenente alla tua organizzazione. I valori potenziali includono nomi di account, codici client, ID tenant o altri identificatori dell’applicazione. |
| `users` **(Obbligatorio)** | Matrice contenente una raccolta di almeno un utente di cui si desidera accedere o eliminare le informazioni. Un massimo di 1000 utenti può essere fornito in una singola richiesta. Ogni oggetto utente contiene le seguenti informazioni: <ul><li>`key`: identificatore per un utente utilizzato per qualificare gli ID processo separati nei dati di risposta. È consigliabile scegliere una stringa univoca e facilmente identificabile per questo valore in modo che possa essere facilmente referenziato o cercato in un secondo momento.</li><li>`action`: array che elenca le azioni da eseguire sui dati dell’utente. A seconda delle azioni che desideri eseguire, questo array deve includere `access`, `delete`, o entrambi.</li><li>`userIDs`: raccolta di identità per l’utente. Il numero di identità che un singolo utente può avere è limitato a nove. Ogni identità è costituita da una `namespace`, a `value`, e un qualificatore dello spazio dei nomi (`type`). Consulta la [appendice](appendix.md) per ulteriori dettagli su queste proprietà richieste.</li></ul> Per una spiegazione più dettagliata di `users` e `userIDs`, vedere [guida alla risoluzione dei problemi](../troubleshooting-guide.md#user-ids). |
| `include` **(Obbligatorio)** | Array di prodotti di Adobe da includere nell’elaborazione. Se questo valore manca o è vuoto, la richiesta verrà rifiutata. Includi solo i prodotti con cui l’organizzazione ha un’integrazione. Consulta la sezione su [valori prodotti accettati](appendix.md) per ulteriori informazioni, consulta l’appendice. |
| `expandIDs` | Proprietà facoltativa che, se impostata su `true`, rappresenta un’ottimizzazione per l’elaborazione degli ID nelle applicazioni (attualmente supportato solo da [!DNL Analytics]). Se omesso, il valore predefinito è `false`. |
| `priority` | Proprietà facoltativa utilizzata da Adobe Analytics che imposta la priorità per l’elaborazione delle richieste. I valori accettati sono `normal` e `low`. Se `priority` viene omesso, il comportamento predefinito è `normal`. |
| `analyticsDeleteMethod` | Proprietà facoltativa che specifica come Adobe Analytics deve gestire i dati personali. Per questo attributo sono accettati due possibili valori: <ul><li>`anonymize`: tutti i dati a cui fa riferimento la raccolta specificata di ID utente vengono resi anonimi. Se `analyticsDeleteMethod` viene omesso. Si tratta del comportamento predefinito.</li><li>`purge`: tutti i dati vengono rimossi completamente.</li></ul> |
| `mergePolicyId` | Quando si eseguono richieste di privacy per Real-Time Customer Profile (`profileService`), puoi facoltativamente fornire l’ID della specifica [criterio di unione](../../profile/merge-policies/overview.md) che desideri utilizzare per l’unione di ID. Specificando un criterio di unione, le richieste di privacy possono includere informazioni sul pubblico quando si restituiscono dati su un cliente. È possibile specificare un solo criterio di unione per richiesta. Se non viene fornito alcun criterio di unione, le informazioni di segmentazione non vengono incluse nella risposta. |
| `regulation` **(Obbligatorio)** | Il regolamento per il lavoro sulla privacy. Sono accettati i seguenti valori: <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>Consulta la panoramica su [normative supportate](../regulations/overview.md) per ulteriori informazioni sulle normative sulla privacy rappresentate dai valori di cui sopra. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli dei nuovi processi creati.

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
| `jobId` | ID univoco di sola lettura generato dal sistema per un processo. Questo valore viene utilizzato nel passaggio successivo della ricerca di un processo specifico. |

{style="table-layout:auto"}

Dopo aver inviato correttamente la richiesta del processo, è possibile procedere al passaggio successivo di [verifica dello stato del processo](#check-status).

## Controllare lo stato di un processo {#check-status}

È possibile recuperare informazioni su un job specifico, ad esempio il relativo stato di elaborazione corrente, includendo `jobId` nel percorso di una richiesta GET al `/jobs` endpoint.

>[!IMPORTANT]
>
>I dati per i processi creati in precedenza sono disponibili per il recupero solo entro 30 giorni dalla data di completamento del processo.

**Formato API**

```http
GET /jobs/{JOB_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{JOB_ID}` | ID del processo che desideri cercare. Questo ID viene restituito in `jobId` in risposte API per [creazione di un processo](#create-job) e [elenco di tutti i processi](#list). |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente recupera i dettagli del processo il cui `jobId` viene fornito nel percorso della richiesta.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del processo specificato.

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
| `productStatusResponse` | Ogni oggetto all&#39;interno del `productResponses` contiene informazioni sullo stato corrente del processo rispetto a un [!DNL Experience Cloud] applicazione. |
| `productStatusResponse.status` | Categoria di stato corrente del processo. Consulta la tabella seguente per un elenco di [categorie di stato disponibili](#status-categories) e il significato corrispondente. |
| `productStatusResponse.message` | Lo stato specifico del processo, corrispondente alla categoria di stato. |
| `productStatusResponse.responseMsgCode` | Un codice standard per i messaggi di risposta del prodotto ricevuti da [!DNL Privacy Service]. I dettagli del messaggio sono forniti in `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | Una spiegazione più dettagliata dello stato del processo. I messaggi con stati simili possono variare tra i prodotti. |
| `productStatusResponse.results` | Per alcuni stati, alcuni prodotti possono restituire un `results` oggetto che fornisce informazioni aggiuntive non coperte `responseMsgDetail`. |
| `downloadURL` | Se lo stato del processo è `complete`, questo attributo fornisce un URL per scaricare i risultati del processo come file ZIP. Questo file è disponibile per il download per 60 giorni dopo il completamento del processo. |

{style="table-layout:auto"}

### Categorie stato processo {#status-categories}

Nella tabella seguente sono elencate le diverse categorie possibili di stato dei job e il relativo significato:

| Categoria di stato | Significato |
| -------------- | -------- |
| `complete` | Il processo è completo e (se necessario) i file vengono caricati da ogni applicazione. |
| `processing` | Le applicazioni hanno riconosciuto il job e sono in fase di elaborazione. |
| `submitted` | Il processo viene inviato a ogni candidatura applicabile. |
| `error` | Si è verificato un errore nell’elaborazione del processo. Per ottenere informazioni più specifiche, è possibile recuperare i dettagli dei singoli processi. |

{style="table-layout:auto"}

>[!NOTE]
>
>Un processo inviato potrebbe rimanere in un `processing` stato se il processo figlio dipendente è ancora in elaborazione.

## Passaggi successivi

Ora sai come creare e monitorare i processi relativi alla privacy utilizzando [!DNL Privacy Service] API. Per informazioni su come eseguire le stesse attività utilizzando l&#39;interfaccia utente, vedere [Panoramica dell’interfaccia utente di Privacy Service](../ui/overview.md).
