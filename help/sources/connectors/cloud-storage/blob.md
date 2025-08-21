---
title: Panoramica del connettore Source BLOB di Azure
description: Scopri come collegare l’account BLOB di Azure ad Experience Platform
exl-id: 62adc74f-3570-42c7-9ae6-3ddbc09eccc7
source-git-commit: 8e932a25026bef2b785cfddfb8b668b1dd47eb0d
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 0%

---

# Origine [!DNL Azure Blob Storage]

[!DNL Azure Blob Storage] è un servizio di archiviazione degli oggetti basato su cloud fornito da [!DNL Microsoft Azure]. È progettato per memorizzare grandi quantità di dati non strutturati, ad esempio testo, immagini, video, backup e registri. È possibile utilizzare [!DNL Azure Blob Storage] per archiviare e gestire grandi quantità di dati non strutturati come documenti, immagini, video e file audio. È ideale per il backup e l&#39;archiviazione dei dati, il supporto del disaster recovery e la gestione dei carichi di lavoro dei big data per l&#39;analisi.

Utilizza l&#39;origine [!DNL Azure Blob Storage] per connettere il tuo account e acquisire i dati da [!DNL Azure Blob Storage] a Adobe Experience Platform.

## Prerequisiti {#prerequisites}

Leggere le sezioni seguenti per completare la configurazione dei prerequisiti prima di connettere l&#39;account [!DNL Azure Blob Storage] ad Experience Platform.

### Indirizzo IP inserisco nell&#39;elenco Consentiti

