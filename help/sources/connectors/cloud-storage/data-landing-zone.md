---
title: Data Landing Zone Source
description: Scopri come collegare Data Landing Zone a Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: b9a409db2f1aee852faf9038a25236b78f76d4dd
workflow-type: tm+mt
source-wordcount: '1282'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

>[!IMPORTANT]
>
>Questa pagina è specifica per il connettore [!DNL Data Landing Zone] *source* in Experience Platform. Per informazioni sulla connessione al connettore [!DNL Data Landing Zone] *destination*, consulta la [[!DNL Data Landing Zone] pagina della documentazione di destinazione](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] è un&#39;interfaccia di archiviazione [!DNL Azure Blob] fornita da Adobe Experience Platform, che consente di accedere a una struttura di archiviazione dei file sicura e basata su cloud per inserire i file in Platform. È possibile accedere a un contenitore [!DNL Data Landing Zone] per sandbox e il volume totale di dati in tutti i contenitori è limitato ai dati totali forniti con la licenza di Platform Products and Services. A tutti i clienti Experience Platform viene fornito un contenitore [!DNL Data Landing Zone] per sandbox. È possibile leggere e scrivere i file nel contenitore tramite [!DNL Azure Storage Explorer] o l&#39;interfaccia della riga di comando.

[!DNL Data Landing Zone] supporta l&#39;autenticazione basata su SAS e i relativi dati sono protetti con meccanismi di protezione di archiviazione standard [!DNL Azure Blob] in modalità di riposo e transito. L&#39;autenticazione basata su SAS consente di accedere in modo sicuro al contenitore [!DNL Data Landing Zone] tramite una connessione Internet pubblica. Non sono necessarie modifiche di rete per accedere al contenitore [!DNL Data Landing Zone], pertanto non è necessario configurare elenchi consentiti o impostazioni per più aree geografiche per la rete. Experience Platform applica un tempo di scadenza di sette giorni rigoroso su tutti i file e le cartelle caricati in un contenitore [!DNL Data Landing Zone]. Tutti i file e le cartelle vengono eliminati dopo sette giorni.

## Configura l&#39;origine [!DNL Data Landing Zone], ad Experience Platform in Azure {#azure}

Segui i passaggi seguenti per scoprire come configurare l&#39;account [!DNL Data Landing Zone], ad Experience Platform in Azure.

