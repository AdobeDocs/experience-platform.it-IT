---
title: Endpoint di configurazione dell'app
description: Scopri come effettuare chiamate all’endpoint /app_configuration nell’API del reattore.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 7%

---

# Endpoint di configurazione dell&#39;app

>[!WARNING]
>
>L’implementazione dell’endpoint `/app_configurations` è in continuo cambiamento in seguito all’aggiunta, alla rimozione e alla rielaborazione delle funzioni.

Le configurazioni dell’app consentono di memorizzare le credenziali e recuperarle per un utilizzo successivo. L’endpoint `/app_configurations` nell’API di Reactor consente di gestire programmaticamente le configurazioni dell’app all’interno dell’applicazione di esperienza.

## Introduzione

L&#39;endpoint utilizzato in questa guida fa parte dell&#39; [API del reattore](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Prima di continuare, controlla la [guida introduttiva](../getting-started.md) per informazioni importanti su come eseguire l&#39;autenticazione nell&#39;API.

## Recupera un elenco di configurazioni dell’app {#list}

**Formato API**

```http
GET /companies/{COMPANY_ID}/app_configurations
```

| Parametro | Descrizione |
| --- | --- |
| `COMPANY_ID` | La `id` della [società](./companies.md) proprietaria delle configurazioni dell&#39;app. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Utilizzando i parametri di query, le configurazioni dell’app elencate possono essere filtrate in base ai seguenti attributi:<ul><li>`app_id`</li><li>`created_at`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`updated_at`</li></ul>Per ulteriori informazioni, consulta la guida sulle [risposte relative al filtro](../guides/filtering.md) .

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/app_configurations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

Una risposta corretta restituisce un elenco di configurazioni dell&#39;app.

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

## Cercare una configurazione dell’app {#lookup}

Puoi cercare una configurazione dell’app fornendo il relativo ID nel percorso di una richiesta GET.

**Formato API**

```http
GET /app_configurations/{APP_CONFIGURATION_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `APP_CONFIGURATION_ID` | La `id` della configurazione dell&#39;app che desideri cercare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

```shell
curl -X GET \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Risposta**

Una risposta corretta restituisce i dettagli della configurazione dell’app.

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

## Creare una configurazione dell’app {#create}

Puoi creare una nuova configurazione dell’app effettuando una richiesta di POST.

**Formato API**

```http
POST /companies/{COMPANY_ID}/app_configurations
```

| Parametro | Descrizione |
| --- | --- |
| `COMPANY_ID` | La `id` della [società](./companies.md) in cui stai definendo la configurazione dell&#39;app. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

```shell
curl -X POST \
  https://reactor.adobe.io/companies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
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
| `platform` | Piattaforma su cui viene eseguita l&#39;applicazione (web o mobile). Questo determina quali servizi di messaggistica sono disponibili. |
| `messaging_service` | Il servizio di messaggistica associato all&#39;app, ad esempio [APN (Apple Push Notification Service)](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html) e [FCM (Firebase Cloud Messaging)](https://firebase.google.com/docs/cloud-messaging). Questo determina quali tipi di chiave possono essere utilizzati. |
| `key_type` | Rappresenta il protocollo supportato da un fornitore di servizi push e determina il formato dell&#39;oggetto `push_credential`. Man mano che i protocolli si evolvono per i servizi di messaggistica, vengono creati nuovi valori `key_type` per supportare i protocolli aggiornati. |
| `push_credential` | Valore credenziale effettivo, crittografato a riposo. Questo campo non viene normalmente decrittografato o incluso nelle risposte API. Solo alcuni servizi di Adobe possono ricevere una risposta contenente una credenziale push decrittografata. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce i dettagli della nuova configurazione dell’app appena creata.

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

## Aggiornare la configurazione dell’app

Puoi aggiornare una configurazione dell’app includendo il relativo ID nel percorso di una richiesta PUT.

**Formato API**

```http
PUT /app_configurations/{APP_CONFIGURATION_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `APP_CONFIGURATION_ID` | La `id` della configurazione dell&#39;app che desideri aggiornare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La richiesta seguente aggiorna il `app_id` per una configurazione dell&#39;app esistente.

```shell
curl -X PUT \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
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
| `attributes` | Un oggetto le cui proprietà rappresentano gli attributi da aggiornare per la configurazione dell’app. Ogni chiave rappresenta il particolare attributo di configurazione dell’app da aggiornare, insieme al valore corrispondente a cui deve essere aggiornato.<br><br>I seguenti attributi possono essere aggiornati per le configurazioni dell’app:<ul><li>`app_id`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`push_credential`</li></ul> |
| `id` | La `id` della configurazione dell&#39;app che desideri aggiornare. Questo deve corrispondere al valore `{APP_CONFIGURATION_ID}` fornito nel percorso della richiesta. |
| `type` | Tipo di risorsa da aggiornare. Per questo endpoint, il valore deve essere `app_configurations`. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce i dettagli della configurazione dell’app aggiornata.

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

Puoi eliminare una configurazione dell’app includendo il relativo ID nel percorso di una richiesta DELETE.

**Formato API**

```http
DELETE /app_configurations/{APP_CONFIGURATION_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `APP_CONFIGURATION_ID` | La `id` della configurazione dell&#39;app che desideri eliminare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

```shell
curl -X DELETE \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (nessun contenuto) senza corpo di risposta, a indicare che la configurazione dell’app è stata eliminata.
