---
keywords: Experience Platform;home;argomenti popolari;sorgenti;connettori;connettori sorgente;origini sdk;sdk;SDK
title: Configurare le specifiche di autenticazione per l'SDK di Origini
topic-legacy: overview
description: Questo documento fornisce una panoramica delle configurazioni da preparare per utilizzare l'SDK di Origini.
hide: true
hidefromtoc: true
exl-id: 68ed22fe-1f22-46d2-9d58-72ad8a9e6b98
source-git-commit: a3bfd3b87343ca1dd2d122f4f82926082965578c
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 2%

---

# Configurare le specifiche di autenticazione per l&#39;SDK di Origini

Le specifiche di autenticazione definiscono come gli utenti Adobe Experience Platform possono connettersi alla tua origine.

La `authSpec` contiene informazioni sui parametri di autenticazione necessari per collegare un’origine a Platform. Qualsiasi origine può supportare diversi tipi di autenticazione.

## Specifiche di autenticazione

Attualmente, [!DNL Sources SDK] supporta i codici di aggiornamento OAuth 2 e l’autenticazione di base. Vedi le tabelle seguenti per informazioni sull’utilizzo di un codice di aggiornamento OAuth 2 e sull’autenticazione di base

### Codice di aggiornamento OAuth 2

Un codice di aggiornamento OAuth 2 consente l’accesso sicuro a un’applicazione generando un token di accesso temporaneo e un token di aggiornamento. Il token di accesso ti consente di accedere in modo sicuro alle risorse senza dover fornire altre credenziali, mentre il token di aggiornamento ti consente di generare un nuovo token di accesso, una volta che il token di accesso scade.

```json
{
  "name": "OAuth2 Refresh Code",
  "type": "OAuth2RefreshCode",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
    "properties": {
      "host": {
        "type": "string",
        "description": "Enter resource url host path."
      },
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
      "host",
      "accessToken"
    ]
  }
}
```

| Proprietà | Descrizione | Esempio |
| --- | --- | --- |
| `authSpec.name` | Visualizza il nome del tipo di autenticazione supportato. | `oAuth2-refresh-code` |
| `authSpec.type` | Definisce il tipo di autenticazione supportato dall&#39;origine. | `oAuth2-refresh-code` |
| `authSpec.spec` | Contiene informazioni sullo schema, il tipo di dati e le proprietà dell&#39;autenticazione. |
| `authSpec.spec.$schema` | Definisce lo schema utilizzato per l&#39;autenticazione. | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | Definisce il tipo di dati dello schema. | `object` |
| `authSpec.spec.properties` | Contiene informazioni sulle credenziali utilizzate per l&#39;autenticazione. |
| `authSpec.spec.properties.description` | Visualizza una breve descrizione della credenziale. |
| `authSpec.spec.properties.type` | Definisce il tipo di dati della credenziale. | `string` |
| `authSpec.spec.properties.clientId` | L&#39;ID client associato all&#39;applicazione. L’ID client viene utilizzato insieme al segreto client per recuperare il token di accesso. |
| `authSpec.spec.properties.clientSecret` | Il segreto client associato all&#39;applicazione. Il segreto client viene utilizzato insieme all’ID client per recuperare il token di accesso. |
| `authSpec.spec.properties.accessToken` | Il token di accesso autorizza l’accesso sicuro all’applicazione. |
| `authSpec.spec.properties.refreshToken` | Il token di aggiornamento viene utilizzato per generare un nuovo token di accesso, alla scadenza del token di accesso. |
| `authSpec.spec.properties.expirationDate` | Definisce la data di scadenza del token di accesso. |
| `authSpec.spec.properties.refreshTokenUrl` | URL utilizzato per recuperare il token di aggiornamento. |
| `authSpec.spec.properties.accessTokenUrl` | URL utilizzato per recuperare il token di aggiornamento. |
| `authSpec.spec.properties.requestParameterOverride` | Consente di specificare i parametri delle credenziali da ignorare durante l’autenticazione. |
| `authSpec.spec.required` | Visualizza le credenziali necessarie per l&#39;autenticazione. | `accessToken` |

{style=&quot;table-layout:auto&quot;}


### Autenticazione di base

L&#39;autenticazione di base è un tipo di autenticazione che consente di accedere all&#39;applicazione utilizzando una combinazione dell&#39;URL host dell&#39;applicazione, del nome utente dell&#39;account e della password dell&#39;account.

```json
{
  "name": "Basic Authentication",
  "type": "BasicAuthentication",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "defines auth params required for connecting to rest service.",
    "properties": {
      "host": {
        "type": "string",
        "description": "Enter resource url host path"
      },
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
      "host",
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
| `authSpec.spec` | Contiene informazioni sullo schema, il tipo di dati e le proprietà dell&#39;autenticazione. |
| `authSpec.spec.$schema` | Definisce lo schema utilizzato per l&#39;autenticazione. | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | Definisce il tipo di dati dello schema. | `object` |
| `authSpec.spec.description` | Visualizza ulteriori informazioni specifiche per il tipo di autenticazione. |
| `authSpec.spec.properties` | Contiene informazioni sulle credenziali utilizzate per l&#39;autenticazione. |
| `authSpec.spec.properties.host` | L&#39;URL host dell&#39;applicazione. |
| `authSpec.spec.properties.username` | Il nome utente dell&#39;account associato all&#39;applicazione. |
| `authSpec.spec.properties.password` | La password dell&#39;account associata all&#39;applicazione. |
| `authSpec.spec.required` | Specifica i campi richiesti come valori obbligatori da inserire in Platform. | `host` |

{style=&quot;table-layout:auto&quot;}

## Esempio di specifica di autenticazione

Di seguito è riportato un esempio di specifica di autenticazione completata che utilizza un [[!DNL MailChimp Members]](../../tutorials/api/create/marketing-automation/mailchimp-members.md) sorgente.

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
          "host": {
            "type": "string",
            "description": "Enter resource url host path"
          },
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
          "host",
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
          "host": {
            "type": "string",
            "description": "Enter resource url host path."
          },
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
          "host",
          "username",
          "password"
        ]
      }
    }
  ],
```

## Passaggi successivi

Con le specifiche di autenticazione compilate, puoi procedere alla configurazione delle specifiche di origine per l’origine che desideri integrare in Platform. Visualizza il documento su [configurazione delle specifiche di origine](./sourcespec.md) per ulteriori informazioni.
