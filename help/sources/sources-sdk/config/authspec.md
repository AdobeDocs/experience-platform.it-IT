---
keywords: Experience Platform;home;argomenti popolari;origini;connettori;source connectors;sources sdk;sdk;SDK
title: Configurare le specifiche di autenticazione per le origini self-service (Batch SDK)
description: Questo documento fornisce una panoramica delle configurazioni da preparare per utilizzare le origini self-service (Batch SDK).
exl-id: 68ed22fe-1f22-46d2-9d58-72ad8a9e6b98
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 3%

---

# Configurare le specifiche di autenticazione per le origini self-service (Batch SDK)

Le specifiche di autenticazione definiscono il modo in cui gli utenti di Adobe Experience Platform possono connettersi all’origine.

L&#39;array `authSpec` contiene informazioni sui parametri di autenticazione necessari per connettere un&#39;origine ad Experience Platform. Qualsiasi origine può supportare più tipi diversi di autenticazione.

## Specifiche di autenticazione

Origini self-service (Batch SDK) supporta i codici di aggiornamento OAuth 2 e l’autenticazione di base. Consulta le tabelle seguenti per indicazioni sull’utilizzo di un codice di aggiornamento OAuth 2 e di un’autenticazione di base

### Codice di aggiornamento OAuth 2

Un codice di aggiornamento OAuth 2 consente l’accesso sicuro a un’applicazione generando un token di accesso temporaneo e un token di aggiornamento. Il token di accesso ti consente di accedere in modo sicuro alle risorse senza dover fornire altre credenziali, mentre il token di aggiornamento ti consente di generare un nuovo token di accesso, una volta scaduto il token di accesso.

+++Visualizza esempio di codice di aggiornamento OAuth 2

```json
{
  "name": "OAuth2 Refresh Code",
  "type": "OAuth2RefreshCode",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
    "properties": {
      "authorizationTestUrl": {
        "description": "Authorization test url to validate accessToken.",
        "type": "string"
      },
      "clientId": {
        "description": "Client id of user account.",
        "type": "string"
      },
      "clientSecret": {
        "description": "Client secret of user account.",
        "type": "string",
        "format": "password"
      },
      "accessToken": {
        "description": "Access Token",
        "type": "string",
        "format": "password"
      },
      "refreshToken": {
        "description": "Refresh Token",
        "type": "string",
        "format": "password"
      },
      "expirationDate": {
        "description": "Date of token expiry.",
        "type": "string",
        "format": "date",
        "uiAttributes": {
          "hidden": true
        }
      },
      "accessTokenUrl": {
        "description": "Access token url to fetch access token.",
        "type": "string"
      },
      "requestParameterOverride": {
        "type": "object",
        "description": "Specify parameter to override.",
        "properties": {
          "accessTokenField": {
            "description": "Access token field name to override.",
            "type": "string"
          },
          "refreshTokenField": {
            "description": "Refresh token field name to override.",
            "type": "string"
          },
          "expireInField": {
            "description": "ExpireIn field name to override.",
            "type": "string"
          },
          "authenticationMethod": {
            "description": "Authentication method override.",
            "type": "string",
            "enum": [
              "GET",
              "POST"
            ]
          },
          "clientId": {
            "description": "ClientId field name override.",
            "type": "string"
          },
          "clientSecret": {
            "description": "ClientSecret field name override.",
            "type": "string"
          }
        }
      }
    },
    "required": [
      "accessToken"
    ]
  }
}
```

