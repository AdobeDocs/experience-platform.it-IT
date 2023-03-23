---
solution: Experience Platform
title: (Beta) Esporta i set di dati utilizzando l’API del servizio di flusso
description: Scopri come utilizzare l’API del servizio di flusso per esportare i set di dati per selezionare le destinazioni.
type: Tutorial
source-git-commit: d0de642eb6118e6597925c12c76917ffa98c3a5a
workflow-type: tm+mt
source-wordcount: '3347'
ht-degree: 4%

---

# (Beta) Esporta i set di dati utilizzando [!DNL Flow Service API]

>[!IMPORTANT]
>
>* La funzionalità di esportazione dei set di dati è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.
>* Questa funzionalità beta supporta l’esportazione di dati di prima generazione, come definito in Real-time Customer Data Platform [descrizione del prodotto](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).
>* Questa funzionalità è disponibile per i clienti che hanno acquistato il pacchetto Real-Time CDP Prime o Ultimate. Per ulteriori informazioni, contatta il tuo rappresentante Adobe.


Questo articolo spiega il flusso di lavoro necessario per utilizzare il [!DNL Flow Service API] da esportare [set di dati](/help/catalog/datasets/overview.md) da Adobe Experience Platform alla posizione di archiviazione cloud preferita, ad esempio [!DNL Amazon S3], posizioni SFTP o [!DNL Google Cloud Storage].

>[!TIP]
>
>Puoi inoltre utilizzare l’interfaccia utente di Experience Platform per esportare i set di dati. Leggi la sezione [esercitazione sull&#39;interfaccia utente per l&#39;esportazione di set di dati](/help/destinations/ui/export-datasets.md) per ulteriori informazioni.

## Destinazioni supportate {#supported-destinations}

Attualmente, puoi esportare i set di dati nelle destinazioni di archiviazione cloud evidenziate nella schermata ed elencate di seguito.

![Destinazioni che supportano le esportazioni di set di dati](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## Introduzione {#get-started}

![Panoramica : i passaggi per creare un set di dati di destinazione ed esportazione](../assets/api/export-datasets/export-datasets-api-workflow-get-started.png)

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Platform datasets]](/help/catalog/datasets/overview.md): Tutti i dati che vengono correttamente acquisiti in Adobe Experience Platform vengono memorizzati nella variabile [!DNL Data Lake] come set di dati. Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene uno schema (colonne) e dei campi (righe). I set di dati contengono anche metadati che descrivono vari aspetti dei dati memorizzati.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per esportare i set di dati nelle destinazioni di archiviazione cloud in Platform.

### Autorizzazioni necessarie {#permissions}

Per esportare i set di dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Visualizzare le destinazioni]**, **[!UICONTROL Attivare le destinazioni]** e **[!UICONTROL Gestire e attivare le destinazioni del set di dati]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per assicurarti di disporre delle autorizzazioni necessarie per esportare i set di dati e che la destinazione supporti l’esportazione dei set di dati, sfoglia il catalogo delle destinazioni. Se una destinazione ha un **[!UICONTROL Attiva]** o **[!UICONTROL Esportare i set di dati]** quindi disponi delle autorizzazioni appropriate.

