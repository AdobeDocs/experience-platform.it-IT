---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Connettersi alle destinazioni batch e attivare i dati utilizzando l’API del servizio Flusso
description: Istruzioni dettagliate per l’utilizzo dell’API del servizio Flusso per creare una destinazione di archiviazione cloud in batch o di e-mail marketing in Experience Platform e attivare i dati
type: Tutorial
exl-id: 41fd295d-7cda-4ab1-a65e-b47e6c485562
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '3411'
ht-degree: 3%

---

# Connettersi a destinazioni di e-mail marketing basate su file e attivare i dati utilizzando l’API del servizio di flusso

>[!IMPORTANT]
> 
>* Per connettersi a una destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions).
>
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions).
>
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}
>
>Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Questo tutorial illustra come utilizzare l&#39;API del servizio di flusso per creare una [destinazione di e-mail marketing](../catalog/email-marketing/overview.md) basata su file, creare un flusso di dati nella nuova destinazione creata ed esportare i dati nella nuova destinazione creata tramite file CSV.

>[!TIP]
> 
>Per informazioni su come attivare i dati nelle destinazioni di archiviazione cloud utilizzando l&#39;API del servizio Flusso, leggere l&#39;[esercitazione sull&#39;API dedicata](/help/destinations/api/activate-segments-file-based-destinations.md).

Questo tutorial utilizza la destinazione [!DNL Adobe Campaign] in tutti gli esempi, ma i passaggi sono identici per le destinazioni di e-mail marketing basate su file.

![Panoramica - i passaggi per creare una destinazione e attivare i tipi di pubblico](../assets/api/email-marketing/overview.png)

Se preferisci utilizzare l&#39;interfaccia utente di Platform per connetterti a una destinazione e attivare i dati, consulta le esercitazioni [Connettere una destinazione](../ui/connect-destination.md) e [Attivare i dati del pubblico per esportare i profili in batch](../ui/activate-batch-profile-destinations.md).

## Introduzione {#get-started}

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
* [[!DNL Segmentation Service]](../../segmentation/api/overview.md): [!DNL Adobe Experience Platform Segmentation Service] consente di creare tipi di pubblico in [!DNL Adobe Experience Platform] dai dati di [!DNL Real-Time Customer Profile].
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per attivare i dati nelle destinazioni batch in Platform.

### Raccogli le credenziali richieste {#gather-required-credentials}

Per completare i passaggi descritti in questa esercitazione, è necessario disporre delle seguenti credenziali pronte, a seconda del tipo di destinazione a cui si connette e si attivano i tipi di pubblico.

* Per [!DNL Amazon S3] connessioni: `accessId`, `secretKey`
* Per [!DNL Amazon S3] connessioni a [!DNL Adobe Campaign]: `accessId`, `secretKey`
* Per le connessioni SFTP: `domain`, `port`, `username`, `password` o `sshKey` (a seconda del metodo di connessione al percorso FTP)
* Per [!DNL Azure Blob] connessioni: `connectionString`

>[!NOTE]
>
>Le credenziali `accessId`, `secretKey` per [!DNL Amazon S3] connessioni e `accessId`, `secretKey` per [!DNL Amazon S3] connessioni a [!DNL Adobe Campaign] sono identiche.

