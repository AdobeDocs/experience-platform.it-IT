---
title: Endpoint “app_configuration”
description: Scopri come effettuare chiamate all’endpoint /app_configuration nell’API di Reactor.
exl-id: 88a1ec36-b4d2-4fb6-92cb-1da04268492a
source-git-commit: 36320addc790e844a1102314890e8692841dc5d0
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 96%

---

# Endpoint “app_configuration”

>[!WARNING]
>
>L’implementazione dell’endpoint `/app_configurations` è in continua evoluzione, di pari passo con l’aggiunta, la rimozione e la rielaborazione delle varie funzioni.

Le configurazioni dell’app consentono di memorizzare le credenziali e recuperarle per un utilizzo successivo. L’endpoint `/app_configurations` nell’API di Reactor consente di gestire programmaticamente le configurazioni di app all’interno dell’applicazione Experience.

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’[API di Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Prima di continuare, consulta la [guida introduttiva](../getting-started.md) per informazioni importanti su come eseguire l’autenticazione nell’API.

## Recuperare un elenco di configurazioni di app {#list}

**Formato API**

```http
GET /companies/{COMPANY_ID}/app_configurations
```

| Parametro | Descrizione |
| --- | --- |
| `COMPANY_ID` | `id` dell’[azienda](./companies.md) proprietaria delle configurazioni di app. |

{style="table-layout:auto"}

>[!NOTE]
>
>Utilizzando i parametri di query, le configurazioni di app elencate possono essere filtrate in base ai seguenti attributi:<ul><li>`app_id`</li><li>`created_at`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`updated_at`</li></ul>Per ulteriori informazioni, consulta la guida su come [filtrare le risposte](../guides/filtering.md).

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/app_configurations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di configurazioni di app.

```json
{
  "data": [
    {
      "id": "AC40c339ab80d24c958b90d67b698602eb",
      "type": "app_configurations",
      "attributes": {
        "created_at": "2020-12-14T17:31:10.626Z",
        "updated_at": "2020-12-14T17:31:10.626Z",
        "app_id": "com.adobe.test_app",
        "name": "Kessel Apns App",
        "platform": "mobile",
        "messaging_service": "apns",
        "key_type": "p8_file"
      },
      "relationships": {
        "company": {
          "links": {
            "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
          },
          "data": {
            "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
            "type": "companies"
          }
        }
      },
      "links": {
        "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
        "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## Cercare una configurazione di app {#lookup}

Per cercare una configurazione di app occorre specificare il relativo ID nel percorso di una richiesta GET.

**Formato API**

```http
GET /app_configurations/{APP_CONFIGURATION_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `APP_CONFIGURATION_ID` | `id` della configurazione di app che desideri cercare. |

{style="table-layout:auto"}

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della configurazione di app.

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:10.626Z",
      "app_id": "com.adobe.test_app",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## Creare una configurazione di app {#create}

Per creare una nuova configurazione di app, devi eseguire una richiesta POST.

**Formato API**

```http
POST /companies/{COMPANY_ID}/app_configurations
```

| Parametro | Descrizione |
| --- | --- |
| `COMPANY_ID` | `id` dell’[azienda](./companies.md) in cui stai definendo la configurazione di app. |

{style="table-layout:auto"}

**Richiesta**

```shell
curl -X POST \
  https://reactor.adobe.io/companies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "attributes": {
            "name": "Kessel Apns App",
            "app_id": "com.adobe.test_app",
            "platform": "mobile",
            "messaging_service": "apns",
            "key_type": "p8_file",
            "push_credential": {
              "bundleId": "com.adobe.test_app",
              "keyId": "{KEY_ID}",
              "p8": "{SECRET}",
              "teamId": "{TEAM_ID}"
            }
          },
          "type": "app_configurations"
        }
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `platform` | Piattaforma su cui viene eseguita l’applicazione (web o mobile). Questo determina quali servizi di messaggistica sono disponibili. |
| `messaging_service` | Il servizio di messaggistica associato all’app, ad esempio [Apple Push Notification Service (APNs)](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html) e [Firebase Cloud Messaging (FCM)](https://firebase.google.com/docs/cloud-messaging). Questo determina quali tipi di chiave possono essere utilizzati. |
| `key_type` | Rappresenta il protocollo supportato da un fornitore di servizi push e determina il formato dell’oggetto `push_credential`. Man mano che i protocolli si evolvono per i servizi di messaggistica, vengono creati nuovi valori `key_type` per supportare i protocolli aggiornati. |
| `push_credential` | Valore effettivo delle credenziali, che a riposo è crittografato. Questo campo non viene normalmente decrittografato né incluso nelle risposte API. Solo alcuni servizi di Adobe possono ricevere una risposta contenente credenziali push decrittografate. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della nuova configurazione di app appena creata.

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:10.626Z",
      "app_id": "com.adobe.test_app",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## Aggiornare una configurazione di app

Per aggiornare la configurazione di un’app, devi includere il relativo ID nel percorso di una richiesta PATCH.

**Formato API**

```http
PATCH /app_configurations/{APP_CONFIGURATION_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `APP_CONFIGURATION_ID` | `id` della configurazione di app che desideri aggiornare. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente aggiorna l’`app_id` per la configurazione di un’app esistente.

```shell
curl -X PATCH \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "attributes": {
            "app_id": "com.adobe.test_app_2"
          },
          "id": "AC40c339ab80d24c958b90d67b698602eb",
          "type": "app_configurations"
        }
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `attributes` | Oggetto le cui proprietà rappresentano gli attributi da aggiornare per la configurazione di app. Ogni chiave rappresenta il particolare attributo di configurazione di app da aggiornare, insieme al valore corrispondente a cui deve essere aggiornato.<br><br>I seguenti attributi possono essere aggiornati per le configurazioni di app:<ul><li>`app_id`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`push_credential`</li></ul> |
| `id` |  `id` della configurazione di app che desideri aggiornare. Deve corrispondere al valore `{APP_CONFIGURATION_ID}` fornito nel percorso della richiesta. |
| `type` | Tipo di risorsa da aggiornare. Per questo endpoint, il valore deve essere `app_configurations`. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della configurazione di app aggiornata.

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:21.787Z",
      "app_id": "com.adobe.test_app_2",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## Eliminare una configurazione di app

Puoi eliminare una configurazione di app includendo il relativo ID nel percorso di una richiesta DELETE.

**Formato API**

```http
DELETE /app_configurations/{APP_CONFIGURATION_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `APP_CONFIGURATION_ID` | `id` della configurazione di app che desideri eliminare. |

{style="table-layout:auto"}

**Richiesta**

```shell
curl -X DELETE \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 204 (nessun contenuto) senza corpo di risposta, a indicare che la configurazione di app è stata eliminata.