### Lettura di chiamate API di esempio {#reading-sample-api-calls}

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori delle intestazioni richieste e facoltative {#gather-values-headers}

Per effettuare chiamate a [!DNL Platform] API, devi prima completare l’ [Experience Platform di esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

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

Questa esercitazione contiene la documentazione di riferimento associata a tutte le operazioni API. Fai riferimento a [[!DNL Flow Service] - Documentazione API sulle destinazioni sul sito web Adobe Developer](https://developer.adobe.com/experience-platform-apis/references/destinations/). È consigliabile utilizzare questa esercitazione e la documentazione di riferimento API in parallelo.

### Glossario {#glossary}

Per una descrizione dei termini che verranno utilizzati in questa esercitazione API, leggi la sezione [sezione glossario](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) della documentazione di riferimento API.

### Raccogli specifiche di connessione e specifiche di flusso per la destinazione desiderata {#gather-connection-spec-flow-spec}

Prima di avviare il flusso di lavoro per esportare un set di dati, identifica le specifiche di connessione e gli ID delle specifiche di flusso della destinazione in cui intendi esportare i set di dati. Utilizzare la tabella seguente per riferimento.


| Destinazione | Specifiche di connessione | Specifiche di flusso |
---------|----------|---------|
| [!DNL Amazon S3] | `4fce964d-3f37-408f-9778-e597338a21ee` | `269ba276-16fc-47db-92b0-c1049a3c131f` |
| [!DNL Azure Blob Storage] | `6d6b59bf-fb58-4107-9064-4d246c0e5bb2` | `95bd8965-fc8a-4119-b9c3-944c2c2df6d2` |
| [!DNL Azure Data Lake Gen 2(ADLS Gen2)] | `be2c3209-53bc-47e7-ab25-145db8b873e1` | `17be2013-2549-41ce-96e7-a70363bec293` |
| [!DNL Data Landing Zone(DLZ)] | `10440537-2a7b-4583-ac39-ed38d4b848e8` | `cd2fc47e-e838-4f38-a581-8fff2f99b63a` |
| [!DNL Google Cloud Storage] | `c5d93acb-ea8b-4b14-8f53-02138444ae99` | `585c15c4-6cbf-4126-8f87-e26bff78b657` |
| SFTP | `36965a81-b1c6-401b-99f8-22508f1e6a26` | `354d6aad-4754-46e4-a576-1b384561c440` |

{style="table-layout:auto"}

Sono necessari questi ID per creare diversi [!DNL Flow Service] entità. È inoltre necessario fare riferimento a parti del [!DNL Connection Spec] per impostare alcune entità in modo da poter recuperare il [!DNL Connection Spec] da [!DNL Flow Service APIs]. Vedi gli esempi seguenti di recupero delle specifiche di connessione per tutte le destinazioni nella tabella:

>[!BEGINTABS]

>[!TAB Amazon S3]

**Richiesta**

+++Recupera [!DNL connection spec] per [!DNL Amazon S3]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/4fce964d-3f37-408f-9778-e597338a21ee' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Risposta**

+++[!DNL Amazon S3] - Specifiche di connessione

```json
{
    "items": [
        {
            "id": "4fce964d-3f37-408f-9778-e597338a21ee",
            "name": "Amazon S3",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Archiviazione BLOB di Azure]

**Richiesta**

+++Recupera [!DNL connection spec] per [!DNL Azure Blob Storage]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/6d6b59bf-fb58-4107-9064-4d246c0e5bb2' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Risposta**

+++[!DNL Azure Blob Storage] - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
            "name": "Azure Blob Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Azure Data Lake Gen 2 (ADLS Gen2)]

**Richiesta**

+++Recupera [!DNL connection spec] per [!DNL Azure Data Lake Gen 2(ADLS Gen2])

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/be2c3209-53bc-47e7-ab25-145db8b873e1' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Risposta**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "be2c3209-53bc-47e7-ab25-145db8b873e1",
            "name": "Azure Data Lake Gen2",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Data Landing Zone (DLZ)]

**Richiesta**

+++Recupera [!DNL connection spec] per [!DNL Data Landing Zone(DLZ)]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/10440537-2a7b-4583-ac39-ed38d4b848e8' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Risposta**

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "10440537-2a7b-4583-ac39-ed38d4b848e8",
            "name": "Data Landing Zone",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Google Cloud Storage]

**Richiesta**

+++Recupera [!DNL connection spec] per [!DNL Google Cloud Storage]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/c5d93acb-ea8b-4b14-8f53-02138444ae99' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Risposta**

+++[!DNL Google Cloud Storage] - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99",
            "name": "Google Cloud Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB SFTP]

**Richiesta**

+++Recupera [!DNL connection spec] per SFTP

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/36965a81-b1c6-401b-99f8-22508f1e6a26' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Risposta**

+++SFTP - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
            "name": "SFTP",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!ENDTABS]

Per impostare un flusso di dati di un set di dati su una destinazione di archiviazione cloud, effettua le seguenti operazioni. Per alcuni passaggi, le richieste e le risposte variano tra le varie destinazioni di archiviazione cloud. In questi casi, utilizza le schede nella pagina per recuperare le richieste e le risposte specifiche della destinazione in cui desideri collegare ed esportare i set di dati. Assicurati di utilizzare la [!DNL connection spec] e [!DNL flow spec] per la destinazione che si sta configurando.

## Recupera un elenco di set di dati {#retrieve-list-of-available-datasets}

![Diagramma che mostra il passaggio 1 nel flusso di lavoro dei set di dati di esportazione](../assets/api/export-datasets/export-datasets-api-workflow-retrieve-datasets.png)

Per recuperare un elenco di set di dati idonei all’attivazione, inizia effettuando una chiamata API all’endpoint seguente.

>[!BEGINSHADEBOX]

**Richiesta**

+++Recupera set di dati idonei - Richiesta

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/23598e46-f560-407b-88d5-ea6207e49db0/configs?outputType=activationDatasets&outputField=datasets&start=0&limit=20&properties=name,state' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

Tieni presente che per recuperare i set di dati idonei, [!DNL connection spec] L’ID utilizzato nell’URL della richiesta deve essere l’ID della specifica di connessione sorgente del lago di dati, `23598e46-f560-407b-88d5-ea6207e49db0`e i due parametri di query `outputField=datasets` e `outputType=activationDatasets` deve essere specificato. Tutti gli altri parametri di query sono quelli standard supportati dalla [API del servizio catalogo](https://developer.adobe.com/experience-platform-apis/references/catalog/).

+++

**Risposta**

+++Recupera set di dati - Risposta

```json
{
    "items": [
        {
            "id": "5ef3e324052581191aa6a466",
            "name": "AAM Authenticated Profiles Meta Data",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        },
        {
            "id": "5ef3e3259ad2a1191ab7dd7d",
            "name": "AAM Devices Data",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        },
        {
            "id": "5ef3e325582424191b1beb42",
            "name": "AAM Devices Profile Meta Data",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        },
        {
            "id": "5ef3e328582424191b1beb44",
            "name": "AAM Realtime",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        },
        {
            "id": "5ef3e328fe742a191b2b3ea5",
            "name": "AAM Realtime Profile Updates",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        }
    ],
    "pageInfo": {
        "start": 0,
        "end": 4,
        "total": 149,
        "hasNext": true
    }
}
```

+++

>[!ENDSHADEBOX]

Una risposta corretta contiene un elenco di set di dati idonei per l’attivazione. Questi set di dati possono essere utilizzati per costruire la connessione di origine nel passaggio successivo.

Per informazioni sui vari parametri di risposta per ciascun set di dati restituito, consulta la [Documentazione per gli sviluppatori API dei set di dati](https://developer.adobe.com/experience-platform-apis/references/catalog/#tag/Datasets/operation/listDatasets).

## Creazione di una connessione sorgente {#create-source-connection}

![Diagramma che mostra il passaggio 2 nel flusso di lavoro dei set di dati di esportazione](../assets/api/export-datasets/export-datasets-api-workflow-create-source-connection.png)

Dopo aver recuperato l’elenco dei set di dati da esportare, puoi creare una connessione sorgente utilizzando gli ID dei set di dati.

>[!BEGINSHADEBOX]

**Richiesta**

+++Crea connessione sorgente - Richiesta

Osserva le righe evidenziate con commenti in linea nell’esempio di richiesta, che forniscono informazioni aggiuntive. Rimuovi i commenti in linea nella richiesta quando copia-incolla la richiesta nel terminale di scelta.

```shell {line-numbers="true" start-line="1" highlight="12,16"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
  "name": "Connecting to Data Lake",
  "description": "Data Lake source connection to export datasets",
  "connectionSpec": {
    "id": "23598e46-f560-407b-88d5-ea6207e49db0", // this connection spec ID is always the same for Source Connections
    "version": "1.0"
  },
  "params": {
    "datasets": [ // datasets to activate
      {
        "dataSetId": "5ef3e3259ad2a1191ab7dd7d",
        "name": "AAM Devices Data"
      }
    ]
  }
}'
```

+++



**Risposta**

+++Crea connessione sorgente - Risposta

```json
{
    "id": "900df191-b983-45cd-90d5-4c7a0326d650",
    "etag": "\"0500ebe1-0000-0200-0000-63e28d060000\""
}
```

+++

>[!ENDSHADEBOX]

Una risposta corretta restituisce l&#39;ID (`id`) della nuova connessione sorgente creata e `etag`. Annotare l’ID della connessione sorgente come sarà necessario in seguito durante la creazione del flusso di dati.

Ricorda inoltre che:

* La connessione di origine creata in questo passaggio deve essere collegata a un flusso di dati per attivare i relativi set di dati in una destinazione. Consulta la sezione [creare un flusso di dati](#create-dataflow) per informazioni su come collegare una connessione sorgente a un flusso di dati.
* Gli ID set di dati di una connessione di origine non possono essere modificati dopo la creazione. Se devi aggiungere o rimuovere set di dati da una connessione di origine, devi creare una nuova connessione di origine e collegare l’ID della nuova connessione di origine al flusso di dati.

## Creare una connessione di base (target) {#create-base-connection}

![Diagramma che mostra il passaggio 3 nel flusso di lavoro dei set di dati di esportazione](../assets/api/export-datasets/export-datasets-api-workflow-create-base-connection.png)

Una connessione di base memorizza le credenziali in modo sicuro nella destinazione. A seconda del tipo di destinazione, le credenziali necessarie per l’autenticazione rispetto a tale destinazione possono variare. Per trovare questi parametri di autenticazione, recupera prima [!DNL connection spec] per la destinazione desiderata come descritto nella sezione [Raccogli specifiche di connessione e specifiche di flusso](#gather-connection-spec-flow-spec) e poi guarda il `authSpec` della risposta. Fai riferimento alle schede seguenti per `authSpec` di tutte le destinazioni supportate.

>[!BEGINTABS]

>[!TAB Amazon S3]

+++[!DNL Amazon S3] - [!DNL Connection spec] mostrare [!DNL auth spec]

Osserva la riga evidenziata con i commenti in linea nel [!DNL connection spec] di seguito, che forniscono informazioni aggiuntive su dove trovare i parametri di autenticazione nel [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "4fce964d-3f37-408f-9778-e597338a21ee",
            "name": "Amazon S3",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "Access Key",
                    "type": "KeyBased",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "Defines auth params required for connecting to amazon-s3",
                        "type": "object",
                        "properties": {
                            "s3AccessKey": {
                                "description": "Access key id",
                                "type": "string",
                                "pattern": "^[A-Z2-7]{20}$"
                            },
                            "s3SecretKey": {
                                "description": "Secret access key for the user account",
                                "type": "string",
                                "format": "password",
                                "pattern": "^[A-Za-z0-9\/\\+]{40}$"
                            }
                        },
                        "required": [
                            "s3SecretKey",
                            "s3AccessKey"
                        ]
                    }
                }
            ],
//...
```

+++

>[!TAB Archiviazione BLOB di Azure]

+++[!DNL Azure Blob Storage] - [!DNL Connection spec] mostrare [!DNL auth spec]

Osserva la riga evidenziata con i commenti in linea nel [!DNL connection spec] di seguito, che forniscono informazioni aggiuntive su dove trovare i parametri di autenticazione nel [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
            "name": "Azure Blob Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "ConnectionString",
                    "type": "ConnectionString",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "Connection String for Azure Blob based destinations",
                        "type": "object",
                        "properties": {
                            "connectionString": {
                                "description": "connection string for login",
                                "type": "string",
                                "format": "password"
                            }
                        },
                        "required": [
                            "connectionString"
                        ]
                    }
                }
            ],
//...
```

+++


>[!TAB Azure Data Lake Gen 2 (ADLS Gen2)]

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec] mostrare [!DNL auth spec]

Osserva la riga evidenziata con i commenti in linea nel [!DNL connection spec] di seguito, che forniscono informazioni aggiuntive su dove trovare i parametri di autenticazione nel [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "be2c3209-53bc-47e7-ab25-145db8b873e1",
            "name": "Azure Data Lake Gen2",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "Azure Service Principal Auth",
                    "type": "AzureServicePrincipal",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to adlsgen2 using service principal",
                        "type": "object",
                        "properties": {
                            "url": {
                                "description": "Endpoint for Azure Data Lake Storage Gen2.",
                                "type": "string"
                            },
                            "servicePrincipalId": {
                                "description": "Service Principal Id to connect to ADLSGen2.",
                                "type": "string"
                            },
                            "servicePrincipalKey": {
                                "description": "Service Principal Key to connect to ADLSGen2.",
                                "type": "string",
                                "format": "password"
                            },
                            "tenant": {
                                "description": "Tenant information(domain name or tenant ID).",
                                "type": "string"
                            }
                        },
                        "required": [
                            "servicePrincipalKey",
                            "url",
                            "tenant",
                            "servicePrincipalId"
                        ]
                    }
                }
            ],
//...
```

+++


>[!TAB Data Landing Zone (DLZ)]

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec] mostrare [!DNL auth spec]