### Lettura delle chiamate API di esempio {#reading-sample-api-calls}

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogli i valori per le intestazioni obbligatorie e facoltative {#gather-values-headers}

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l&#39;[esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Completando il tutorial sull’autenticazione si ottengono i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di [!DNL Experience Platform], come mostrato di seguito:

* Autorizzazione: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Le risorse in [!DNL Experience Platform] possono essere isolate in specifiche sandbox virtuali. Nelle richieste alle API [!DNL Platform], puoi specificare il nome e l&#39;ID della sandbox in cui verrà eseguita l&#39;operazione. Si tratta di parametri facoltativi.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Experience Platform], consulta la [documentazione di panoramica sulle sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* Tipo di contenuto: `application/json`

### Documentazione di riferimento API {#api-reference-documentation}

Questa esercitazione contiene la documentazione di riferimento per tutte le operazioni API. Consulta la documentazione API del servizio [Flow su Adobe I/O](https://www.adobe.io/experience-platform-apis/references/flow-service/). È consigliabile utilizzare questa esercitazione e la documentazione di riferimento API in parallelo.

## Ottieni l’elenco delle destinazioni disponibili {#get-the-list-of-available-destinations}

![Passaggio 1](../assets/api/batch-destination/step1.png) della panoramica dei passaggi di destinazione

In primo luogo, devi decidere a quale destinazione attivare i dati. Per iniziare, effettua una chiamata per richiedere un elenco delle destinazioni disponibili a cui puoi connettere e attivare i tipi di pubblico. Eseguire la seguente richiesta di GET all&#39;endpoint `connectionSpecs` per restituire un elenco di destinazioni disponibili:

**Formato API**

```http
GET /connectionSpecs
```

**Richiesta**

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**Risposta**

Una risposta corretta contiene un elenco di destinazioni disponibili e i relativi identificatori univoci (`id`). Memorizza il valore della destinazione che intendi utilizzare, come richiesto nei passaggi successivi. Ad esempio, se desideri connettere e inviare tipi di pubblico a [!DNL Adobe Campaign], cerca il seguente snippet nella risposta:

```json
{
    "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
  "name": "Adobe Campaign",
  ...
  ...
}
```

Per riferimento, la tabella seguente contiene gli ID delle specifiche di connessione per le destinazioni batch di uso comune:

| Destinazione | ID specifica di connessione |
---------|----------|
| [!DNL Adobe Campaign] | `0b23e41a-cb4a-4321-a78f-3b654f5d7d97` |
| [!DNL Oracle Eloqua] | `c1e44b6b-e7c8-404b-9031-58f0ef760604` |
| [!DNL Oracle Responsys] | `a5e28ddf-e265-426e-83a1-9d03a3a6822b` |
| [!DNL Salesforce Marketing Cloud] | `f599a5b3-60a7-4951-950a-cc4115c7ea27` |

{style="table-layout:auto"}

## Connetti ai dati di [!DNL Experience Platform] {#connect-to-your-experience-platform-data}

![Passaggio 2](../assets/api/batch-destination/step2.png) della panoramica dei passaggi di destinazione

Successivamente, devi connetterti ai tuoi dati di [!DNL Experience Platform], in modo da poter esportare i dati del profilo e attivarli nella tua destinazione preferita. Si tratta di due passaggi che sono descritti di seguito.

1. Innanzitutto, devi eseguire una chiamata per autorizzare l&#39;accesso ai tuoi dati in [!DNL Experience Platform], impostando una connessione di base.
2. Quindi, utilizzando l&#39;ID connessione di base, eseguire un&#39;altra chiamata in cui si crea una *connessione di origine*, che stabilisce la connessione ai dati di [!DNL Experience Platform].

### Autorizza l&#39;accesso ai tuoi dati in [!DNL Experience Platform]

**Formato API**

```http
POST /connections
```

**Richiesta**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Base connection to Experience Platform",
            "description": "This call establishes the connection to Experience Platform data",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            }
}'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `name` | Specificare un nome per la connessione di base all&#39;Experience Platform [!DNL Profile store]. |
| `description` | In alternativa, è possibile fornire una descrizione della connessione di base. |
| `connectionSpec.id` | Utilizza l&#39;ID della specifica di connessione per l&#39;[archivio profili di Experience Platform](/help/profile/home.md#profile-data-store) - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`. |

{style="table-layout:auto"}

**Risposta**

Una risposta corretta contiene l&#39;identificatore univoco della connessione di base (`id`). Memorizza questo valore come richiesto nel passaggio successivo per creare la connessione sorgente.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Connetti ai dati di [!DNL Experience Platform] {#connect-to-platform-data}

**Formato API**

```http
POST /sourceConnections
```

**Richiesta**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Connecting to Profile store",
            "description": "Optional",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            },
            "baseConnectionId": "{BASE_CONNECTION_ID}",
            "data": {
                "format": "CSV",
                "schema": null
            },
            "params" : {}
}'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `name` | Specificare un nome per la connessione di origine all&#39;Experience Platform [!DNL Profile store]. |
| `description` | Facoltativamente, è possibile fornire una descrizione per la connessione di origine. |
| `connectionSpec.id` | Utilizza l&#39;ID della specifica di connessione per l&#39;[archivio profili di Experience Platform](/help/profile/home.md#profile-data-store) - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`. |
| `baseConnectionId` | Utilizza l’ID connessione di base ottenuto nel passaggio precedente. |
| `data.format` | `CSV` è attualmente l&#39;unico formato di esportazione file supportato. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce l&#39;identificatore univoco (`id`) per la nuova connessione di origine creata a [!DNL Profile store]. Ciò conferma che la connessione ai dati di [!DNL Experience Platform] è stata eseguita correttamente. Memorizza questo valore come richiesto in un passaggio successivo.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```

## Connetti a destinazione batch {#connect-to-batch-destination}

![Passaggio 3](../assets/api/batch-destination/step3.png) della panoramica dei passaggi di destinazione

In questo passaggio, stai impostando una connessione alla destinazione di archiviazione cloud batch desiderata o al marketing via e-mail. Si tratta di due passaggi che sono descritti di seguito.

1. Innanzitutto, devi eseguire una chiamata per autorizzare l’accesso alla piattaforma di destinazione, impostando una connessione di base.
2. Quindi, utilizzando l&#39;ID connessione di base, effettuerai un&#39;altra chiamata in cui crei una *connessione di destinazione*, che specifica la posizione nell&#39;account di archiviazione in cui verranno consegnati i file di dati esportati e il formato dei dati che verranno esportati.

### Autorizza l’accesso alla destinazione batch {#authorize-access-to-batch-destination}

**Formato API**

```http
POST /connections
```

**Richiesta**

