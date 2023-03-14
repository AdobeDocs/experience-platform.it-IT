---
title: Creare una connessione di base SFTP utilizzando l’API del servizio Flusso
description: Scopri come connettere Adobe Experience Platform a un server SFTP (Secure File Transfer Protocol) utilizzando l’API del servizio Flusso.
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: 922e9a26f1791056b251ead2ce2702dfbf732193
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 1%

---

# Creare una connessione di base SFTP utilizzando [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL SFTP] (Secure File Transfer Protocol) tramite il [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): un Experience Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

>[!IMPORTANT]
>
>Si consiglia di evitare il ritorno a capo o a nuove righe durante l’acquisizione di oggetti JSON con un [!DNL SFTP] connessione sorgente. Per aggirare il limite, utilizza un singolo oggetto JSON per riga e utilizza più righe per i file successivi.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a un [!DNL SFTP] server che utilizza [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Per ottenere [!DNL Flow Service] per connettersi a [!DNL SFTP], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Nome o indirizzo IP associato al [!DNL SFTP] server. |
| `port` | Porta del server SFTP a cui ti stai connettendo. Se non specificato, il valore predefinito è `22`. |
| `username` | Il nome utente con accesso al [!DNL SFTP] server. |
| `password` | La password per [!DNL SFTP] server. |
| `privateKeyContent` | Il contenuto della chiave privata SSH con codifica Base64. Il tipo di chiave OpenSSH deve essere classificato come RSA o DSA. |
| `passPhrase` | La passphrase o password per decrittografare la chiave privata se il file di chiave o il contenuto della chiave è protetto da una passphrase. Se il `privateKeyContent` è protetto da password, questo parametro deve essere utilizzato con la passphrase del contenuto della chiave privata come valore. |
| `maxConcurrentConnections` | Questo parametro consente di specificare un limite massimo per il numero di connessioni simultanee che Platform creerà durante la connessione al server SFTP. Devi impostare questo valore su un valore inferiore al limite impostato da SFTP. **Nota**: quando questa impostazione è abilitata per un account SFTP esistente, influirà solo sui flussi di dati futuri e non sui flussi di dati esistenti. |
| `folderPath` | Percorso della cartella a cui desideri fornire l’accesso. [!DNL SFTP] origine, è possibile fornire il percorso della cartella per specificare l&#39;accesso utente alla sottocartella desiderata. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL SFTP] è: `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Il [!DNL SFTP] l&#39;origine supporta sia l&#39;autenticazione di base che l&#39;autenticazione tramite la chiave pubblica SSH. Durante questo passaggio, puoi anche designare il percorso della sottocartella a cui desideri fornire l’accesso.

Per creare un ID di connessione di base, effettua una richiesta POST al `/connections` endpoint durante la fornitura del [!DNL SFTP] credenziali di autenticazione come parte dei parametri della richiesta.

>[!IMPORTANT]
>
>Il [!DNL SFTP] il connettore supporta una chiave OpenSSH di tipo RSA o DSA. Assicurati che il contenuto del file chiave inizi con `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` e termina con `"-----END [RSA/DSA] PRIVATE KEY-----"`. Se il file della chiave privata è in formato PPK, utilizzare lo strumento PuTTY per convertire il formato PPK in OpenSSH.

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
              "maxConcurrentConnections": 5,
              "folderPath": "acme/business/customers/holidaySales"
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
| `auth.params.port` | Porta del server SFTP. Il valore predefinito è 22. |
| `auth.params.username` | Il nome utente associato al server SFTP. |
| `auth.params.password` | La password associata al server SFTP. |
| `auth.params.maxConcurrentConnections` | Il numero massimo di connessioni simultanee specificate durante la connessione di Platform a SFTP. Se attivato, questo valore deve essere impostato su almeno 1. |
| `auth.params.folderPath` | Percorso della cartella a cui desideri fornire l’accesso. |
| `connectionSpec.id` | ID della specifica di connessione al server SFTP: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

>[!TAB Autenticazione chiave pubblica SSH]

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
              "maxConcurrentConnections": 5,
              "folderPath": "acme/business/customers/holidaySales"
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
| `auth.params.host` | Il nome host del [!DNL SFTP] server. |
| `auth.params.port` | Porta del server SFTP. Il valore predefinito è 22. |
| `auth.params.username` | Il nome utente associato al tuo [!DNL SFTP] server. |
| `auth.params.privateKeyContent` | Il contenuto della chiave privata SSH con codifica Base64. Il tipo di chiave OpenSSH deve essere classificato come RSA o DSA. |
| `auth.params.passPhrase` | La passphrase o password per decrittografare la chiave privata se il file di chiave o il contenuto della chiave è protetto da una passphrase. Se PrivateKeyContent è protetto da password, questo parametro deve essere utilizzato con la passphrase di PrivateKeyContent come valore. |
| `auth.params.maxConcurrentConnections` | Il numero massimo di connessioni simultanee specificate durante la connessione di Platform a SFTP. Se attivato, questo valore deve essere impostato su almeno 1. |
| `auth.params.folderPath` | Percorso della cartella a cui desideri fornire l’accesso. |
| `connectionSpec.id` | Il [!DNL SFTP] ID specifica connessione server: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

>[!ENDTABS]

**Risposta**

In caso di esito positivo, la risposta restituisce l’identificatore univoco (`id`) della connessione appena creata. Questo ID è necessario per esplorare il server SFTP nella prossima esercitazione.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un’ [!DNL SFTP] connessione tramite [!DNL Flow Service] e hanno ottenuto il valore ID univoco della connessione. Puoi usare questo ID connessione per [esplorare gli archivi cloud utilizzando l’API del servizio Flow](../../explore/cloud-storage.md).