>[!NOTE]
>
>La destinazione Data Landing Zone non richiede un [!DNL auth spec].

```json
{
    "items": [
        {
            "id": "10440537-2a7b-4583-ac39-ed38d4b848e8",
            "name": "Data Landing Zone",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [],
//...
```

+++

>[!TAB Google Cloud Storage]

+++[!DNL Google Cloud Storage] - [!DNL Connection spec] mostrare [!DNL auth spec]

Osserva la riga evidenziata con i commenti in linea nel [!DNL connection spec] di seguito, che forniscono informazioni aggiuntive su dove trovare i parametri di autenticazione nel [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99",
            "name": "Google Cloud Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "Google Cloud Storage authentication credentials",
                    "type": "GoogleCloudStorageAuth",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to google cloud storage connector.",
                        "type": "object",
                        "properties": {
                            "accessKeyId": {
                                "description": "Access Key Id for the user account",
                                "type": "string"
                            },
                            "secretAccessKey": {
                                "description": "Secret Access Key for the user account",
                                "type": "string",
                                "format": "password"
                            }
                        },
                        "required": [
                            "accessKeyId",
                            "secretAccessKey"
                        ]
                    }
                }
            ],
//...
```

+++

>[!TAB SFTP]

+++SFTP - [!DNL Connection spec] mostrare [!DNL auth spec]

>[!NOTE]
>
>La destinazione SFTP contiene due elementi separati nel [!DNL auth spec], in quanto supporta sia l’autenticazione tramite password che l’autenticazione tramite chiave SSH.

Osserva la riga evidenziata con i commenti in linea nel [!DNL connection spec] di seguito, che forniscono informazioni aggiuntive su dove trovare i parametri di autenticazione nel [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
            "name": "SFTP",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "SFTP with Password",
                    "type": "SFTP",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to sftp locations with a password",
                        "type": "object",
                        "properties": {
                            "domain": {
                                "description": "Domain of server",
                                "type": "string"
                            },
                            "username": {
                                "description": "Username",
                                "type": "string"
                            },
                            "password": {
                                "description": "Password",
                                "type": "string",
                                "format": "password"
                            }
                        },
                        "required": [
                            "password",
                            "domain",
                            "username"
                        ]
                    }
                },
                {
                    "name": "SFTP with SSH Key",
                    "type": "SFTP",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to sftp locations using SSH Key",
                        "type": "object",
                        "properties": {
                            "domain": {
                                "description": "Domain of server",
                                "type": "string"
                            },
                            "username": {
                                "description": "Username",
                                "type": "string"
                            },
                            "sshKey": {
                                "description": "Base64 string of the private SSH key",
                                "type": "string",
                                "format": "password",
                                "contentEncoding": "base64",
                                "uiAttributes": {
                                    "tooltip": {
                                        "id": "platform_destinations_connect_sftp_ssh",
                                        "fallbackUrl": "http://www.adobe.com/go/destinations-sftp-connection-parameters-en "
                                    }
                                }
                            }
                        },
                        "required": [
                            "sshKey",
                            "domain",
                            "username"
                        ]
                    }
                }
            ],
//...
```