La richiesta seguente stabilisce una connessione di base a [!DNL Adobe Campaign] destinazioni. A seconda del percorso di archiviazione in cui desideri esportare i file in ([!DNL Amazon S3], SFTP, [!DNL Azure Blob]), mantieni la specifica `auth` appropriata ed elimina gli altri.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "S3 Connection for Adobe Campaign",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
        "version": "1.0"
    },
    "auth": {
        "specName": "S3",
        "params": {
            "accessId": "{ACCESS_ID}",
            "secretKey": "{SECRET_KEY}"
        }
    }
    "auth": {
        "specName": "SFTP with Password",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
    "auth": {
        "specName": "SFTP with SSH Key",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "sshKey": "{SSH_KEY}"
        }
    }        
    "auth": {
        "specName": "Azure Blob",
        "params": {
            "connectionString": "{AZURE_BLOB_CONNECTION_STRING}"
        }
    }    
}'
```

Vedi gli esempi di richieste seguenti per connettersi ad altre destinazioni di archiviazione cloud in batch e marketing via e-mail supportate.

+++ Esempio di richiesta di connessione a [!DNL Amazon S3] destinazioni

La richiesta seguente stabilisce una connessione di base a [!DNL Amazon S3] destinazioni.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Amazon S3",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
        "version": "1.0"
    },
    "auth": {
        "specName": "Access Key",
        "params": {
            "s3AccessKey": "{AMAZON_S3_ACCESS_KEY}",
            "s3SecretKey": "{AMAZON_S3_SECRET_KEY}"
        }
    }
}'
```

+++

+++ Esempio di richiesta di connessione a [!DNL Azure Blob] destinazioni

La richiesta seguente stabilisce una connessione di base a [!DNL Azure Blob] destinazioni.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Azure Blob",
    "description": "Summer advertising campaign",
    "connectionSpec": {
        "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
        "version": "1.0"
    },
    "auth": {
        "specName": "ConnectionString",
        "params": {
            "connectionString": "{AZURE_BLOB_CONNECTION_STRING}"
        }
    }
}'
```

+++

+++ Esempio di richiesta di connessione a [!DNL Oracle Eloqua] destinazioni

La richiesta seguente stabilisce una connessione di base a [!DNL Oracle Eloqua] destinazioni. A seconda del percorso di archiviazione in cui desideri esportare i file, mantieni la specifica `auth` appropriata ed elimina gli altri.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Eloqua destination",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "c1e44b6b-e7c8-404b-9031-58f0ef760604",
        "version": "1.0"
    },
    "auth": {
        "specName": "SFTP with Password",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
    "auth": {
        "specName": "SFTP with SSH Key",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "sshKey": "{SSH_KEY}"
        }
    }    
}'
```

+++

+++ Esempio di richiesta di connessione a [!DNL Oracle Responsys] destinazioni

La richiesta seguente stabilisce una connessione di base a [!DNL Oracle Responsys] destinazioni. A seconda del percorso di archiviazione in cui desideri esportare i file, mantieni la specifica `auth` appropriata ed elimina gli altri.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Responsys destination",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "a5e28ddf-e265-426e-83a1-9d03a3a6822b",
        "version": "1.0"
    },
    "auth": {
        "specName": "SFTP with Password",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
    "auth": {
        "specName": "SFTP with SSH Key",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "sshKey": "{SSH_KEY}"
        }
    }    
}'
```

+++

+++ Esempio di richiesta di connessione a [!DNL Salesforce Marketing Cloud] destinazioni

La richiesta seguente stabilisce una connessione di base a [!DNL Salesforce Marketing Cloud] destinazioni. A seconda del percorso di archiviazione in cui desideri esportare i file, mantieni la specifica `auth` appropriata ed elimina gli altri.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Salesforce Marketing Cloud",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "f599a5b3-60a7-4951-950a-cc4115c7ea27",
        "version": "1.0"
    },
    "auth": {
        "specName": "SFTP with Password",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
    "auth": {
        "specName": "SFTP with SSH Key",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "sshKey": "{SSH_KEY}"
        }
    }    
}'
```

+++

+++ Esempio di richiesta di connessione a SFTP con destinazioni password