Prima di collegare le origini a Experience Platform, è necessario aggiungere al elenco Consentiti di indirizzi IP specifici per l’area geografica. Per ulteriori informazioni, consulta la guida su [inserire nell&#39;elenco Consentiti gli indirizzi IP per connettersi ad Experience Platform](../../ip-address-allow-list.md).

>[!IMPORTANT]
>
>L&#39;origine [!DNL Azure Blob] non supporta la connettività della stessa area ad Experience Platform. Se l&#39;istanza di [!DNL Azure] utilizza la stessa area di rete di Experience Platform, non è possibile stabilire una connessione alle origini di Experience Platform. Attualmente, è supportata solo la connettività tra aree geografiche.

### Vincoli di denominazione per file e directory

Di seguito è riportato un elenco di vincoli di cui è necessario tenere conto per la denominazione del file di archiviazione cloud o della directory.

- I nomi dei componenti di directory e file non possono superare i 255 caratteri.
- I nomi di file e directory non possono terminare con una barra (`/`). Se fornito, verrà rimosso automaticamente.
- I seguenti caratteri URL riservati devono essere correttamente preceduti dall&#39;escape: `! ' ( ) ; @ & = + $ , % # [ ]`
- I seguenti caratteri non sono consentiti: `" \ / : | < > * ?`.
- Caratteri di percorso URL non validi non consentiti. I punti di codice come `\uE000`, sebbene validi nei nomi di file NTFS, non sono caratteri Unicode validi. Inoltre, alcuni caratteri ASCII o Unicode, come i caratteri di controllo (da 0x00 a 0x1F, \u0081, ecc.), non sono consentiti. Per le regole che regolano le stringhe Unicode in HTTP/1.1, vedere [RFC 2616, Sezione 2.2: Regole di base](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Non sono consentiti i seguenti nomi di file: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carattere punto (.) e due caratteri punto (..).

### Autentica [!DNL Azure Blob Storage] in Experience Platform {#authentication}

È possibile connettere l&#39;account [!DNL Azure Blob Storage] ad Experience Platform utilizzando i seguenti tipi di autenticazione:

- **Autenticazione chiave account**: utilizza la chiave di accesso dell&#39;account di archiviazione per autenticare e connettersi all&#39;account [!DNL Azure Blob Storage].
- **Firma di accesso condiviso (SAS)**: utilizza un URI SAS per fornire accesso delegato e limitato nel tempo alle risorse nell&#39;account [!DNL Azure Blob Storage].
- **Autenticazione basata sull&#39;entità servizio**: utilizza un&#39;entità servizio Azure Active Directory (AAD) (ID client e segreto) per l&#39;autenticazione sicura nell&#39;account di archiviazione BLOB di Azure.

>[!BEGINTABS]

>[!TAB Autenticazione chiave account]

Immetti i valori per le credenziali seguenti per connettere l&#39;account [!DNL Azure Blob Storage] ad Experience Platform utilizzando l&#39;autenticazione della chiave dell&#39;account.

| Credenziali | Descrizione |
| --- | --- |
| `connectionString` | Stringa di connessione [!DNL Azure Blob Storage] per l&#39;account di archiviazione. Questa stringa contiene le informazioni necessarie per autenticare e connettersi all&#39;istanza [!DNL Azure Blob Storage]. Esempio di formato: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY};EndpointSuffix=core.windows.net` |
| `container` | Nome del contenitore [!DNL Azure Blob Storage] in cui sono archiviati i file di dati. Un contenitore organizza un set di BLOB, simile a una directory in un file system. |
| `folderPath` | Percorso all’interno del contenitore specificato in cui si trovano i file. Si tratta di un percorso di sottodirectory facoltativo (cartella virtuale) all’interno del contenitore. Se questo campo viene lasciato vuoto, viene utilizzata la directory principale del contenitore. |
| `connectionSpec.id` | L&#39;ID della specifica di connessione restituisce le proprietà del connettore di origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Azure Blob Storage]: `4c10e202-c428-4796-9208-5f1f5732b1cf`. **Nota**: queste credenziali sono necessarie solo per la connessione tramite l&#39;API [!DNL Flow Service]. |

Per ulteriori informazioni sull&#39;utilizzo dell&#39;autenticazione della chiave dell&#39;account con [!DNL Azure Blob Storage], leggere la [Guida all&#39;autenticazione di Microsoft Azure](https://learn.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage?tabs=data-factory#account-key-authentication) ufficiale.

>[!TAB Firma di accesso condiviso]

Immetti i valori per le credenziali seguenti per connettere l&#39;account [!DNL Azure Blob Storage] ad Experience Platform utilizzando la firma di accesso condiviso.

| Credenziali | Descrizione |
| --- | --- |
| `SasURI` | URI della firma di accesso condiviso che è possibile utilizzare come tipo di autenticazione alternativo per connettere l&#39;account. Schema URI SAS: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}`. Per ulteriori informazioni, vedere il documento [!DNL Azure] in [URI di firma di accesso condiviso](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `container` | Nome del contenitore [!DNL Azure Blob Storage] in cui sono archiviati i file di dati. Un contenitore organizza un set di BLOB, simile a una directory in un file system. |
| `folderPath` | Percorso all’interno del contenitore specificato in cui si trovano i file. Si tratta di un percorso di sottodirectory facoltativo (cartella virtuale) all’interno del contenitore. Se questo campo viene lasciato vuoto, viene utilizzata la directory principale del contenitore. |
| `connectionSpec.id` | L&#39;ID della specifica di connessione restituisce le proprietà del connettore di origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Azure Blob Storage]: `4c10e202-c428-4796-9208-5f1f5732b1cf`. **Nota**: queste credenziali sono necessarie solo per la connessione tramite l&#39;API [!DNL Flow Service]. |

Per ulteriori informazioni sull&#39;utilizzo della firma di accesso condiviso con [!DNL Azure Blob Storage], leggere la [Guida all&#39;autenticazione di Microsoft Azure](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication) ufficiale.

>[!TAB Autenticazione basata su entità servizio]

Specificare i valori per le credenziali seguenti per connettere l&#39;account [!DNL Azure Blob Storage] ad Experience Platform utilizzando l&#39;autenticazione basata sull&#39;entità servizio.

| Credenziali | Descrizione |
| --- | --- |
| `serviceEndpoint` | L&#39;URL dell&#39;endpoint dell&#39;account [!DNL Azure Blob Storage]. In genere nel formato: `https://{ACCOUNT_NAME}.blob.core.windows.net`. |
| `accountKind` | Il tipo del tuo account [!DNL Azure Blob Storage]. I valori comuni includono `Storage` (finalità generale V1), `StorageV2` (finalità generale V2), `BlobStorage` e `BlockBlobStorage`. |
| `servicePrincipalId` | ID client/applicazione dell&#39;entità servizio Azure Active Directory (AAD) utilizzata per l&#39;autenticazione. |
| `servicePrincipalKey` | Il segreto client o la password associata all&#39;entità servizio Azure. |
| `tenant` | ID tenant di Azure Active Directory (AAD) in cui è registrata l&#39;entità servizio. |
| `container` | Nome del contenitore Archiviazione BLOB di Azure in cui sono archiviati i file di dati. |
| `folderPath` | Percorso all’interno del contenitore specificato in cui si trovano i file. Si tratta di un percorso di sottodirectory facoltativo (cartella virtuale) all’interno del contenitore. Se questo campo viene lasciato vuoto, viene utilizzata la directory principale del contenitore. |
| `connectionSpec.id` | L&#39;ID della specifica di connessione restituisce le proprietà del connettore di origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per l&#39;archiviazione BLOB di Azure: `4c10e202-c428-4796-9208-5f1f5732b1cf`. **Nota**: queste credenziali sono necessarie solo per la connessione tramite l&#39;API [!DNL Flow Service]. |

Per ulteriori informazioni sull&#39;utilizzo dell&#39;autenticazione basata sull&#39;entità servizio con [!DNL Azure Blob Storage], leggere la [Guida all&#39;autenticazione di Microsoft Azure](https://learn.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage?tabs=data-factory#service-principal-authentication) ufficiale.

>[!ENDTABS]

## Connetti [!DNL Azure Blob Storage] a [!DNL Experience Platform]

La documentazione seguente fornisce informazioni su come collegare BLOB di Azure a Adobe Experience Platform utilizzando le API o l’interfaccia utente:

### Utilizzo delle API

- [Connetti [!DNL Azure Blob Storage] ad Experience Platform](../../tutorials/api/create/cloud-storage/blob.md)
- [Esplorare la struttura dati e il contenuto di un’origine di archiviazione cloud utilizzando l’API del servizio Flusso](../../tutorials/api/explore/cloud-storage.md)
- [Creare un flusso di dati per un’origine di archiviazione cloud utilizzando l’API del servizio Flusso](../../tutorials/api/collect/cloud-storage.md)

### Utilizzo dell’interfaccia utente

- [Connetti [!DNL Azure Blob Storage] ad Experience Platform](../../tutorials/ui/create/cloud-storage/blob.md)
- [Creare un flusso di dati per una connessione all’archiviazione cloud nell’interfaccia utente](../../tutorials/ui/dataflow/batch/cloud-storage.md)