+++

>[!ENDTABS]

Utilizzo delle proprietà specificate nelle specifiche di autenticazione (ad es. `authSpec` dalla risposta) è possibile creare una connessione di base con le credenziali richieste, specifiche per ogni tipo di destinazione, come mostrato negli esempi seguenti:

>[!BEGINTABS]

>[!TAB Amazon S3]

**Richiesta**

+++[!DNL Amazon S3] - Richiesta di connessione di base

>[!TIP]
>
>Per informazioni su come ottenere le credenziali di autenticazione richieste, consulta la [autenticare a destinazione](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) della pagina della documentazione di destinazione di Amazon S3.

Osserva le righe evidenziate con commenti in linea nell’esempio di richiesta, che forniscono informazioni aggiuntive. Rimuovi i commenti in linea nella richiesta quando copia-incolla la richiesta nel terminale di scelta.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Amazon S3 Base Connection",
  "auth": {
    "specName": "Access Key",
    "params": {
      "s3SecretKey": "<Add secret key>",
      "s3AccessKey": "<Add access key>"
    }
  },
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee", // Amazon S3 connection spec
    "version": "1.0"
  }
}'
```

+++

**Risposta**

+++[!DNL Amazon S3] Risposta di connessione di base

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Archiviazione BLOB di Azure]

**Richiesta**

+++[!DNL Azure Blob Storage] - Richiesta di connessione di base

>[!TIP]
>
>Per informazioni su come ottenere le credenziali di autenticazione richieste, consulta la [autenticare a destinazione](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) sezione della pagina della documentazione della destinazione Azure Blob Storage.

Osserva le righe evidenziate con commenti in linea nell’esempio di richiesta, che forniscono informazioni aggiuntive. Rimuovi i commenti in linea nella richiesta quando copia-incolla la richiesta nel terminale di scelta.

```shell {line-numbers="true" start-line="1" highlight="16"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Azure Blob Storage Base Connection",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "connectionString": "<Add Azure Blob connection string>"
    }
  },
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2", // Azure Blob Storage connection spec
    "version": "1.0"
  }
}'
```

+++

**Risposta**

+++[!DNL Azure Blob Storage] - Risposta di connessione di base

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen 2 (ADLS Gen2)]

**Richiesta**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - Richiesta di connessione di base

>[!TIP]
>
>Per informazioni su come ottenere le credenziali di autenticazione richieste, consulta la [autenticare a destinazione](/help/destinations/catalog/cloud-storage/adls-gen2.md#authenticate) sezione della pagina della documentazione di destinazione del Azure Data Lake Gen 2 (ADLS Gen2).

Osserva le righe evidenziate con commenti in linea nell’esempio di richiesta, che forniscono informazioni aggiuntive. Rimuovi i commenti in linea nella richiesta quando copia-incolla la richiesta nel terminale di scelta.

```shell {line-numbers="true" start-line="1" highlight="20"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Azure Data Lake Gen 2(ADLS Gen2) Base Connection",
  "auth": {
    "specName": "Azure Service Principal Auth",
    "params": {
      "servicePrincipalKey": "<Add servicePrincipalKey>",
      "url": "<Add url>",
      "tenant": "<Add tenant>",
      "servicePrincipalId": "<Add servicePrincipalId>"
    }
  },
  "connectionSpec": {
    "id": "be2c3209-53bc-47e7-ab25-145db8b873e1", // Azure Data Lake Gen 2(ADLS Gen2) connection spec
    "version": "1.0"
  }
}'
```

+++

**Risposta**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - Risposta di connessione di base

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Data Landing Zone (DLZ)]

**Richiesta**

+++[!DNL Data Landing Zone(DLZ)] - Richiesta di connessione di base

>[!TIP]
>
>Non sono necessarie credenziali di autenticazione per la destinazione della zona di destinazione dei dati. Per ulteriori informazioni, consulta la [autenticare a destinazione](/help/destinations/catalog/cloud-storage/data-landing-zone.md#authenticate) della pagina di documentazione sulla destinazione della zona di destinazione dei dati .

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Data Landing Zone(DLZ) Base Connection"
}'
```

+++

**Risposta**

+++[!DNL Data Landing Zone] - Risposta di connessione di base

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Google Cloud Storage]

**Richiesta**

+++[!DNL Google Cloud Storage] - Richiesta di connessione di base

>[!TIP]
>
>Per informazioni su come ottenere le credenziali di autenticazione richieste, consulta la [autenticare a destinazione](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#authenticate) della pagina della documentazione relativa alla destinazione di Google Cloud Storage.

Osserva le righe evidenziate con commenti in linea nell’esempio di richiesta, che forniscono informazioni aggiuntive. Rimuovi i commenti in linea nella richiesta quando copia-incolla la richiesta nel terminale di scelta.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Google Cloud Storage Base Connection",
  "auth": {
    "specName": "Google Cloud Storage authentication credentials",
    "params": {
      "accessKeyId": "<Add accessKeyId>",
      "secretAccessKey": "<Add secret Access Key>"
    }
  },
  "connectionSpec": {
    "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99", // Google Cloud Storage connection spec
    "version": "1.0"
  }
}'
```

+++

**Risposta**

+++[!DNL Google Cloud Storage] - Risposta di connessione di base

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**Richiesta**

+++SFTP con password - Richiesta di connessione di base

>[!TIP]
>
>Per informazioni su come ottenere le credenziali di autenticazione richieste, consulta la [autenticare a destinazione](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information) della pagina della documentazione sulla destinazione SFTP.

Osserva le righe evidenziate con commenti in linea nell’esempio di richiesta, che forniscono informazioni aggiuntive. Rimuovi i commenti in linea nella richiesta quando copia-incolla la richiesta nel terminale di scelta.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "SFTP with password Base Connection",
  "auth": {
    "specName": "SFTP with Password",
    "params": {
      "domain": "<Add domain>",
      "username": "<Add username>",
      "password": "<Add password>"
    }
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec
    "version": "1.0"
  }
}'
```

