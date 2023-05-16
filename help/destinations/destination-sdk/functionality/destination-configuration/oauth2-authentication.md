---
description: Questa pagina descrive i vari flussi di autenticazione OAuth 2 supportati da Destination SDK e fornisce istruzioni per configurare l’autenticazione OAuth 2 per la destinazione.
title: Autenticazione OAuth 2
exl-id: 280ecb63-5739-491c-b539-3c62bd74e433
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '2155'
ht-degree: 4%

---

# Autenticazione OAuth 2

Destination SDK supporta diversi metodi di autenticazione per la destinazione. Tra questi c&#39;è l&#39;opzione per l&#39;autenticazione alla tua destinazione utilizzando il [Framework di autenticazione di OAuth 2](https://tools.ietf.org/html/rfc6749).

Questa pagina descrive i vari flussi di autenticazione OAuth 2 supportati da Destination SDK e fornisce istruzioni per configurare l’autenticazione OAuth 2 per la destinazione.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Tipi di integrazione supportati {#supported-integration-types}

Per informazioni dettagliate sui tipi di integrazioni che supportano le funzionalità descritte in questa pagina, consulta la tabella seguente.

| Tipo di integrazione | Supporta funzionalità |
|---|---|
| Integrazioni in tempo reale (streaming) | Sì |
| Integrazioni basate su file (batch) | No |

## Come aggiungere i dettagli di autenticazione OAuth 2 alla configurazione di destinazione {#how-to-setup}

### Prerequisiti nel sistema {#prerequisites}

Come primo passo, devi creare un’app nel tuo sistema per Adobe Experience Platform o registrare in altro modo l’Experience Platform nel tuo sistema. L&#39;obiettivo è quello di generare un ID client e un segreto client, necessari per autenticare l&#39;Experience Platform nella destinazione. Come parte di questa configurazione del sistema, hai bisogno degli URL di reindirizzamento/callback di Adobe Experience Platform OAuth 2, che puoi ottenere dall’elenco seguente.

* `https://platform-va7.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-nld2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-aus5.adobe.io/data/core/activation/oauth/api/v1/callback`

>[!IMPORTANT]
>
>Il passaggio per registrare un URL di reindirizzamento/callback per Adobe Experience Platform nel sistema è necessario solo per il [OAuth 2 con codice di autorizzazione](oauth2-authentication.md#authorization-code) tipo di sovvenzione. Per gli altri due tipi di sovvenzione supportati (password e credenziali client), puoi saltare questo passaggio.

Alla fine di questo passaggio, dovresti avere:
* Un ID cliente;
* un segreto cliente;
* URL di callback del Adobe (per la concessione del codice di autorizzazione).

### Cosa devi fare nella Destination SDK {#to-do-in-destination-sdk}

Per configurare l’autenticazione OAuth 2 per la destinazione nell’Experience Platform, devi aggiungere i dettagli OAuth 2 al [configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md), `customerAuthenticationConfigurations` parametro . Vedi [autenticazione cliente](../../functionality/destination-configuration/customer-authentication.md) per esempi dettagliati. Istruzioni specifiche su quali campi devi aggiungere al modello di configurazione, a seconda del tipo di concessione di autenticazione OAuth 2, sono più avanti in questa pagina.

## Tipi di sovvenzione OAuth 2 supportati {#oauth2-grant-types}

L’Experience Platform supporta i tre tipi di sovvenzione OAuth 2 nella tabella seguente. Se disponi di una configurazione OAuth 2 personalizzata, Adobe è in grado di supportarla con l’aiuto di campi personalizzati nella tua integrazione. Per ulteriori informazioni, consulta le sezioni relative a ciascun tipo di sovvenzione.

>[!IMPORTANT]
>
>* Fornisci i parametri di input come indicato nelle sezioni seguenti. I sistemi interni di Adobe si collegano al sistema di autenticazione della piattaforma e acquisiscono i parametri di output, utilizzati per autenticare l’utente e mantenere l’autenticazione nella destinazione.
>* I parametri di input evidenziati in grassetto nella tabella sono parametri richiesti nel flusso di autenticazione OAuth 2. Gli altri parametri sono facoltativi. Ci sono altri parametri di input personalizzati che non vengono visualizzati qui, ma sono descritti in dettaglio nelle sezioni [Personalizzare la configurazione OAuth 2](#customize-configuration) e [Accedere al token refresh](#access-token-refresh).


| Sovvenzione OAuth 2 | Ingressi | Uscite |
|---------|----------|---------|
| Codice di autorizzazione | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>scope</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Password | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>scope</li><li><b>accessTokenUrl</b></li><li><b>username</b></li><li><b>password</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Credenziali client | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>scope</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

Nella tabella riportata sopra sono elencati i campi utilizzati nei flussi OAuth 2 standard. Oltre a questi campi standard, diverse integrazioni dei partner possono richiedere ingressi e uscite aggiuntive. Adobe ha progettato un framework flessibile di autenticazione/autorizzazione OAuth 2 per Destination SDK che può gestire le varianti al pattern di campi standard di cui sopra, mentre supporta un meccanismo per rigenerare automaticamente le uscite non valide, ad esempio i token di accesso scaduti.

L&#39;output in tutti i casi include un token di accesso, utilizzato da Experience Platform per autenticare e mantenere l&#39;autenticazione nella destinazione.

Il sistema progettato da Adobe per l’autenticazione OAuth 2:
* Supporta tutte e tre le sovvenzioni OAuth 2 tenendo conto delle eventuali varianti, ad esempio campi di dati aggiuntivi, chiamate API non standard e altro ancora.
* Supporta token di accesso con diversi valori di ciclo di vita, siano essi 90 giorni, 30 minuti o qualsiasi altro valore di ciclo di vita specificato.
* Supporta i flussi di autorizzazione OAuth 2 con o senza token di aggiornamento.

## OAuth 2 con codice di autorizzazione {#authorization-code}

Se la destinazione supporta un flusso di codice di autorizzazione OAuth 2.0 standard (consulta la sezione [Specifiche degli standard RFC](https://tools.ietf.org/html/rfc6749#section-4.1)) o una sua variazione, consulta i campi obbligatori e facoltativi di seguito:

| Sovvenzione OAuth 2 | Ingressi | Uscite |
|---------|----------|---------|
| Codice di autorizzazione | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>scope</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

Per impostare questo metodo di autenticazione per la destinazione, aggiungi le seguenti righe alla configurazione quando [creare una configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md):

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_AUTHORIZATION_CODE",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "authorizationUrl": "https://www.moviestar.com/dialog/OAuth",
      "refreshTokenUrl": "https://api.moviestar.com/OAuth/refresh_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
//...
}
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `authType` | Stringa | Usa &quot;OAUTH2&quot;. |
| `grant` | Stringa | Utilizzare &quot;OAUTH2_AUTHORIZATION_CODE&quot;. |
| `accessTokenUrl` | Stringa | L’URL sul tuo lato, che rilascia token di accesso e, facoltativamente, aggiorna i token. |
| `authorizationUrl` | Stringa | L’URL del server di autorizzazione, in cui l’utente viene reindirizzato per accedere all’applicazione. |
| `refreshTokenUrl` | Stringa | *Facoltativo.* L’URL sul tuo lato, che causa problemi con i token di aggiornamento. Spesso, il `refreshTokenUrl` è uguale a `accessTokenUrl`. |
| `clientId` | Stringa | L&#39;ID client che il sistema assegna a Adobe Experience Platform. |
| `clientSecret` | Stringa | Il segreto client assegnato dal sistema a Adobe Experience Platform. |
| `scope` | Elenco delle stringhe | *Facoltativo*. Imposta l’ambito di ciò che il token di accesso consente ad Experience Platform di eseguire sulle risorse. Esempio: &quot;leggi, scrivi&quot;. |

{style="table-layout:auto"}

## OAuth 2 con concessione password

Per la concessione della password OAuth 2 (leggere il [Specifiche degli standard RFC](https://tools.ietf.org/html/rfc6749#section-4.3)), Experience Platform richiede il nome utente e la password dell’utente. Nel flusso di autenticazione, Experience Platform scambia queste credenziali per un token di accesso e, facoltativamente, un token di aggiornamento.
L&#39;Adobe utilizza gli input standard riportati di seguito per semplificare la configurazione della destinazione, con la possibilità di ignorare i valori:

| Sovvenzione OAuth 2 | Ingressi | Uscite |
|---------|----------|---------|
| Password | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>scope</li><li><b>accessTokenUrl</b></li><li><b>username</b></li><li><b>password</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

>[!NOTE]
>
> Non è necessario aggiungere parametri per `username` e `password` nella configurazione seguente. Quando aggiungi `"grant": "OAUTH2_PASSWORD"` nella configurazione di destinazione, il sistema richiederà all&#39;utente di fornire un nome utente e una password nell&#39;interfaccia utente di Experience Platform, quando si autentica nella tua destinazione.

Per impostare questo metodo di autenticazione per la destinazione, aggiungi le seguenti righe alla configurazione quando [creare una configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md):

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_PASSWORD",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `authType` | Stringa | Usa &quot;OAUTH2&quot;. |
| `grant` | Stringa | Utilizzare &quot;OAUTH2_PASSWORD&quot;. |
| `accessTokenUrl` | Stringa | L’URL sul tuo lato, che rilascia token di accesso e, facoltativamente, aggiorna i token. |
| `clientId` | Stringa | L&#39;ID client che il sistema assegna a Adobe Experience Platform. |
| `clientSecret` | Stringa | Il segreto client assegnato dal sistema a Adobe Experience Platform. |
| `scope` | Elenco delle stringhe | *Facoltativo*. Imposta l’ambito di ciò che il token di accesso consente ad Experience Platform di eseguire sulle risorse. Esempio: &quot;leggi, scrivi&quot;. |

{style="table-layout:auto"}

## Concessione di OAuth 2 con credenziali client

Puoi configurare le credenziali client OAuth 2 (leggi la sezione [Specifiche degli standard RFC](https://tools.ietf.org/html/rfc6749#section-4.4)), che supporta gli ingressi e le uscite standard elencati di seguito. Puoi personalizzare i valori. Vedi [Personalizzare la configurazione OAuth 2](#customize-configuration) per i dettagli.

| Sovvenzione OAuth 2 | Ingressi | Uscite |
|---------|----------|---------|
| Credenziali client | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>scope</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

Per impostare questo metodo di autenticazione per la destinazione, aggiungi le seguenti righe alla configurazione quando [creare una configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md):

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_CLIENT_CREDENTIALS",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "refreshTokenUrl": "https://api.moviestar.com/OAuth/refresh_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
//...
}
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `authType` | Stringa | Usa &quot;OAUTH2&quot;. |
| `grant` | Stringa | Utilizzare &quot;OAUTH2_CLIENT_CREDENTIALS&quot;. |
| `accessTokenUrl` | Stringa | L’URL del server di autorizzazione che rilascia un token di accesso e un token di aggiornamento facoltativo. |
| `refreshTokenUrl` | Stringa | *Facoltativo.* L’URL sul tuo lato, che causa problemi con i token di aggiornamento. Spesso, il `refreshTokenUrl` è uguale a `accessTokenUrl`. |
| `clientId` | Stringa | L&#39;ID client che il sistema assegna a Adobe Experience Platform. |
| `clientSecret` | Stringa | Il segreto client assegnato dal sistema a Adobe Experience Platform. |
| `scope` | Elenco delle stringhe | *Facoltativo*. Imposta l’ambito di ciò che il token di accesso consente ad Experience Platform di eseguire sulle risorse. Esempio: &quot;leggi, scrivi&quot;. |

{style="table-layout:auto"}

## Personalizzare la configurazione OAuth 2 {#customize-configuration}

Le configurazioni descritte nelle sezioni sopra descrivono le sovvenzioni standard OAuth 2. Tuttavia, il sistema progettato da Adobe offre flessibilità e consente di utilizzare parametri personalizzati per qualsiasi variante della sovvenzione OAuth 2. Per personalizzare le impostazioni standard di OAuth 2, utilizza il `authenticationDataFields` , come illustrato negli esempi seguenti.

### Esempio 1: Utilizzo `authenticationDataFields` per acquisire informazioni provenienti dalla risposta di autenticazione {#example-1}

In questo esempio, una piattaforma di destinazione dispone di token di aggiornamento che scadono dopo un certo periodo di tempo. In questo caso, il partner imposta il `refreshTokenExpiration` campo personalizzato per ottenere la scadenza del token di aggiornamento dal `refresh_token_expires_in` nella risposta API.

```json
{
   "customerAuthenticationConfigurations":[
      {
         "authType":"OAUTH2",
         "options":{
            
         },
         "grant":"OAUTH2_AUTHORIZATION_CODE",
         "accessTokenUrl":"https://api.moviestar.com/OAuth/access_token",
         "authorizationUrl":"https://api.moviestar.com/OAuth/authorization",
         "scope":[
            "read",
            "write",
            "delete"
         ],
         "refreshTokenUrl":"https://api.moviestar.com/OAuth/accessToken",
         "clientSecret":"client-secret-here",
         "authenticationDataFields":[
            {
               "name":"refreshTokenExpiration",
               "title":"Refresh Token Expires In",
               "description":"Time in seconds when the refresh token will expire",
               "type":"string",
               "isRequired":false,
               "source":"CUSTOMER",
               "authenticationResponsePath":"refresh_token_expires_in"
            }
         ]
      }
   ]
}  
```

### Esempio 2: Utilizzo `authenticationDataFields` per fornire un token di aggiornamento speciale {#example-2}

In questo esempio, un partner imposta la propria destinazione per fornire un token di aggiornamento speciale. Inoltre, la data di scadenza dei token di accesso non viene restituita nella risposta API, in modo che possano codificare un valore predefinito, in questo caso 3600 secondi.

```json
      "authenticationDataFields": [
        {
            "name": "refreshToken",
            "value": "special_refresh_token"
        },
        {
            "name": "expiresIn",
            "value": 3600
        } 
      ]
```

### Esempio 3: L’utente immette l’ID client e il segreto client quando configura la destinazione {#example-3}

In questo esempio, invece di creare un ID client globale e un segreto client come mostrato nella sezione . [Prerequisiti nel sistema](#prerequisites), il cliente deve inserire l’ID client, il segreto client e l’ID account (l’ID che il cliente utilizza per accedere alla destinazione)

```json
{
    //...
    "customerAuthenticationConfigurations": [
        {
            "authType": "OAUTH2",
            "grant": "OAUTH2_CLIENT_CREDENTIALS",
            "authenticationDataFields": [
                {
                    "name": "clientId",
                    "title": "Client ID",
                    "description": "Client ID",
                    "type": "string",
                    "isRequired": true,
                    "source": "CUSTOMER"
                },
                {
                    "name": "clientSecret",
                    "title": "Client Secret",
                    "description": "Client Secret",
                    "type": "string",
                    "isRequired": true,
                    "format": "password",
                    "source": "CUSTOMER"
                },
                {
                    "name": "moviestarId",
                    "title": "Moviestar ID",
                    "description": "Moviestar ID",
                    "type": "string",
                    "isRequired": true,
                    "source": "CUSTOMER"
                }
            ],
            "accessTokenRequest": {
                "destinationServerType": "URL_BASED",
                "urlBasedDestination": {
                    "url": {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "https://{{ authData.moviestarId }}.yourdestination.com/identity/oauth/token"
                    }
                },
                "httpTemplate": {
                    "requestBody": {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ formUrlEncode('grant_type', 'client_credentials', 'client_id', authData.clientId, 'client_secret', authData.clientSecret) | raw }}"
                    },
                    "httpMethod": "POST",
                    "contentType": "application/x-www-form-urlencoded"
                },
                "responseFields": [
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.access_token }}",
                        "name": "accessToken"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.scope }}",
                        "name": "scope"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.token_type }}",
                        "name": "tokenType"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.expires_in }}",
                        "name": "expiresIn"
                    }
                ]
            }
        }
    ]
//...
}
```



Puoi utilizzare i seguenti parametri in `authenticationDataFields` per personalizzare la configurazione OAuth 2:

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `authenticationDataFields.name` | Stringa | Nome del campo personalizzato. |
| `authenticationDataFields.title` | Stringa | Titolo che è possibile specificare per il campo personalizzato. |
| `authenticationDataFields.description` | Stringa | Descrizione del campo dati personalizzato configurato. |
| `authenticationDataFields.type` | Stringa | Definisce il tipo di campo dati personalizzato. <br> Valori accettati: `string`, `boolean`, `integer` |
| `authenticationDataFields.isRequired` | Booleano | Specifica se il campo dati personalizzato è richiesto nel flusso di autenticazione. |
| `authenticationDataFields.format` | Stringa | Quando selezioni `"format":"password"`, Adobe crittografa il valore del campo dati di autenticazione . Quando utilizzato con `"fieldType": "CUSTOMER"`, nasconde anche l’input nell’interfaccia utente quando l’utente digita nel campo . |
| `authenticationDataFields.fieldType` | Stringa | Indica se l’input proviene dal partner (tu) o dall’utente, quando configura la destinazione nell’Experience Platform. |
| `authenticationDataFields.value` | Stringa. Booleano. Intero | Valore del campo dati personalizzato. Il valore corrisponde al tipo scelto da `authenticationDataFields.type`. |
| `authenticationDataFields.authenticationResponsePath` | Stringa | Indica il campo dal percorso di risposta API a cui si sta facendo riferimento. |

{style="table-layout:auto"}

## Accedere al token refresh {#access-token-refresh}

Adobe ha progettato un sistema che aggiorna i token di accesso scaduti senza richiedere all’utente di effettuare nuovamente l’accesso alla piattaforma. Il sistema è in grado di generare un nuovo token in modo che l’attivazione alla destinazione continui senza soluzione di continuità per il cliente.

Per impostare l’aggiornamento del token di accesso, potrebbe essere necessario configurare una richiesta HTTP modellata che consenta ad Adobe di ottenere un nuovo token di accesso, utilizzando un token di aggiornamento. Se il token di accesso è scaduto, Adobe accetta la richiesta temporanea fornita dall’utente, aggiungendo i parametri forniti. Utilizza la `accessTokenRequest` per configurare un meccanismo di aggiornamento del token di accesso.


```json
{
   "customerAuthenticationConfigurations":[
      {
         "authType":"OAUTH2",
         "grant":"OAUTH2_CLIENT_CREDENTIALS",
         "accessTokenRequest":{
            "destinationServerType":"URL_BASED",
            "urlBasedDestination":{
               "url":{
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"https://{{authData.customerId}}.yourdestination.com/identity/oauth/token"
               }
            },
            "httpTemplate":{
               "requestBody":{
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ formUrlEncode('grant_type', 'client_credentials', 'client_id', authData.clientId, 'client_secret', authData.clientSecret) | raw }}"
               },
               "httpMethod":"POST",
               "contentType":"application/x-www-form-urlencoded",
               "headers":[
                  
               ]
            },
            "responseFields":[
               {
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ response.body.expires_in }}",
                  "name":"expiresIn"
               },
               {
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ response.body.access_token }}",
                  "name":"accessToken"
               }
            ],
            "validations":[
               {
                  "name":"access_token validation",
                  "actualValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"{{response.body.access_token is empty }}"
                  },
                  "expectedValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"false"
                  }
               },
               {
                  "name":"response status",
                  "actualValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"{{ response.status }}"
                  },
                  "expectedValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"200"
                  }
               }
            ]
         }
      }
   ]
}
```

Puoi utilizzare i seguenti parametri in `accessTokenRequest` per personalizzare il processo di aggiornamento del token:

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `accessTokenRequest.destinationServerType` | Stringa | Seleziona `URL_BASED`. |
| `accessTokenRequest.urlBasedDestination.url.templatingStrategy` | Stringa | <ul><li>Utilizzo `PEBBLE_V1` se utilizzi modelli per il valore in `accessTokenRequest.urlBasedDestination.url.value`.</li><li> Utilizzo `NONE` se il valore nel campo `accessTokenRequest.urlBasedDestination.url.value` è una costante. </li></li> |
| `accessTokenRequest.urlBasedDestination.url.value` | Stringa | URL in cui Experience Platform richiede il token di accesso. |
| `accessTokenRequest.httpTemplate.requestBody.templatingStrategy` | Stringa | <ul><li>Utilizzo `PEBBLE_V1` se utilizzi modelli per i valori in `accessTokenRequest.httpTemplate.requestBody.value`.</li><li> Utilizzo `NONE` se il valore nel campo `accessTokenRequest.httpTemplate.requestBody.value` è una costante. </li></li> |
| `accessTokenRequest.httpTemplate.requestBody.value` | Stringa | Utilizza il linguaggio dei modelli per personalizzare i campi nella richiesta HTTP all’endpoint del token di accesso. Per informazioni su come utilizzare i modelli per personalizzare i campi, consulta [convenzioni di modellazione](#templating-conventions) sezione . |
| `accessTokenRequest.httpTemplate.httpMethod` | Stringa | Specifica il metodo HTTP utilizzato per chiamare l&#39;endpoint del token di accesso. Nella maggior parte dei casi, questo valore è `POST`. |
| `accessTokenRequest.httpTemplate.contentType` | Stringa | Specifica il tipo di contenuto della chiamata HTTP all&#39;endpoint del token di accesso. <br> Ad esempio: `application/x-www-form-urlencoded` o `application/json`. |
| `accessTokenRequest.httpTemplate.headers` | Stringa | Specifica se è necessario aggiungere intestazioni alla chiamata HTTP all&#39;endpoint del token di accesso. |
| `accessTokenRequest.responseFields.templatingStrategy` | Stringa | <ul><li>Utilizzo `PEBBLE_V1` se utilizzi modelli per i valori in `accessTokenRequest.responseFields.value`.</li><li> Utilizzo `NONE` se il valore nel campo `accessTokenRequest.responseFields.value` è una costante. </li></li> |
| `accessTokenRequest.responseFields.value` | Stringa | Utilizza il linguaggio dei modelli per accedere ai campi della risposta HTTP dall’endpoint del token di accesso. Per informazioni su come utilizzare i modelli per personalizzare i campi, consulta [convenzioni di modellazione](#templating-conventions) sezione . |
| `accessTokenRequest.validations.name` | Stringa | Indica il nome fornito per la convalida. |
| `accessTokenRequest.validations.actualValue.templatingStrategy` | Stringa | <ul><li>Utilizzo `PEBBLE_V1` se utilizzi modelli per i valori in `accessTokenRequest.validations.actualValue.value`.</li><li> Utilizzo `NONE` se il valore nel campo `accessTokenRequest.validations.actualValue.value` è una costante. </li></li> |
| `accessTokenRequest.validations.actualValue.value` | Stringa | Utilizza il linguaggio dei modelli per accedere ai campi nella risposta HTTP. Per informazioni su come utilizzare i modelli per personalizzare i campi, consulta [convenzioni di modellazione](#templating-conventions) sezione . |
| `accessTokenRequest.validations.expectedValue.templatingStrategy` | Stringa | <ul><li>Utilizzo `PEBBLE_V1` se utilizzi modelli per i valori in `accessTokenRequest.validations.expectedValue.value`.</li><li> Utilizzo `NONE` se il valore nel campo `accessTokenRequest.validations.expectedValue.value` è una costante. </li></li> |
| `accessTokenRequest.validations.expectedValue.value` | Stringa | Utilizza il linguaggio dei modelli per accedere ai campi nella risposta HTTP. Per informazioni su come utilizzare i modelli per personalizzare i campi, consulta [convenzioni di modellazione](#templating-conventions) sezione . |

{style="table-layout:auto"}

## Convenzioni di modellazione {#templating-conventions}

A seconda della personalizzazione dell’autenticazione, potrebbe essere necessario accedere ai campi di dati nella risposta all’autenticazione, come illustrato nella sezione precedente. Per farlo, ti preghiamo di familiarizzare con il [Linguaggio di template di pallina](https://pebbletemplates.io/) utilizzato dall’Adobe e fai riferimento alle convenzioni di modello riportate di seguito per personalizzare l’implementazione di OAuth 2.


| Prefisso | Descrizione | Esempio |
|---------|----------|---------|
| authData | Accedi al valore di qualsiasi campo dati partner o cliente. | ``{{ authData.accessToken }}`` |
| response.body | corpo di risposta HTTP | ``{{ response.body.access_token }}`` |
| response.status | Stato della risposta HTTP | ``{{ response.status }}`` |
| response.headers | Intestazioni di risposta HTTP | ``{{ response.headers.server[0] }}`` |
| userContext | Accedere alle informazioni sul tentativo di autenticazione corrente | <ul><li>`{{ userContext.sandboxName }} `</li><li>`{{ userContext.sandboxId }} `</li><li>`{{ userContext.imsOrgId }} `</li><li>`{{ userContext.client }} // the client executing the authentication attempt `</li></ul> |

{style="table-layout:auto"}

## Passaggi successivi {#next-steps}

Leggendo questo articolo, ora conosci i pattern di autenticazione OAuth 2 supportati da Adobe Experience Platform e sai come configurare la destinazione con il supporto di autenticazione OAuth 2. Successivamente, puoi impostare la destinazione supportata OAuth 2 utilizzando Destination SDK. Leggi [Utilizza Destination SDK per configurare la destinazione](../../guides/configure-destination-instructions.md) per i passaggi successivi.
