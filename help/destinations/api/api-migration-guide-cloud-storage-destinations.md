---
solution: Experience Platform
title: Guida alla migrazione delle API per le destinazioni dell’archiviazione cloud
description: Scopri le modifiche nel flusso di lavoro per attivare le destinazioni di archiviazione cloud come parte della migrazione alle nuove schede di destinazione di archiviazione cloud con funzionalità aggiuntive.
type: Tutorial
exl-id: 4acaf718-794e-43a3-b8f0-9b19177a2bc0
source-git-commit: 07a91ef15075b6c438e85aecff12dfab704cc6a2
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 0%

---

# Guida alla migrazione delle API per le destinazioni dell’archiviazione cloud

>[!IMPORTANT]
>
>* La funzionalità descritta in questa pagina è disponibile per i clienti che hanno acquistato i pacchetti Real-Time CDP Prime e Ultimate. Per ulteriori informazioni, contatta il rappresentante del tuo Adobe.


## Contesto di migrazione {#migration-context}

Avvio [Ottobre 2022](/help/release-notes/2022/october-2022.md#new-or-updated-destinations), puoi utilizzare le nuove funzionalità di esportazione dei file per accedere a funzionalità di personalizzazione avanzate durante l’esportazione di file, ad Experience Platform:

* Aggiuntivo [opzioni di denominazione file](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).
* Possibilità di impostare intestazioni di file personalizzate nei file esportati tramite [nuovo passaggio di mappatura](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* Possibilità di selezionare [tipo di file](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options) del file esportato.
* Possibilità di [personalizzare la formattazione dei file di dati CSV esportati](/help/destinations/ui/batch-destinations-file-formatting-options.md).

Questa funzionalità è supportata dalle schede di archiviazione cloud beta elencate di seguito:

* [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

<!--

Commenting out the three net new cloud storage destinations

* [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)

-->

Tieni presente che attualmente nell’interfaccia utente di Experience Platform puoi visualizzare due schede di destinazione affiancate delle tre destinazioni. Di seguito sono riportati i [!DNL Amazon S3] destinazioni legacy e nuove. In tutti i casi, le schede contrassegnate con **Beta** sono le nuove schede di destinazione.

![Immagine delle due schede di destinazione Amazon S3 in una visualizzazione affiancata.](../assets/catalog/cloud-storage/amazon-s3/two-amazons3-destination-cards.png)

Anche se queste destinazioni con funzionalità avanzate sono state inizialmente offerte come versione beta, *Adobe sta ora spostando tutti i clienti Real-Time CDP nelle nuove destinazioni di archiviazione cloud*. Per i clienti che utilizzavano già [!DNL Amazon S3], [!DNL Azure Blob], o SFTP, significa che i flussi di dati esistenti verranno migrati alle nuove schede. Continua a leggere per ulteriori informazioni sulle modifiche specifiche come parte della migrazione.

## A chi si applica questa pagina {#who-this-applies-to}

Se utilizzi già il [API del servizio Flusso](https://developer.adobe.com/experience-platform-apis/references/destinations/) per esportare i profili nelle destinazioni dell’archiviazione cloud Amazon S3, Azure Blob o SFTP, questa guida alla migrazione API è applicabile al tuo caso.

Se gli script sono in esecuzione in [!DNL Amazon S3], [!DNL Azure Blob], o le posizioni di archiviazione cloud SFTP sopra i file esportati da Experience Platform, tieni presente che alcuni parametri stanno cambiando per quanto riguarda le specifiche di connessione e flusso delle nuove schede, nonché per quanto riguarda il passaggio di mappatura.

Ad esempio, se utilizzi uno script per filtrare i flussi di dati di destinazione in [!DNL Amazon S3] destinazione, in base alla specifica di connessione del [!DNL Amazon S3] destinazione, tieni presente che la specifica di connessione cambierà, pertanto dovrai aggiornare i filtri.

## Collegamenti alla documentazione pertinente {#relevant-documentation-links}

Questa sezione include il tutorial API pertinente e la documentazione di riferimento per la funzionalità avanzata di esportazione dei dati nelle destinazioni di archiviazione cloud.

<!--

TBD if we keep this link but will likely remove it

[Legacy API tutorial to export data to cloud storage destinations](/help/destinations/api/connect-activate-batch-destinations.md) (outdated, do not use anymore)

-->
* [Tutorial API per esportare segmenti nelle destinazioni di archiviazione cloud](/help/destinations/api/activate-segments-file-based-destinations.md)
* [Documentazione di riferimento API del servizio Flusso delle destinazioni](https://developer.adobe.com/experience-platform-apis/references/destinations/)

## Riepilogo delle modifiche non compatibili con le versioni precedenti {#summary-backwards-incompatible-changes}

Con la migrazione alle nuove destinazioni, tutti i flussi di dati esistenti vengono [!DNL Amazon S3], [!DNL Azure Blob]Alle destinazioni SFTP e, ora verranno assegnate nuove connessioni di destinazione e connessioni di base. Anche il passaggio di mappatura del profilo cambia. Le modifiche non compatibili con le versioni precedenti sono riepilogate nelle sezioni seguenti per ciascuna destinazione. Visualizza anche [glossario delle destinazioni](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) per ulteriori informazioni sui termini del diagramma seguente.

![Immagine panoramica della guida alla migrazione](/help/destinations/assets/api/api-migration-guide/migration-guide-diagram.png)

### Modifiche non compatibili con le versioni precedenti di [!DNL Amazon S3] destinazione {#changes-amazon-s3-destination}

Le modifiche non compatibili con le versioni precedenti per gli utenti API sono un aggiornamento `connection spec ID` e `flow spec ID` come indicato nella tabella seguente:

| [!DNL Amazon S3] | Legacy | Nuova |
|---------|----------|---------|
| Specifica di flusso | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 1a0514a6-33d4-4c7f-aff8-594799c47549 |
| Specifica di connessione | 4890fc95-5a1f-4983-94bb-e060c08e3f81 | 4fce964d-3f37-408f-9778-e597338a21ee |

Visualizza gli esempi completi di connessione di base e di connessione di destinazione legacy e nuova per [!DNL Amazon S3] nelle schede seguenti. Parametri necessari per creare connessioni di base per [!DNL Amazon S3] le destinazioni non cambiano.

Analogamente, non vi sono modifiche incompatibili con le versioni precedenti nei parametri necessari per creare connessioni target.

>[!BEGINTABS]

>[!TAB Connessione di base legacy e connessione di destinazione]

+++Visualizza legacy [!DNL base connection] per [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "amazon-s3",
  "connectionSpec": {
    "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Access Key",
    "params": {
      "authorizedDate": "2022-10-26",
      "s3SecretKey": "<your-secret-key>",
      "s3AccessKey": "<your-access-key>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"640418e2-0000-0200-0000-6359b9ef0000\"",
  "etag": "\"640418e2-0000-0200-0000-6359b9ef0000\""
}
```

+++

+++Visualizza legacy [!DNL target connection] per [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="12"}
{
  ...
  "name": "test 121",
  "baseConnectionId": "ee86d122-10d3-434b-81c7-7252e4d747a7",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
    "version": "1.0"
  },
  "params": {
    "mode": "S3",
    "path": "testpath",
    "bucketName": "test"
  },
  "version": "\"1609cd86-0000-0200-0000-63892cbb0000\"",
  "etag": "\"1609cd86-0000-0200-0000-63892cbb0000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "ee86d122-10d3-434b-81c7-7252e4d747a7",
      "connectionSpec": {
        "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB Nuova connessione di base e connessione di destinazione]

+++Visualizza nuovo [!DNL base connection] per [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "Amazon S3",
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Access Key",
    "params": {
      "authorizedDate": "2022-10-26",
      "s3SecretKey": "<your-secret-key>",
      "s3AccessKey": "<your-access-key>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"3708da21-0000-0200-0000-638940b10000\"",
  "etag": "\"3708da21-0000-0200-0000-638940b10000\""
}
```

+++

+++Visualizza nuovo [!DNL target connection] per [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="12, 16-27"}
{
  ...
  "name": "test 121",
  "baseConnectionId": "d114c86f-fd47-4bb6-846c-cb1d15a00fe9",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "Server-to-server",
    "path": "testpath",
    "bucketName": "test"
  },
  "version": "\"1b0985c6-0000-0200-0000-638940b10000\"",
  "etag": "\"1b0985c6-0000-0200-0000-638940b10000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "d114c86f-fd47-4bb6-846c-cb1d15a00fe9",
      "connectionSpec": {
        "id": "4fce964d-3f37-408f-9778-e597338a21ee",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### Modifiche non compatibili con le versioni precedenti di [!DNL Azure Blob] destinazione {#changes-azure-blob-destination}

Le modifiche non compatibili con le versioni precedenti per gli utenti API sono un aggiornamento `connection spec ID` e `flow spec ID` come indicato nella tabella seguente:

| [!DNL Azure Blob] | Legacy | Nuova |
|---------|----------|---------|
| Specifica di flusso | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 752d422f-b16f-4f0d-b1c6-26e448e3b388 |
| Specifica di connessione | e258278b-a4cf-43ac-b158-4fa0ca0d948b | 6d6b59bf-fb58-4107-9064-4d246c0e5bb2 |

Visualizza gli esempi completi di connessione di base e di connessione di destinazione legacy e nuova per [!DNL Azure Blob] nelle schede seguenti. I parametri necessari per creare connessioni di base per le destinazioni BLOB di Azure non cambiano.

Analogamente, non vi sono modifiche incompatibili con le versioni precedenti nei parametri necessari per creare connessioni target.

>[!BEGINTABS]

>[!TAB Connessione di base legacy e connessione di destinazione]

+++Visualizza legacy [!DNL base connection] per [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "azure-blob",
  "connectionSpec": {
    "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "authorizedDate": "2022-06-02",
      "connectionString": "<your-connection-string>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  }, 
  "version": "\"d000d23c-0000-0200-0000-6299051c0000\"",
  "etag": "\"d000d23c-0000-0200-0000-6299051c0000\""
}
```

+++

+++Visualizza legacy [!DNL target connection] per [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="13"}
{
  ...
  "name": "v1",
  "description": "v2",
  "baseConnectionId": "d10fcecf-9963-4062-820c-0f878be98805",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
    "version": "1.0"
  },
  "params": {
    "mode": "AZURE_BLOB",
    "container": "usdasda",
    "path": "v3"
  },
  "version": "\"cb0468ba-0000-0200-0000-631ab0790000\"",
  "etag": "\"cb0468ba-0000-0200-0000-631ab0790000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "d10fcecf-9963-4062-820c-0f878be98805",
      "connectionSpec": {
        "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB Nuova connessione di base e connessione di destinazione]

+++Visualizza nuovo [!DNL base connection] per [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "Azure Blob Storage",
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "authorizedDate": "2022-06-02",      
      "connectionString": "<your-connection-string>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"4008a892-0000-0200-0000-6389890d0000\"",
  "etag": "\"4008a892-0000-0200-0000-6389890d0000\""
}
```

+++

+++Visualizza nuovo [!DNL target connection] per [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="13, 17-25"}
{
  ...
  "name": "v1",
  "description": "v2",
  "baseConnectionId": "1329d183-a3ee-4454-ab3f-e2388082bf29",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "Server-to-server",
    "container": "usdasda",
    "path": "v3"
  },
  "version": "\"5509fe3f-0000-0200-0000-638a28880000\"",
  "etag": "\"5509fe3f-0000-0200-0000-638a28880000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "1329d183-a3ee-4454-ab3f-e2388082bf29",
      "connectionSpec": {
        "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### Modifiche alla destinazione SFTP non compatibili con le versioni precedenti {#changes-sftp-destination}

Le modifiche non compatibili con le versioni precedenti per gli utenti API sono un aggiornamento `connection spec ID` e `flow spec ID` come indicato nella tabella seguente:

| SFTP | Legacy | Nuova |
|---------|----------|---------|
| Specifica di flusso | 71471eba-b620-49e4-90fd-23f1fa0174d8 | fd36aaa4-bf2b-43fb-9387-43785eeeeb799 |
| Specifica di connessione | 64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0 | 36965a81-b1c6-401b-99f8-22508f1e6a26 |

Oltre al flusso aggiornato e alle specifiche di connessione di cui sopra, vengono apportate modifiche ai parametri necessari per la creazione delle connessioni di base SFTP.

* In precedenza, la connessione di base per le destinazioni SFTP richiedeva una `host` parametro. Questo parametro è stato rinominato in `domain`.

Visualizza gli esempi completi di connessione di base nuova e legacy e di connessione di destinazione per SFTP nelle schede seguenti, evidenziando le righe che cambiano. I parametri necessari per creare connessioni di destinazione per le destinazioni SFTP non cambiano.

>[!BEGINTABS]

>[!TAB Connessione di base legacy e connessione di destinazione]

+++Visualizza legacy [!DNL base connection] per SFTP - autenticazione tramite password

```json {line-numbers="true" start-line="1" highlight="5,15"}
{
  ...
  "name": "sftp",
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "password": "<your-password>",
      "userName": "DPID12345",
      "host": "ftp-out.demdex.com"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"d000013c-0000-0200-0000-629903bd0000\"",
  "etag": "\"d000013c-0000-0200-0000-629903bd0000\""
}
```

+++

+++Visualizza legacy [!DNL base connection] per [!DNL SFTP - SSH key] autenticazione

```json {line-numbers="true" start-line="1" highlight="5,15"}
{
  ...
  "name": "sftp",
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "sshKey": "<your-ssh-key>",
      "userName": "DPID12345",
      "port": 22
      "domain": "ftp-out.demdex.com"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"d000013c-0000-0200-0000-629903bd0000\"",
  "etag": "\"d000013c-0000-0200-0000-629903bd0000\""
}
```

+++

+++Visualizza legacy [!DNL target connection] per SFTP

```json {line-numbers="true" start-line="1" highlight="13"}
{
  ...
  "name": "test sftp 6/2",
  "description": "",
  "baseConnectionId": "e6f3a300-0bf7-4755-b7f8-308dc2a99133",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "params": {
    "mode": "FTP",
    "remotePath": "test"
  },
  "version": "\"8503ab91-0000-0200-0000-629903ce0000\"",
  "etag": "\"8503ab91-0000-0200-0000-629903ce0000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "e6f3a300-0bf7-4755-b7f8-308dc2a99133",
      "connectionSpec": {
        "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB Nuova connessione di base e connessione di destinazione]

+++Visualizza nuovo [!DNL base connection] per [!DNL SFTP - password authentication]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "SFTP",
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "SFTP with Password",
    "params": {
      "authorizedDate": "2022-06-02",
      "domain": "ftp-out.demdex.com",
      "username": "DPID12345",
      "password": "<your-password>",
      "port": 22      
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"420826cc-0000-0200-0000-638999a60000\"",
  "etag": "\"420826cc-0000-0200-0000-638999a60000\""
}
```

+++

+++Visualizza nuovo [!DNL base connection] per [!DNL SFTP - SSH key] autenticazione

```json {line-numbers="true" start-line="1" highlight="5,12"}
{
  ...
  "name": "SFTP",
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "domain": "ftp-out.demdex.com",
      "username": "DPID12345",
      "sshKey": "<your-ssh-key>",
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"420826cc-0000-0200-0000-638999a60000\"",
  "etag": "\"420826cc-0000-0200-0000-638999a60000\""
}
```

+++

+++Visualizza nuovo [!DNL target connection] per SFTP

```json {line-numbers="true" start-line="1" highlight="13, 17-25"}
{
  ...
  "name": "test sftp 6/2",
  "description": "",
  "baseConnectionId": "af63fbe1-45ff-4722-a9de-fbbe789dc7b0",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "FTP",
    "remotePath": "test"
  },
  "version": "\"5509b5cf-0000-0200-0000-638a2ab60000\"",
  "etag": "\"5509b5cf-0000-0200-0000-638a2ab60000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "af63fbe1-45ff-4722-a9de-fbbe789dc7b0",
      "connectionSpec": {
        "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### Modifiche non compatibili con le versioni precedenti comuni a [!DNL Amazon S3], [!DNL Azure Blob]Destinazioni SFTP e {#changes-all-destinations}

Il passaggio del selettore di profilo in tutte e tre le destinazioni viene sostituito da un passaggio di mappatura che consente di rinominare, se necessario, le intestazioni di colonna nei file esportati. Osserva l’immagine affiancata seguente con il vecchio passaggio del selettore di attributi a sinistra e il nuovo passaggio di mappatura a destra.

![Immagine panoramica della guida alla migrazione](/help/destinations/assets/api/api-migration-guide/old-and-new-mapping-step.png)

Osserva come `profileSelectors` negli esempi precedenti viene sostituito dal nuovo `profileMapping` oggetto.

Trova informazioni complete sulla configurazione di `profileMapping` oggetto in [Tutorial API per esportare i dati nelle destinazioni di archiviazione cloud](/help/destinations/api/activate-segments-file-based-destinations.md#attribute-and-identity-mapping).

>[!BEGINTABS]

>[!TAB Parametri di trasformazione precedenti]

+++Visualizza un esempio di parametri di trasformazione precedenti

```json{line-numbers="true" start-line="1" highlight="4-40, 45-53"}
{
  "segmentSelectors": { // shortened for brevity since nothing changes in the segment selectors
  },  
  "profileSelectors": {
    "selectors": [
      {
        "type": "JSON_PATH",
        "value": {
          "path": "CORE",
          "operator": "EXISTS",
          "mapping": {
            "sourceType": "text/x.schema-path",
            "source": "CORE",
            "destination": "CORE",
            "identity": false,
            "primaryIdentity": false,
            "functionVersion": 0,
            "sourceAttribute": "CORE",
            "destinationXdmPath": "CORE"
          },
          "identity": {
            "namespace": "CORE"
          }
        }
      },
      ...
      {
        "type": "JSON_PATH",
        "value": {
          "path": "segmentMembership.status",
          "operator": "EXISTS",
          "mapping": {
            "sourceType": "text/x.schema-path",
            "source": "segmentMembership.status",
            "destination": "segmentMembership.status",
            "identity": false,
            "primaryIdentity": false,
            "functionVersion": 0,
            "sourceAttribute": "segmentMembership.status",
            "destinationXdmPath": "segmentMembership.status"
          }
        }
      }
    ],
    "mandatoryFields": [
      "CORE",
      "person.name.lastName",
      "personalEmail.address"
    ],
    "primaryFields": [
      {
        "identityNamespace": "CORE",
        "fieldType": "IDENTITY"
      }
    ]
  }
}
```

+++

>[!TAB Nuovi parametri di trasformazione]

+++Visualizza un esempio di parametri di trasformazione dopo la migrazione

Osserva nell’esempio di configurazione seguente come `profileSelectors` i campi sono stati sostituiti da `profileMapping` oggetto.

```json {line-numbers="true" start-line="1" highlight="4-12, 18-20"}
{
  "segmentSelectors": { // shortened for brevity since nothing changes in the segment selectors
  },  
  "mandatoryFields": [
    "CORE",
    "person_name_lastName",
    "personalEmail_address"
  ],
  "primaryFields": [
    {
      "identityNamespace": "CORE",
      "fieldType": "IDENTITY"
    }
  ],
  "identityMapping": {
    "mappings": []
  },
  "profileMapping": {
    "mappingId": "40dfd952fe09498ba65145c7a5de3e07",
    "mappingVersion": 0
  },
  "attributeMapping": {}
}
```

+++

>[!ENDTABS]

## Timeline di migrazione e azioni {#timeline-and-action-items}

Migrazione dei flussi di dati legacy alle nuove schede di destinazione per [!DNL Amazon S3], [!DNL Azure Blob], e le destinazioni SFTP si verificheranno non appena la tua organizzazione sarà pronta per la migrazione e non più tardi di **30 giugno 2023**.

Riceverai e-mail di promemoria da Adobe con l’avvicinarsi della data di migrazione. In preparazione, leggi la sezione Azioni di seguito per prepararti alla migrazione.

### Elementi azione {#action-items}

In preparazione della migrazione del [!DNL Amazon S3], [!DNL Azure Blob], e le destinazioni dell’archiviazione cloud SFTP nelle nuove schede, prepara l’aggiornamento degli script e delle chiamate API automatizzate come suggerito di seguito.

1. Aggiornare script o chiamate API automatizzate per qualsiasi [!DNL Amazon S3], [!DNL Azure Blob], o le destinazioni dell’archiviazione cloud SFTP entro il 30 giugno 2023. Tutte le chiamate o gli script API automatizzati che sfruttano le specifiche di connessione o di flusso legacy devono essere aggiornati alle nuove specifiche di connessione o di flusso.
2. Rivolgiti al rappresentante del tuo account Adobe quando gli script saranno stati aggiornati prima del 30 giugno.
3. Ad esempio, il `targetConnectionSpecId` può essere utilizzato come flag per determinare se il flusso di dati è stato migrato alla nuova scheda di destinazione. È possibile aggiornare gli script con un `if` condizione per esaminare le specifiche di connessione di destinazione legacy e aggiornate in `flow.inheritedAttributes.targetConnections[0].connectionSpec.id` e determinare se il flusso di dati è stato migrato. Puoi visualizzare gli ID delle specifiche di connessione nuovi e precedenti nelle sezioni specifiche di questa pagina per ogni destinazione.
4. Il team del tuo account Adobe riceverà ulteriori informazioni su quando verrà effettuata la migrazione dei flussi di dati.
5. Dopo il 30 giugno, tutti i flussi di dati verranno migrati. Tutti i flussi di dati esistenti avranno ora nuove entità di flusso (specifiche di connessione, specifiche di flusso, connessioni di base e connessioni di destinazione). Qualsiasi script o chiamata API sul tuo lato che utilizzi le entità di flusso legacy cesserà di funzionare.

## Altre considerazioni sulla migrazione {#other-considerations}

Tieni presente che non vi è alcun impatto sulla pianificazione esistente per le esportazioni durante o dopo la migrazione.

## Passaggi successivi {#next-steps}

Una volta letta questa pagina, saprai se è necessario intraprendere un’azione in preparazione alla migrazione delle destinazioni dell’archiviazione cloud. Saprai anche quali pagine della documentazione fare riferimento quando configuri flussi di lavoro basati su API per esportare file da Experience Platform nelle destinazioni di archiviazione cloud preferite. Ora puoi visualizzare l’esercitazione API per [esportare i dati nelle destinazioni dell’archiviazione cloud](/help/destinations/api/activate-segments-file-based-destinations.md).
