---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Origine della zona di destinazione dati
description: Scopri come collegare Data Landing Zone a Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: d57060ddeed64d3863f71ac1ea34ccc5c97265ea
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

>[!IMPORTANT]
>
>Questa pagina è specifica per [!DNL Data Landing Zone] *sorgente* connettore in Experience Platform. Per informazioni sulla connessione al [!DNL Data Landing Zone] *destinazione* connettore, fare riferimento al [[!DNL Data Landing Zone] pagina della documentazione di destinazione](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] è un [!DNL Azure Blob] con il provisioning di Adobe Experience Platform, ti consente di accedere a una struttura di archiviazione dei file sicura e basata su cloud per inserire i file in Platform. Puoi accedervi [!DNL Data Landing Zone] contenitore per sandbox e il volume totale di dati in tutti i contenitori è limitato al totale dei dati forniti con la licenza Platform Products and Services. Tutti i clienti di Platform e dei relativi servizi applicativi, ad esempio [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services], e [!DNL Adobe Real-Time Customer Data Platform] dispongono di un [!DNL Data Landing Zone] contenitore per sandbox. Puoi leggere e scrivere i file nel contenitore tramite [!DNL Azure Storage Explorer] o dall&#39;interfaccia della riga di comando.

[!DNL Data Landing Zone] supporta l&#39;autenticazione basata su SAS e i relativi dati sono protetti con [!DNL Azure Blob] meccanismi di sicurezza dello stoccaggio a riposo e in transito. L&#39;autenticazione basata su SAS consente di accedere in modo sicuro al [!DNL Data Landing Zone] tramite una connessione Internet pubblica. Non sono necessarie modifiche di rete per accedere al [!DNL Data Landing Zone] Contenitore, che significa che non è necessario configurare elenchi consentiti o configurazioni per più aree geografiche per la rete. Platform impone una scadenza di sette giorni su tutti i file caricati in un [!DNL Data Landing Zone] contenitore. Tutti i file vengono eliminati dopo sette giorni.

## Vincoli di denominazione per file e directory

Di seguito è riportato un elenco di vincoli di cui è necessario tenere conto per la denominazione dei file o delle directory di archiviazione cloud.

