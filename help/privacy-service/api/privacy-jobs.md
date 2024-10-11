---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Endpoint API per processi di privacy
description: Scopri come gestire i processi sulla privacy per le applicazioni Experience Cloud utilizzando l’API Privacy Service.
role: Developer
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
source-git-commit: 02a95212ff8a018b2b7f0a06978307d08a6915af
workflow-type: tm+mt
source-wordcount: '1821'
ht-degree: 2%

---

# Endpoint &quot;privacy jobs&quot;

Questo documento illustra come lavorare con i processi relativi alla privacy utilizzando le chiamate API. In particolare, riguarda l&#39;utilizzo dell&#39;endpoint `/job` nell&#39;API [!DNL Privacy Service]. Prima di leggere questa guida, consulta la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API, incluse le intestazioni richieste e la lettura delle chiamate API di esempio.

>[!NOTE]
>
>Se stai tentando di gestire le richieste di consenso o rinuncia dei clienti, consulta la [guida dell&#39;endpoint del consenso](./consent.md).

## Elenca tutti i processi {#list}

È possibile visualizzare un elenco di tutti i processi di privacy disponibili all&#39;interno dell&#39;organizzazione effettuando una richiesta GET all&#39;endpoint `/jobs`.

**Formato API**

Questo formato di richiesta utilizza un parametro di query `regulation` sull&#39;endpoint `/jobs`, quindi inizia con un punto interrogativo (`?`) come mostrato di seguito. Quando vengono elencate le risorse, l’API Privacy Service restituisce fino a 1000 processi e impagina la risposta. Utilizzare altri parametri di query (`page`, `size` e filtri di data) per filtrare la risposta. È possibile separare più parametri utilizzando il simbolo commerciale (`&`).

>[!TIP]
>
>Utilizza parametri di query aggiuntivi per filtrare ulteriormente i risultati per query specifiche. È ad esempio possibile individuare il numero di processi per la privacy inviati in un determinato periodo di tempo e il relativo stato utilizzando i parametri di query `status`, `fromDate` e `toDate`.

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
GET /jobs?regulation={REGULATION}&fromDate={FROMDATE}&toDate={TODATE}&status={STATUS}
```

| Parametro | Descrizione |
| --- | --- |
| `{REGULATION}` | Tipo di regolamento per cui eseguire la query. I valori accettati includono: <ul><li>`apa_aus`</li><li>`cpa_usa`</li><li>`cpra_usa`</li><li>`ctdpa_usa`</li><li>`fdbr_usa`</li><li>`gdpr` - Nota: viene utilizzato anche per le richieste relative alle normative **ccpa**.</li><li>`hipaa_usa`</li><li>`icdpa_usa`</li><li>`lgpd_bra`</li><li>`mcdpa_usa`</li><li>`mhmda_usa`</li><li>`ndpa_usa`</li><li>`nhpa_usa`</li><li>`njdpa_usa`</li><li>`nzpa_nzl`</li><li>`ocpa_usa`</li><li>`pdpa_tha`</li><li>`tdpsa_usa`</li><li>`ucpa_usa`</li><li>`vcdpa_usa`</li></ul><br>Per ulteriori informazioni sulle normative sulla privacy rappresentate dai valori sopra riportati, consulta la panoramica sulle [normative supportate](../regulations/overview.md). |
| `{PAGE}` | Pagina di dati da visualizzare, utilizzando la numerazione basata su 0. Il valore predefinito è `0`. |
| `{SIZE}` | Il numero di risultati da visualizzare su ogni pagina. Il valore predefinito è `100` e il massimo è `1000`. Se si supera il valore massimo, l’API restituisce un errore 400 codici. |
| `{status}` | Il comportamento predefinito consiste nell’includere tutti gli stati. Se si specifica un tipo di stato, la richiesta restituisce solo i processi di privacy che corrispondono a tale tipo di stato. I valori accettati includono: <ul><li>`processing`</li><li>`complete`</li><li>`error`</li></ul> |
| `{toDate}` | Questo parametro limita i risultati a quelli elaborati prima di una data specificata. Dalla data della richiesta, il sistema può tornare indietro di 45 giorni. Tuttavia, l’intervallo non può essere superiore a 30 giorni.<br>Accetta il formato AAAA-MM-GG. La data fornita viene interpretata come data di cessazione espressa in ora di Greenwich (GMT).<br>Se non fornisci questo parametro (e un `fromDate` corrispondente), il comportamento predefinito restituisce i processi che hanno restituito i dati negli ultimi sette giorni. Se si utilizza `toDate`, è necessario utilizzare anche il parametro di query `fromDate`. Se non utilizzi entrambi, la chiamata restituisce un errore 400. |
| `{fromDate}` | Questo parametro limita i risultati a quelli elaborati dopo una data specificata. Dalla data della richiesta, il sistema può tornare indietro di 45 giorni. Tuttavia, l’intervallo non può essere superiore a 30 giorni.<br>Accetta il formato AAAA-MM-GG. La data fornita viene interpretata come la data di origine della richiesta espressa in ora di Greenwich (GMT).<br>Se non fornisci questo parametro (e un `toDate` corrispondente), il comportamento predefinito restituisce i processi che hanno restituito i dati negli ultimi sette giorni. Se si utilizza `fromDate`, è necessario utilizzare anche il parametro di query `toDate`. Se non utilizzi entrambi, la chiamata restituisce un errore 400. |
| `{filterDate}` | Questo parametro limita i risultati a quelli elaborati in una data specificata. Accetta il formato AAAA-MM-GG. Il sistema può tornare indietro negli ultimi 45 giorni. |

{style="table-layout:auto"}

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

In caso di esito positivo, la risposta restituisce un elenco di processi, ognuno dei quali contiene dettagli quali `jobId`. In questo esempio, la risposta conterrà un elenco di 50 processi, a partire dalla terza pagina dei risultati.

### Accesso alle pagine successive

Per recuperare il successivo set di risultati in una risposta impaginata, è necessario effettuare un&#39;altra chiamata API allo stesso endpoint aumentando di 1 il parametro di query `page`.

## Creare un processo di privacy {#create-job}

>[!IMPORTANT]
>
>Privacy Service è destinato solo alle richieste degli interessati e dei diritti dei consumatori. Qualsiasi altro utilizzo di Privacy Service per la pulizia o la manutenzione dei dati non è supportato o consentito. L&#39;Adobe ha l&#39;obbligo giuridico di adempiere tali obblighi in modo tempestivo. Di conseguenza, il test di carico su Privacy Service non è consentito in quanto si tratta di un ambiente di sola produzione e crea un backlog inutile di richieste di privacy valide.
>
>È ora disponibile un limite massimo di caricamento giornaliero per evitare abusi del servizio. Se gli utenti rilevano un abuso del sistema, l’accesso al servizio verrà disattivato. Successivamente si terrà una riunione con i Privacy Service per discutere le loro azioni e l&#39;uso accettabile di tali strumenti.

Prima di creare una nuova richiesta di lavoro, devi raccogliere informazioni di identificazione sulle persone interessate a cui desideri accedere, eliminare o rinunciare alla vendita dei dati. Una volta ottenuti i dati richiesti, questi devono essere forniti nel payload di una richiesta POST all&#39;endpoint `/jobs`.

>[!NOTE]
>
>Le applicazioni Adobe Experience Cloud compatibili utilizzano valori diversi per identificare le persone interessate. Per ulteriori informazioni sugli identificatori richiesti per le applicazioni, consulta la guida su [applicazioni Privacy Service e Experience Cloud](../experience-cloud-apps.md). Per indicazioni più generali su come determinare quali ID inviare a [!DNL Privacy Service], consulta il documento su [dati di identità nelle richieste di privacy](../identity-data.md).

L&#39;API [!DNL Privacy Service] supporta due tipi di richieste di processi per dati personali:

* [Accesso e/o eliminazione](#access-delete): accesso (lettura) o eliminazione di dati personali.
* [Rinuncia](#opt-out): contrassegna i dati personali come non venduti.

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
    "mergePolicyId": 124,
    "regulation": "ccpa"
}'
```

| Proprietà | Descrizione |
| --- | --- |
| `companyContexts` **(Obbligatorio)** | Array contenente le informazioni di autenticazione per l’organizzazione. Ogni identificatore elencato include i seguenti attributi: <ul><li>`namespace`: spazio dei nomi di un identificatore.</li><li>`value`: valore dell&#39;identificatore.</li></ul>È **obbligatorio** che uno degli identificatori utilizzi `imsOrgId` come `namespace`, con il relativo `value` contenente l&#39;ID univoco per la tua organizzazione. <br/><br/>Ulteriori identificatori possono essere qualificatori aziendali specifici per prodotto (ad esempio, `Campaign`), che identificano un&#39;integrazione con un&#39;applicazione di Adobe appartenente alla tua organizzazione. I valori potenziali includono nomi di account, codici client, ID tenant o altri identificatori dell’applicazione. |
| `users` **(Obbligatorio)** | Matrice contenente una raccolta di almeno un utente di cui si desidera accedere o eliminare le informazioni. Un massimo di 1000 utenti può essere fornito in una singola richiesta. Ogni oggetto utente contiene le seguenti informazioni: <ul><li>`key`: identificatore di un utente utilizzato per qualificare gli ID di processo separati nei dati di risposta. È consigliabile scegliere una stringa univoca e facilmente identificabile per questo valore in modo che possa essere facilmente referenziato o cercato in un secondo momento.</li><li>`action`: array che elenca le azioni desiderate da eseguire sui dati dell&#39;utente. A seconda delle azioni che si desidera eseguire, l&#39;array deve includere `access`, `delete` o entrambi.</li><li>`userIDs`: raccolta di identità per l&#39;utente. Il numero di identità che un singolo utente può avere è limitato a nove. Ogni identità è costituita da un `namespace`, un `value` e un qualificatore dello spazio dei nomi (`type`). Per ulteriori dettagli su queste proprietà obbligatorie, vedere l&#39;[appendice](appendix.md).</li></ul> Per una spiegazione più dettagliata di `users` e `userIDs`, vedere la [guida alla risoluzione dei problemi](../troubleshooting-guide.md#user-ids). |
| `include` **(Obbligatorio)** | Array di prodotti di Adobe da includere nell’elaborazione. Se questo valore manca o è vuoto, la richiesta verrà rifiutata. Includi solo i prodotti con cui l’organizzazione ha un’integrazione. Per ulteriori informazioni, consulta la sezione sui [valori di prodotto accettati](appendix.md) nell&#39;appendice. |
| `expandIDs` | Proprietà facoltativa che, se impostata su `true`, rappresenta un&#39;ottimizzazione per l&#39;elaborazione degli ID nelle applicazioni (attualmente supportata solo da [!DNL Analytics]). Se omesso, il valore predefinito sarà `false`. |
| `priority` | Proprietà facoltativa utilizzata da Adobe Analytics che imposta la priorità per l’elaborazione delle richieste. I valori consentiti sono `normal` e `low`. Se `priority` viene omesso, il comportamento predefinito è `normal`. |
| `mergePolicyId` | Quando si eseguono richieste di accesso a dati personali per Real-Time Customer Profile (`profileService`), è possibile fornire facoltativamente l&#39;ID del [criterio di unione](../../profile/merge-policies/overview.md) specifico che si desidera utilizzare per l&#39;unione degli ID. Specificando un criterio di unione, le richieste di privacy possono includere informazioni sul pubblico quando si restituiscono dati su un cliente. È possibile specificare un solo criterio di unione per richiesta. Se non viene fornito alcun criterio di unione, le informazioni di segmentazione non vengono incluse nella risposta. |
| `regulation` **(Obbligatorio)** | Il regolamento per il lavoro sulla privacy. Sono accettati i seguenti valori: <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>Per ulteriori informazioni sulle normative sulla privacy rappresentate dai valori sopra riportati, consulta la panoramica sulle [normative supportate](../regulations/overview.md). |

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

Dopo aver inviato correttamente la richiesta del processo, puoi procedere al passaggio successivo di [verifica dello stato del processo](#check-status).

## Controllare lo stato di un processo {#check-status}

È possibile recuperare informazioni su un processo specifico, ad esempio il relativo stato di elaborazione corrente, includendo il processo `jobId` nel percorso di una richiesta GET all&#39;endpoint `/jobs`.

>[!IMPORTANT]
>
>I dati per i processi creati in precedenza sono disponibili per il recupero solo entro 30 giorni dalla data di completamento del processo.

**Formato API**

```http
GET /jobs/{JOB_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{JOB_ID}` | ID del processo che desideri cercare. Questo ID viene restituito in `jobId` nelle risposte API riuscite per [la creazione di un processo](#create-job) e [l&#39;elenco di tutti i processi](#list). |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente recupera i dettagli del processo di cui viene fornito `jobId` nel percorso della richiesta.

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
| `productStatusResponse` | Ogni oggetto all&#39;interno dell&#39;array `productResponses` contiene informazioni sullo stato corrente del processo rispetto a una specifica applicazione [!DNL Experience Cloud]. |
| `productStatusResponse.status` | Categoria di stato corrente del processo. Per un elenco delle [categorie di stato disponibili](#status-categories) e dei relativi significati, vedere la tabella seguente. |
| `productStatusResponse.message` | Lo stato specifico del processo, corrispondente alla categoria di stato. |
| `productStatusResponse.responseMsgCode` | Codice standard per i messaggi di risposta del prodotto ricevuti da [!DNL Privacy Service]. I dettagli del messaggio sono forniti in `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | Una spiegazione più dettagliata dello stato del processo. I messaggi con stati simili possono variare tra i prodotti. |
| `productStatusResponse.results` | Per alcuni stati, alcuni prodotti potrebbero restituire un oggetto `results` che fornisce informazioni aggiuntive non coperte da `responseMsgDetail`. |
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
>Un processo inviato potrebbe rimanere nello stato `processing` se ha un processo figlio dipendente in fase di elaborazione.

## Passaggi successivi

È ora possibile creare e monitorare i processi relativi alla privacy utilizzando l&#39;API [!DNL Privacy Service]. Per informazioni su come eseguire le stesse attività utilizzando l&#39;interfaccia utente, vedere la [panoramica dell&#39;interfaccia utente Privacy Service](../ui/overview.md).
