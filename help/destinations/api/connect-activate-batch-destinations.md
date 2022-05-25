---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Connettersi a destinazioni batch e attivare i dati utilizzando l’API del servizio di flusso
description: Istruzioni dettagliate per utilizzare l’API del servizio Flusso per creare un archivio cloud batch o una destinazione di marketing via e-mail in Experience Platform e attivare i dati
topic-legacy: tutorial
type: Tutorial
exl-id: 41fd295d-7cda-4ab1-a65e-b47e6c485562
source-git-commit: 95dd6982eeecf6b13b6c8a6621b5e6563c25ae26
workflow-type: tm+mt
source-wordcount: '3334'
ht-degree: 2%

---

# Connettersi a destinazioni batch e attivare i dati utilizzando l’API del servizio di flusso

>[!IMPORTANT]
> 
>Per connettersi a una destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions).
>
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions).
>
>Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Questa esercitazione illustra come utilizzare l’API del servizio di flusso per creare un batch [archiviazione cloud](../catalog/cloud-storage/overview.md) o [destinazione di e-mail marketing](../catalog/email-marketing/overview.md), crea un flusso di dati per la destinazione appena creata ed esporta i dati per la destinazione appena creata tramite file CSV.

Questa esercitazione utilizza la funzione [!DNL Adobe Campaign] in tutti gli esempi, ma i passaggi sono identici per tutte le destinazioni di archiviazione cloud batch e marketing via e-mail.

![Panoramica : i passaggi per creare una destinazione e attivare i segmenti](../assets/api/email-marketing/overview.png)

Se preferisci utilizzare l’interfaccia utente di Platform per connettersi a una destinazione e attivare i dati, consulta la [Collegare una destinazione](../ui/connect-destination.md) e [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../ui/activate-batch-profile-destinations.md) esercitazioni.

## Introduzione {#get-started}

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
* [[!DNL Segmentation Service]](../../segmentation/api/overview.md): [!DNL Adobe Experience Platform Segmentation Service] consente di generare segmenti e generare tipi di pubblico in [!DNL Adobe Experience Platform] dal [!DNL Real-time Customer Profile] dati.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per attivare i dati nelle destinazioni batch in Platform.

### Raccogli credenziali richieste {#gather-required-credentials}

Per completare i passaggi descritti in questa esercitazione, devi disporre delle seguenti credenziali, a seconda del tipo di destinazione a cui stai connettendo e attivando i segmenti.

* Per [!DNL Amazon S3] connessioni: `accessId`, `secretKey`
* Per [!DNL Amazon S3] collegamenti a [!DNL Adobe Campaign]: `accessId`, `secretKey`
* Per le connessioni SFTP: `domain`, `port`, `username`, `password` o `sshKey` (a seconda del metodo di connessione alla posizione FTP)
* Per [!DNL Azure Blob] connessioni: `connectionString`

>[!NOTE]
>
>Le credenziali `accessId`, `secretKey` per [!DNL Amazon S3] collegamenti e `accessId`, `secretKey` per [!DNL Amazon S3] collegamenti a [!DNL Adobe Campaign] sono identici.

