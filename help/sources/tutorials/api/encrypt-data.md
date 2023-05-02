---
title: Acquisizione di dati crittografati
description: Adobe Experience Platform consente di acquisire file crittografati tramite origini batch di archiviazione cloud.
hide: true
hidefromtoc: true
exl-id: 83a7a154-4f55-4bf0-bfef-594d5d50f460
source-git-commit: 8531459da97be648d0a63ffc2af77ce41124585d
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 2%

---

# Acquisizione di dati crittografati

Adobe Experience Platform consente di acquisire file crittografati tramite origini batch di archiviazione cloud. Con l’inserimento di dati crittografati, puoi sfruttare meccanismi di crittografia asimmetrici per trasferire in modo sicuro i dati batch in Experience Platform. Attualmente, i meccanismi di crittografia asimmetrica supportati sono PGP e GPG.

Il processo di acquisizione dei dati crittografati è il seguente:

1. [Creare una coppia di chiavi di crittografia utilizzando le API di Experience Platform](#create-encryption-key-pair). La coppia di chiavi di crittografia è costituita da una chiave privata e una chiave pubblica. Una volta creata, puoi copiare o scaricare la chiave pubblica, insieme al corrispondente ID della chiave pubblica e all’ora di scadenza. Durante questo processo, la chiave privata verrà memorizzata per Experience Platform in un archivio protetto. **NOTA:** La chiave pubblica nella risposta è codificata in Base64 e deve essere decrittografata prima di utilizzare.
2. Utilizza la chiave pubblica per crittografare il file di dati da acquisire.
3. Posiziona il file crittografato nell’archivio cloud.
4. Quando il file crittografato è pronto, [creare una connessione sorgente e un flusso di dati per l&#39;origine di archiviazione cloud](#create-a-dataflow-for-encrypted-data). Durante il passaggio di creazione del flusso, devi fornire un `encryption` e includi l&#39;ID della chiave pubblica.
5. Experience Platform recupera la chiave privata dall’archivio protetto per decrittografare i dati al momento dell’acquisizione.

>[!IMPORTANT]
>
>La dimensione massima di un singolo file crittografato è di 1 GB. Ad esempio, è possibile acquisire 2 GB di dati in una singola esecuzione di un flusso di dati, tuttavia, qualsiasi singolo file in tali dati non può superare 1 GB.

Questo documento fornisce passaggi su come generare una coppia di chiavi di crittografia per crittografare i dati e acquisire tali dati crittografati per Experience Platform utilizzando origini di archiviazione cloud.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
   * [Origini di archiviazione cloud](../api/collect/cloud-storage.md): Crea un flusso di dati per portare ad Experience Platform i dati batch dall&#39;origine di archiviazione cloud.
* [Sandbox](../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../landing/api-guide.md).

## Crea coppia di chiavi di crittografia {#create-encryption-key-pair}

Il primo passaggio in cui si acquisiscono dati crittografati in Experience Platform consiste nel creare la coppia di chiavi di crittografia effettuando una richiesta di POST al `/encryption/keys` punto finale [!DNL Connectors] API.

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
| `encryptionAlgorithm` | Il tipo di algoritmo di crittografia utilizzato. I tipi di crittografia supportati sono `PGP` e `GPG`. |
| `params.passPhrase` | La passphrase fornisce un ulteriore livello di protezione per le chiavi di crittografia. Al momento della creazione, Experience Platform memorizza la passphrase in un insieme di credenziali protetto diverso dalla chiave pubblica. È necessario fornire una stringa non vuota come passphrase. |

**Risposta**

Una risposta corretta restituisce la chiave pubblica con codifica Base64, l&#39;ID della chiave pubblica e l&#39;ora di scadenza delle chiavi. L’ora di scadenza viene impostata automaticamente su 180 giorni dopo la data di generazione della chiave. Il tempo di scadenza non è attualmente configurabile.

```json
{
    ​"publicKey": "{PUBLIC_KEY}",
    ​"publicKeyId": "{PUBLIC_KEY_ID}",
    ​"expiryTime": "1684843168"
}
```

## Collegare l&#39;origine di archiviazione cloud all&#39;Experience Platform utilizzando [!DNL Flow Service] API

Dopo aver recuperato la coppia di chiavi di crittografia, ora puoi procedere e creare una connessione sorgente per l’origine di archiviazione cloud e trasferire i dati crittografati in Platform.

Innanzitutto, devi creare una connessione di base per autenticare l’origine rispetto a Platform. Per creare una connessione di base e autenticare l&#39;origine, selezionare l&#39;origine che si desidera utilizzare dall&#39;elenco seguente:

* [Amazon S3](../api/create/cloud-storage/s3.md)
* [[!DNL Apache HDFS]](../api/create/cloud-storage/hdfs.md)
* [BLOB di Azure](../api/create/cloud-storage/blob.md)
* [Azure Data Lake Storage Gen2](../api/create/cloud-storage/adls-gen2.md)
* [Archiviazione file di Azure](../api/create/cloud-storage/azure-file-storage.md)
* [Data Landing Zone](../api/create/cloud-storage/data-landing-zone.md)
* [FTP](../api/create/cloud-storage/ftp.md)
* [Google Cloud Storage](../api/create/cloud-storage/google.md)
* [Archiviazione oggetti Oracle](../api/create/cloud-storage/oracle-object-storage.md)
* [SFTP](../api/create/cloud-storage/sftp.md)

Dopo aver creato una connessione di base, segui i passaggi descritti nell’esercitazione per [creazione di una connessione di origine per un&#39;origine di archiviazione cloud](../api/collect/cloud-storage.md) per creare una connessione sorgente, una connessione di destinazione e una mappatura.

## Creazione di un flusso di dati per i dati crittografati {#create-a-dataflow-for-encrypted-data}

>[!NOTE]
>
>Per creare un flusso di dati per l’inserimento di dati crittografati, è necessario disporre dei seguenti elementi:
>* [ID chiave pubblica](#create-encryption-key-pair)
>* [ID connessione di origine](../api/collect/cloud-storage.md#source)
>* [ID connessione di destinazione](../api/collect/cloud-storage.md#target)
>* [ID di mappatura](../api/collect/cloud-storage.md#mapping)


Per creare un flusso di dati, invia una richiesta POST al `/flows` punto finale [!DNL Flow Service] API. Per acquisire i dati crittografati, devi aggiungere un `encryption` alla sezione `transformations` e includere `publicKeyId` creato in un passaggio precedente.

**Formato API**

```http
POST /flows
```

**Richiesta**

La seguente richiesta crea un flusso di dati per l’acquisizione di dati crittografati per un’origine di archiviazione cloud.

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
| `flowSpec.id` | ID delle specifiche di flusso che corrisponde alle origini di archiviazione cloud. |
| `sourceConnectionIds` | ID della connessione di origine. Questo ID rappresenta il trasferimento di dati dall’origine a Platform. |
| `targetConnectionIds` | ID della connessione di destinazione. Questo ID rappresenta il punto in cui i dati arrivano una volta trasferiti su Platform. |
| `transformations[x].params.mappingId` | ID mappatura. |
| `transformations.name` | Quando si acquisiscono file crittografati, è necessario fornire `Encryption` come parametro di trasformazione aggiuntivo per il flusso di dati. |
| `transformations[x].params.publicKeyId` | ID chiave pubblica creato. Questo ID è la metà della coppia di chiavi di crittografia utilizzata per crittografare i dati di archiviazione cloud. |
| `scheduleParams.startTime` | Ora di inizio del flusso di dati in epoch time. |
| `scheduleParams.frequency` | Frequenza con cui il flusso di dati raccoglie i dati. I valori accettabili includono: `once`, `minute`, `hour`, `day`oppure `week`. |
| `scheduleParams.interval` | L&#39;intervallo indica il periodo tra due esecuzioni di flusso consecutive. Il valore dell&#39;intervallo deve essere un numero intero diverso da zero. L&#39;intervallo non è necessario quando la frequenza è impostata come `once` e deve essere maggiore o uguale a `15` per altri valori di frequenza. |

**Risposta**

Una risposta corretta restituisce l&#39;ID (`id`) del flusso di dati appena creato per i dati crittografati.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una coppia di chiavi di crittografia per i dati di archiviazione cloud e un flusso di dati per acquisire i dati crittografati utilizzando [!DNL Flow Service API]. Per aggiornamenti sullo stato della completezza, degli errori e delle metriche del flusso di dati, consulta la guida su [monitoraggio del flusso di dati tramite [!DNL Flow Service] API](./monitor.md).