| Proprietà | Descrizione | Esempio |
| --- | --- | --- |
| `authSpec.name` | Visualizza il nome del tipo di autenticazione supportato. | `oAuth2-refresh-code` |
| `authSpec.type` | Definisce il tipo di autenticazione supportato dall&#39;origine. | `oAuth2-refresh-code` |
| `authSpec.spec` | Contiene informazioni sullo schema, il tipo di dati e le proprietà dell’autenticazione. |  |
| `authSpec.spec.$schema` | Definisce lo schema utilizzato per l’autenticazione. | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | Definisce il tipo di dati dello schema. | `object` |
| `authSpec.spec.properties` | Contiene informazioni sulle credenziali utilizzate per l’autenticazione. |  |
| `authSpec.spec.properties.description` | Visualizza una breve descrizione delle credenziali. |  |
| `authSpec.spec.properties.type` | Definisce il tipo di dati delle credenziali. | `string` |
| `authSpec.spec.properties.clientId` | L’ID client associato all’applicazione. L’ID client viene utilizzato insieme al segreto client per recuperare il token di accesso. |  |
| `authSpec.spec.properties.clientSecret` | Il segreto client associato all’applicazione. Il segreto client viene utilizzato insieme all’ID client per recuperare il token di accesso. |  |
| `authSpec.spec.properties.accessToken` | Il token di accesso autorizza l’accesso sicuro all’applicazione. |  |
| `authSpec.spec.properties.refreshToken` | Il token di aggiornamento viene utilizzato per generare un nuovo token di accesso, alla scadenza del token. |  |
| `authSpec.spec.properties.expirationDate` | Definisce la data di scadenza del token di accesso. |  |
| `authSpec.spec.properties.refreshTokenUrl` | URL utilizzato per recuperare il token di aggiornamento. |  |
| `authSpec.spec.properties.accessTokenUrl` | URL utilizzato per recuperare il token di aggiornamento. |  |
| `authSpec.spec.properties.requestParameterOverride` | Consente di specificare i parametri delle credenziali da ignorare durante l&#39;autenticazione. |  |
| `authSpec.spec.required` | Visualizza le credenziali necessarie per l&#39;autenticazione. | `accessToken` |

{style="table-layout:auto"}

+++

### Autenticazione di base

L’autenticazione di base è un tipo di autenticazione che ti consente di accedere all’applicazione utilizzando una combinazione del nome utente dell’account e della password dell’account.

+++ Visualizza esempio di autenticazione di base

```json
{
  "name": "Basic Authentication",
  "type": "BasicAuthentication",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "defines auth params required for connecting to rest service.",
    "properties": {
      "username": {
        "description": "Username to connect rest endpoint.",
        "type": "string"
      },
      "password": {
        "description": "Password to connect rest endpoint.",
        "type": "string",
        "format": "password"
      }
    },
    "required": [
      "username",
      "password"
    ]
  }
}
```

| Proprietà | Descrizione | Esempio |
| --- | --- | --- |
| `authSpec.name` | Visualizza il nome del tipo di autenticazione supportato. | `Basic Authentication` |
| `authSpec.type` | Definisce il tipo di autenticazione supportato dall&#39;origine. | `BasicAuthentication` |
| `authSpec.spec` | Contiene informazioni sullo schema, il tipo di dati e le proprietà dell’autenticazione. |  |
| `authSpec.spec.$schema` | Definisce lo schema utilizzato per l’autenticazione. | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | Definisce il tipo di dati dello schema. | `object` |
| `authSpec.spec.description` | Visualizza ulteriori informazioni specifiche per il tipo di autenticazione. |  |
| `authSpec.spec.properties` | Contiene informazioni sulle credenziali utilizzate per l’autenticazione. |  |
| `authSpec.spec.properties.username` | Il nome utente dell’account associato all’applicazione. |  |
| `authSpec.spec.properties.password` | La password dell&#39;account associata all&#39;applicazione. |  |
| `authSpec.spec.required` | Specifica i campi obbligatori come valori obbligatori da immettere in Experience Platform. | `username` |

{style="table-layout:auto"}

+++

### Autenticazione chiave API {#api-key-authentication}

L’autenticazione tramite chiave API è un metodo sicuro per accedere alle API, fornendo una chiave API e altri parametri di autenticazione rilevanti nelle richieste. A seconda delle informazioni API specifiche, puoi inviare la chiave API come parte dell’intestazione della richiesta, dei parametri della query o del corpo.

I seguenti parametri sono generalmente necessari quando si utilizza l’autenticazione con chiave API:

| Parametro | Tipo | Obbligatorio | Descrizione |
| --- | --- | --- | --- |
| `host` | stringa | No | URL della risorsa. |
| `authKey1` | stringa | Sì | La prima chiave di autenticazione necessaria per l’accesso API. In genere viene inviato nell’intestazione della richiesta o nei parametri di query. |
| `authKey2` | stringa | Facoltativo | Una seconda chiave di autenticazione. Se necessario, questo sistema operativo chiave viene spesso utilizzato per convalidare ulteriormente le richieste. |
| `authKeyN` | stringa | Facoltativo | Variabile di autenticazione aggiuntiva che può essere utilizzata in base alle esigenze, ma con l’API. |

