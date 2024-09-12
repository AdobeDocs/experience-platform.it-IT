---
title: Acquisizione di dati crittografati
description: Scopri come acquisire i file crittografati tramite le origini batch di archiviazione cloud utilizzando l’API.
exl-id: 83a7a154-4f55-4bf0-bfef-594d5d50f460
source-git-commit: 9a5599473f874d86e2b3c8449d1f4d0cf54b672c
workflow-type: tm+mt
source-wordcount: '1806'
ht-degree: 3%

---

# Acquisizione di dati crittografati

Puoi acquisire i file di dati crittografati in Adobe Experience Platform utilizzando origini batch di archiviazione cloud. Con l’acquisizione di dati crittografati, puoi sfruttare meccanismi di crittografia asimmetrica per trasferire in modo sicuro i dati batch in Experience Platform. Attualmente, i meccanismi di crittografia asimmetrica supportati sono PGP e GPG.

Il processo di acquisizione dei dati crittografati è il seguente:

1. [Creare una coppia di chiavi di crittografia utilizzando le API Experience Platform](#create-encryption-key-pair). La coppia di chiavi di crittografia è costituita da una chiave privata e da una chiave pubblica. Una volta creata, puoi copiare o scaricare la chiave pubblica, insieme all’ID della chiave pubblica e all’ora di scadenza corrispondenti. Durante questa procedura, la chiave privata verrà memorizzata da Experience Platform in un archivio protetto. **NOTA:** la chiave pubblica nella risposta è codificata in Base64 e deve essere decodificata prima di utilizzare.
2. Utilizza la chiave pubblica per crittografare il file di dati che desideri acquisire.
3. Inserisci il file crittografato nell’archiviazione cloud.
4. Quando il file crittografato è pronto, [crea una connessione di origine e un flusso di dati per l&#39;origine dell&#39;archiviazione cloud](#create-a-dataflow-for-encrypted-data). Durante il passaggio di creazione del flusso, devi fornire un parametro `encryption` e includere l&#39;ID della chiave pubblica.
5. L’Experience Platform recupera la chiave privata dall’archivio protetto per decrittografare i dati al momento dell’acquisizione.

>[!IMPORTANT]
>
>La dimensione massima di un singolo file crittografato è di 1 GB. Ad esempio, puoi acquisire dati per un valore di 2 GB in una singola esecuzione del flusso di dati; tuttavia, qualsiasi singolo file in tali dati non può superare 1 GB.

In questo documento vengono descritti i passaggi necessari per generare una coppia di chiavi di crittografia per crittografare i dati e acquisirli per l’Experience Platform utilizzando origini di archiviazione cloud.

## Introduzione {#get-started}

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
   * [Origini archiviazione cloud](../api/collect/cloud-storage.md): crea un flusso di dati per portare all&#39;Experience Platform i dati batch dall&#39;origine archiviazione cloud.
* [Sandbox](../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../landing/api-guide.md).

### Estensioni di file supportate per i file crittografati {#supported-file-extensions-for-encrypted-files}

L’elenco delle estensioni di file supportate per i file crittografati è:

* .csv
* .tsv
* .json
* parquet
* .csv.gpg
* .tsv.gpg
* .json.gpg
* parquet, gpg
* .csv.pgp
* .tsv.pgp
* .json.pgp
* .parquet.pgp
* gpg
* .pgp

>[!NOTE]
>
>L’acquisizione di file crittografati in Adobe Experience Platform Sources supporta openPGP e non qualsiasi versione proprietaria specifica di PGP.

## Crea coppia di chiavi di crittografia {#create-encryption-key-pair}

>[!IMPORTANT]
>
>Le chiavi di crittografia sono specifiche per una data sandbox. Pertanto, se desideri acquisire i dati crittografati in una sandbox diversa all’interno della tua organizzazione, devi creare nuove chiavi di crittografia.

Il primo passaggio per l&#39;acquisizione di dati crittografati in Experience Platform consiste nel creare la coppia di chiavi di crittografia effettuando una richiesta POST all&#39;endpoint `/encryption/keys` dell&#39;API [!DNL Connectors].

**Formato API**

```http
POST /data/foundation/connectors/encryption/keys
```

**Richiesta**

+++Visualizza richiesta di esempio

La richiesta seguente genera una coppia di chiavi di crittografia utilizzando l’algoritmo di crittografia PGP.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' 
  -d '{
      "name": "acme-encryption",
      "encryptionAlgorithm": "PGP",
      "params": {
          "passPhrase": "{{PASSPHRASE}}"
      }
  }'
```

| Parametro | Descrizione |
| --- | --- |
| `name` | Nome della coppia di chiavi di crittografia. |
| `encryptionAlgorithm` | Tipo di algoritmo di crittografia in uso. I tipi di crittografia supportati sono `PGP` e `GPG`. |
| `params.passPhrase` | La passphrase fornisce un ulteriore livello di protezione per le chiavi di crittografia. Al momento della creazione, Experience Platform memorizza la passphrase in un archivio protetto diverso dalla chiave pubblica. Specificare una stringa non vuota come passphrase. |

+++

**Risposta**

+++Visualizza risposta di esempio

In caso di esito positivo, la risposta restituisce la chiave pubblica con codifica Base64, l’ID della chiave pubblica e l’ora di scadenza delle chiavi. Il tempo di scadenza viene impostato automaticamente su 180 giorni dopo la data di generazione della chiave. L’ora di scadenza non è attualmente configurabile.

```json
{
    ​"publicKey": "{PUBLIC_KEY}",
    ​"publicKeyId": "{PUBLIC_KEY_ID}",
    ​"expiryTime": "1684843168"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `publicKey` | La chiave pubblica viene utilizzata per crittografare i dati nell’archiviazione cloud. Questa chiave corrisponde alla chiave privata creata durante questo passaggio. Tuttavia, la chiave privata viene immediatamente recapitata all’Experience Platform. |
| `publicKeyId` | L’ID della chiave pubblica viene utilizzato per creare un flusso di dati e acquisire i dati di archiviazione cloud crittografati per Experience Platform. |
| `expiryTime` | L&#39;ora di scadenza definisce la data di scadenza della coppia di chiavi di crittografia. Questa data viene impostata automaticamente su 180 giorni dopo la data di generazione della chiave e viene visualizzata in formato timestamp unix. |

+++

### Recuperare le chiavi di crittografia {#retrieve-encryption-keys}

Per recuperare tutte le chiavi di crittografia dell&#39;organizzazione, eseguire una richiesta di GET all&#39;endpoint `/encryption/keys`=nt.

**Formato API**

```http
GET /data/foundation/connectors/encryption/keys
```

**Richiesta**

+++Visualizza richiesta di esempio

La richiesta seguente recupera tutte le chiavi di crittografia dell’organizzazione.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Risposta**

+++Visualizza risposta di esempio

In caso di esito positivo, la risposta restituisce l’algoritmo di crittografia, il nome, la chiave pubblica, l’ID della chiave pubblica, il tipo di chiave e la scadenza corrispondente delle chiavi.

```json
{
    "encryptionAlgorithm": "{ENCRYPTION_ALGORITHM}",
    "name": "{NAME}",
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "publicKey": "{PUBLIC_KEY}",
    "keyType": "{KEY_TYPE}",
    "expiryTime": "{EXPIRY_TIME}"
}
```

+++

### Recupera chiavi di crittografia per ID {#retrieve-encryption-keys-by-id}

Per recuperare un set specifico di chiavi di crittografia, effettuare una richiesta GET all&#39;endpoint `/encryption/keys` e fornire l&#39;ID della chiave pubblica come parametro di intestazione.

**Formato API**

```http
GET /data/foundation/connectors/encryption/keys/{PUBLIC_KEY_ID}
```

**Richiesta**

+++Visualizza richiesta di esempio

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys/{publicKeyId}' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Risposta**

+++Visualizza risposta di esempio

In caso di esito positivo, la risposta restituisce l’algoritmo di crittografia, il nome, la chiave pubblica, l’ID della chiave pubblica, il tipo di chiave e la scadenza corrispondente delle chiavi.

```json
{
    "encryptionAlgorithm": "{ENCRYPTION_ALGORITHM}",
    "name": "{NAME}",
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "publicKey": "{PUBLIC_KEY}",
    "keyType": "{KEY_TYPE}",
    "expiryTime": "{EXPIRY_TIME}"
}
```

+++

### Creare una coppia di chiavi gestite dal cliente {#create-customer-managed-key-pair}

Facoltativamente, puoi creare una coppia di chiavi per la verifica della firma per firmare e acquisire i dati crittografati.

Durante questa fase, devi generare la tua combinazione di chiave privata e chiave pubblica e quindi utilizzare la tua chiave privata per firmare i dati crittografati. Successivamente, devi codificare la chiave pubblica in Base64 e condividerla con Experience Platform affinché Platform possa verificare la firma.

### Condividi la chiave pubblica per Experience Platform

Per condividere la chiave pubblica, effettuare una richiesta POST all&#39;endpoint `/customer-keys` fornendo al contempo l&#39;algoritmo di crittografia e la chiave pubblica con codifica Base64.

**Formato API**

```http
POST /data/foundation/connectors/encryption/customer-keys
```

**Richiesta**

+++Visualizza richiesta di esempio

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/customer-keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' 
  -d '{
      "name": "acme-sign-verification-keys"
      "encryptionAlgorithm": {{ENCRYPTION_ALGORITHM}},       
      "publicKey": {{BASE_64_ENCODED_PUBLIC_KEY}},
      "params": {
          "passPhrase": {{PASS_PHRASE}}
      }
    }'
```

| Parametro | Descrizione |
| --- | --- |
| `encryptionAlgorithm` | Tipo di algoritmo di crittografia in uso. I tipi di crittografia supportati sono `PGP` e `GPG`. |
| `publicKey` | La chiave pubblica che corrisponde alle chiavi gestite dal cliente utilizzate per la firma del file crittografato. Questa chiave deve avere la codifica Base64. |

+++

**Risposta**

+++Visualizza risposta di esempio

```json
{    
  "publicKeyId": "e31ae895-7896-469a-8e06-eb9207ddf1c2" 
} 
```

| Proprietà | Descrizione |
| --- | --- |
| `publicKeyId` | Questo ID di chiave pubblica viene restituito in risposta alla condivisione della chiave gestita dal cliente con Experience Platform. Puoi fornire questo ID di chiave pubblica come ID della chiave di verifica della firma durante la creazione di un flusso di dati per dati firmati e crittografati. |

+++

### Recupera coppia di chiavi gestite dal cliente

Per recuperare le chiavi gestite dal cliente, effettuare una richiesta GET all&#39;endpoint `/customer-keys`.

**Formato API**

```http
GET /data/foundation/connectors/encryption/customer-keys
```

**Richiesta**

+++Visualizza richiesta di esempio

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/customer-keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Risposta**

+++Visualizza risposta di esempio

```json
[
    {
        "encryptionAlgorithm": "{ENCRYPTION_ALGORITHM}",
        "name": "{NAME}",
        "publicKeyId": "{PUBLIC_KEY_ID}",
        "publicKey": "{PUBLIC_KEY}",
        "keyType": "{KEY_TYPE}",
    }
]
```

+++

## Connetti l&#39;origine dell&#39;archiviazione cloud ad Experience Platform utilizzando l&#39;API [!DNL Flow Service]

Dopo aver recuperato la coppia di chiavi di crittografia, ora puoi procedere e creare una connessione di origine per l’origine dell’archiviazione cloud e trasferire i dati crittografati a Platform.

Innanzitutto, devi creare una connessione di base per autenticare l’origine su Platform. Per creare una connessione di base e autenticare l&#39;origine, selezionare dall&#39;elenco seguente l&#39;origine che si desidera utilizzare:

* [Amazon S3](../api/create/cloud-storage/s3.md)
* [[!DNL Apache HDFS]](../api/create/cloud-storage/hdfs.md)
* [BLOB di Azure](../api/create/cloud-storage/blob.md)
* [Azure Data Lake Storage Gen2](../api/create/cloud-storage/adls-gen2.md)
* [Archiviazione file di Azure](../api/create/cloud-storage/azure-file-storage.md)
* [Data Landing Zone](../api/create/cloud-storage/data-landing-zone.md)
* [FTP](../api/create/cloud-storage/ftp.md)
* [Google Cloud Storage](../api/create/cloud-storage/google.md)
* [Archiviazione di oggetti di Oracle](../api/create/cloud-storage/oracle-object-storage.md)
* [SFTP](../api/create/cloud-storage/sftp.md)

Dopo aver creato una connessione di base, è necessario seguire i passaggi descritti nell&#39;esercitazione per [creare una connessione di origine per un&#39;origine di archiviazione cloud](../api/collect/cloud-storage.md) per creare una connessione di origine, una connessione di destinazione e una mappatura.

## Creare un flusso di dati per i dati crittografati {#create-a-dataflow-for-encrypted-data}

>[!NOTE]
>
>Per creare un flusso di dati per l’acquisizione di dati crittografati, è necessario disporre dei seguenti elementi:
>
>* [ID chiave pubblica](#create-encryption-key-pair)
>* [ID connessione Source](../api/collect/cloud-storage.md#source)
>* [ID connessione di destinazione](../api/collect/cloud-storage.md#target)
>* [ID mappatura](../api/collect/cloud-storage.md#mapping)

Per creare un flusso di dati, effettuare una richiesta POST all&#39;endpoint `/flows` dell&#39;API [!DNL Flow Service]. Per acquisire i dati crittografati, è necessario aggiungere una sezione `encryption` alla proprietà `transformations` e includere `publicKeyId` creato in un passaggio precedente.

**Formato API**

```http
POST /flows
```

>[!BEGINTABS]

>[!TAB Crea un flusso di dati per l&#39;acquisizione di dati crittografati]

**Richiesta**

+++Visualizza richiesta di esempio

La seguente richiesta crea un flusso di dati per acquisire dati crittografati per un’origine di archiviazione cloud.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Customer Data",
    "description": "ACME Customer Data (Encrypted)",
    "flowSpec": {
        "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "655f7c1b-1977-49b3-a429-51379ecf0e15"
    ],
    "targetConnectionIds": [
        "de688225-d619-481c-ae3b-40c250fd7c79"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "6b6e24213dbe4f57bd8207d21034ff03",
                "mappingVersion":"0"
            }
        },
        {
            "name": "Encryption",
            "params": {
                "publicKeyId":"311ef6f8-9bcd-48cf-a9e9-d12c45fb7a17"
            }
        }
    ],
    "scheduleParams": {
        "startTime": "1675793392",
        "frequency": "once"
    }
}'
```

| Proprietà | Descrizione |
| --- | --- |
| `flowSpec.id` | ID della specifica di flusso che corrisponde alle origini dell’archiviazione cloud. |
| `sourceConnectionIds` | ID della connessione di origine. Questo ID rappresenta il trasferimento di dati dall’origine a Platform. |
| `targetConnectionIds` | ID della connessione di destinazione. Questo ID rappresenta dove arrivano i dati una volta trasferiti a Platform. |
| `transformations[x].params.mappingId` | ID di mappatura. |
| `transformations.name` | Durante l&#39;acquisizione di file crittografati, devi fornire `Encryption` come parametro di trasformazione aggiuntivo per il flusso di dati. |
| `transformations[x].params.publicKeyId` | ID della chiave pubblica creato. Questo ID è la metà della coppia di chiavi di crittografia utilizzata per crittografare i dati di archiviazione cloud. |
| `scheduleParams.startTime` | L’ora di inizio del flusso di dati in tempo epoca. |
| `scheduleParams.frequency` | La frequenza con cui il flusso di dati raccoglierà i dati. I valori accettabili includono: `once`, `minute`, `hour`, `day` o `week`. |
| `scheduleParams.interval` | L’intervallo indica il periodo tra due esecuzioni consecutive del flusso. Il valore dell&#39;intervallo deve essere un numero intero diverso da zero. L&#39;intervallo non è necessario quando la frequenza è impostata come `once` e deve essere maggiore o uguale a `15` per gli altri valori di frequenza. |

+++

**Risposta**

+++Visualizza risposta di esempio

In caso di esito positivo, la risposta restituisce l&#39;ID (`id`) del flusso di dati appena creato per i dati crittografati.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++

>[!TAB Crea un flusso di dati per acquisire dati crittografati e firmati]

**Richiesta**

+++Visualizza richiesta di esempio

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Customer Data (with Sign Verification)",
    "description": "ACME Customer Data (with Sign Verification)",
    "flowSpec": {
        "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "655f7c1b-1977-49b3-a429-51379ecf0e15"
    ],
    "targetConnectionIds": [
        "de688225-d619-481c-ae3b-40c250fd7c79"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "6b6e24213dbe4f57bd8207d21034ff03",
                "mappingVersion":"0"
            }
        },
        {
            "name": "Encryption",
            "params": {
                "publicKeyId":"311ef6f8-9bcd-48cf-a9e9-d12c45fb7a17",
                "signVerificationKeyId":"e31ae895-7896-469a-8e06-eb9207ddf1c2"
            }
        }
    ],
    "scheduleParams": {
        "startTime": "1675793392",
        "frequency": "once"
    }
}'
```

| Proprietà | Descrizione |
| --- | --- |
| `params.signVerificationKeyId` | L’ID della chiave di verifica della firma è uguale all’ID della chiave pubblica recuperato dopo la condivisione della chiave pubblica con codifica Base64 con Experience Platform. |

+++

**Risposta**

+++Visualizza risposta di esempio

In caso di esito positivo, la risposta restituisce l&#39;ID (`id`) del flusso di dati appena creato per i dati crittografati.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++

>[!ENDTABS]

### Elimina chiavi di crittografia {#delete-encryption-keys}

Per eliminare le chiavi di crittografia, effettua una richiesta DELETE all&#39;endpoint `/encryption/keys` e fornisci l&#39;ID della chiave pubblica come parametro di intestazione.

**Formato API**

```http
DELETE /data/foundation/connectors/encryption/keys/{PUBLIC_KEY_ID}
```

**Richiesta**

+++Visualizza richiesta di esempio

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys/{publicKeyId}' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 204 (nessun contenuto) e un corpo vuoto.

### Convalidare le chiavi di crittografia {#validate-encryption-keys}

Per convalidare le chiavi di crittografia, effettuare una richiesta di GET all&#39;endpoint `/encryption/keys/validate/` e fornire l&#39;ID della chiave pubblica da convalidare come parametro di intestazione.

```http
GET /data/foundation/connectors/encryption/keys/validate/{PUBLIC_KEY_ID}
```

**Richiesta**

+++Visualizza richiesta di esempio

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys/validate/{publicKeyId}' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce la conferma che gli ID sono validi o non validi.

>[!BEGINTABS]

>[!TAB Valido]

Un ID chiave pubblica valido restituisce lo stato `Active` insieme all&#39;ID chiave pubblica.

```json
{
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "status": "Active"
}
```

>[!TAB Non valido]

Un ID di chiave pubblica non valido restituisce lo stato `Expired` insieme all&#39;ID di chiave pubblica.

```json
{
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "status": "Expired"
}
```

>[!ENDTABS]


## Limitazioni all’acquisizione ricorrente {#restrictions-on-recurring-ingestion}

L’acquisizione di dati crittografati non supporta l’acquisizione di cartelle ricorrenti o a più livelli nelle origini. Tutti i file crittografati devono essere contenuti in una singola cartella. Non sono supportati neanche i caratteri jolly con più cartelle in un unico percorso di origine.

Di seguito è riportato un esempio di struttura di cartelle supportata, dove il percorso di origine è `/ACME-customers/*.csv.gpg`.

In questo scenario, i file in grassetto vengono acquisiti in Experience Platform.

* ACME-clienti
   * **File1.csv.gpg**
   * File2.json.gpg
   * **File3.csv.gpg**
   * File4.json
   * **File5.csv.gpg**

Di seguito è riportato un esempio di struttura di cartelle non supportata in cui il percorso di origine è `/ACME-customers/*`.

In questo scenario, l’esecuzione del flusso non riuscirà e restituirà un messaggio di errore che indica che i dati non possono essere copiati dall’origine.

* ACME-clienti
   * File1.csv.gpg
   * File2.json.gpg
   * Sottocartella1
      * File3.csv.gpg
      * File4.json.gpg
      * File5.csv.gpg
* fedeltà ACME
   * File6.csv.gpg


## Passaggi successivi

Seguendo questa esercitazione, hai creato una coppia di chiavi di crittografia per i dati dell&#39;archiviazione cloud e un flusso di dati per acquisire i dati crittografati utilizzando [!DNL Flow Service API]. Per gli aggiornamenti sullo stato di completezza, errori e metriche del flusso di dati, leggi la guida sul [monitoraggio del flusso di dati tramite l&#39;API [!DNL Flow Service] 2}.](./monitor.md)