+++

+++SFTP con chiave SSH - Richiesta di connessione di base

>[!TIP]
>
>Per informazioni su come ottenere le credenziali di autenticazione richieste, consulta la [autenticare a destinazione](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information) della pagina della documentazione sulla destinazione SFTP.

Osserva le righe evidenziate con commenti in linea nell’esempio di richiesta, che forniscono informazioni aggiuntive. Rimuovi i commenti in linea nella richiesta quando copia-incolla la richiesta nel terminale di scelta.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "SFTP with SSH key Base Connection",
  "auth": {
    "specName": "SFTP with SSH Key",
    "params": {
      "domain": "<Add domain>",
      "username": "<Add username>",
      "sshKey": "<Add SSH key>"
    }
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec
    "version": "1.0"
  }
}'
```

+++

**Risposta**

+++SFTP - Risposta alla connessione di base

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

Prendi nota dell’ID di connessione dalla risposta. Questo ID sarà necessario nel passaggio successivo durante la creazione della connessione di destinazione.

## Creare una connessione di destinazione {#create-target-connection}

![Diagramma che mostra il passaggio 4 nel flusso di lavoro dei set di dati di esportazione](../assets/api/export-datasets/export-datasets-api-workflow-create-target-connection.png)

Successivamente, è necessario creare una connessione di destinazione che memorizzi i parametri di esportazione per i set di dati. I parametri di esportazione includono posizione, formato file, compressione e altri dettagli. Fai riferimento a `targetSpec` proprietà fornite nella specifica di connessione della destinazione per comprendere le proprietà supportate per ciascun tipo di destinazione. Fai riferimento alle schede seguenti per `targetSpec` di tutte le destinazioni supportate.

>[!BEGINTABS]

>[!TAB Amazon S3]

+++[!DNL Amazon S3] - [!DNL Connection spec] visualizzazione dei parametri di connessione di destinazione

Osserva le righe evidenziate con i commenti in linea nel [!DNL connection spec] di seguito, un esempio che fornisce informazioni aggiuntive su dove trovare il [!DNL target spec] nelle specifiche di connessione. Puoi vedere anche nell’esempio sottostante quali parametri target sono *not* applicabile alle destinazioni di esportazione del set di dati.

```json {line-numbers="true" start-line="1" highlight="10,41,56"}
{
    "items": [
        {
            "id": "4fce964d-3f37-408f-9778-e597338a21ee",
            "name": "Amazon S3",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "bucketName": {
                            "title": "Bucket name",
                            "description": "Bucket name",
                            "type": "string",
                            "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
                            "uiAttributes": {
                                "tooltip": {
                                    "id": "platform_destinations_connect_s3_bucket",
                                    "fallbackUrl": "http://www.adobe.com/go/destinations-amazon-s3-connection-parameters-en"
                                }
                            }
                        },
                        "path": {
                            "title": "Folder path",
                            "description": "Output path for copying files",
                            "type": "string",
                            "pattern": "^[0-9a-zA-Z\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\/?)+$",
                            "uiAttributes": {
                                "tooltip": {
                                    "id": "platform_destinations_connect_s3_folderpath",
                                    "fallbackUrl": "http://www.adobe.com/go/destinations-amazon-s3-connection-parameters-en"
                                }
                            }
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "bucketName",
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB Archiviazione BLOB di Azure]

+++[!DNL Azure Blob Storage] - [!DNL Connection spec] visualizzazione dei parametri di connessione di destinazione

Osserva le righe evidenziate con i commenti in linea nel [!DNL connection spec] di seguito, un esempio che fornisce informazioni aggiuntive su dove trovare il [!DNL target spec] nelle specifiche di connessione. Puoi vedere anche nell’esempio sottostante quali parametri target sono *not* applicabile alle destinazioni di esportazione del set di dati.

```json {line-numbers="true" start-line="1" highlight="10,29,44"}
{
    "items": [
        {
            "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
            "name": "Azure Blob Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "path": {
                            "title": "Folder path",
                            "description": "Output path (relative) indicating where to upload the data",
                            "type": "string",
                            "pattern": "^[0-9a-zA-Z\/\\!\\-_\\.\\*\\'\\(\\)]+$"
                        },
                        "container": {
                            "title": "Container",
                            "description": "Container within the storage where to upload the data",
                            "type": "string",
                            "pattern": "^[a-z0-9](?!.*--)[a-z0-9-]{1,61}[a-z0-9]$"
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "container",
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++


>[!TAB Azure Data Lake Gen 2 (ADLS Gen2)]

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec] visualizzazione dei parametri di connessione di destinazione

Osserva le righe evidenziate con i commenti in linea nel [!DNL connection spec] di seguito, un esempio che fornisce informazioni aggiuntive su dove trovare il [!DNL target spec] nelle specifiche di connessione. Puoi vedere anche nell’esempio sottostante quali parametri target sono *not* applicabile alle destinazioni di esportazione del set di dati.

```json {line-numbers="true" start-line="1" highlight="10,22,37"}
{
    "items": [
        {
            "id": "be2c3209-53bc-47e7-ab25-145db8b873e1",
            "name": "Azure Data Lake Gen2",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "path": {
                            "title": "Folder path",
                            "description": "Enter the path to your Azure Data Lake Storage folder",
                            "type": "string"
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions":{...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB Data Landing Zone (DLZ)]

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec] visualizzazione dei parametri di connessione di destinazione

Osserva le righe evidenziate con i commenti in linea nel [!DNL connection spec] di seguito, un esempio che fornisce informazioni aggiuntive su dove trovare il [!DNL target spec] nelle specifiche di connessione. Puoi vedere anche nell’esempio sottostante quali parametri target sono *not* applicabile alle destinazioni di esportazione del set di dati.

```json {line-numbers="true" start-line="1" highlight="9,21,36"}
"items": [
    {
        "id": "10440537-2a7b-4583-ac39-ed38d4b848e8",
        "name": "Data Landing Zone",
        "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
        "version": "1.0",
        "authSpec": [],
        "encryptionSpecs": [],
        "targetSpec": { // describes the target connection parameters
            "name": "User based target",
            "type": "UserNamespace",
            "spec": {
                "$schema": "http://json-schema.org/draft-07/schema#",
                "type": "object",
                "properties": {
                    "path": {
                        "title": "Folder path",
                        "description": "Enter the path to your Azure Data Lake Storage folder",
                        "type": "string"
                    },
                    "fileType": {...}, // not applicable to dataset destinations
                    "datasetFileType": {
                        "conditional": {
                            "field": "flowSpec.attributes._workflow",
                            "operator": "CONTAINS",
                            "value": "DATASETS"
                        },
                        "title": "File Type",
                        "description": "Select file format",
                        "type": "string",
                        "enum": [
                            "JSON",
                            "PARQUET"
                        ]
                    },
                    "csvOptions": {...}, // not applicable to dataset destinations
                    "compression": {
                        "title": "Compression format",
                        "description": "Select the desired file compression format.",
                        "type": "string",
                        "enum": [
                            "NONE",
                            "GZIP"
                        ]
                    }
                },
                "required": [
                    "path",
                    "datasetFileType",
                    "compression",
                    "fileType"
                ]
            }
//...
```

+++

>[!TAB Google Cloud Storage]

+++[!DNL Google Cloud Storage] - [!DNL Connection spec] visualizzazione dei parametri di connessione di destinazione

Osserva le righe evidenziate con i commenti in linea nel [!DNL connection spec] di seguito, un esempio che fornisce informazioni aggiuntive su dove trovare il [!DNL target spec] nelle specifiche di connessione. Puoi vedere anche nell’esempio sottostante quali parametri target sono *not* applicabile alle destinazioni di esportazione del set di dati.

```json {line-numbers="true" start-line="1" highlight="10,29,44"}
{
    "items": [
        {
            "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99",
            "name": "Google Cloud Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "bucketName": {
                            "title": "Bucket name",
                            "description": "Bucket name",
                            "type": "string",
                            "pattern": "(?!^goog.*$)(?!^.*g(o|0)(o|0)gle.*$)(((?=^.{3,63}$)(^([a-z0-9]|[a-z0-9][a-z0-9\\-_]*)[a-z0-9]$))|((?=^.{3,222}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]{1,63}|[a-z0-9][a-z0-9\\-_]{1,61}[a-z0-9])\\.)*([a-z0-9]{1,63}|[a-z0-9][a-z0-9\\-_]{1,61}[a-z0-9])$)))"
                        },
                        "path": {
                            "title": "Folder path",
                            "description": "Output path for copying files",
                            "type": "string",
                            "pattern": "^[0-9a-zA-Z\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\/?)+$"
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "bucketName",
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB SFTP]

+++SFTP - [!DNL Connection spec] visualizzazione dei parametri di connessione di destinazione

Osserva le righe evidenziate con i commenti in linea nel [!DNL connection spec] di seguito, un esempio che fornisce informazioni aggiuntive su dove trovare il [!DNL target spec] nelle specifiche di connessione. Puoi vedere anche nell’esempio sottostante quali parametri target sono *not* applicabile alle destinazioni di esportazione del set di dati.

```json {line-numbers="true" start-line="1" highlight="10,22,37"}
{
    "items": [
        {
            "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
            "name": "SFTP",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "remotePath": {
                            "title": "Folder path",
                            "description": "Enter your folder path",
                            "type": "string"
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "GZIP",
                                "NONE"
                            ]
                        }
                    },
                    "required": [
                        "remotePath",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                },
//...
```

+++

>[!ENDTABS]


Utilizzando le specifiche di cui sopra, puoi creare una richiesta di connessione di destinazione specifica per la destinazione di archiviazione cloud desiderata, come illustrato nelle schede seguenti.

>[!BEGINTABS]

>[!TAB Amazon S3]

**Richiesta**

+++[!DNL Amazon S3] - Richiesta di connessione Target

>[!TIP]
>
>Per informazioni su come ottenere i parametri target richiesti, consulta la [compila i dettagli della destinazione](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) della sezione [!DNL Amazon S3] pagina della documentazione di destinazione.
>Per altri valori supportati di `datasetFileType`, consulta la documentazione di riferimento API .

Osserva le righe evidenziate con commenti in linea nell’esempio di richiesta, che forniscono informazioni aggiuntive. Rimuovi i commenti in linea nella richiesta quando copia-incolla la richiesta nel terminale di scelta.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Amazon S3 Beta Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "bucketName": "your-bucket-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "4fce964d-3f37-408f-9778-e597338a21ee", // Amazon S3 connection spec id
        "version": "1.0"
    }
}'
```

+++

**Risposta**

+++Connessione di destinazione - Risposta

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Archiviazione BLOB di Azure]

**Richiesta**

+++[!DNL Azure Blob Storage] - Richiesta di connessione Target

>[!TIP]
>
>Per informazioni su come ottenere i parametri target richiesti, consulta la [compila i dettagli della destinazione](/help/destinations/catalog/cloud-storage/azure-blob.md#destination-details) della sezione [!DNL Azure Blob Storage] pagina della documentazione di destinazione.
>Per altri valori supportati di `datasetFileType`, consulta la documentazione di riferimento API .


Osserva le righe evidenziate con commenti in linea nell’esempio di richiesta, che forniscono informazioni aggiuntive. Rimuovi i commenti in linea nella richiesta quando copia-incolla la richiesta nel terminale di scelta.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Azure Blob Storage Beta Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "container": "your-container-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2", // Azure Blob Storage connection spec id
        "version": "1.0"
    }
}'
```

+++

**Risposta**

+++Connessione di destinazione - Risposta

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen 2 (ADLS Gen2)]

**Richiesta**

+++[!DNL Azure Blob Storage] - Richiesta di connessione Target

>[!TIP]
>
>Per informazioni su come ottenere i parametri target richiesti, consulta la [compila i dettagli della destinazione](/help/destinations/catalog/cloud-storage/adls-gen2.md#destination-details) sezione di Azure [!DNL Data Lake Gen 2(ADLS Gen2)] pagina della documentazione di destinazione.
>Per altri valori supportati di `datasetFileType`, consulta la documentazione di riferimento API .

Osserva le righe evidenziate con commenti in linea nell’esempio di richiesta, che forniscono informazioni aggiuntive. Rimuovi i commenti in linea nella richiesta quando copia-incolla la richiesta nel terminale di scelta.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Azure Data Lake Gen 2(ADLS Gen2) Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "be2c3209-53bc-47e7-ab25-145db8b873e1", // Azure Data Lake Gen 2(ADLS Gen2) connection spec id
        "version": "1.0"
    }
}'
```

+++

**Risposta**

+++Connessione di destinazione - Risposta

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Data Landing Zone (DLZ)]

**Richiesta**

+++[!DNL Data Landing Zone] - Richiesta di connessione Target

>[!TIP]
>
>Per informazioni su come ottenere i parametri target richiesti, consulta la [compila i dettagli della destinazione](/help/destinations/catalog/cloud-storage/data-landing-zone.md#destination-details) della sezione [!DNL Data Landing Zone] pagina della documentazione di destinazione.
>Per altri valori supportati di `datasetFileType`, consulta la documentazione di riferimento API .

Osserva le righe evidenziate con commenti in linea nell’esempio di richiesta, che forniscono informazioni aggiuntive. Rimuovi i commenti in linea nella richiesta quando copia-incolla la richiesta nel terminale di scelta.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Data Landing Zone Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "10440537-2a7b-4583-ac39-ed38d4b848e8", // Data Landing Zone connection spec id
        "version": "1.0"
    }
}'
```

+++

**Risposta**

+++Connessione di destinazione - Risposta

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Google Cloud Storage]

**Richiesta**

+++[!DNL Google Cloud Storage] - Richiesta di connessione Target

>[!TIP]
>
>Per informazioni su come ottenere i parametri target richiesti, consulta la [compila i dettagli della destinazione](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#destination-details) della sezione [!DNL Google Cloud Storage] pagina della documentazione di destinazione.
>Per altri valori supportati di `datasetFileType`, consulta la documentazione di riferimento API .


Osserva le righe evidenziate con commenti in linea nell’esempio di richiesta, che forniscono informazioni aggiuntive. Rimuovi i commenti in linea nella richiesta quando copia-incolla la richiesta nel terminale di scelta.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Google Cloud Storage Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "bucketName": "your-bucket-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99", // Google Cloud Storage connection spec id
        "version": "1.0"
    }
}'
```

+++

**Risposta**

+++Connessione di destinazione - Risposta

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**Richiesta**

+++SFTP - Richiesta di connessione Target

>[!TIP]
>
>Per informazioni su come ottenere i parametri target richiesti, consulta la [compila i dettagli della destinazione](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#destination-details) della pagina della documentazione sulla destinazione SFTP.
>Per altri valori supportati di `datasetFileType`, consulta la documentazione di riferimento API .

Osserva le righe evidenziate con commenti in linea nell’esempio di richiesta, che forniscono informazioni aggiuntive. Rimuovi i commenti in linea nella richiesta quando copia-incolla la richiesta nel terminale di scelta.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "SFTP Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "remotePath": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec id
        "version": "1.0"
    }
}'
```

+++

**Risposta**

Connessione +++Target - Risposta

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

Prendi nota dell’ID di connessione di Target dalla risposta. Questo ID sarà necessario nel passaggio successivo durante la creazione del flusso di dati per esportare i set di dati.

## Creare un flusso di dati {#create-dataflow}

![Diagramma che mostra il passaggio 5 nel flusso di lavoro dei set di dati di esportazione](../assets/api/export-datasets/export-datasets-api-workflow-set-up-dataflow.png)

Il passaggio finale nella configurazione di destinazione consiste nell’impostare un flusso di dati. Un flusso di dati unisce le entità create in precedenza e fornisce anche opzioni per configurare la pianificazione dell’esportazione del set di dati. Per creare il flusso di dati, utilizza i payload seguenti, a seconda della destinazione di archiviazione cloud desiderata, e sostituisci gli ID entità dai passaggi precedenti.

>[!BEGINTABS]

>[!TAB Amazon S3]

**Richiesta**

+++Crea flusso di dati set a [!DNL Amazon S3] destinazione - Richiesta

Osserva le righe evidenziate con commenti in linea nell’esempio di richiesta, che forniscono informazioni aggiuntive. Rimuovi i commenti in linea nella richiesta quando copia-incolla la richiesta nel terminale di scelta.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to an Amazon S3 cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to an Amazon S3 cloud storage destination",
    "flowSpec": {
        "id": "269ba276-16fc-47db-92b0-c1049a3c131f", // Amazon S3 flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. Use "interval": 1 when you select "timeUnit": "day"
        "startTime": 1675901210 // UNIX timestamp start time (in seconds)
    }
}'
```

+++

**Risposta**

+++Crea flusso di dati - Risposta

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Archiviazione BLOB di Azure]

**Richiesta**

+++Crea flusso di dati set a [!DNL Azure Blob Storage] destinazione - Richiesta

Osserva le righe evidenziate con commenti in linea nell’esempio di richiesta, che forniscono informazioni aggiuntive. Rimuovi i commenti in linea nella richiesta quando copia-incolla la richiesta nel terminale di scelta.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to an Azure Blob Storage cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to an Azure Blob Storage cloud storage destination",
    "flowSpec": {
        "id": "95bd8965-fc8a-4119-b9c3-944c2c2df6d2", // Azure Blob Storage flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "interval": 3, // also supports 6, 9, 12, 24 hour increments
        "timeUnit": "hour",
        "startTime": 1675901210 // UNIX timestamp start time(in seconds)
    }
}'
```

+++

**Risposta**

+++Crea flusso di dati - Risposta

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen 2 (ADLS Gen2)]

**Richiesta**

+++Crea flusso di dati set a [!DNL Azure Data Lake Gen 2(ADLS Gen2)] destinazione - Richiesta

Osserva le righe evidenziate con commenti in linea nell’esempio di richiesta, che forniscono informazioni aggiuntive. Rimuovi i commenti in linea nella richiesta quando copia-incolla la richiesta nel terminale di scelta.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to an Azure Data Lake Gen 2(ADLS Gen2) cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to an Azure Data Lake Gen 2(ADLS Gen2) cloud storage destination",
    "flowSpec": {
        "id": "17be2013-2549-41ce-96e7-a70363bec293", // Azure Data Lake Gen 2(ADLS Gen2) flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "interval": 3, // also supports 6, 9, 12, 24 hour increments
        "timeUnit": "hour",
        "startTime": 1675901210 // UNIX timestamp start time(in seconds)
    }
}'
```

