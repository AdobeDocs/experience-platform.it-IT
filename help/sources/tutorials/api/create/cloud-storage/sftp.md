---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creazione di un connettore SFTP tramite l'API del servizio di flusso
topic: overview
translation-type: tm+mt
source-git-commit: a038abcdc411b638f41b94dea0140518c12f5600

---


# Creazione di un connettore SFTP tramite l&#39;API del servizio di flusso

Flow Service è utilizzato per raccogliere e centralizzare i dati dei clienti da varie origini diverse all&#39;interno di Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l&#39;API del servizio di flusso per guidarti attraverso i passaggi necessari per connettere Experience Platform a un server SFTP (Secure File Transfer Protocol).

Se preferisci utilizzare l’interfaccia utente in Experience Platform, l’esercitazione [](../../../ui/create/cloud-storage/ftp-sftp.md) UI fornisce istruzioni dettagliate per eseguire azioni simili.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie fonti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi della piattaforma.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che dividono una singola istanza della piattaforma in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi correttamente a un server SFTP tramite l&#39;API del servizio di flusso.

### Raccogli credenziali richieste

Affinché il servizio di flusso possa connettersi a SFTP, è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Nome o indirizzo IP associato al server SFTP. |
| `username` | Il nome utente con accesso al server SFTP. |
| `password` | La password per il server SFTP. |

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione [come leggere le chiamate](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi della piattaforma Experience.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle API della piattaforma, dovete prima completare l&#39;esercitazione [di](../../../../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in Experience Platform, incluse quelle appartenenti al servizio di flusso, sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API della piattaforma richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

* Content-Type: `application/json`

## Cercare le specifiche di connessione

Per creare una connessione SFTP, in Flow Service deve esistere una serie di specifiche di connessione SFTP. Il primo passo per collegare Platform a SFTP è recuperare queste specifiche.

**Formato API**

Ogni origine disponibile dispone di un proprio set di specifiche di connessione per descrivere le proprietà del connettore, ad esempio i requisiti di autenticazione. Potete cercare le specifiche di connessione per SFTP eseguendo una richiesta GET e utilizzando i parametri di query.

L&#39;invio di una richiesta GET senza parametri di query restituirà le specifiche di connessione per tutte le origini disponibili. Potete includere la query `property=name=="sftp"` per ottenere informazioni specifiche per SFTP.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="sftp"
```

**Richiesta**

La richiesta seguente recupera le specifiche di connessione per un server SFTP.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="sftp"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce la specifica di connessione per il server SFTP, incluso il relativo identificatore univoco (`id`). Questo ID è richiesto nel passaggio successivo per creare una connessione di base.

```json
{
    "items": [
        {
            "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
            "name": "sftp",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication for sftp",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to sftp",
                        "properties": {
                            "host": {
                                "type": "string",
                                "description": "Specify the name or IP address of the SFTP server."
                            },
                            "userName": {
                                "type": "string",
                                "description": "Specify the user who has access to the SFTP server."
                            },
                            "password": {
                                "type": "string",
                                "description": "Specify the password for the user (userName).",
                                "format": "password"
                            }
                        },
                        "required": [
                            "host",
                            "userName",
                            "password"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Creazione di una connessione di base

Una connessione di base specifica un&#39;origine e contiene le credenziali per tale origine. È necessaria una sola connessione di base per account SFTP, in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

**Formato API**

```http
POST /connections
```

**Richiesta**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  "auth": {
        "specName": "Basic Authentication for sftp",
        "params": {
            "host": "{HOST_NAME}",
            "userName": "{USER_NAME}",
            "password": "{PASSWORD}"
        }
    },
    "connectionSpec": {
        "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
        "version": "1.0"
    }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.host` | Il nome host del server SFTP. |
| `auth.params.username` | Nome utente associato al server SFTP. |
| `auth.params.password` | La password associata al server SFTP. |
| `connectionSpec.id` | Specifica di connessione `id` del server SFTP recuperato nel passaggio precedente. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) della connessione di base appena creata. Questo ID è necessario per esplorare il server SFTP nell&#39;esercitazione successiva.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione SFTP utilizzando l&#39;API del servizio di flusso e hai ottenuto il valore ID univoco della connessione. Potete utilizzare questo ID connessione per [esplorare gli storage cloud utilizzando l&#39;API](../../explore/cloud-storage.md) del servizio di flusso o per [assimilare i dati del parquet tramite l&#39;API](../../cloud-storage-parquet.md)del servizio di flusso.
