---
title: Segreti nell’API di Reactor
description: Scopri le nozioni di base su come configurare i segreti nell’API di Reactor per l’inoltro degli eventi.
exl-id: 0298c0cd-9fba-4b54-86db-5d2d8f9ade54
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1232'
ht-degree: 2%

---

# Segreti nell’API di Reactor

Nell’API di Reactor, un segreto è una risorsa che rappresenta una credenziale di autenticazione. I segreti vengono utilizzati nell’inoltro degli eventi per l’autenticazione in un altro sistema per lo scambio sicuro dei dati. Pertanto, i segreti possono essere creati solo all’interno delle proprietà di inoltro degli eventi (proprietà la cui `platform` attributo impostato su `edge`).

Al momento sono tre i tipi di segreto supportati indicati nella `type_of` attributo:

| Tipo di segreto | Descrizione |
| --- | --- |
| `token` | Una singola stringa di caratteri che rappresenta un valore del token di autenticazione noto e compreso da entrambi i sistemi. |
| `simple-http` | Contiene due attributi di stringa rispettivamente per nome utente e password. |
| `oauth2-client_credentials` | Contiene diversi attributi per supportare [OAuth](https://datatracker.ietf.org/doc/html/rfc6749) specifica di autenticazione. L’inoltro degli eventi richiede le informazioni richieste, quindi gestisce il rinnovo di questi token per te in un intervallo specificato. |

{style="table-layout:auto"}

Questa guida fornisce una panoramica di alto livello sulla configurazione dei segreti da utilizzare nell’inoltro degli eventi. Per istruzioni dettagliate su come gestire i segreti nell’API di Reactor, incluso un esempio di JSON della struttura di un segreto, consulta [guida dell’endpoint &quot;secrets&quot;](../endpoints/secrets.md).

## Credenziali 

Ogni segreto contiene un `credentials` che contiene i rispettivi valori delle credenziali. Quando [creazione di un segreto nell’API](../endpoints/secrets.md#create), ogni tipo di segreto ha diversi attributi richiesti, come illustrato nelle sezioni seguenti:

* [`token`](#token)
* [&#39;simple-http&#39;](#simple-http)
* [&quot;oauth2-client_credentials&quot;](#oauth2-client_credentials)
* [&quot;oauth2-google&quot;](#oauth2-google)

### `token` {#token}

Segreti con un `type_of` valore di `token` richiede un solo attributo in `credentials`:

| Attributo credenziali | Tipo di dati | Descrizione |
| --- | --- | --- |
| `token` | Stringa | Un token segreto riconosciuto dal sistema di destinazione. |

{style="table-layout:auto"}

Il token viene memorizzato come valore statico, e quindi il segreto `expires_at` e `refresh_at` proprietà impostate su `null` quando viene creato il segreto.

### `simple-http` {#simple-http}

Segreti con un `type_of` valore di `simple-http` richiedi i seguenti attributi in `credentials`:

| Attributo credenziali | Tipo di dati | Descrizione |
| --- | --- | --- |
| `username` | Stringa | Un nome utente. |
| `password` | Stringa | Una password. Questo valore non è incluso nella risposta API. |

{style="table-layout:auto"}

Quando viene creato il segreto, i due attributi vengono scambiati con una codifica BASE64 di `username:password`. Dopo lo scambio, il segreto è `expires_at` e `refresh_at` proprietà impostate su `null`.

### `oauth2-client_credentials` {#oauth2-client_credentials}

Segreti con un `type_of` valore di `oauth2-client_credentials` richiedi i seguenti attributi in `credentials`:

| Attributo credenziali | Tipo di dati | Descrizione |
| --- | --- | --- |
| `client_id` | Stringa | ID client per l’integrazione OAuth. |
| `client_secret` | Stringa | Il segreto client per l’integrazione OAuth. Questo valore non è incluso nella risposta API. |
| `token_url` | Stringa | URL di autorizzazione per l’integrazione OAuth. |
| `refresh_offset` | Intero | *(Facoltativo)* Il valore, in secondi, di cui eseguire l&#39;offset dell&#39;operazione di aggiornamento. Se questo attributo viene omesso durante la creazione del segreto, il valore viene impostato su `14400` (quattro ore) per impostazione predefinita. |
| `options` | Oggetto | *(Facoltativo)* Specifica le opzioni aggiuntive per l&#39;integrazione OAuth:<ul><li>`scope`: stringa che rappresenta [Ambito OAuth 2.0](https://oauth.net/2/scope/) per le credenziali.</li><li>`audience`: stringa che rappresenta un elemento [Token di accesso Auth0](https://auth0.com/docs/protocols/protocol-oauth2).</li></ul> |

Quando un `oauth2-client_credentials` il segreto viene creato o aggiornato, il `client_id` e `client_secret` (ed eventualmente `options`) vengono scambiati in una richiesta POST al `token_url`, in base al flusso delle credenziali client del protocollo OAuth.

>[!NOTE]
>
>Il corpo della risposta del servizio di autorizzazione deve essere compatibile con il protocollo OAuth.

Se il servizio di autorizzazione risponde con `200 OK` e un corpo di risposta JSON, il corpo viene analizzato e il `access_token` viene inviato all’ambiente edge e `expires_in` viene utilizzato per calcolare `expires_at` e `refresh_at` attributi del segreto. Se sul segreto non è presente alcuna associazione di ambiente, `access_token` viene scartato.

Uno scambio di credenziali viene considerato riuscito nelle seguenti condizioni:

* `expires_in` è maggiore di `28800` (otto ore).
* `refresh_offset` è minore del valore di `expires_in` meno `14400` (quattro ore). Ad esempio, se `expires_in` è `36000` (dieci ore) e `refresh_offset` è `28800` (otto ore), lo scambio è considerato non riuscito perché `28800` è maggiore di `36000` - `14400` (`21600`).

Se lo scambio ha esito positivo, l’attributo di stato del segreto viene impostato su `succeeded` e valori per `expires_at` e `refresh_at` sono impostati:

* `expires_at` è l’ora UTC corrente più il valore di `expires_in`.
* `refresh_at` è l’ora UTC corrente più il valore di `expires_in`, meno il valore di `refresh_offset`. Ad esempio, se `expires_in` è `43200` (dodici ore) e `refresh_offset` è `14400` (quattro ore), il `refresh_at` proprietà impostata su `28800` (otto ore) dopo l’ora UTC corrente.

Se lo scambio non riesce per qualsiasi motivo, il `status_details` attributo in `meta` l&#39;oggetto viene aggiornato con le relative informazioni.

#### Aggiornamento di un `oauth2-client_credentials` segreto

Se un `oauth2-client_credentials` il segreto è stato assegnato a un ambiente e il suo stato è `succeeded` (le credenziali sono state scambiate correttamente), viene eseguito automaticamente un nuovo scambio il `refresh_at`.

Se lo scambio ha esito positivo, il `refresh_status` attributo in `meta` l&#39;oggetto è impostato su `succeeded` durante `expires_at`, `refresh_at`, e `activated_at` vengono aggiornati di conseguenza.

Se lo scambio non riesce, l’operazione viene tentata altre tre volte, con l’ultimo tentativo non più di due ore prima della scadenza del token di accesso. Se tutti i tentativi falliscono, il `refresh_status_details` attributo da `meta` l&#39;oggetto viene aggiornato con i relativi dettagli.

### `oauth2-google` {#oauth2-google}

Segreti con un `type_of` valore di `oauth2-google` richiede il seguente attributo in `credentials`:

| Attributo credenziali | Tipo di dati | Descrizione |
| --- | --- | --- |
| `scopes` | Array | Elenca gli ambiti di prodotto di Google per l’autenticazione. Sono supportati i seguenti ambiti:<ul><li>[Google Ads](https://developers.google.com/google-ads/api/docs/oauth/overview): `https://www.googleapis.com/auth/adwords`</li><li>[Google Pub/Sub](https://cloud.google.com/pubsub/docs/reference/service_apis_overview): `https://www.googleapis.com/auth/pubsub`</li></ul> |

Dopo aver creato `oauth2-google` segreto, la risposta include un `meta.authorization_url` proprietà. È necessario copiare e incollare questo URL in un browser per completare il flusso di autenticazione di Google.

#### Autorizza nuovamente un `oauth2-google` segreto

L’URL di autorizzazione per un `oauth2-google` il segreto scade un&#39;ora dopo la creazione del segreto (come indicato da `meta.authorization_url_expires_at`). Trascorso questo periodo, il segreto deve essere nuovamente autorizzato per rinnovare il processo di autenticazione.

Consulta la sezione [guida dell’endpoint &quot;secrets&quot;](../endpoints/secrets.md#reauthorize) per informazioni dettagliate su come autorizzare nuovamente un `oauth2-google` segreta, effettuando una richiesta PATCH all’API di Reactor.

## Relazione ambiente

Quando crei un segreto, devi specificare [ambiente](../endpoints/environments.md) in cui esisterà. I segreti vengono distribuiti immediatamente nell’ambiente in cui vengono creati.

Un segreto può essere associato a un solo ambiente. Una volta stabilita la relazione tra un segreto e un ambiente, il segreto non può essere cancellato dall’ambiente e non può essere associato a un ambiente diverso.

>[!NOTE]
>
>L’unica eccezione a questa regola è se l’ambiente in questione viene eliminato. In questo caso, la relazione viene cancellata e il segreto può essere assegnato a un ambiente diverso.

Dopo aver scambiato le credenziali di un segreto con successo, affinché un segreto venga associato a un ambiente, l’artefatto di scambio (la stringa del token per `token`, la stringa con codifica Base64 per `simple-http`o il token di accesso per `oauth2-client_credentials`) viene salvato in modo sicuro nell&#39;ambiente.

Una volta salvato correttamente l’artefatto di scambio nell’ambiente, il segreto `activated_at` L&#39;attributo è impostato sull&#39;ora UTC corrente e ora è possibile farvi riferimento utilizzando un elemento dati. Consulta la [sezione successiva](#referencing-secrets) per ulteriori informazioni sui riferimenti ai segreti.

## Segreti di riferimento {#referencing-secrets}

Per fare riferimento a un segreto, devi creare un elemento dati di tipo &quot;[!UICONTROL Segreto]&quot; (fornito da [[!UICONTROL Core] estensione](../../extensions/client/core/overview.md)) su una proprietà di inoltro degli eventi. Durante la configurazione di questo elemento dati, viene richiesto di indicare il segreto da utilizzare per ogni ambiente. Puoi quindi creare regole che fanno riferimento a un elemento dati segreto, ad esempio all’interno dell’intestazione di una chiamata HTTP.

![Elemento dati segreto](../../images/api/guides/secrets/data-element.png)

>[!NOTE]
>
>Per aggiungere un elemento dati segreto a una libreria, è necessario averne almeno uno `succeeded` segreto associato all’ambiente in cui viene generata la libreria. Ad esempio, se una libreria ha un elemento dati segreto che non ha un `succeeded` segreto configurato per [!UICONTROL Segreto gestione temporanea] , il tentativo di generare tale libreria nell&#39;ambiente di staging genererà un errore.

In fase di esecuzione, l’elemento dati segreto viene sostituito con il corrispondente artefatto di scambio segreto salvato nell’ambiente.

## Passaggi successivi

Questa guida descrive le nozioni di base sull’utilizzo dei segreti nell’API di Reactor. Per informazioni dettagliate su come gestire i segreti utilizzando le chiamate API, consulta [guida dell’endpoint &quot;secrets&quot;](../endpoints/secrets.md).