{style="table-layout:auto"}

+++Visualizza autenticazione chiave API

```json
{
  "name": "API Key Authentication",
  "type": "KeyBased",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define authentication parameters required for API access",
    "properties": {
      "host": {
        "type": "string",
        "description": "Enter resource URL host path"
      },
      "authKey1": {
        "type": "string",
        "format": "password",
        "title": "Authentication Key 1",
        "description": "Primary authentication key for accessing the API",
        "restAttributes": {
          "headerParamName": "X-Auth-Key1"
        }
      },
      "authKey2": {
        "type": "string",
        "format": "password",
        "title": "Authentication Key 2",
        "description": "Secondary authentication key, if required",
        "restAttributes": {
          "headerParamName": "X-Auth-Key2"
        }
      },
      ..
      ..
      "authKeyN": {
        "type": "string",
        "format": "password",
        "title": "Additional Authentication Key",
        "description": "Additional authentication keys as needed by the API",
        "restAttributes": {
          "headerParamName": "X-Auth-KeyN"
        }
      }
    },
    "required": [
      "authKey1"
    ]
  }
}
```

+++

### Comportamento di autenticazione

È possibile utilizzare il parametro `restAttributes` per definire la modalità di inclusione della chiave API nella richiesta. Ad esempio, nell&#39;esempio seguente, l&#39;attributo `headerParamName` indica che `X-Auth-Key1` deve essere inviato come intestazione.

```json
  "restAttributes": {
      "headerParamName": "X-Auth-Key1"
  }
```

Ogni chiave di autenticazione (ad esempio `authKey1`, `authKey2` e così via) può essere associata a `restAttributes` per determinare la modalità di invio come richieste.

Se `authKey1` ha `"headerParamName": "X-Auth-Key1"`. L&#39;intestazione della richiesta deve quindi includere `X-Auth-Key:{YOUR_AUTH_KEY1}`. Inoltre, il nome della chiave e `headerParamName` non devono necessariamente essere uguali. Ad esempio:

* `authKey1` può avere `headerParamName: X-Custom-Auth-Key`. Ciò significa che l&#39;intestazione della richiesta utilizzerà `X-Custom-Auth-Key` invece di `authKey1`.
* `authKey1` può invece avere `headerParamName: authKey1`. Ciò significa che il nome dell’intestazione della richiesta rimane invariato.

**Esempio di formato API**

```http
GET /data?X-Auth-Key1={YOUR_AUTH_KEY1}&X-Auth-Key2={YOUR_AUTH_KEY2}
```

## Esempio di specifica di autenticazione

Di seguito è riportato un esempio di specifica di autenticazione completata che utilizza un&#39;origine [[!DNL MailChimp Members]](../../tutorials/api/create/marketing-automation/mailchimp-members.md).

+++Visualizza esempio di specifica di autenticazione

```json
  "authSpec": [
    {
      "name": "OAuth2 Refresh Code",
      "type": "OAuth2RefreshCode",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
        "properties": {
          "authorizationTestUrl": {
            "description": "Authorization test url to validate accessToken.",
            "type": "string"
          },
          "accessToken": {
            "description": "Access Token of mailChimp endpoint.",
            "type": "string",
            "format": "password"
          }
        },
        "required": [
          "accessToken"
        ]
      }
    },
    {
      "name": "Basic Authentication",
      "type": "BasicAuthentication",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines auth params required for connecting to rest service.",
        "properties": {
          "username": {
            "description": "Username to connect mailChimp endpoint.",
            "type": "string"
          },
          "password": {
            "description": "Password to connect mailChimp endpoint.",
            "type": "string",
            "format": "password"
          }
        },
        "required": [
          "username",
          "password"
        ]
      }
    }
  ],
```

+++

## Passaggi successivi

Con le specifiche di autenticazione compilate, puoi procedere alla configurazione delle specifiche di origine per l’origine che desideri integrare in Experience Platform. Per ulteriori informazioni, vedere il documento sulla [configurazione delle specifiche di origine](./sourcespec.md).