+++

**Risposta**

+++Crea flusso di dati - Risposta

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Data Landing Zone (DLZ)]

**Richiesta**

+++Crea flusso di dati set a [!DNL Data Landing Zone] destinazione - Richiesta

Osserva le righe evidenziate con commenti in linea nell’esempio di richiesta, che forniscono informazioni aggiuntive. Rimuovi i commenti in linea nella richiesta quando copia-incolla la richiesta nel terminale di scelta.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to a Data Landing Zone cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to a Data Landing Zone cloud storage destination",
    "flowSpec": {
        "id": "cd2fc47e-e838-4f38-a581-8fff2f99b63a", // Data Landing Zone flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "interval": 3, // also supports 6, 9, 12, 24 hour increments
        "timeUnit": "hour",
        "startTime": 1675901210 // UNIX timestamp start time(in seconds)
    }
}'
```

+++

**Risposta**

+++Crea flusso di dati - Risposta

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Google Cloud Storage]

**Richiesta**

+++Crea flusso di dati set a [!DNL Google Cloud Storage] destinazione - Richiesta

Osserva le righe evidenziate con commenti in linea nell’esempio di richiesta, che forniscono informazioni aggiuntive. Rimuovi i commenti in linea nella richiesta quando copia-incolla la richiesta nel terminale di scelta.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to a Google Cloud Storage cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to a Google Cloud Storage destination",
    "flowSpec": {
        "id": "585c15c4-6cbf-4126-8f87-e26bff78b657", // Google Cloud Storage flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "interval": 3, // also supports 6, 9, 12, 24 hour increments
        "timeUnit": "hour",
        "startTime": 1675901210 // UNIX timestamp start time(in seconds)
    }
}'
```

