---
keywords: Experience Platform;home;popular topics;SFTP;sftp;Secure File Transfer Protocol;secure file transfer protocol
solution: Experience Platform
title: Creazione di un connettore SFTP tramite l'API del servizio di flusso
topic: overview
type: Tutorial
description: Questa esercitazione utilizza l'API del servizio di flusso per guidarvi attraverso i passaggi necessari per connettere  Experience Platform a un server SFTP (Secure File Transfer Protocol).
translation-type: tm+mt
source-git-commit: c88b9400144f511ef456fd5fdc968a5a6b7a3dc0
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 1%

---


# Creare un connettore SFTP utilizzando l&#39;API [!DNL Flow Service]

>[!NOTE]
>
>Il connettore SFTP è in versione beta. Le funzioni e la documentazione sono soggette a modifiche. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, vedere [Panoramica delle sorgenti](../../../../home.md#terms-and-conditions).

Questa esercitazione utilizza l&#39;API [!DNL Flow Service] per guidarti attraverso i passaggi necessari per connettere  Experience Platform a un server SFTP (Secure File Transfer Protocol).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md):  Experience Platform consente l&#39;acquisizione di dati da varie fonti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Piattaforma.
* [Sandbox](../../../../../sandboxes/home.md):  Experience Platform fornisce sandbox virtuali che dividono una singola istanza della piattaforma in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

>[!IMPORTANT]
>
>Si consiglia di evitare la presenza di newline o ritorni a capo durante l&#39;assimilazione di oggetti JSON con una connessione sorgente SFTP. Per aggirare il limite, utilizzate un singolo oggetto JSON per riga e più righe per i file successivi.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi correttamente a un server SFTP utilizzando l&#39;API [!DNL Flow Service].

### Raccogli credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a SFTP, è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Nome o indirizzo IP associato al server SFTP. |
| `username` | Il nome utente con accesso al server SFTP. |
| `password` | La password per il server SFTP. |
| `privateKeyContent` | Il contenuto della chiave privata SSH con codifica Base64. Formato della chiave privata SSH OpenSSH (RSA/DSA). |
| `passPhrase` | La frase di autorizzazione o la password per decifrare la chiave privata se il file chiave o il contenuto chiave sono protetti da una frase di autorizzazione. Se PrivateKeyContent è protetto da password, questo parametro deve essere utilizzato con la passphrase PrivateKeyContent come valore. |

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi del Experience Platform .

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle API della piattaforma, è innanzitutto necessario completare l&#39;esercitazione sull&#39;autenticazione [a1/>. ](../../../../../tutorials/authentication.md) Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte  chiamate API di Experience Platform, come illustrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], incluse quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui verrà eseguita l&#39;operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

* `Content-Type: application/json`

## Creare una connessione

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. È necessaria una sola connessione, in quanto può essere utilizzata per creare più flussi di dati per inserire dati diversi.

### Creazione di una connessione SFTP tramite autenticazione di base

Per creare una connessione SFTP utilizzando l&#39;autenticazione di base, effettuare una richiesta POST all&#39;API [!DNL Flow Service] fornendo al contempo i valori per le connessioni `host`, `userName` e `password`.

**Formato API**

```http
POST /connections
```

**Richiesta**

Per creare una connessione SFTP, è necessario fornire l&#39;ID univoco della specifica di connessione come parte della richiesta POST. L&#39;ID della specifica di connessione per SFTP è `b7bf2577-4520-42c9-bae9-cad01560f7bc`.

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
| `auth.params.password` | La password associata al server SFTP. |
| `connectionSpec.id` | ID specifica connessione server SFTP: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) della connessione appena creata. Questo ID è necessario per esplorare il server SFTP nell&#39;esercitazione successiva.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

### Creare una connessione SFTP utilizzando l&#39;autenticazione a chiave pubblica SSH

Per creare una connessione SFTP utilizzando l&#39;autenticazione a chiave pubblica SSH, effettuare una richiesta POST all&#39;API [!DNL Flow Service] fornendo al contempo i valori per le connessioni `host`, `userName`, `privateKeyContent` e `passPhrase`.

**Formato API**

```http
POST /connections
```

**Richiesta**

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
| `auth.params.host` | Il nome host del server SFTP. |
| `auth.params.username` | Nome utente associato al server SFTP. |
| `auth.params.privateKeyContent` | Il contenuto della chiave privata SSH con codifica base64. Formato della chiave privata SSH OpenSSH (RSA/DSA). |
| `auth.params.passPhrase` | La frase di autorizzazione o la password per decifrare la chiave privata se il file chiave o il contenuto chiave sono protetti da una frase di autorizzazione. Se PrivateKeyContent è protetto da password, questo parametro deve essere utilizzato con la passphrase PrivateKeyContent come valore. |
| `connectionSpec.id` | ID specifica connessione server SFTP: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) della connessione appena creata. Questo ID è necessario per esplorare il server SFTP nell&#39;esercitazione successiva.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione SFTP utilizzando l&#39;API [!DNL Flow Service] e hai ottenuto il valore ID univoco della connessione. Puoi utilizzare questo ID connessione per [esplorare gli archivi cloud utilizzando l&#39;API del servizio di flusso](../../explore/cloud-storage.md) o [assimilare i dati del parquet tramite l&#39;API del servizio di flusso](../../cloud-storage-parquet.md).
