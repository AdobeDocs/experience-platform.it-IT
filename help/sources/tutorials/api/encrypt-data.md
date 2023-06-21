---
title: Acquisizione di dati crittografati
description: Scopri come acquisire i file crittografati tramite le origini batch di archiviazione cloud utilizzando l’API.
hide: true
hidefromtoc: true
exl-id: 83a7a154-4f55-4bf0-bfef-594d5d50f460
source-git-commit: f0e518459eca72d615b380d11cabee6c1593dd9a
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 2%

---

# Acquisizione di dati crittografati

Adobe Experience Platform consente di acquisire file crittografati tramite origini batch di archiviazione cloud. Con l’acquisizione di dati crittografati, puoi sfruttare meccanismi di crittografia asimmetrica per trasferire in modo sicuro i dati batch in Experience Platform. Attualmente, i meccanismi di crittografia asimmetrica supportati sono PGP e GPG.

Il processo di acquisizione dei dati crittografati è il seguente:

1. [Creare una coppia di chiavi di crittografia utilizzando le API Experience Platform](#create-encryption-key-pair). La coppia di chiavi di crittografia è costituita da una chiave privata e da una chiave pubblica. Una volta creata, puoi copiare o scaricare la chiave pubblica, insieme all’ID della chiave pubblica e all’ora di scadenza corrispondenti. Durante questa procedura, la chiave privata verrà memorizzata da Experience Platform in un archivio protetto. **NOTA:** La chiave pubblica nella risposta è codificata in Base64 e deve essere decrittografata prima dell’utilizzo.
2. Utilizza la chiave pubblica per crittografare il file di dati che desideri acquisire.
3. Inserisci il file crittografato nell’archiviazione cloud.
4. Quando il file crittografato è pronto, [creare una connessione di origine e un flusso di dati per l’origine di archiviazione cloud](#create-a-dataflow-for-encrypted-data). Durante il passaggio di creazione del flusso, devi fornire un `encryption` e includere l&#39;ID della chiave pubblica.
5. L’Experience Platform recupera la chiave privata dall’archivio protetto per decrittografare i dati al momento dell’acquisizione.

>[!IMPORTANT]
>
>La dimensione massima di un singolo file crittografato è di 1 GB. Ad esempio, puoi acquisire dati per un valore di 2 GB in una singola esecuzione del flusso di dati; tuttavia, qualsiasi singolo file in tali dati non può superare 1 GB.

In questo documento vengono descritti i passaggi necessari per generare una coppia di chiavi di crittografia per crittografare i dati e acquisirli per l’Experience Platform utilizzando origini di archiviazione cloud.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../home.md): un Experience Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
   * [Sorgenti di archiviazione cloud](../api/collect/cloud-storage.md): crea un flusso di dati per portare all’Experience Platform i dati batch dall’origine dell’archiviazione cloud.
* [Sandbox](../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../landing/api-guide.md).

### Estensioni di file supportate per i file crittografati

Di seguito è riportato l&#39;elenco delle estensioni di file supportate per i file crittografati:

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

Il primo passaggio nell’acquisizione di dati crittografati da Experience Platform consiste nel creare la coppia di chiavi di crittografia effettuando una richiesta POST al `/encryption/keys` endpoint del [!DNL Connectors] API.

**Formato API**

```http
POST /data/foundation/connectors/encryption/keys
```

**Richiesta**

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
      "encryptionAlgorithm": "PGP",
      "params": {
          "passPhrase": "{{PASSPHRASE}}"
      }
  }'