+++

**Risposta**

+++Crea flusso di dati - Risposta

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**Richiesta**

+++Crea flusso di dati di set di dati per la destinazione SFTP - Richiesta

Osserva le righe evidenziate con commenti in linea nell’esempio di richiesta, che forniscono informazioni aggiuntive. Rimuovi i commenti in linea nella richiesta quando copia-incolla la richiesta nel terminale di scelta.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to an SFTP cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to an SFTP cloud storage destination",
    "flowSpec": {
        "id": "354d6aad-4754-46e4-a576-1b384561c440", // SFTP flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "interval": 3, // also supports 6, 9, 12, 24 hour increments
        "timeUnit": "hour",
        "startTime": 1675901210 // UNIX timestamp start time(in seconds)
    }
}'
```

+++

**Risposta**

+++Crea flusso di dati - Risposta

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

Prendi nota dell’ID del flusso di dati dalla risposta. Questo ID sarà necessario nel passaggio successivo quando si recuperano i flussi di dati per convalidare le esportazioni del set di dati.

## Ottieni le esecuzioni del flusso di dati {#get-dataflow-runs}

![Diagramma che mostra il passaggio 6 nel flusso di lavoro dei set di dati di esportazione](../assets/api/export-datasets/export-datasets-api-workflow-validate-dataflow.png)

Per controllare le esecuzioni di un flusso di dati, utilizza l’API di esecuzione del flusso di dati:

>[!BEGINSHADEBOX]

**Richiesta**

+++Ottieni esecuzioni del flusso di dati - Richiesta

Nella richiesta di recupero delle esecuzioni del flusso di dati, aggiungi come parametro di query l’ID del flusso di dati ottenuto nel passaggio precedente, durante la creazione del flusso di dati.

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==eb54b3b3-3949-4f12-89c8-64eafaba858f' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
```

