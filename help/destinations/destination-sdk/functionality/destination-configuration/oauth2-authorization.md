---
description: Questa pagina descrive i vari flussi di autorizzazione OAuth 2 supportati da Destination SDK e fornisce istruzioni per impostare l’autorizzazione OAuth 2 per la destinazione.
title: Autorizzazione OAuth 2
exl-id: 280ecb63-5739-491c-b539-3c62bd74e433
source-git-commit: 7ba9971b44410e609c64f4dcf956a1976207353e
workflow-type: tm+mt
source-wordcount: '2181'
ht-degree: 2%

---


# Autorizzazione OAuth 2

Destination SDK supporta diversi metodi di autorizzazione per la destinazione. Tra queste è inclusa l&#39;opzione per l&#39;autenticazione nella destinazione utilizzando il [framework di autorizzazione OAuth 2](https://tools.ietf.org/html/rfc6749).

Questa pagina descrive i vari flussi di autorizzazione OAuth 2 supportati da Destination SDK e fornisce istruzioni per impostare l’autorizzazione OAuth 2 per la destinazione.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **con distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Tipi di integrazione supportati {#supported-integration-types}

Consulta la tabella seguente per informazioni dettagliate sui tipi di integrazioni che supportano le funzionalità descritte in questa pagina.

| Tipo di integrazione | Supporta la funzionalità |
|---|---|
| Integrazioni in tempo reale (streaming) | Sì |
| Integrazioni basate su file (batch) | No |

## Come aggiungere i dettagli di autorizzazione OAuth 2 alla configurazione di destinazione {#how-to-setup}

### Prerequisiti nel sistema {#prerequisites}

Come primo passo, devi creare un’app per Adobe Experience Platform o registrare in altro modo un Experience Platform. L’obiettivo è generare un ID client e un segreto client, necessari per autenticare l’Experience Platform nella destinazione.

Come parte di questa configurazione nel tuo sistema, devi disporre degli URL di reindirizzamento/callback di Adobe Experience Platform OAuth 2, che puoi ottenere dall’elenco seguente.

* `https://platform-va7.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-nld2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-aus5.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-can2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-gbr9.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform.adobe.io/data/core/activation/oauth/api/v1/callback`

>[!IMPORTANT]
>
>Il passaggio per registrare un URL di reindirizzamento/callback per Adobe Experience Platform nel sistema è necessario solo per il tipo di concessione [OAuth 2 con codice di autorizzazione](#authorization-code). Per gli altri due tipi di concessione supportati (password e credenziali client), puoi saltare questo passaggio.

Al termine di questo passaggio, dovresti disporre di:
* Un ID cliente;
* Un segreto cliente;
* URL di callback di Adobe (per la concessione del codice di autorizzazione).

### Cosa devi fare nella Destination SDK {#to-do-in-destination-sdk}

Per impostare l&#39;autorizzazione OAuth 2 per la destinazione in Experience Platform, è necessario aggiungere i dettagli OAuth 2 alla [configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md), con il parametro `customerAuthenticationConfigurations`. Per esempi dettagliati, consulta [autenticazione cliente](../../functionality/destination-configuration/customer-authentication.md). Di seguito sono riportate istruzioni specifiche sui campi da aggiungere al modello di configurazione, a seconda del tipo di concessione di autorizzazione OAuth 2.

## Tipi di concessione OAuth 2 supportati {#oauth2-grant-types}

L’Experience Platform supporta i tre tipi di sovvenzione OAuth 2 riportati nella tabella seguente. Se disponi di una configurazione OAuth 2 personalizzata, Adobe è in grado di supportarla con l’aiuto di campi personalizzati nell’integrazione. Per ulteriori informazioni, consulta le sezioni per ogni tipo di sovvenzione.

>[!IMPORTANT]
>
>* Fornite i parametri di input come indicato nelle sezioni seguenti. I sistemi interni Adobe si connettono al sistema di autorizzazione della piattaforma e acquisiscono i parametri di output, utilizzati per autenticare l’utente e mantenere l’autorizzazione alla destinazione.
>* I parametri di input evidenziati in grassetto nella tabella sono parametri richiesti nel flusso di autorizzazione OAuth 2. Gli altri parametri sono facoltativi. Altri parametri di input personalizzati non sono visualizzati qui, ma sono descritti dettagliatamente nelle sezioni [Personalizzare la configurazione OAuth 2](#customize-configuration) e [Aggiornare il token di accesso](#access-token-refresh).

| Concessione OAuth 2 | Input | Uscite |
|---------|----------|---------|
| Codice di autorizzazione | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>ambito</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Password | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>ambito</li><li><b>accessTokenUrl</b></li><li><b>nomeutente</b></li><li><b>password</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Credenziali client | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>ambito</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

La tabella precedente elenca i campi utilizzati nei flussi standard OAuth 2. Oltre a questi campi standard, varie integrazioni di partner possono richiedere input e output aggiuntivi. Adobe ha progettato un framework di autorizzazione OAuth 2 flessibile per Destination SDK che può gestire le varianti al modello di campi standard di cui sopra, supportando al contempo un meccanismo per rigenerare automaticamente gli output non validi, come i token di accesso scaduti.

L’output include sempre un token di accesso, utilizzato da Experience Platform per autenticare e mantenere l’autorizzazione per la destinazione.

Il sistema che Adobe ha progettato per l’autorizzazione OAuth 2:
* Supporta tutte e tre le sovvenzioni OAuth 2 tenendo conto di eventuali varianti di esse, come campi di dati aggiuntivi, chiamate API non standard e altro ancora.
* Supporta i token di accesso con valori di durata variabili, che si tratti di 90 giorni, 30 minuti o qualsiasi altro valore di durata specificato.
* Supporta i flussi di autorizzazione OAuth 2 con o senza token di aggiornamento.

## OAuth 2 con codice di autorizzazione {#authorization-code}

Se la destinazione supporta un flusso standard del codice di autorizzazione OAuth 2.0 (leggi le [specifiche degli standard RFC](https://tools.ietf.org/html/rfc6749#section-4.1)) o una relativa variante, consulta i campi obbligatori e facoltativi riportati di seguito:

| Concessione OAuth 2 | Input | Uscite |
|---------|----------|---------|
| Codice di autorizzazione | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>ambito</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

Per impostare questo metodo di autorizzazione per la destinazione, aggiungi le seguenti righe alla configurazione quando [crei una configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md):

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
| `authType` | Stringa | Usare &quot;OAUTH2&quot;. |
| `grant` | Stringa | Utilizzare &quot;OAUTH2_AUTHORIZATION_CODE&quot;. |
| `accessTokenUrl` | Stringa | L’URL sul lato dell’utente che rilascia i token di accesso e, facoltativamente, i token di aggiornamento. |
| `authorizationUrl` | Stringa | L’URL del server di autorizzazione, in cui reindirizzare l’utente per accedere all’applicazione. |
| `refreshTokenUrl` | Stringa | *Facoltativo.* L&#39;URL sul tuo lato, che rilascia i token di aggiornamento. Spesso `refreshTokenUrl` è uguale a `accessTokenUrl`. |
| `clientId` | Stringa | ID client assegnato dal sistema a Adobe Experience Platform. |
| `clientSecret` | Stringa | Il segreto client assegnato dal sistema a Adobe Experience Platform. |
| `scope` | Elenco di stringhe | *Facoltativo*. Imposta l’ambito di ciò che il token di accesso consente a Experience Platform di eseguire sulle risorse. Esempio: &quot;read, write&quot; (lettura, scrittura). |

{style="table-layout:auto"}

## OAuth 2 con concessione password

Per la concessione della password OAuth 2 (leggi le [specifiche degli standard RFC](https://tools.ietf.org/html/rfc6749#section-4.3)), l&#39;Experience Platform richiede il nome utente e la password dell&#39;utente. Nel flusso di autorizzazione, Experience Platform scambia queste credenziali per un token di accesso e, facoltativamente, per un token di aggiornamento.
Adobe utilizza gli input standard riportati di seguito per semplificare la configurazione di destinazione, con la possibilità di ignorare i valori:

| Concessione OAuth 2 | Input | Uscite |
|---------|----------|---------|
| Password | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>ambito</li><li><b>accessTokenUrl</b></li><li><b>nomeutente</b></li><li><b>password</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

>[!NOTE]
>
> Non è necessario aggiungere parametri per `username` e `password` nella configurazione seguente. Quando aggiungi `"grant": "OAUTH2_PASSWORD"` nella configurazione di destinazione, il sistema richiederà all&#39;utente di fornire un nome utente e una password nell&#39;interfaccia utente di Experience Platform, al momento dell&#39;autenticazione nella destinazione.

Per impostare questo metodo di autorizzazione per la destinazione, aggiungi le seguenti righe alla configurazione quando [crei una configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md):

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
| `authType` | Stringa | Usare &quot;OAUTH2&quot;. |
| `grant` | Stringa | Utilizzare &quot;OAUTH2_PASSWORD&quot;. |
| `accessTokenUrl` | Stringa | L’URL sul lato dell’utente che rilascia i token di accesso e, facoltativamente, i token di aggiornamento. |
| `clientId` | Stringa | ID client assegnato dal sistema a Adobe Experience Platform. |
| `clientSecret` | Stringa | Il segreto client assegnato dal sistema a Adobe Experience Platform. |
| `scope` | Elenco di stringhe | *Facoltativo*. Imposta l’ambito di ciò che il token di accesso consente a Experience Platform di eseguire sulle risorse. Esempio: &quot;read, write&quot; (lettura, scrittura). |

{style="table-layout:auto"}

## Concessione OAuth 2 con credenziali client

È possibile configurare una destinazione client OAuth 2 (leggere le [specifiche degli standard RFC](https://tools.ietf.org/html/rfc6749#section-4.4)) che supporta gli input e gli output standard elencati di seguito. Puoi personalizzare i valori. Per informazioni dettagliate, consulta [Personalizzare la configurazione OAuth 2](#customize-configuration).

| Concessione OAuth 2 | Input | Uscite |
|---------|----------|---------|
| Credenziali client | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>ambito</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

Per impostare questo metodo di autorizzazione per la destinazione, aggiungi le seguenti righe alla configurazione quando [crei una configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md):

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
| `authType` | Stringa | Usare &quot;OAUTH2&quot;. |
| `grant` | Stringa | Utilizzare &quot;OAUTH2_CLIENT_CREDENTIALS&quot;. |
| `accessTokenUrl` | Stringa | L’URL del server di autorizzazione, che emette un token di accesso e un token di aggiornamento facoltativo. |
| `refreshTokenUrl` | Stringa | *Facoltativo.* L&#39;URL sul tuo lato, che rilascia i token di aggiornamento. Spesso `refreshTokenUrl` è uguale a `accessTokenUrl`. |
| `clientId` | Stringa | ID client assegnato dal sistema a Adobe Experience Platform. |
| `clientSecret` | Stringa | Il segreto client assegnato dal sistema a Adobe Experience Platform. |
| `scope` | Elenco di stringhe | *Facoltativo*. Imposta l’ambito di ciò che il token di accesso consente a Experience Platform di eseguire sulle risorse. Esempio: &quot;read, write&quot; (lettura, scrittura). |

{style="table-layout:auto"}

## Personalizzare la configurazione di OAuth 2 {#customize-configuration}

Le configurazioni descritte nelle sezioni precedenti descrivono le sovvenzioni standard OAuth 2. Tuttavia, il sistema progettato da Adobe offre flessibilità che consente di utilizzare parametri personalizzati per qualsiasi variante nella sovvenzione OAuth 2. Per personalizzare le impostazioni standard di OAuth 2, utilizzare i parametri `authenticationDataFields`, come illustrato negli esempi seguenti.

### Esempio 1: utilizzo di `authenticationDataFields` per acquisire informazioni provenienti dalla risposta di autorizzazione {#example-1}

In questo esempio, una piattaforma di destinazione dispone di token di aggiornamento che scadono dopo un certo periodo di tempo. In questo caso, il partner configura il campo personalizzato `refreshTokenExpiration` per ottenere la scadenza del token di aggiornamento dal campo `refresh_token_expires_in` nella risposta API.

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

### Esempio 2: utilizzo di `authenticationDataFields` per fornire un token di aggiornamento speciale {#example-2}

In questo esempio, un partner imposta la propria destinazione in modo da fornire un token di aggiornamento speciale. Inoltre, la data di scadenza per i token di accesso non viene restituita nella risposta API, in modo che possano codificare un valore predefinito, in questo caso 3600 secondi.

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

### Esempio 3: l’utente immette l’ID client e il segreto client quando configura la destinazione {#example-3}

In questo esempio, invece di creare un ID client globale e un segreto client come mostrato nella sezione [Prerequisiti nel sistema](#prerequisites), il cliente deve immettere l&#39;ID client, il segreto client e l&#39;ID account (l&#39;ID utilizzato dal cliente per accedere alla destinazione)

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
| `authenticationDataFields.title` | Stringa | Titolo che puoi fornire per il campo personalizzato. |
| `authenticationDataFields.description` | Stringa | Descrizione del campo dati personalizzato configurato. |
| `authenticationDataFields.type` | Stringa | Definisce il tipo di campo dati personalizzato. <br> Valori accettati: `string`, `boolean`, `integer` |
| `authenticationDataFields.isRequired` | Booleano | Specifica se il campo dati personalizzato è obbligatorio nel flusso di autorizzazione. |
| `authenticationDataFields.format` | Stringa | Quando si seleziona `"format":"password"`, Adobe crittografa il valore del campo dei dati di autorizzazione. Se utilizzato con `"fieldType": "CUSTOMER"`, nasconde anche l&#39;input nell&#39;interfaccia utente quando l&#39;utente digita nel campo. |
| `authenticationDataFields.fieldType` | Stringa | Indica se l’input proviene dal partner (te) o dall’utente, quando ha impostato la destinazione in Experience Platform. |
| `authenticationDataFields.value` | Stringa. Booleano. Intero | Il valore del campo dati personalizzato. Il valore corrisponde al tipo scelto da `authenticationDataFields.type`. |
| `authenticationDataFields.authenticationResponsePath` | Stringa | Indica a quale campo del percorso di risposta API stai facendo riferimento. |

{style="table-layout:auto"}

## Aggiornamento del token di accesso {#access-token-refresh}

Adobe ha progettato un sistema che aggiorna i token di accesso scaduti senza richiedere all’utente di accedere nuovamente alla piattaforma. Il sistema è in grado di generare un nuovo token in modo che l’attivazione nella destinazione continui senza problemi per il cliente.

Per impostare l’aggiornamento del token di accesso, potrebbe essere necessario configurare una richiesta HTTP con modello che consenta ad Adobe di ottenere un nuovo token di accesso, utilizzando un token di aggiornamento. Se il token di accesso è scaduto, Adobe accetta la richiesta basata su modelli fornita dall’utente, aggiungendo i parametri forniti. Utilizzare il parametro `accessTokenRequest` per configurare un meccanismo di aggiornamento dei token di accesso.


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

È possibile utilizzare i seguenti parametri in `accessTokenRequest` per personalizzare il processo di aggiornamento del token:

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `accessTokenRequest.destinationServerType` | Stringa | Usa `URL_BASED`. |
| `accessTokenRequest.urlBasedDestination.url.templatingStrategy` | Stringa | <ul><li>Utilizzare `PEBBLE_V1` se si utilizzano i modelli per il valore in `accessTokenRequest.urlBasedDestination.url.value`.</li><li> Utilizzare `NONE` se il valore nel campo `accessTokenRequest.urlBasedDestination.url.value` è una costante. </li></li> |
| `accessTokenRequest.urlBasedDestination.url.value` | Stringa | L’URL in cui Experience Platform richiede il token di accesso. |
| `accessTokenRequest.httpTemplate.requestBody.templatingStrategy` | Stringa | <ul><li>Utilizzare `PEBBLE_V1` se si utilizzano modelli per i valori in `accessTokenRequest.httpTemplate.requestBody.value`.</li><li> Utilizzare `NONE` se il valore nel campo `accessTokenRequest.httpTemplate.requestBody.value` è una costante. </li></li> |
| `accessTokenRequest.httpTemplate.requestBody.value` | Stringa | Utilizza il linguaggio dei modelli per personalizzare i campi nella richiesta HTTP per l’endpoint del token di accesso. Per informazioni su come utilizzare la creazione di modelli per personalizzare i campi, consulta la sezione [convenzioni di creazione di modelli](#templating-conventions). |
| `accessTokenRequest.httpTemplate.httpMethod` | Stringa | Specifica il metodo HTTP utilizzato per chiamare l&#39;endpoint del token di accesso. Nella maggior parte dei casi, questo valore è `POST`. |
| `accessTokenRequest.httpTemplate.contentType` | Stringa | Specifica il tipo di contenuto della chiamata HTTP all’endpoint del token di accesso. <br> Ad esempio: `application/x-www-form-urlencoded` o `application/json`. |
| `accessTokenRequest.httpTemplate.headers` | Stringa | Specifica se è necessario aggiungere intestazioni alla chiamata HTTP all’endpoint del token di accesso. |
| `accessTokenRequest.responseFields.templatingStrategy` | Stringa | <ul><li>Utilizzare `PEBBLE_V1` se si utilizzano modelli per i valori in `accessTokenRequest.responseFields.value`.</li><li> Utilizzare `NONE` se il valore nel campo `accessTokenRequest.responseFields.value` è una costante. </li></li> |
| `accessTokenRequest.responseFields.value` | Stringa | Utilizza il linguaggio dei modelli per accedere ai campi nella risposta HTTP dall’endpoint del token di accesso. Per informazioni su come utilizzare la creazione di modelli per personalizzare i campi, consulta la sezione [convenzioni di creazione di modelli](#templating-conventions). |
| `accessTokenRequest.validations.name` | Stringa | Indica il nome fornito per la convalida. |
| `accessTokenRequest.validations.actualValue.templatingStrategy` | Stringa | <ul><li>Utilizzare `PEBBLE_V1` se si utilizzano modelli per i valori in `accessTokenRequest.validations.actualValue.value`.</li><li> Utilizzare `NONE` se il valore nel campo `accessTokenRequest.validations.actualValue.value` è una costante. </li></li> |
| `accessTokenRequest.validations.actualValue.value` | Stringa | Utilizza il linguaggio dei modelli per accedere ai campi nella risposta HTTP. Per informazioni su come utilizzare la creazione di modelli per personalizzare i campi, consulta la sezione [convenzioni di creazione di modelli](#templating-conventions). |
| `accessTokenRequest.validations.expectedValue.templatingStrategy` | Stringa | <ul><li>Utilizzare `PEBBLE_V1` se si utilizzano modelli per i valori in `accessTokenRequest.validations.expectedValue.value`.</li><li> Utilizzare `NONE` se il valore nel campo `accessTokenRequest.validations.expectedValue.value` è una costante. </li></li> |
| `accessTokenRequest.validations.expectedValue.value` | Stringa | Utilizza il linguaggio dei modelli per accedere ai campi nella risposta HTTP. Per informazioni su come utilizzare la creazione di modelli per personalizzare i campi, consulta la sezione [convenzioni di creazione di modelli](#templating-conventions). |

{style="table-layout:auto"}

## Convenzioni di modelli {#templating-conventions}

A seconda della personalizzazione dell’autorizzazione, potrebbe essere necessario accedere ai campi dati nella risposta di autorizzazione, come illustrato nella sezione precedente. Per farlo, acquisisci familiarità con il [linguaggio di modelli Pebble](https://pebbletemplates.io/) utilizzato da Adobe e fai riferimento alle convenzioni di modelli riportate di seguito per personalizzare l&#39;implementazione di OAuth 2.


| Prefisso | Descrizione | Esempio |
|---------|----------|---------|
| authData | Accedi al valore di qualsiasi campo dati partner o cliente. | ``{{ authData.accessToken }}`` |
| response.body | Corpo della risposta HTTP | ``{{ response.body.access_token }}`` |
| response.status | Stato della risposta HTTP | ``{{ response.status }}`` |
| response.headers | Intestazioni di risposta HTTP | ``{{ response.headers.server[0] }}`` |
| userContext | Accedi alle informazioni sul tentativo di autorizzazione corrente | <ul><li>`{{ userContext.sandboxName }} `</li><li>`{{ userContext.sandboxId }} `</li><li>`{{ userContext.imsOrgId }} `</li><li>`{{ userContext.client }} // the client executing the authorization attempt `</li></ul> |

{style="table-layout:auto"}

## Passaggi successivi {#next-steps}

Leggendo questo articolo, conosci i modelli di autorizzazione OAuth 2 supportati da Adobe Experience Platform e sai come configurare la tua destinazione con il supporto per l’autorizzazione OAuth 2. Successivamente, puoi impostare la destinazione supportata da OAuth 2 tramite Destination SDK. Leggi [Utilizza Destination SDK per configurare la tua destinazione](../../guides/configure-destination-instructions.md) per i passaggi successivi.
