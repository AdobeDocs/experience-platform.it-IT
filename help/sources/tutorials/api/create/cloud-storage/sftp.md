---
keywords: Experience Platform;home;argomenti popolari;SFTP;sftp;Secure File Transfer Protocol;Secure File Transfer Protocol (protocollo di trasferimento file sicuro)
solution: Experience Platform
title: Creare una connessione di base SFTP utilizzando l’API del servizio di flusso
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a un server SFTP (Secure File Transfer Protocol) utilizzando l’API del servizio di flusso.
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 1%

---

# Creare una connessione di base SFTP utilizzando [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL SFTP] (Secure File Transfer Protocol) utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

>[!IMPORTANT]
>
>Si consiglia di evitare la restituzione di nuove righe o carrelli durante l’acquisizione di oggetti JSON con un [!DNL SFTP] connessione di origine. Per aggirare il limite, utilizza un singolo oggetto JSON per riga e utilizza più righe per i file successivi.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a un [!DNL SFTP] utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi a [!DNL SFTP], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Nome o indirizzo IP associato al tuo [!DNL SFTP] server. |
| `port` | La porta server SFTP a cui ti connetti. Se non viene fornito, il valore predefinito è `22`. |
| `username` | Il nome utente con accesso al tuo [!DNL SFTP] server. |
| `password` | La password [!DNL SFTP] server. |
| `privateKeyContent` | Contenuto della chiave privata SSH codificata Base64. Il tipo di chiave OpenSSH deve essere classificato come RSA o DSA. |
| `passPhrase` | La frase o password per decrittografare la chiave privata se il file di chiave o il contenuto della chiave sono protetti da una frase di passaggio. Se la `privateKeyContent` è protetto da password, questo parametro deve essere utilizzato con la passphrase del contenuto della chiave privata come valore. |
| `maxConcurrentConnections` | Questo parametro consente di specificare un limite massimo per il numero di connessioni simultanee che Platform creerà quando si connette al server SFTP. Devi impostare questo valore affinché sia inferiore al limite impostato da SFTP. **Nota**: Quando questa impostazione è abilitata per un account SFTP esistente, influenzerà solo i flussi di dati futuri e non i flussi di dati esistenti. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL SFTP] è: `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

La [!DNL SFTP] source supporta sia l’autenticazione di base che l’autenticazione tramite la chiave pubblica SSH.

Per creare un ID di connessione di base, invia una richiesta POST al `/connections` l&#39;endpoint durante la fornitura del [!DNL SFTP] credenziali di autenticazione come parte dei parametri della richiesta.

>[!IMPORTANT]
>
>La [!DNL SFTP] Il connettore supporta una chiave OpenSSH di tipo RSA o DSA. Assicurati che il contenuto del tuo file chiave inizi con `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` e termina con `"-----END [RSA/DSA] PRIVATE KEY-----"`. Se il file della chiave privata è un file in formato PPK, utilizza lo strumento PuTTY per convertire da PPK a formato OpenSSH.

**Formato API**

```http
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL SFTP]:

>[!BEGINTABS]

>[!TAB Autenticazione di base]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d  '{
      "name": "SFTP connector with password",
      "description": "SFTP connector password",
      "auth": {
          "specName": "Basic Authentication for sftp",
          "params": {
              "host": "{HOST}",
              "port": 22,
              "userName": "{USERNAME}",
              "password": "{PASSWORD}",
              "maxConcurrentConnections": 1
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
| `auth.params.port` | La porta del server SFTP. Il valore intero predefinito è 22. |
| `auth.params.username` | Nome utente associato al server SFTP. |
| `auth.params.password` | Password associata al server SFTP. |
| `auth.params.maxConcurrentConnections` | Numero massimo di connessioni simultanee specificate durante la connessione di Platform a SFTP. Quando abilitato, questo valore deve essere impostato su almeno 1. |
| `connectionSpec.id` | ID delle specifiche di connessione del server SFTP: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

>[!TAB Autenticazione a chiave pubblica SSH]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SFTP connector with SSH authentication",
      "description": "SFTP connector with SSH authentication",
      "auth": {
          "specName": "SSH PublicKey Authentication for sftp",
          "params": {
              "host": "{HOST}",
              "port": 22,
              "userName": "{USERNAME}",
              "privateKeyContent": "{PRIVATE_KEY_CONTENT}",
              "passPhrase": "{PASSPHRASE}",
              "maxConcurrentConnections": 1

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
| `auth.params.host` | Il nome host del tuo [!DNL SFTP] server. |
| `auth.params.port` | La porta del server SFTP. Il valore intero predefinito è 22. |
| `auth.params.username` | Il nome utente associato al tuo [!DNL SFTP] server. |
| `auth.params.privateKeyContent` | Contenuto della chiave privata SSH codificata Base64. Il tipo di chiave OpenSSH deve essere classificato come RSA o DSA. |
| `auth.params.passPhrase` | La frase o password per decrittografare la chiave privata se il file di chiave o il contenuto della chiave sono protetti da una frase di passaggio. Se PrivateKeyContent è protetto da password, questo parametro deve essere utilizzato con la passphrase PrivateKeyContent come valore. |
| `auth.params.maxConcurrentConnections` | Numero massimo di connessioni simultanee specificate durante la connessione di Platform a SFTP. Quando abilitato, questo valore deve essere impostato su almeno 1. |
| `connectionSpec.id` | La [!DNL SFTP] ID specifica connessione server: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

>[!ENDTABS]

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) della nuova connessione creata. Questo ID è necessario per esplorare il server SFTP nella prossima esercitazione.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un [!DNL SFTP] connessione tramite [!DNL Flow Service] e hanno ottenuto il valore ID univoco della connessione. Puoi usare questo ID connessione per [esplorare gli archivi cloud utilizzando l’API del servizio di flusso](../../explore/cloud-storage.md).