### Lettura di chiamate API di esempio {#reading-sample-api-calls}

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori delle intestazioni richieste e facoltative {#gather-values-headers}

Per effettuare chiamate a [!DNL Platform] API, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Risorse in [!DNL Experience Platform] possono essere isolate in sandbox virtuali specifiche. Nelle richieste a [!DNL Platform] API, puoi specificare il nome e l’ID della sandbox in cui avrà luogo l’operazione. Si tratta di parametri facoltativi.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Experience Platform], vedi [documentazione panoramica su sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* Content-Type: `application/json`

### Documentazione di riferimento API {#api-reference-documentation}

Questa esercitazione contiene la documentazione di riferimento associata a tutte le operazioni API. Fai riferimento a [Documentazione API del servizio di flusso sull’Adobe I/O](https://www.adobe.io/experience-platform-apis/references/flow-service/). È consigliabile utilizzare questa esercitazione e la documentazione di riferimento API in parallelo.

## Ottieni l’elenco delle destinazioni disponibili {#get-the-list-of-available-destinations}

![Passaggio 1: panoramica dei passaggi di destinazione](../assets/api/batch-destination/step1.png)

Come primo passo, devi decidere a quale destinazione attivare i dati. Per iniziare, esegui una chiamata per richiedere un elenco di destinazioni disponibili a cui puoi collegare e attivare i segmenti. Esegui la seguente richiesta di GET al `connectionSpecs` per restituire un elenco di destinazioni disponibili:

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

Una risposta corretta contiene un elenco delle destinazioni disponibili e dei relativi identificatori univoci (`id`). Memorizza il valore della destinazione che intendi utilizzare, come sarà necessario in ulteriori passaggi. Ad esempio, se desideri collegare e distribuire segmenti a [!DNL Adobe Campaign], cerca il seguente frammento nella risposta:

```json
{
    "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
  "name": "Adobe Campaign",
  ...
  ...
}
```

Per riferimento, la tabella seguente contiene gli ID delle specifiche di connessione per le destinazioni batch di uso comune:

| Destinazione | ID della specifica di connessione |
---------|----------|
| [!DNL Adobe Campaign] | `0b23e41a-cb4a-4321-a78f-3b654f5d7d97` |
| [!DNL Amazon S3] | `4890fc95-5a1f-4983-94bb-e060c08e3f81` |
| [!DNL Azure Blob] | `e258278b-a4cf-43ac-b158-4fa0ca0d948b` |
| [!DNL Oracle Eloqua] | `c1e44b6b-e7c8-404b-9031-58f0ef760604` |
| [!DNL Oracle Responsys] | `a5e28ddf-e265-426e-83a1-9d03a3a6822b` |
| [!DNL Salesforce Marketing Cloud] | `f599a5b3-60a7-4951-950a-cc4115c7ea27` |
| SFTP | `64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0` |

{style=&quot;table-layout:auto&quot;}

## Collegati al tuo [!DNL Experience Platform] dati {#connect-to-your-experience-platform-data}

![Passaggio 2: panoramica dei passaggi di destinazione](../assets/api/batch-destination/step2.png)

Successivamente, è necessario connettersi al [!DNL Experience Platform] in modo da esportare i dati del profilo e attivarli nella destinazione desiderata. Si tratta di due sottoregimi descritti di seguito.

1. Innanzitutto, devi eseguire una chiamata per autorizzare l’accesso ai tuoi dati in [!DNL Experience Platform], impostando una connessione di base.
2. Quindi, utilizzando l&#39;ID di connessione di base, esegui un&#39;altra chiamata in cui crei un *connessione sorgente*, che stabilisce la connessione al tuo [!DNL Experience Platform] dati.

### Autorizzare l’accesso ai dati in [!DNL Experience Platform]

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
| `name` | Specifica un nome per la connessione di base all&#39;Experience Platform [!DNL Profile Store]. |
| `description` | Facoltativamente, è possibile fornire una descrizione per la connessione di base. |
| `connectionSpec.id` | Utilizza l’ID delle specifiche di connessione per [Experience Platform Profile Store](/help/profile/home.md#profile-data-store) - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta contiene l&#39;identificatore univoco della connessione di base (`id`). Memorizza questo valore come necessario nel passaggio successivo per creare la connessione sorgente.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Collegati al tuo [!DNL Experience Platform] dati {#connect-to-platform-data}

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
            "name": "Connecting to Profile Store",
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
| `name` | Specifica un nome per la connessione di origine all&#39;Experience Platform [!DNL Profile Store]. |
| `description` | Facoltativamente, puoi fornire una descrizione per la connessione di origine. |
| `connectionSpec.id` | Utilizza l’ID delle specifiche di connessione per [Experience Platform Profile Store](/help/profile/home.md#profile-data-store) - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`. |
| `baseConnectionId` | Utilizza l&#39;ID di connessione di base ottenuto nel passaggio precedente. |
| `data.format` | `CSV` è attualmente l’unico formato supportato per l’esportazione di file. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) per la nuova connessione sorgente a [!DNL Profile Store]. Ciò conferma che la connessione al [!DNL Experience Platform] dati. Memorizza questo valore come richiesto in un passaggio successivo.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```

## Connetti a destinazione batch {#connect-to-batch-destination}

![Passaggi di destinazione: passaggio 3](../assets/api/batch-destination/step3.png)

In questo passaggio, stai configurando una connessione alla destinazione di archiviazione cloud batch o di marketing e-mail desiderata. Si tratta di due sottoregimi descritti di seguito.

1. Innanzitutto, devi eseguire una chiamata per autorizzare l’accesso alla piattaforma di destinazione, impostando una connessione di base.
2. Quindi, utilizzando l&#39;ID di connessione di base, effettuerai un&#39;altra chiamata in cui crei un *connessione di destinazione*, che specifica la posizione nell’account di archiviazione in cui verranno inviati i file di dati esportati, nonché il formato dei dati da esportare.

### Autorizzare l&#39;accesso alla destinazione batch {#authorize-access-to-batch-destination}

**Formato API**

```http
POST /connections
```

**Richiesta**

La richiesta seguente stabilisce una connessione di base a [!DNL Adobe Campaign] destinazioni. A seconda del percorso di archiviazione in cui si desidera esportare i file in ([!DNL Amazon S3], SFTP, [!DNL Azure Blob]), conserva le `auth` specificare ed eliminare gli altri.

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

Vedi gli esempi di richieste riportati di seguito per connetterti ad altre destinazioni di marketing e archiviazione di batch cloud supportate.

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

La richiesta seguente stabilisce una connessione di base a [!DNL Oracle Eloqua] destinazioni. A seconda del percorso di archiviazione in cui si desidera esportare i file, mantenere il `auth` specificare ed eliminare gli altri.

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

La richiesta seguente stabilisce una connessione di base a [!DNL Oracle Responsys] destinazioni. A seconda del percorso di archiviazione in cui si desidera esportare i file, mantenere il `auth` specificare ed eliminare gli altri.

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

La richiesta seguente stabilisce una connessione di base a [!DNL Salesforce Marketing Cloud] destinazioni. A seconda del percorso di archiviazione in cui si desidera esportare i file, mantenere il `auth` specificare ed eliminare gli altri.

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

+++ Esempio di richiesta per la connessione a SFTP con destinazioni password

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
| `name` | Specificare un nome per la connessione di base alla destinazione del batch. |
| `description` | Facoltativamente, è possibile fornire una descrizione per la connessione di base. |
| `connectionSpec.id` | Utilizza l&#39;ID delle specifiche di connessione per la destinazione batch desiderata. Hai ottenuto questo ID nel passaggio [Ottieni l’elenco delle destinazioni disponibili](#get-the-list-of-available-destinations). |
| `auth.specname` | Indica il formato di autenticazione per la destinazione. Per scoprire il specName della destinazione, esegui una [Chiamata GET all&#39;endpoint delle specifiche di connessione](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec), fornendo le specifiche di connessione della destinazione desiderata. Cerca il parametro `authSpec.name` nella risposta. <br> Ad esempio, per le destinazioni Adobe Campaign, puoi utilizzare uno qualsiasi dei `S3`, `SFTP with Password`oppure `SFTP with SSH Key`. |
| `params` | A seconda della destinazione di connessione, è necessario fornire diversi parametri di autenticazione richiesti. Per le connessioni Amazon S3, devi fornire il tuo ID di accesso e la chiave segreta al tuo percorso di archiviazione Amazon S3. <br> Per scoprire i parametri richiesti per la destinazione, esegui una [Chiamata GET all&#39;endpoint delle specifiche di connessione](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec), fornendo le specifiche di connessione della destinazione desiderata. Cerca il parametro `authSpec.spec.required` nella risposta. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta contiene l&#39;identificatore univoco della connessione di base (`id`). Memorizza questo valore come necessario nel passaggio successivo per creare una connessione di destinazione.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Specificare il percorso di archiviazione e il formato dei dati {#specify-storage-location-data-format}

[!DNL Adobe Experience Platform] esporta i dati per le destinazioni di marketing e archiviazione cloud in batch, sotto forma di [!DNL CSV] file. In questo passaggio, è possibile determinare il percorso nel percorso di archiviazione in cui verranno esportati i file.

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] divide automaticamente i file di esportazione a 5 milioni di record (righe) per file. Ogni riga rappresenta un profilo.
>
>I nomi dei file divisi vengono aggiunti con un numero che indica che il file fa parte di un’esportazione più grande, in quanto tale: `filename.csv`, `filename_2.csv`, `filename_3.csv`.

**Formato API**

```http
POST /targetConnections
```

**Richiesta**

La richiesta seguente stabilisce una connessione target a [!DNL Adobe Campaign] le destinazioni, per determinare dove verranno inviati i file esportati nel percorso di archiviazione. A seconda del percorso di archiviazione in cui si desidera esportare i file, mantenere il `params` specificare ed eliminare gli altri.

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

Vedi gli esempi di richieste riportati di seguito per impostare un percorso di archiviazione per altre destinazioni di marketing e di archiviazione di batch cloud supportate.

+++ Esempio di richiesta per impostare un percorso di archiviazione per [!DNL Amazon S3] destinazioni

La richiesta seguente stabilisce una connessione target a [!DNL Amazon S3] le destinazioni, per determinare dove verranno inviati i file esportati nel percorso di archiviazione.

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
        "mode": "Cloud Storage",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
}'
```

+++

+++ Esempio di richiesta per impostare un percorso di archiviazione per [!DNL Azure Blob] destinazioni

La richiesta seguente stabilisce una connessione target a [!DNL Azure Blob] le destinazioni, per determinare dove verranno inviati i file esportati nel percorso di archiviazione.

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
        "mode": "Cloud Storage",
        "container": "{CONTAINER}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
}'
```

+++

+++ Esempio di richiesta per impostare un percorso di archiviazione per [!DNL Oracle Eloqua] destinazioni

La richiesta seguente stabilisce una connessione target a [!DNL Oracle Eloqua] le destinazioni, per determinare dove verranno inviati i file esportati nel percorso di archiviazione. A seconda del percorso di archiviazione in cui si desidera esportare i file, mantenere il `params` specificare ed eliminare gli altri.

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

+++ Esempio di richiesta per impostare un percorso di archiviazione per [!DNL Oracle Responsys] destinazioni

La richiesta seguente stabilisce una connessione target a [!DNL Oracle Responsys] le destinazioni, per determinare dove verranno inviati i file esportati nel percorso di archiviazione. A seconda del percorso di archiviazione in cui si desidera esportare i file, mantenere il `params` specificare ed eliminare gli altri.

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

+++ Esempio di richiesta per impostare un percorso di archiviazione per [!DNL Salesforce Marketing Cloud] destinazioni

La richiesta seguente stabilisce una connessione target a [!DNL Salesforce Marketing Cloud] le destinazioni, per determinare dove verranno inviati i file esportati nel percorso di archiviazione. A seconda del percorso di archiviazione in cui si desidera esportare i file, mantenere il `params` specificare ed eliminare gli altri.

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

+++ Esempio di richiesta per impostare un percorso di archiviazione per le destinazioni SFTP

La richiesta seguente stabilisce una connessione di destinazione alle destinazioni SFTP, per determinare dove arriveranno i file esportati nella posizione di archiviazione.

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
        "mode": "Cloud Storage",
        "remotePath": "{REMOTE_PATH}",
    }
}'
```

+++


| Proprietà | Descrizione |
| --------- | ----------- |
| `name` | Specifica un nome per la connessione di destinazione alla destinazione del batch. |
| `description` | Facoltativamente, puoi fornire una descrizione per la connessione di destinazione. |
| `baseConnectionId` | Utilizza l&#39;ID della connessione di base creata nel passaggio precedente. |
| `connectionSpec.id` | Utilizza l&#39;ID delle specifiche di connessione per la destinazione batch desiderata. Hai ottenuto questo ID nel passaggio [Ottieni l’elenco delle destinazioni disponibili](#get-the-list-of-available-destinations). |
| `params` | A seconda della destinazione a cui ci si connette, è necessario fornire diversi parametri richiesti alla posizione di archiviazione. Per le connessioni Amazon S3, devi fornire il tuo ID di accesso e la chiave segreta al tuo percorso di archiviazione Amazon S3. <br> Per scoprire i parametri richiesti per la destinazione, esegui una [Chiamata GET all&#39;endpoint delle specifiche di connessione](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec), fornendo le specifiche di connessione della destinazione desiderata. Cerca il parametro `targetSpec.spec.required` nella risposta. |
| `params.mode` | A seconda della modalità supportata per la destinazione, è necessario fornire un valore diverso in questo caso. Per scoprire i parametri richiesti per la destinazione, esegui una [Chiamata GET all&#39;endpoint delle specifiche di connessione](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec), fornendo le specifiche di connessione della destinazione desiderata. Cerca il parametro `targetSpec.spec.properties.mode.enum` nella risposta e seleziona la modalità desiderata. |
| `params.bucketName` | Per le connessioni S3, specifica il nome del bucket in cui verranno esportati i file. |
| `params.path` | Per le connessioni S3, fornire il percorso file nel percorso di archiviazione in cui verranno esportati i file. |
| `params.format` | `CSV` è attualmente l’unico tipo di esportazione file supportato. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) per la nuova connessione di destinazione alla destinazione batch. Memorizza questo valore come richiesto nei passaggi successivi.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Creare un flusso di dati {#create-dataflow}

![Passaggi di destinazione: passaggio 4](../assets/api/batch-destination/step4.png)

Utilizzando le specifiche di flusso, la connessione sorgente e gli ID di connessione di destinazione ottenuti nei passaggi precedenti, ora puoi creare un flusso di dati tra le [!DNL Experience Platform] i dati e la destinazione in cui verranno esportati i file di dati. Considera questo passaggio come la costruzione della pipeline attraverso la quale i dati scorreranno successivamente tra [!DNL Experience Platform] e la destinazione desiderata.

Per creare un flusso di dati, esegui una richiesta POST come mostrato di seguito, fornendo al tempo stesso i valori indicati di seguito all’interno del payload.

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
   
        "name": "Activate segments to Adobe Campaign",
        "description": "This operation creates a dataflow which we will later use to activate segments to Adobe Campaign",
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
| `description` | Facoltativamente, puoi fornire una descrizione per il flusso di dati. |
| `flowSpec.Id` | Utilizza l&#39;ID delle specifiche di flusso per la destinazione batch a cui desideri connetterti. Per recuperare l’ID della specifica di flusso, esegui un’operazione di GET sul `flowspecs` come mostrato nella [documentazione di riferimento API per le specifiche di flusso](https://www.adobe.io/experience-platform-apis/references/flow-service/#operation/retrieveFlowSpec). Nella risposta , cerca `upsTo` e copia l&#39;ID corrispondente della destinazione batch a cui desideri connetterti. Ad esempio, per Adobe Campaign, cerca `upsToCampaign` e copia il `id` parametro . |
| `sourceConnectionIds` | Utilizza l’ID di connessione sorgente ottenuto nel passaggio [Connettersi ai dati di Experience Platform](#connect-to-your-experience-platform-data). |
| `targetConnectionIds` | Utilizza l’ID di connessione di destinazione ottenuto nel passaggio [Connetti a destinazione batch](#connect-to-batch-destination). |
| `transformations` | Nel passaggio successivo, popolerai questa sezione con i segmenti e gli attributi di profilo da attivare. |

Per riferimento, la tabella seguente contiene gli ID delle specifiche di flusso per le destinazioni batch di uso comune:

| Destinazione | ID delle specifiche di flusso |
---------|----------|
| Tutte le destinazioni di archiviazione cloud ([!DNL Amazon S3], SFTP, [!DNL Azure Blob]) e [!DNL Oracle Eloqua] | `71471eba-b620-49e4-90fd-23f1fa0174d8` |
| [!DNL Oracle Responsys] | `51d675ce-e270-408d-91fc-22717bdf2148` |
| [!DNL Salesforce Marketing Cloud] | `493b2bd6-26e4-4167-ab3b-5e910bba44f0` |

**Risposta**

Una risposta corretta restituisce l&#39;ID (`id`) del flusso di dati appena creato e un `etag`. Prendi nota di entrambi i valori secondo le tue esigenze nel passaggio successivo, per attivare segmenti ed esportare file di dati.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Attiva i dati nella nuova destinazione {#activate-data}

![Passaggi di destinazione: passaggio 5](../assets/api/batch-destination/step5.png)

Dopo aver creato tutte le connessioni e il flusso di dati, ora puoi attivare i dati del profilo sulla piattaforma di destinazione. In questo passaggio, seleziona quali segmenti e quali attributi di profilo esportare nella destinazione.

È inoltre possibile determinare il formato di denominazione dei file esportati e quali attributi devono essere utilizzati come [chiavi di deduplicazione](../ui/activate-batch-profile-destinations.md#mandatory-keys) o [attributi obbligatori](../ui/activate-batch-profile-destinations.md#mandatory-attributes). In questo passaggio, puoi anche determinare la pianificazione per l’invio di dati alla destinazione.

Per attivare i segmenti nella nuova destinazione, è necessario eseguire un’operazione JSON PATCH, simile all’esempio seguente. Puoi attivare più segmenti e attributi di profilo in una sola chiamata. Per ulteriori informazioni su JSON PATCH, consulta la sezione [Specifica RFC](https://tools.ietf.org/html/rfc6902).

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
                "name": "Name of the segment that you are activating",
                "description": "Description of the segment that you are activating",
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
                "name": "Name of the segment that you are activating",
                "description": "Description of the segment that you are activating",
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
| `{ETAG}` | Utilizza il tag ottenuto nel passaggio precedente. |
| `{SEGMENT_ID}` | Fornisci l’ID del segmento da esportare a questa destinazione. Per recuperare gli ID dei segmenti per i segmenti che desideri attivare, vedi [recuperare una definizione di segmento](https://www.adobe.io/experience-platform-apis/references/segmentation/#operation/retrieveSegmentDefinitionById) nel riferimento API di Experience Platform. |
| `{PROFILE_ATTRIBUTE}` | Ad esempio, `"person.lastName"` |
| `op` | La chiamata dell’operazione utilizzata per definire l’azione necessaria per aggiornare il flusso di dati. Le operazioni includono: `add`, `replace`e `remove`. Per aggiungere un segmento a un flusso di dati, utilizza il `add` funzionamento. |
| `path` | Definisce la parte del flusso da aggiornare. Quando aggiungi un segmento a un flusso di dati, utilizza il percorso specificato nell’esempio. |
| `value` | Il nuovo valore con cui si desidera aggiornare il parametro. |
| `id` | Specifica l’ID del segmento che stai aggiungendo al flusso di dati di destinazione. |
| `name` | *Facoltativo*. Specifica il nome del segmento che stai aggiungendo al flusso di dati di destinazione. Tieni presente che questo campo non è obbligatorio ed è possibile aggiungere correttamente un segmento al flusso di dati di destinazione senza specificarne il nome. |
| `filenameTemplate` | Questo campo determina il formato del nome file dei file esportati nella destinazione. <br> Sono disponibili le seguenti opzioni: <br> <ul><li>`%DESTINATION_NAME%`: Obbligatorio. I file esportati contengono il nome della destinazione.</li><li>`%SEGMENT_ID%`: Obbligatorio. I file esportati contengono l’ID del segmento esportato.</li><li>`%SEGMENT_NAME%`: Facoltativo. I file esportati contengono il nome del segmento esportato.</li><li>`DATETIME(YYYYMMdd_HHmmss)` o `%TIMESTAMP%`: Facoltativo. Selezionare una di queste due opzioni affinché i file includano l’ora in cui sono generati dall’Experience Platform.</li><li>`custom-text`: Facoltativo. Sostituire il segnaposto con il testo personalizzato che si desidera aggiungere alla fine dei nomi dei file.</li></ul> <br> Per ulteriori informazioni sulla configurazione dei nomi dei file, consulta [configurare i nomi dei file](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) nell’esercitazione sull’attivazione delle destinazioni batch. |
| `exportMode` | Obbligatorio. Seleziona `"DAILY_FULL_EXPORT"` (Mostra origine dati) o `"FIRST_FULL_THEN_INCREMENTAL"` (Blocca selezione). Per ulteriori informazioni sulle due opzioni, consulta [esportare file completi](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) e [esportare file incrementali](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) nell’esercitazione sull’attivazione delle destinazioni batch. |
| `startDate` | Seleziona la data in cui il segmento deve iniziare l’esportazione dei profili nella tua destinazione. |
| `frequency` | Obbligatorio. <br> <ul><li>Per `"DAILY_FULL_EXPORT"` modalità di esportazione, puoi selezionare `ONCE` o `DAILY`.</li><li>Per `"FIRST_FULL_THEN_INCREMENTAL"` modalità di esportazione, puoi selezionare `"DAILY"`, `"EVERY_3_HOURS"`, `"EVERY_6_HOURS"`, `"EVERY_8_HOURS"`, `"EVERY_12_HOURS"`.</li></ul> |
| `triggerType` | Per *destinazioni batch* solo. Questo campo è necessario solo quando si seleziona la `"DAILY_FULL_EXPORT"` nella modalità `frequency` selettore. <br> Obbligatorio. <br> <ul><li>Seleziona `"AFTER_SEGMENT_EVAL"` per eseguire il processo di attivazione immediatamente dopo il completamento del processo di segmentazione batch giornaliero di Platform. In questo modo, quando il processo di attivazione viene eseguito, i profili più aggiornati vengono esportati nella destinazione.</li><li>Seleziona `"SCHEDULED"` per far sì che il processo di attivazione venga eseguito a un orario fisso. In questo modo i dati del profilo di Experience Platform vengono esportati allo stesso tempo ogni giorno, ma i profili esportati potrebbero non essere i più aggiornati, a seconda che il processo di segmentazione del batch sia stato completato prima dell’avvio del processo di attivazione. Quando selezioni questa opzione, devi anche aggiungere una `startTime` per indicare l’ora in UTC in cui devono essere eseguite le esportazioni giornaliere.</li></ul> |
| `endDate` | Per *destinazioni batch* solo. Questo campo è necessario solo quando si aggiunge un segmento a un flusso di dati in destinazioni di esportazione di file batch come Amazon S3, SFTP o Azure Blob. <br> Non applicabile quando si seleziona `"exportMode":"DAILY_FULL_EXPORT"` e `"frequency":"ONCE"`. <br> Imposta la data in cui i membri del segmento smettono di essere esportati nella destinazione. |
| `startTime` | Per *destinazioni batch* solo. Questo campo è necessario solo quando si aggiunge un segmento a un flusso di dati in destinazioni di esportazione di file batch come Amazon S3, SFTP o Azure Blob. <br> Obbligatorio. Seleziona l’ora in cui i file contenenti i membri del segmento devono essere generati ed esportati nella destinazione. |

{style=&quot;table-layout:auto&quot;}

>[!TIP]
>
> Vedi [Aggiornare i componenti di un segmento in un flusso di dati](/help/destinations/api/update-destination-dataflows.md#update-segment) per scoprire come aggiornare vari componenti (modello di nome file, tempo di esportazione e così via) dei segmenti esportati.

**Risposta**

Cerca una risposta accettata da 202. Non viene restituito alcun corpo di risposta. Per verificare che la richiesta fosse corretta, vedi il passaggio successivo, [Convalida il flusso di dati](#validate-dataflow).

## Convalida il flusso di dati {#validate-dataflow}

![Passaggi di destinazione: passaggio 6](../assets/api/batch-destination/step6.png)

Come passaggio finale nell’esercitazione, dovresti verificare che i segmenti e gli attributi di profilo siano stati mappati correttamente nel flusso di dati.

Per convalidarlo, esegui la seguente richiesta di GET:

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

* `{DATAFLOW_ID}`: Utilizza il flusso di dati del passaggio precedente.
* `{ETAG}`: Utilizza il tag del passaggio precedente.

**Risposta**

La risposta restituita deve includere nel `transformations` i segmenti e gli attributi di profilo inviati nel passaggio precedente. Un campione `transformations` nella risposta potrebbe essere simile al seguente:

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

## Passaggi successivi

Seguendo questa esercitazione, hai collegato Platform a una delle tue destinazioni preferite per l’archiviazione cloud o il marketing via e-mail e hai impostato un flusso di dati sulla rispettiva destinazione per esportare i file di dati. I dati in uscita possono ora essere utilizzati nella destinazione per campagne e-mail, pubblicità mirata e molti altri casi d’uso. Per ulteriori dettagli, consulta le pagine seguenti, ad esempio come modificare i flussi di dati esistenti utilizzando l’API del servizio di flusso:

* [Panoramica sulle destinazioni](../home.md)
* [Panoramica del catalogo delle destinazioni](../catalog/overview.md)
* [Aggiornare i flussi di dati di destinazione utilizzando l’API del servizio di flusso](../api/update-destination-dataflows.md)