```

| Parametro | Descrizione |
| --- | --- |
| `encryptionAlgorithm` | Tipo di algoritmo di crittografia in uso. I tipi di crittografia supportati sono `PGP` e `GPG`. |
| `params.passPhrase` | La passphrase fornisce un ulteriore livello di protezione per le chiavi di crittografia. Al momento della creazione, Experience Platform memorizza la passphrase in un archivio protetto diverso dalla chiave pubblica. Specificare una stringa non vuota come passphrase. |

**Risposta**

In caso di esito positivo, la risposta restituisce la chiave pubblica con codifica Base64, l’ID della chiave pubblica e l’ora di scadenza delle chiavi. Il tempo di scadenza viene impostato automaticamente su 180 giorni dopo la data di generazione della chiave. L’ora di scadenza non è attualmente configurabile.

```json
{
    ​"publicKey": "{PUBLIC_KEY}",
    ​"publicKeyId": "{PUBLIC_KEY_ID}",
    ​"expiryTime": "1684843168"
}
```

## Connetti l’origine dell’archiviazione cloud a Experience Platform utilizzando [!DNL Flow Service] API

Dopo aver recuperato la coppia di chiavi di crittografia, ora puoi procedere e creare una connessione di origine per l’origine dell’archiviazione cloud e trasferire i dati crittografati a Platform.

Innanzitutto, devi creare una connessione di base per autenticare l’origine su Platform. Per creare una connessione di base e autenticare l&#39;origine, selezionare dall&#39;elenco seguente l&#39;origine che si desidera utilizzare:

* [Amazon S3](../api/create/cloud-storage/s3.md)
* [[!DNL Apache HDFS]](../api/create/cloud-storage/hdfs.md)
* [BLOB di Azure](../api/create/cloud-storage/blob.md)
* [Archiviazione Azure Data Lake Gen2](../api/create/cloud-storage/adls-gen2.md)
* [Archiviazione file di Azure](../api/create/cloud-storage/azure-file-storage.md)
* [Data Landing Zone](../api/create/cloud-storage/data-landing-zone.md)
* [FTP](../api/create/cloud-storage/ftp.md)
* [Archiviazione cloud Google](../api/create/cloud-storage/google.md)
* [Oracle archiviazione oggetti](../api/create/cloud-storage/oracle-object-storage.md)
* [SFTP](../api/create/cloud-storage/sftp.md)

Dopo aver creato una connessione di base, è necessario seguire i passaggi descritti nell&#39;esercitazione per [creazione di una connessione di origine per un&#39;origine di archiviazione cloud](../api/collect/cloud-storage.md) per creare una connessione sorgente, una connessione di destinazione e una mappatura.

## Creare un flusso di dati per i dati crittografati {#create-a-dataflow-for-encrypted-data}

>[!NOTE]
>
>Per creare un flusso di dati per l’acquisizione di dati crittografati, è necessario disporre dei seguenti elementi:
>
>* [ID chiave pubblica](#create-encryption-key-pair)
>* [ID connessione sorgente](../api/collect/cloud-storage.md#source)
>* [ID connessione di destinazione](../api/collect/cloud-storage.md#target)
>* [ID di mappatura](../api/collect/cloud-storage.md#mapping)

Per creare un flusso di dati, effettua una richiesta POST al `/flows` endpoint del [!DNL Flow Service] API. Per acquisire i dati crittografati, è necessario aggiungere una `encryption` sezione al `transformations` e includere `publicKeyId` creato in un passaggio precedente.

**Formato API**

```http
POST /flows
```

**Richiesta**

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
| `transformations.name` | Quando si acquisiscono file crittografati, è necessario fornire `Encryption` come parametro di trasformazione aggiuntivo per il flusso di dati. |
| `transformations[x].params.publicKeyId` | ID della chiave pubblica creato. Questo ID è la metà della coppia di chiavi di crittografia utilizzata per crittografare i dati di archiviazione cloud. |
| `scheduleParams.startTime` | L’ora di inizio del flusso di dati in tempo epoca. |
| `scheduleParams.frequency` | La frequenza con cui il flusso di dati raccoglierà i dati. I valori accettabili includono: `once`, `minute`, `hour`, `day`, o `week`. |
| `scheduleParams.interval` | L’intervallo indica il periodo tra due esecuzioni consecutive del flusso. Il valore dell&#39;intervallo deve essere un numero intero diverso da zero. Intervallo non richiesto quando la frequenza è impostata come `once` e deve essere maggiore o uguale a `15` per altri valori di frequenza. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID (`id`) del flusso di dati appena creato per i dati crittografati.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una coppia di chiavi di crittografia per i dati dell’archiviazione cloud e un flusso di dati per acquisire i dati crittografati utilizzando [!DNL Flow Service API]. Per gli aggiornamenti sullo stato relativi a completezza, errori e metriche del flusso di dati, consulta la guida su [monitoraggio del flusso di dati tramite [!DNL Flow Service] API](./monitor.md).