- I nomi dei componenti di directory e file non possono superare i 255 caratteri.
- I nomi di file e directory non possono terminare con una barra (`/`). Se fornito, verrà rimosso automaticamente.
- I seguenti caratteri URL riservati devono avere un escape corretto: `! ' ( ) ; @ & = + $ , % # [ ]`
- I seguenti caratteri non sono consentiti: `" \ / : | < > * ?`.
- Caratteri di percorso URL non validi non consentiti. Punti di codice come `\uE000`, anche se valido nei nomi di file NTFS, non è costituito da caratteri Unicode validi. Inoltre, alcuni caratteri ASCII o Unicode, come i caratteri di controllo (ad esempio `0x00` a `0x1F`, `\u0081`e così via), non sono consentiti. Per le regole che disciplinano le stringhe Unicode in HTTP/1.1, consulta [RFC 2616, sezione 2.2: regole di base](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Non sono consentiti i seguenti nomi di file: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carattere punto (.) e due caratteri punto (..).

## Gestisci i contenuti del tuo [!DNL Data Landing Zone]

È possibile utilizzare [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/) per gestire il contenuto del [!DNL Data Landing Zone] contenitore.

In [!DNL Azure Storage Explorer] UI, seleziona l’icona di connessione nell’area di navigazione a sinistra. Il **Seleziona risorsa** viene visualizzata una finestra che fornisce le opzioni per la connessione. Seleziona **[!DNL Blob container]** per connettersi a [!DNL Data Landing Zone].

![select-resource](../../images/tutorials/create/dlz/select-resource.png)

Quindi, seleziona **URL firma di accesso condiviso (SAS)** come metodo di connessione e quindi selezionare **Successivo**.

![select-connection-method](../../images/tutorials/create/dlz/select-connection-method.png)

Dopo aver selezionato il metodo di connessione, devi fornire un **nome visualizzato** e **[!DNL Blob]URL SAS contenitore** che corrisponde al tuo [!DNL Data Landing Zone] contenitore.

>[!TIP]
>
>Puoi recuperare [!DNL Data Landing Zone] credenziali dal catalogo delle origini nell’interfaccia utente di Platform.

Fornisci [!DNL Data Landing Zone] URL SAS, quindi selezionare **Successivo**

![enter-connection-info](../../images/tutorials/create/dlz/enter-connection-info.png)

Il **Riepilogo** viene visualizzata una finestra che fornisce una panoramica delle impostazioni, incluse informazioni [!DNL Blob] endpoint e autorizzazioni. Quando è pronto, seleziona **Connetti**.

![riepilogo](../../images/tutorials/create/dlz/summary.png)

Una connessione corretta aggiorna il tuo [!DNL Azure Storage Explorer] Interfaccia utente con [!DNL Data Landing Zone] contenitore.

![dlz-user-container](../../images/tutorials/create/dlz/dlz-user-container.png)

Con [!DNL Data Landing Zone] contenitore connesso a [!DNL Azure Storage Explorer], ora puoi iniziare a caricare i file sul tuo [!DNL Data Landing Zone] contenitore. Per caricare, seleziona **Carica** e quindi seleziona **Carica file**.

![caricare](../../images/tutorials/create/dlz/upload.png)

Dopo aver selezionato il file da caricare, devi identificare [!DNL Blob] digita che desideri caricare come e la directory di destinazione desiderata. Al termine, seleziona **Carica**.

| [!DNL Blob] tipi | Descrizione |
| --- | --- |
| Blocca [!DNL Blob] | Blocca [!DNL Blobs] sono ottimizzate per caricare grandi quantità di dati in modo efficiente. Blocca [!DNL Blobs] sono l’opzione predefinita per [!DNL Data Landing Zone]. |
| Aggiungi [!DNL Blob] | Aggiungi [!DNL Blobs] sono ottimizzate per aggiungere dati alla fine del file. |

![upload-files](../../images/tutorials/create/dlz/upload-files.png)

## Carica i file nel tuo [!DNL Data Landing Zone] utilizzo dell’interfaccia della riga di comando

Puoi anche utilizzare l’interfaccia della riga di comando del dispositivo e accedere ai file di caricamento sul tuo [!DNL Data Landing Zone].

### Caricare un file con Bash

Nell&#39;esempio seguente vengono utilizzati Bash e cURL per caricare un file in un [!DNL Data Landing Zone] con [!DNL Azure Blob Storage] API REST:

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

L’esempio che segue utilizza [!DNL Microsoft's] Python v12 SDK per caricare un file in una [!DNL Data Landing Zone]:

>[!TIP]
>
>Nell&#39;esempio seguente viene utilizzato l&#39;URI SAS completo per la connessione a un [!DNL Azure Blob] Contenitore, puoi utilizzare altri metodi e operazioni per l’autenticazione. Vedi questo [[!DNL Microsoft] documento sull’SDK Python v12](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-python) per ulteriori informazioni.

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

### Carica un file tramite [!DNL AzCopy]

L’esempio che segue utilizza [!DNL Microsoft's] [!DNL AzCopy] utilità per caricare un file in una [!DNL Data Landing Zone]:

>[!TIP]
>
>Mentre l’esempio seguente utilizza `copy` , puoi utilizzare altri comandi e opzioni per caricare un file nel tuo [!DNL Data Landing Zone], utilizzando [!DNL AzCopy]. Vedi questo [[!DNL Microsoft AzCopy] documento](https://docs.microsoft.com/en-us/azure/storage/common/storage-ref-azcopy?toc=/azure/storage/blobs/toc.json) per ulteriori informazioni.

```bat
set sasUri=<FULL SAS URI, PROPERLY ESCAPED>
set srcFilePath=<PATH TO LOCAL FILE(S); WORKS WITH WILDCARD PATTERNS>

azcopy copy "%srcFilePath%" "%sasUri%" --overwrite=true --recursive=true
```

## Connetti [!DNL Data Landing Zone] a [!DNL Platform]

La documentazione seguente fornisce informazioni su come estrarre i dati dal [!DNL Data Landing Zone] da contenitore a Adobe Experience Platform tramite API o l’interfaccia utente.

### Utilizzo delle API

- [Creare un [!DNL Data Landing Zone] connessione sorgente tramite l’API del servizio Flow](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Creare un flusso di dati per un’origine di archiviazione cloud utilizzando l’API del servizio Flusso](../../tutorials/api/collect/cloud-storage.md)

### Utilizzo dell’interfaccia utente

- [Connetti [!DNL Data Landing Zone] a Platform tramite l’interfaccia utente](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Creare un flusso di dati per una connessione all’archiviazione cloud nell’interfaccia utente](../../tutorials/ui/dataflow/batch/cloud-storage.md)