>[!NOTE]
>
>Se si desidera accedere a [!DNL Data Landing Zone] da [!DNL Azure Data Factory], è necessario creare un servizio collegato per [!DNL Data Landing Zone] utilizzando le [credenziali SAS](../../tutorials/ui/create/cloud-storage/data-landing-zone.md#retrieve-your-data-landing-zone-credentials) fornite da Experience Platform. Dopo aver creato il servizio collegato, puoi esplorare [!DNL Data Landing Zone] selezionando il percorso del contenitore invece del percorso principale predefinito.

### Vincoli di denominazione per file e directory

Di seguito è riportato un elenco di vincoli di cui è necessario tenere conto per la denominazione dei file o delle directory di archiviazione cloud.

- I nomi dei componenti di directory e file non possono superare i 255 caratteri.
- I nomi di file e directory non possono terminare con una barra (`/`). Se fornito, verrà rimosso automaticamente.
- I seguenti caratteri URL riservati devono essere correttamente preceduti dall&#39;escape: `! ' ( ) ; @ & = + $ , % # [ ]`
- I seguenti caratteri non sono consentiti: `" \ / : | < > * ?`.
- Caratteri di percorso URL non validi non consentiti. I punti di codice come `\uE000`, sebbene validi nei nomi di file NTFS, non sono caratteri Unicode validi. Inoltre, alcuni caratteri ASCII o Unicode, come i caratteri di controllo (ad esempio da `0x00` a `0x1F`, `\u0081` e così via), non sono consentiti. Per le regole che regolano le stringhe Unicode in HTTP/1.1, vedere [RFC 2616, Sezione 2.2: Regole di base](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Non sono consentiti i seguenti nomi di file: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carattere punto (.) e due caratteri punto (..).

### Gestione dei contenuti dell’area di destinazione dati{#manage-the-contents-of-your-data-landing-zone}

È possibile utilizzare [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/) per gestire il contenuto del contenitore [!DNL Data Landing Zone].

Nell&#39;interfaccia utente [!DNL Azure Storage Explorer], selezionare l&#39;icona di connessione nell&#39;area di navigazione a sinistra. Viene visualizzata la finestra **Seleziona risorsa** che fornisce le opzioni per la connessione. Selezionare **[!DNL Blob container]** per connettersi a [!DNL Data Landing Zone].

![L&#39;area di lavoro della risorsa selezionata in Azure Explorer.](../../images/tutorials/create/dlz/select-resource.png)

Selezionare **URL firma di accesso condiviso (SAS)** come metodo di connessione, quindi selezionare **Avanti**.

![Il metodo di connessione selezionato in Azure Explorer, con la firma di accesso condiviso selezionata.](../../images/tutorials/create/dlz/select-connection-method.png)

Dopo aver selezionato il metodo di connessione, è necessario fornire **nome visualizzato** e l&#39;URL SAS del contenitore **[!DNL Blob]** che corrisponde al contenitore [!DNL Data Landing Zone].

>[!TIP]
>
>È possibile recuperare le credenziali di [!DNL Data Landing Zone] dal catalogo delle origini nell&#39;interfaccia utente di Platform.

Fornisci l&#39;URL SAS [!DNL Data Landing Zone] e seleziona **Avanti**

![Immettere l&#39;area di lavoro delle informazioni di connessione in Azure Explorer in cui vengono immessi il nome visualizzato e l&#39;URL SAS.](../../images/tutorials/create/dlz/enter-connection-info.png)

Viene visualizzata la finestra **Riepilogo** che fornisce una panoramica delle impostazioni, incluse informazioni sull&#39;endpoint [!DNL Blob] e sulle autorizzazioni. Al termine, selezionare **Connetti**.

![L&#39;area di lavoro di riepilogo di Azure Explorer che ridefinisce le impostazioni della connessione delle risorse.](../../images/tutorials/create/dlz/summary.png)

Una connessione riuscita aggiorna l&#39;interfaccia utente di [!DNL Azure Storage Explorer] con il contenitore [!DNL Data Landing Zone].

![Area di lavoro di navigazione dell&#39;area di destinazione dati in Azure Explorer.](../../images/tutorials/create/dlz/dlz-user-container.png)

Con il contenitore [!DNL Data Landing Zone] connesso a [!DNL Azure Storage Explorer], ora puoi iniziare a caricare i file nel contenitore [!DNL Data Landing Zone]. Per caricare, selezionare **Carica**, quindi selezionare **Carica file**.

![Area di lavoro di caricamento file di Azure Explorer.](../../images/tutorials/create/dlz/upload.png)

Dopo aver selezionato il file da caricare, è necessario identificare il tipo [!DNL Blob] che si desidera caricare e la directory di destinazione desiderata. Al termine, selezionare **Carica**.

| [!DNL Blob] tipi | Descrizione |
| --- | --- |
| Blocca [!DNL Blob] | Il blocco [!DNL Blobs] è ottimizzato per il caricamento di grandi quantità di dati in modo efficiente. Blocco [!DNL Blobs]: opzione predefinita per [!DNL Data Landing Zone]. |
| Aggiungi [!DNL Blob] | Aggiunta di [!DNL Blobs] ottimizzata per l&#39;aggiunta di dati alla fine del file. |

![Finestra Carica file di Azure Explorer in cui vengono visualizzati i file selezionati, il tipo di BLOB e la categoria di destinazione.](../../images/tutorials/create/dlz/upload-files.png)

### Carica i file in [!DNL Data Landing Zone] tramite l&#39;interfaccia della riga di comando

È inoltre possibile utilizzare l&#39;interfaccia della riga di comando del dispositivo e accedere ai file di caricamento in [!DNL Data Landing Zone].

### Caricare un file con Bash

Nell&#39;esempio seguente vengono utilizzati Bash e cURL per caricare un file in un [!DNL Data Landing Zone] con l&#39;API REST [!DNL Azure Blob Storage]:

```shell
# Set Azure Blob-related settings
DATE_NOW=$(date -Ru | sed 's/\+0000/GMT/')
AZ_VERSION="2018-03-28"
AZ_BLOB_URL="<URL TO BLOB ACCOUNT>"
AZ_BLOB_CONTAINER="<BLOB CONTAINER NAME>"
AZ_BLOB_TARGET="${AZ_BLOB_URL}/${AZ_BLOB_CONTAINER}"
AZ_SAS_TOKEN="<SAS TOKEN, STARTING WITH ? AND ENDING WITH %3D>"

# Path to the file we wish to upload
FILE_PATH="</PATH/TO/FILE>"
FILE_NAME=$(basename "$FILE_PATH")

# Execute HTTP PUT to upload file (remove '-v' flag to suppress verbose output)
curl -v -X PUT \
   -H "Content-Type: application/octet-stream" \
   -H "x-ms-date: ${DATE_NOW}" \
   -H "x-ms-version: ${AZ_VERSION}" \
   -H "x-ms-blob-type: BlockBlob" \
   --data-binary "@${FILE_PATH}" "${AZ_BLOB_TARGET}/${FILE_NAME}${AZ_SAS_TOKEN}"
```

### Caricare un file con Python

Nell&#39;esempio seguente viene utilizzato [!DNL Microsoft's] Python v12 SDK per caricare un file in un [!DNL Data Landing Zone]:

>[!TIP]
>
>Nell&#39;esempio seguente viene utilizzato l&#39;URI SAS completo per la connessione a un contenitore [!DNL Azure Blob], ma è possibile utilizzare altri metodi e operazioni per l&#39;autenticazione. Per ulteriori informazioni, vedere il documento [[!DNL Microsoft] su Python v12 SDK](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-python).

```py
import os
from azure.storage.blob import ContainerClient

try:
    # Set Azure Blob-related settings
    sasUri = "<SAS URI>"
    srcFilePath = "<FULL PATH TO FILE>" 
    srcFileName = os.path.basename(srcFilePath)

    # Connect to container using SAS URI
    containerClient = ContainerClient.from_container_url(sasUri)

    # Upload file to Data Landing Zone with overwrite enabled
    with open(srcFilePath, "rb") as fileToUpload:
        containerClient.upload_blob(srcFileName, fileToUpload, overwrite=True)

except Exception as ex:
    print("Exception: " + ex.strerror)
```

### Carica un file con [!DNL AzCopy]

Nell&#39;esempio seguente viene utilizzata l&#39;utilità [!DNL Microsoft's] [!DNL AzCopy] per caricare un file in un [!DNL Data Landing Zone]:

>[!TIP]
>
>Mentre l&#39;esempio seguente utilizza il comando `copy`, è possibile utilizzare altri comandi e opzioni per caricare un file in [!DNL Data Landing Zone], utilizzando [!DNL AzCopy]. Per ulteriori informazioni, vedere il [[!DNL Microsoft AzCopy] documento](https://docs.microsoft.com/en-us/azure/storage/common/storage-ref-azcopy?toc=/azure/storage/blobs/toc.json).

```bat
set sasUri=<FULL SAS URI, PROPERLY ESCAPED>
set srcFilePath=<PATH TO LOCAL FILE(S); WORKS WITH WILDCARD PATTERNS>

azcopy copy "%srcFilePath%" "%sasUri%" --overwrite=true --recursive=true
```

## Configura l&#39;origine [!DNL Data Landing Zone], ad Experience Platform su Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Questa sezione si applica alle implementazioni di Experience Platform in esecuzione su Amazon Web Services (AWS). Un Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta l&#39;[panoramica sul cloud multiplo di Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).

Segui i passaggi seguenti per scoprire come configurare l&#39;account [!DNL Data Landing Zone], ad Experience Platform su Amazon Web Services (AWS).

### Configurazione di AWS CLI ed esecuzione delle operazioni

- Leggi la guida sull&#39;installazione o l&#39;aggiornamento di [alla versione più recente di AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).

### Configurare AWS CLI con credenziali temporanee

Utilizza il comando AWS `configure` per configurare CLI con chiavi di accesso e token di sessione.

```shell
aws configure
```

Quando richiesto, immetti i seguenti valori:

- ID chiave di accesso AWS: `{YOUR_ACCESS_KEY_ID}`
- Chiave di accesso segreta AWS: `{YOUR_SECRET_ACCESS_KEY}`
- Nome area predefinito: `{YOUR_REGION}` (ad esempio, `us-west-2`)
- Formato di output predefinito: `json`

Quindi, imposta il token di sessione:

```shell
aws configure set aws_session_token your-session-token
```

### Utilizzare i file in [!DNL Amazon S3]

>[!BEGINTABS]

>[!TAB Carica un file in Amazon S3]

Modello:

```shell
aws s3 cp local-file-path s3://bucketName/dlzFolder/remote-file-Name
```

Esempio:

```shell
aws s3 cp example.txt s3://bucketName/dlzFolder/example.txt
```


>[!TAB Scarica un file da Amazon S3]

Modello:

```shell
aws s3 cp s3://bucketName/dlzFolder/remote-file local-file-path
```

Esempio:

```shell
aws s3 cp s3://bucketName/dlzFolder/example.txt example.txt
```

>[!ENDTABS]

### Usa le credenziali di [!DNL Data Landing Zone] per accedere alla console AWS

#### Estrai le tue credenziali

Innanzitutto, devi ottenere quanto segue:

- `awsAccessKeyId`
- `awsSecretAccessKey`
- `awsSessionToken`

#### Generare un token di accesso

Quindi, utilizza le credenziali estratte per creare una sessione e generare un token di accesso utilizzando l’endpoint AWS Federation:

```py
import json
import requests
 
# Example DLZ response with credentials
response_json = '''{
    "credentials": {
        "awsAccessKeyId": "your-access-key",
        "awsSecretAccessKey": "your-secret-key",
        "awsSessionToken": "your-session-token"
    }
}'''
 
# Parse credentials
response_data = json.loads(response_json)
aws_access_key_id = response_data['credentials']['awsAccessKeyId']
aws_secret_access_key = response_data['credentials']['awsSecretAccessKey']
aws_session_token = response_data['credentials']['awsSessionToken']
 
# Create session dictionary
session = {
    'sessionId': aws_access_key_id,
    'sessionKey': aws_secret_access_key,
    'sessionToken': aws_session_token
}
 
# Generate the sign-in token
signin_token_url = "https://signin.aws.amazon.com/federation"
signin_token_payload = {
    "Action": "getSigninToken",
    "Session": json.dumps(session)
}
signin_token_response = requests.post(signin_token_url, data=signin_token_payload)
signin_token = signin_token_response.json()['SigninToken']
```

#### Creare l’URL di accesso alla console AWS

Una volta ottenuto il token di accesso, puoi generare l’URL che ti registra nella console AWS e punta direttamente al bucket [!DNL Amazon S3] desiderato.

```py
from urllib.parse import quote
 
# Define the S3 bucket and folder path you want to access
bucket_name = "your-bucket-name"
bucket_path = "your-bucket-folder"
 
# Construct the destination URL
destination_url = f"https://s3.console.aws.amazon.com/s3/buckets/{bucket_name}?prefix={bucket_path}/&tab=objects"
 
# Create the final sign-in URL
signin_url = f"https://signin.aws.amazon.com/federation?Action=login&Issuer=YourAppName&Destination={quote(destination_url)}&SigninToken={signin_token}"
 
print(f"Sign-in URL: {signin_url}")
```

#### Accedere alla console AWS

Infine, passa all&#39;URL generato per accedere direttamente alla console AWS con le tue credenziali [!DNL Data Landing Zone], che forniscono l&#39;accesso a una cartella specifica all&#39;interno di un bucket [!DNL Amazon S3]. L’URL di accesso ti porterà direttamente a tale cartella, assicurandoti di visualizzare e gestire solo i dati consentiti.

## Connetti [!DNL Data Landing Zone] a Experience Platform

La documentazione seguente fornisce informazioni su come portare dati dal contenitore [!DNL Data Landing Zone] a Adobe Experience Platform utilizzando le API o l&#39;interfaccia utente.

### Utilizzo delle API

- [Crea una connessione di origine  [!DNL Data Landing Zone]  tramite l&#39;API del servizio Flusso](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Creare un flusso di dati per un’origine di archiviazione cloud utilizzando l’API del servizio Flusso](../../tutorials/api/collect/cloud-storage.md)

### Utilizzo dell’interfaccia utente

- [Connetti [!DNL Data Landing Zone] a Platform tramite l&#39;interfaccia utente](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Creare un flusso di dati per una connessione all’archiviazione cloud nell’interfaccia utente](../../tutorials/ui/dataflow/batch/cloud-storage.md)

>[!IMPORTANT]
>
>I collegamenti privati non sono attualmente supportati per la connessione ad Experience Platform tramite [!DNL Data Landing Zone]. Gli unici metodi supportati per l&#39;accesso sono i metodi elencati [qui](#manage-the-contents-of-your-data-landing-zone).