La richiesta seguente stabilisce una connessione di base alle destinazioni SFTP.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to SFTP with password",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
        "version": "1.0"
    },
    "auth": {
        "specName": "Basic Authentication for sftp",
        "params": {
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
}'
```

+++

| Proprietà | Descrizione |
| --------- | ----------- |
| `name` | Specificare un nome per la connessione di base alla destinazione batch. |
| `description` | In alternativa, è possibile fornire una descrizione della connessione di base. |
| `connectionSpec.id` | Utilizza l’ID della specifica di connessione per la destinazione batch desiderata. Hai ottenuto questo ID nel passaggio [Ottieni l&#39;elenco delle destinazioni disponibili](#get-the-list-of-available-destinations). |
| `auth.specname` | Indica il formato di autenticazione per la destinazione. Per individuare il nome della specifica per la destinazione, eseguire una chiamata [GET all&#39;endpoint delle specifiche di connessione](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec), fornendo la specifica di connessione della destinazione desiderata. Cercare il parametro `authSpec.name` nella risposta. <br> Ad esempio, per le destinazioni Adobe Campaign è possibile utilizzare uno qualsiasi di `S3`, `SFTP with Password` o `SFTP with SSH Key`. |
| `params` | A seconda della destinazione a cui ti stai connettendo, devi fornire diversi parametri di autenticazione richiesti. Per le connessioni Amazon S3, devi fornire l’ID di accesso e la chiave segreta alla posizione di archiviazione Amazon S3. GET <br> Per individuare i parametri richiesti per la destinazione, eseguire una [chiamata all&#39;endpoint delle specifiche di connessione](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec), fornendo la specifica di connessione della destinazione desiderata. Cercare il parametro `authSpec.spec.required` nella risposta. |

{style="table-layout:auto"}

**Risposta**

Una risposta corretta contiene l&#39;identificatore univoco della connessione di base (`id`). Memorizza questo valore come richiesto nel passaggio successivo per creare una connessione di destinazione.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Specificare il percorso di archiviazione e il formato dei dati {#specify-storage-location-data-format}

[!DNL Adobe Experience Platform] esporta i dati per le destinazioni del marketing e-mail in batch e dell&#39;archiviazione cloud sotto forma di [!DNL CSV] file. In questo passaggio è possibile determinare il percorso nel percorso di archiviazione in cui verranno esportati i file.

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] divide automaticamente i file di esportazione in 5 milioni di record (righe) per file. Ogni riga rappresenta un profilo.
>
>Ai nomi dei file suddivisi viene aggiunto un numero che indica che il file fa parte di un&#39;esportazione più grande: `filename.csv`, `filename_2.csv`, `filename_3.csv`.

**Formato API**

```http
POST /targetConnections
```

**Richiesta**

La richiesta seguente stabilisce una connessione di destinazione a [!DNL Adobe Campaign] destinazioni, per determinare dove verranno inviati i file esportati nel percorso di archiviazione. A seconda del percorso di archiviazione in cui desideri esportare i file, mantieni la specifica `params` appropriata ed elimina gli altri.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Adobe Campaign",
    "description": "Connection to Adobe Campaign",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
    "params": {
        "mode": "AZURE_BLOB",
        "container": "{CONTAINER}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "format": "CSV"
    }        
}'
```

Consulta l’esempio di richieste riportato di seguito per configurare una posizione di archiviazione per altre destinazioni di archiviazione cloud in batch e marketing via e-mail supportate.

+++ Esempio di richiesta di impostazione di un percorso di archiviazione per [!DNL Amazon S3] destinazioni

La richiesta seguente stabilisce una connessione di destinazione a [!DNL Amazon S3] destinazioni, per determinare dove verranno inviati i file esportati nel percorso di archiviazione.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Amazon S3",
    "description": "Connection to Amazon S3",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
}'
```

+++

+++ Esempio di richiesta di impostazione di un percorso di archiviazione per [!DNL Azure Blob] destinazioni

La richiesta seguente stabilisce una connessione di destinazione a [!DNL Azure Blob] destinazioni, per determinare dove verranno inviati i file esportati nel percorso di archiviazione.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Azure Blob",
    "description": "Connection to Azure Blob",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "AZURE_BLOB",
        "container": "{CONTAINER}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
}'
```

+++

+++ Esempio di richiesta di impostazione di un percorso di archiviazione per [!DNL Oracle Eloqua] destinazioni

La richiesta seguente stabilisce una connessione di destinazione a [!DNL Oracle Eloqua] destinazioni, per determinare dove verranno inviati i file esportati nel percorso di archiviazione. A seconda del percorso di archiviazione in cui desideri esportare i file, mantieni la specifica `params` appropriata ed elimina gli altri.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Oracle Eloqua",
    "description": "Connection to Oracle Eloqua",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "c1e44b6b-e7c8-404b-9031-58f0ef760604",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "format": "CSV"
    }        
}'
```

+++

+++ Esempio di richiesta di impostazione di un percorso di archiviazione per [!DNL Oracle Responsys] destinazioni

La richiesta seguente stabilisce una connessione di destinazione a [!DNL Oracle Responsys] destinazioni, per determinare dove verranno inviati i file esportati nel percorso di archiviazione. A seconda del percorso di archiviazione in cui desideri esportare i file, mantieni la specifica `params` appropriata ed elimina gli altri.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Oracle Responsys",
    "description": "Connection to Oracle Responsys",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "a5e28ddf-e265-426e-83a1-9d03a3a6822b",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "format": "CSV"
    }        
}'
```

+++

+++ Esempio di richiesta di impostazione di un percorso di archiviazione per [!DNL Salesforce Marketing Cloud] destinazioni