+++

**Risposta**

+++Ottieni esecuzioni del flusso di dati - Risposta

```json
{
    "items": [
        {
            "id": "4b7728dd-83c9-4c38-95a4-24ddab545404",
            "createdAt": 1675807718296,
            "updatedAt": 1675807731834,
            "createdBy": "aep_activation_batch@AdobeID",
            "updatedBy": "acp_foundation_connectors@AdobeID",
            "createdClient": "aep_activation_batch",
            "updatedClient": "acp_foundation_connectors",
            "sandboxId": "7dfdcd30-0a09-11ea-8ea6-7bf93ce86c28",
            "sandboxName": "sand-1",
            "imsOrgId": "5555467B5D8013E50A494220@AdobeOrg",
            "flowId": "aae5ec63-b0ac-4808-9a44-abf2ea67bd5a",
            "flowSpec": {
                "id": "615d3489-36d2-4671-9467-4ae1129facd3",
                "version": "1.0"
            },
            "providerRefId": "ba56f98e0c49b572adb249980c39b1c7",
            "etag": "\"08005e9e-0000-0200-0000-63e2cbf30000\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1675807719411,
                    "completedAtUTC": 1675807719416
                },
                "sizeSummary": {
                    "inputBytes": 0
                },
                "recordSummary": {
                    "inputRecordCount": 0,
                    "skippedRecordCount": 0,
                    "sourceSummaries": [
                        {
                            "id": "ea2b1205-4692-49de-b448-ebf75b1d188a",
                            "inputRecordCount": 0,
                            "skippedRecordCount": 0,
                            "entitySummaries": [
                                {
//...
```

+++

>[!ENDSHADEBOX]

Puoi trovare informazioni sulle [vari parametri restituiti da Dataflow esegue API](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Dataflow-runs/operation/getFlowRuns) nella documentazione di riferimento API.

## Gestione degli errori API {#api-error-handling}

Gli endpoint API in questa esercitazione seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](/help/landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](/help/landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform per ulteriori informazioni sull’interpretazione delle risposte agli errori.

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai collegato Platform a una delle destinazioni di archiviazione cloud batch preferite e hai impostato un flusso di dati per la rispettiva destinazione per esportare i set di dati. Per ulteriori dettagli, consulta le pagine seguenti, ad esempio come modificare i flussi di dati esistenti utilizzando l’API del servizio di flusso:

* [Panoramica sulle destinazioni](../home.md)
* [Panoramica del catalogo delle destinazioni](../catalog/overview.md)
* [Aggiornare i flussi di dati di destinazione utilizzando l’API del servizio di flusso](../api/update-destination-dataflows.md)