---
keywords: Experience Platform;home;argomenti popolari;SFTP;sftp;Secure File Transfer Protocol;Secure File Transfer Protocol (protocollo di trasferimento file sicuro)
solution: Experience Platform
title: Creare una connessione di base SFTP utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a un server SFTP (Secure File Transfer Protocol) utilizzando l’API del servizio di flusso.
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: 9ad09fba3119b631576f22574a2151c74f91e07b
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 2%

---

# Creare una connessione di base SFTP utilizzando l&#39;API [!DNL Flow Service]

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL SFTP] (Secure File Transfer Protocol) utilizzando l&#39; [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

>[!IMPORTANT]
>
>Si consiglia di evitare l’esecuzione di nuove righe o ritorni a capo durante l’acquisizione di oggetti JSON con una connessione sorgente [!DNL SFTP]. Per aggirare il limite, utilizza un singolo oggetto JSON per riga e utilizza più righe per i file successivi.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a un server [!DNL SFTP] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL SFTP], è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Nome o indirizzo IP associato al server [!DNL SFTP]. |
| `port` | La porta server SFTP a cui ti connetti. Se non viene fornito, il valore predefinito è `22`. |
| `username` | Il nome utente con accesso al server [!DNL SFTP]. |
| `password` | Password per il server [!DNL SFTP]. |
| `privateKeyContent` | Contenuto della chiave privata SSH codificata Base64. Il tipo di chiave OpenSSH deve essere classificato come RSA o DSA. |
| `passPhrase` | La frase o password per decrittografare la chiave privata se il file di chiave o il contenuto della chiave sono protetti da una frase di passaggio. Se `privateKeyContent` è protetto da password, è necessario utilizzare questo parametro con la passphrase del contenuto della chiave privata come valore. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. L&#39;ID della specifica di connessione per [!DNL SFTP] è: `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md) .

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL SFTP] come parte dei parametri della richiesta.

### Creare una connessione di base [!DNL SFTP] utilizzando l&#39;autenticazione di base

Per creare una connessione di base [!DNL SFTP] utilizzando l’autenticazione di base, invia una richiesta POST all’API [!DNL Flow Service] fornendo al contempo i valori per le connessioni `host`, `userName` e `password` della connessione.

**Formato API**

```http
POST /connections
```

**Richiesta**

La seguente richiesta crea una connessione di base per [!DNL SFTP] utilizzando l&#39;autenticazione di base:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
        "name": "SFTP connector with password",
        "description": "SFTP connector password",
        "auth": {
            "specName": "Basic Authentication for sftp",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.host` | Il nome host del server SFTP. |
| `auth.params.username` | Nome utente associato al server SFTP. |
| `auth.params.password` | Password associata al server SFTP. |
| `connectionSpec.id` | ID delle specifiche di connessione del server SFTP: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) della nuova connessione creata. Questo ID è necessario per esplorare il server SFTP nella prossima esercitazione.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

### Creare una connessione di base [!DNL SFTP] utilizzando l’autenticazione a chiave pubblica SSH

Per creare una connessione di base [!DNL SFTP] utilizzando l’autenticazione a chiave pubblica SSH, invia una richiesta POST all’API [!DNL Flow Service] fornendo al contempo i valori per le connessioni `host`, `userName`, `privateKeyContent` e `passPhrase`.

>[!IMPORTANT]
>
>Il connettore [!DNL SFTP] supporta una chiave OpenSSH di tipo RSA o DSA. Assicurati che il contenuto del file chiave inizi con `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` e termini con `"-----END [RSA/DSA] PRIVATE KEY-----"`. Se il file della chiave privata è un file in formato PPK, utilizza lo strumento PuTTY per convertire da PPK a formato OpenSSH.

**Formato API**

```http
POST /connections
```

**Richiesta**

La seguente richiesta crea una connessione di base per [!DNL SFTP] utilizzando l’autenticazione a chiave pubblica SSH:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "SFTP connector with SSH authentication",
        "description": "SFTP connector with SSH authentication",
        "auth": {
            "specName": "SSH PublicKey Authentication for sftp",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "privateKeyContent": "{PRIVATE_KEY_CONTENT}",
                "passPhrase": "{PASSPHRASE}"
            }
        },
        "connectionSpec": {
            "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.host` | Il nome host del server [!DNL SFTP]. |
| `auth.params.username` | Il nome utente associato al server [!DNL SFTP]. |
| `auth.params.privateKeyContent` | Contenuto della chiave privata SSH codificata Base64. Il tipo di chiave OpenSSH deve essere classificato come RSA o DSA. |
| `auth.params.passPhrase` | La frase o password per decrittografare la chiave privata se il file di chiave o il contenuto della chiave sono protetti da una frase di passaggio. Se PrivateKeyContent è protetto da password, questo parametro deve essere utilizzato con la passphrase PrivateKeyContent come valore. |
| `connectionSpec.id` | ID delle specifiche di connessione del server [!DNL SFTP]: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) della nuova connessione creata. Questo ID è necessario per esplorare il server [!DNL SFTP] nell&#39;esercitazione successiva.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione [!DNL SFTP] utilizzando l&#39;API [!DNL Flow Service] e hai ottenuto il valore ID univoco della connessione. Puoi utilizzare questo ID connessione per [esplorare gli archivi cloud utilizzando l&#39;API del servizio di flusso](../../explore/cloud-storage.md) o [acquisire i dati del parquet utilizzando l&#39;API del servizio di flusso](../../cloud-storage-parquet.md).