La richiesta seguente stabilisce una connessione di destinazione a [!DNL Salesforce Marketing Cloud] destinazioni, per determinare dove verranno inviati i file esportati nel percorso di archiviazione. A seconda del percorso di archiviazione in cui desideri esportare i file, mantieni la specifica `params` appropriata ed elimina gli altri.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Salesforce Marketing Cloud",
    "description": "Connection to Salesforce Marketing Cloud",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "f599a5b3-60a7-4951-950a-cc4115c7ea27",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "format": "CSV"
    }        
}'
```

+++

+++ Richiesta di esempio per impostare una posizione di archiviazione per le destinazioni SFTP

La richiesta seguente stabilisce una connessione di destinazione alle destinazioni SFTP per determinare dove verranno inviati i file esportati nel percorso di archiviazione.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for SFTP",
    "description": "Connection to SFTP",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
    }
}'
```

+++


| Proprietà | Descrizione |
| --------- | ----------- |
| `name` | Specificare un nome per la connessione di destinazione alla destinazione batch. |
| `description` | Facoltativamente, puoi fornire una descrizione della connessione di destinazione. |
| `baseConnectionId` | Utilizza l’ID della connessione di base creata nel passaggio precedente. |
| `connectionSpec.id` | Utilizza l’ID della specifica di connessione per la destinazione batch desiderata. Hai ottenuto questo ID nel passaggio [Ottieni l&#39;elenco delle destinazioni disponibili](#get-the-list-of-available-destinations). |
| `params` | A seconda della destinazione a cui ti stai connettendo, devi fornire diversi parametri richiesti alla posizione di archiviazione. Per le connessioni Amazon S3, devi fornire l’ID di accesso e la chiave segreta alla posizione di archiviazione Amazon S3. GET <br> Per individuare i parametri richiesti per la destinazione, eseguire una [chiamata all&#39;endpoint delle specifiche di connessione](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec), fornendo la specifica di connessione della destinazione desiderata. Cercare il parametro `targetSpec.spec.required` nella risposta. |
| `params.mode` | A seconda della modalità supportata per la destinazione, è necessario fornire un valore diverso qui. Per individuare i parametri richiesti per la destinazione, eseguire una chiamata [GET all&#39;endpoint delle specifiche di connessione](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec), fornendo la specifica di connessione della destinazione desiderata. Cercare il parametro `targetSpec.spec.properties.mode.enum` nella risposta e selezionare la modalità desiderata. |
| `params.bucketName` | Per le connessioni S3, fornisci il nome del bucket in cui verranno esportati i file. |
| `params.path` | Per le connessioni S3, specifica il percorso del file nel percorso di archiviazione in cui verranno esportati i file. |
| `params.format` | `CSV` è attualmente l&#39;unico tipo di esportazione file supportato. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce l&#39;identificatore univoco (`id`) per la connessione di destinazione appena creata alla destinazione batch. Memorizza questo valore come richiesto nei passaggi successivi.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Creare un flusso di dati {#create-dataflow}

![Passaggio 4](../assets/api/batch-destination/step4.png) della panoramica dei passaggi di destinazione

Utilizzando la specifica di flusso, la connessione di origine e gli ID di connessione di destinazione ottenuti nei passaggi precedenti, è ora possibile creare un flusso di dati tra i dati [!DNL Experience Platform] e la destinazione in cui verranno esportati i file di dati. Considera questo passaggio come la costruzione della pipeline attraverso la quale i dati scorreranno in seguito tra [!DNL Experience Platform] e la destinazione desiderata.

Per creare un flusso di dati, esegui una richiesta POST come mostrato di seguito, fornendo i valori menzionati di seguito all’interno del payload.

**Formato API**

```http
POST /flows
```

**Richiesta**

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/flows' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {ORG_ID}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d  '{
   
        "name": "activate audiences to Adobe Campaign",
        "description": "This operation creates a dataflow which we will later use to activate audiences to Adobe Campaign",
        "flowSpec": {
            "id": "{FLOW_SPEC_ID}",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "{SOURCE_CONNECTION_ID}"
        ],
        "targetConnectionIds": [
            "{TARGET_CONNECTION_ID}"
        ],
        "transformations": [
            {
                "name": "GeneralTransform",
                "params": {
                    "segmentSelectors": {
                        "selectors": []
                    },
                    "profileSelectors": {
                        "selectors": []
                    }
                }
            }
        ]
    }
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `name` | Specifica un nome per il flusso di dati che stai creando. |
| `description` | Facoltativamente, puoi fornire una descrizione del flusso di dati. |
| `flowSpec.Id` | Utilizzare l&#39;ID della specifica di flusso per la destinazione batch a cui si desidera connettersi. Per recuperare l&#39;ID della specifica di flusso, eseguire un&#39;operazione di GET sull&#39;endpoint `flowspecs`, come illustrato nella [documentazione di riferimento API delle specifiche di flusso](https://www.adobe.io/experience-platform-apis/references/flow-service/#operation/retrieveFlowSpec). Nella risposta, cerca `upsTo` e copia l&#39;ID corrispondente della destinazione batch a cui desideri connetterti. Ad esempio, per Adobe Campaign, cerca `upsToCampaign` e copia il parametro `id`. |
| `sourceConnectionIds` | Utilizza l&#39;ID della connessione di origine ottenuto nel passaggio [Connetti ai dati di Experience Platform](#connect-to-your-experience-platform-data). |
| `targetConnectionIds` | Utilizzare l&#39;ID connessione di destinazione ottenuto nel passaggio [Connetti alla destinazione batch](#connect-to-batch-destination). |
| `transformations` | Nel passaggio successivo, compilerai questa sezione con i tipi di pubblico e gli attributi del profilo da attivare. |

Per riferimento, la tabella seguente contiene gli ID delle specifiche di flusso per le destinazioni batch di uso comune:

| Destinazione | ID specifica di flusso |
---------|----------|
| Tutte le destinazioni di archiviazione cloud ([!DNL Amazon S3], SFTP, [!DNL Azure Blob]) e [!DNL Oracle Eloqua] | `71471eba-b620-49e4-90fd-23f1fa0174d8` |
| [!DNL Oracle Responsys] | `51d675ce-e270-408d-91fc-22717bdf2148` |
| [!DNL Salesforce Marketing Cloud] | `493b2bd6-26e4-4167-ab3b-5e910bba44f0` |

**Risposta**

In caso di esito positivo, la risposta restituisce l&#39;ID (`id`) del flusso di dati appena creato e un `etag`. Per attivare i tipi di pubblico ed esportare i file di dati, prendi nota di entrambi i valori in base alle tue esigenze nel passaggio successivo.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Attiva i dati nella nuova destinazione {#activate-data}

![Passaggio 5](../assets/api/batch-destination/step5.png) della panoramica dei passaggi di destinazione

Dopo aver creato tutte le connessioni e il flusso di dati, ora puoi attivare i dati del profilo nella piattaforma di destinazione. In questo passaggio, seleziona i tipi di pubblico e gli attributi di profilo da esportare nella destinazione.

È inoltre possibile determinare il formato di denominazione dei file esportati e gli attributi da utilizzare come [chiavi di deduplicazione](../ui/activate-batch-profile-destinations.md#mandatory-keys) o [attributi obbligatori](../ui/activate-batch-profile-destinations.md#mandatory-attributes). In questo passaggio puoi anche determinare la pianificazione per inviare dati alla destinazione.

Per attivare i tipi di pubblico nella nuova destinazione, devi eseguire un’operazione JSON PATCH, simile all’esempio di seguito. Puoi attivare più tipi di pubblico e attributi di profilo in una sola chiamata. Per ulteriori informazioni su JSON PATCH, consulta la [specifica RFC](https://tools.ietf.org/html/rfc6902).

**Formato API**

```http
PATCH /flows
```

**Richiesta**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'If-Match: "{ETAG}"' \
--data-raw '[
    {
        "op": "add",
        "path": "/transformations/0/params/segmentSelectors/selectors/-",
        "value": {
            "type": "PLATFORM_SEGMENT",
            "value": {
                "name": "Name of the audience that you are activating",
                "description": "Description of the audience that you are activating",
                "id": "{SEGMENT_ID}",
                "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                "exportMode": "DAILY_FULL_EXPORT",
                "schedule": {
                    "frequency": "ONCE",
                    "startDate": "2021-12-20",
                    "startTime": "17:00"
                } 
            }
        }
    },
{
        "op": "add",
        "path": "/transformations/0/params/segmentSelectors/selectors/-",
        "value": {
            "type": "PLATFORM_SEGMENT",
            "value": {
                "name": "Name of the audience that you are activating",
                "description": "Description of the audience that you are activating",
                "id": "{SEGMENT_ID}",
                "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                "exportMode": "DAILY_FULL_EXPORT",
                "schedule": {
                    "frequency": "ONCE",
                    "triggerType": "SCHEDULED",
                    "startDate": "2021-12-20",
                    "startTime": "17:00"
                },   
            }
        }
    },
{
        "op": "add",
        "path": "/transformations/0/params/profileSelectors/selectors/-",
        "value": {
            "type": "JSON_PATH",
            "value": {
                "path": "{PROFILE_ATTRIBUTE}"
            }
        }
    }
]
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `{DATAFLOW_ID}` | Nell’URL, utilizza l’ID del flusso di dati creato nel passaggio precedente. |
| `{ETAG}` | Ottieni `{ETAG}` dalla risposta nel passaggio precedente, [Crea un flusso di dati](#create-dataflow). Il formato della risposta nel passaggio precedente contiene virgolette di escape. Devi utilizzare i valori senza escape nell’intestazione della richiesta. Vedi l&#39;esempio seguente: <br> <ul><li>Esempio di risposta: `"etag":""7400453a-0000-1a00-0000-62b1c7a90000""`</li><li>Valore da utilizzare nella richiesta: `"etag": "7400453a-0000-1a00-0000-62b1c7a90000"`</li></ul> <br> Il valore etag viene aggiornato a ogni aggiornamento riuscito di un flusso di dati. |
| `{SEGMENT_ID}` | Specifica l’ID del pubblico da esportare in questa destinazione. Per recuperare gli ID del pubblico per i tipi di pubblico che desideri attivare, consulta [recuperare una definizione di pubblico](https://www.adobe.io/experience-platform-apis/references/segmentation/#operation/retrieveSegmentDefinitionById) nel riferimento API di Experience Platform. |
| `{PROFILE_ATTRIBUTE}` | Ad esempio, `"person.lastName"` |
| `op` | Chiamata di operazione utilizzata per definire l’azione necessaria per aggiornare il flusso di dati. Le operazioni includono: `add`, `replace` e `remove`. Per aggiungere un pubblico a un flusso di dati, utilizzare l&#39;operazione `add`. |
| `path` | Definisce la parte del flusso da aggiornare. Quando aggiungi un pubblico a un flusso di dati, utilizza il percorso specificato nell’esempio. |
| `value` | Il nuovo valore con cui desideri aggiornare il parametro. |
| `id` | Specifica l’ID del pubblico che stai aggiungendo al flusso di dati di destinazione. |
| `name` | *Facoltativo*. Specifica il nome del pubblico che stai aggiungendo al flusso di dati di destinazione. Tieni presente che questo campo non è obbligatorio e puoi aggiungere correttamente un pubblico al flusso di dati di destinazione senza specificarne il nome. |
| `filenameTemplate` | Questo campo determina il formato del nome file dei file esportati nella destinazione. <br> Sono disponibili le seguenti opzioni: <br> <ul><li>`%DESTINATION_NAME%`: obbligatorio. I file esportati contengono il nome della destinazione.</li><li>`%SEGMENT_ID%`: obbligatorio. I file esportati contengono l’ID del pubblico esportato.</li><li>`%SEGMENT_NAME%`: facoltativo. I file esportati contengono il nome del pubblico esportato.</li><li>`DATETIME(YYYYMMdd_HHmmss)` o `%TIMESTAMP%`: facoltativo. Seleziona una di queste due opzioni per includere l&#39;ora in cui vengono generati da Experience Platform.</li><li>`custom-text`: facoltativo. Sostituire questo segnaposto con qualsiasi testo personalizzato che si desidera aggiungere alla fine dei nomi dei file.</li></ul> <br> Per ulteriori informazioni sulla configurazione dei nomi di file, fare riferimento alla sezione [Configura nomi di file](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) nell&#39;esercitazione sull&#39;attivazione delle destinazioni batch. |
| `exportMode` | Obbligatorio Selezionare `"DAILY_FULL_EXPORT"` o `"FIRST_FULL_THEN_INCREMENTAL"`. Per ulteriori informazioni sulle due opzioni, fare riferimento a [esporta file completi](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) e [esporta file incrementali](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) nell&#39;esercitazione di attivazione delle destinazioni batch. |
| `startDate` | Seleziona la data in cui il pubblico deve iniziare a esportare i profili nella tua destinazione. |
| `frequency` | Obbligatorio <br> <ul><li>Per la modalità di esportazione `"DAILY_FULL_EXPORT"`, è possibile selezionare `ONCE` o `DAILY`.</li><li>Per la modalità di esportazione `"FIRST_FULL_THEN_INCREMENTAL"`, è possibile selezionare `"DAILY"`, `"EVERY_3_HOURS"`, `"EVERY_6_HOURS"`, `"EVERY_8_HOURS"`, `"EVERY_12_HOURS"`.</li></ul> |
| `triggerType` | Solo per *destinazioni batch*. Questo campo è obbligatorio solo quando si seleziona la modalità `"DAILY_FULL_EXPORT"` nel selettore `frequency`. <br> obbligatorio. <br> <ul><li>Selezionare `"AFTER_SEGMENT_EVAL"` per eseguire il processo di attivazione subito dopo il completamento del processo di segmentazione batch giornaliero di Platform. In questo modo, quando viene eseguito il processo di attivazione, i profili più aggiornati vengono esportati nella destinazione.</li><li>Selezionare `"SCHEDULED"` per eseguire il processo di attivazione a un orario fisso. In questo modo i dati del profilo di Experience Platform vengono esportati ogni giorno alla stessa ora, ma i profili esportati potrebbero non essere quelli più aggiornati, a seconda che il processo di segmentazione batch sia stato completato prima dell’avvio del processo di attivazione. Quando si seleziona questa opzione, è necessario aggiungere anche un `startTime` per indicare in quale momento in UTC devono essere eseguite le esportazioni giornaliere.</li></ul> |
| `endDate` | Solo per *destinazioni batch*. Questo campo è necessario solo quando si aggiunge un pubblico a un flusso di dati in destinazioni di esportazione di file batch come Amazon S3, SFTP o Azure Blob. <br> Non applicabile quando si selezionano `"exportMode":"DAILY_FULL_EXPORT"` e `"frequency":"ONCE"`. <br> Imposta la data in cui i membri del pubblico cessano di essere esportati nella destinazione. |
| `startTime` | Solo per *destinazioni batch*. Questo campo è necessario solo quando si aggiunge un pubblico a un flusso di dati in destinazioni di esportazione di file batch come Amazon S3, SFTP o Azure Blob. <br> obbligatorio. Seleziona il momento in cui generare ed esportare nella destinazione i file contenenti i membri del pubblico. |

{style="table-layout:auto"}

>[!TIP]
>
> Consulta [Aggiornare i componenti di un pubblico in un flusso di dati](/help/destinations/api/update-destination-dataflows.md#update-segment) per scoprire come aggiornare vari componenti (modello di nome file, tempo di esportazione e così via) dei tipi di pubblico esportati.

**Risposta**

Cerca una risposta 202 Accepted (Accettata). Nessun corpo di risposta restituito. Per verificare che la richiesta sia corretta, vedere il passaggio successivo, [Convalidare il flusso di dati](#validate-dataflow).

## Convalidare il flusso di dati {#validate-dataflow}

![Passaggio 6 della panoramica dei passaggi di destinazione](../assets/api/batch-destination/step6.png)

Come ultimo passaggio dell’esercitazione, verifica che i tipi di pubblico e gli attributi del profilo siano stati effettivamente mappati correttamente al flusso di dati.

Per convalidarlo, esegui la seguente richiesta GET:

**Formato API**

```http
GET /flows
```

**Richiesta**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`: utilizza il flusso di dati del passaggio precedente.
* `{ETAG}`: utilizzare l&#39;etag del passaggio precedente.

**Risposta**

La risposta restituita deve includere nel parametro `transformations` i tipi di pubblico e gli attributi di profilo inviati nel passaggio precedente. Un parametro `transformations` di esempio nella risposta potrebbe essere simile al seguente:

```json
"transformations":[
   {
      "name":"GeneralTransform",
      "params":{
         "profileSelectors":{
            "selectors":[
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"homeAddress.countryCode",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"homeAddress.countryCode",
                        "destination":"homeAddress.countryCode",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"homeAddress.countryCode",
                        "destinationXdmPath":"homeAddress.countryCode"
                     }
                  }
               },
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"person.name.firstName",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"person.name.firstName",
                        "destination":"person.name.firstName",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"person.name.firstName",
                        "destinationXdmPath":"person.name.firstName"
                     }
                  }
               },
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"person.name.lastName",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"person.name.lastName",
                        "destination":"person.name.lastName",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"person.name.lastName",
                        "destinationXdmPath":"person.name.lastName"
                     }
                  }
               },
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"personalEmail.address",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"personalEmail.address",
                        "destination":"personalEmail.address",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"personalEmail.address",
                        "destinationXdmPath":"personalEmail.address"
                     }
                  }
               },
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"segmentMembership.status",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"segmentMembership.status",
                        "destination":"segmentMembership.status",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"segmentMembership.status",
                        "destinationXdmPath":"segmentMembership.status"
                     }
                  }
               }
            ],
            "mandatoryFields":[
               "person.name.firstName",
               "person.name.lastName"
            ],
            "primaryFields":[
               {
                  "fieldType":"ATTRIBUTE",
                  "attributePath":"personalEmail.address"
               }
            ]
         },
         "segmentSelectors":{
            "selectors":[
               {
                  "type":"PLATFORM_SEGMENT",
                  "value":{
                     "id":"9f7d37fd-7039-4454-94ef-2b0cd6c3206a",
                     "name":"Interested in Mountain Biking",
                     "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                     "exportMode":"DAILY_FULL_EXPORT",
                     "schedule":{
                        "frequency":"ONCE",
                        "startDate":"2021-12-20",
                        "startTime":"17:00"
                     },
                     "createTime":"1640016962",
                     "updateTime":"1642534355"
                  }
               },
               {
                  "type":"PLATFORM_SEGMENT",
                  "value":{
                     "id":"25768be6-ebd5-45cc-8913-12fb3f348613",
                     "name":"Loyalty Segment",
                     "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                     "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                     "schedule":{
                        "frequency":"EVERY_6_HOURS",
                        "startDate":"2021-12-22",
                        "endDate":"2021-12-31",
                        "startTime":"17:00"
                     },
                     "createTime":"1640016962",
                     "updateTime":"1642534355"
                  }
               }
            ]
         }
      }
   }
]
```

## Gestione degli errori API {#api-error-handling}

Gli endpoint API in questa esercitazione seguono i principi generali dei messaggi di errore API di Experience Platform. Per ulteriori informazioni sull&#39;interpretazione delle risposte di errore, consultare [codici di stato API](/help/landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](/help/landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai connesso Platform a una delle destinazioni di e-mail marketing basate su file preferite e hai impostato un flusso di dati nella rispettiva destinazione per esportare i file di dati. I dati in uscita possono ora essere utilizzati nella destinazione per campagne e-mail, pubblicità mirata e molti altri casi d’uso. Per ulteriori dettagli, vedi le pagine seguenti, ad esempio come modificare i flussi di dati esistenti utilizzando l’API del servizio Flusso:

* [Panoramica sulle destinazioni](../home.md)
* [Panoramica del catalogo delle destinazioni](../catalog/overview.md)
* [Aggiornare i flussi di dati di destinazione utilizzando l’API del servizio Flusso](../api/update-destination-dataflows.md)
