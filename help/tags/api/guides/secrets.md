---
title: Segreti nell'API del reattore
description: Scopri le basi di come configurare i segreti nell’API di Reactor da utilizzare nell’inoltro degli eventi.
exl-id: 0298c0cd-9fba-4b54-86db-5d2d8f9ade54
source-git-commit: 24e79c14268b9eab0e8286eb8cd1352c1dfcd1b6
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 2%

---

# Segreti nell&#39;API del reattore

Nell’API di Reactor, un segreto è una risorsa che rappresenta una credenziale di autenticazione. I segreti vengono utilizzati nell&#39;inoltro degli eventi per autenticarsi in un altro sistema per lo scambio sicuro dei dati. Pertanto, i segreti possono essere creati solo all&#39;interno delle proprietà di inoltro degli eventi (proprietà di cui `platform` attributo impostato su `edge`).

Al momento esistono tre tipi di segreti supportati indicati nella variabile `type_of` attributo:

| Tipo di segreto | Descrizione |
| --- | --- |
| `token` | Una singola stringa di caratteri che rappresenta un valore del token di autenticazione noto e compreso da entrambi i sistemi. |
| `simple-http` | Contiene rispettivamente due attributi di stringa per un nome utente e una password. |
| `oauth2-client_credentials` | Contiene diversi attributi per supportare il [OAuth](https://datatracker.ietf.org/doc/html/rfc6749) specifiche di autenticazione. L’inoltro eventi richiede le informazioni richieste, quindi gestisce il rinnovo di questi token per te in un intervallo specificato. |

{style=&quot;table-layout:auto&quot;}

Questa guida fornisce una panoramica di alto livello sulle modalità di configurazione dei segreti da utilizzare nell’inoltro degli eventi. Per informazioni dettagliate su come gestire i segreti nell’API del reattore, incluso l’esempio JSON della struttura di un segreto, consulta la sezione [guida all’endpoint segreti](../endpoints/secrets.md).

## Credenziali 

Ogni segreto contiene un `credentials` attributo che detiene i rispettivi valori delle credenziali. Quando [creazione di un segreto nell’API](../endpoints/secrets.md#create), ogni tipo di segreto ha attributi richiesti diversi come mostrato nelle sezioni seguenti:

* [`token`](#token)
* [`simple-http`](#simple-http)
* [`oauth2-client_credentials`](#oauth2-client_credentials)
* [`oauth2-google`](#oauth2-google)

### `token` {#token}

Segreti con un `type_of` valore `token` richiede solo un singolo attributo in `credentials`:

| Attributo di credito | Tipo di dati | Descrizione |
| --- | --- | --- |
| `token` | Stringa | Un token segreto compreso dal sistema di destinazione. |

{style=&quot;table-layout:auto&quot;}

Il token viene memorizzato come valore statico e quindi il `expires_at` e `refresh_at` le proprietà sono impostate su `null` quando viene creato il segreto.

### `simple-http` {#simple-http}

Segreti con un `type_of` valore `simple-http` richiedere i seguenti attributi in `credentials`:

| Attributo di credito | Tipo di dati | Descrizione |
| --- | --- | --- |
| `username` | Stringa | Nome utente. |
| `password` | Stringa | Una password. Questo valore non è incluso nella risposta API. |

{style=&quot;table-layout:auto&quot;}

Quando viene creato il segreto, i due attributi vengono scambiati con una codifica BASE64 di `username:password`. Dopo lo scambio, il segreto e&#39; `expires_at` e `refresh_at` le proprietà sono impostate su `null`.

### `oauth2-client_credentials` {#oauth2-client_credentials}

Segreti con un `type_of` valore `oauth2-client_credentials` richiedere i seguenti attributi in `credentials`:

| Attributo di credito | Tipo di dati | Descrizione |
| --- | --- | --- |
| `client_id` | Stringa | ID client per l’integrazione OAuth. |
| `client_secret` | Stringa | Il segreto client per l’integrazione di OAuth. Questo valore non è incluso nella risposta API. |
| `token_url` | Stringa | URL di autorizzazione per l’integrazione OAuth. |
| `refresh_offset` | Intero | *(Facoltativo)* Il valore, in secondi, per l&#39;offset dell&#39;operazione di aggiornamento. Se questo attributo viene omesso durante la creazione del segreto, il valore viene impostato su `14400` (quattro ore) per impostazione predefinita. |
| `options` | Oggetto | *(Facoltativo)* Specifica opzioni aggiuntive per l’integrazione OAuth:<ul><li>`scope`: Una stringa che rappresenta il [Ambito OAuth 2.0](https://oauth.net/2/scope/) per le credenziali.</li><li>`audience`: Una stringa che rappresenta un [Token di accesso Auth0](https://auth0.com/docs/protocols/protocol-oauth2).</li></ul> |

Quando un `oauth2-client_credentials` il segreto viene creato o aggiornato, il `client_id` e `client_secret` (e possibilmente `options`) sono scambiate con richiesta POST al `token_url`, in base al flusso delle credenziali client del protocollo OAuth.

>[!NOTE]
>
>Si prevede che il corpo di risposta del servizio di autorizzazione sia compatibile con il protocollo OAuth.

Se il servizio di autorizzazione risponde con `200 OK` e un corpo di risposta JSON, il corpo viene analizzato e il `access_token` viene inviato all’ambiente Edge e `expires_in` viene utilizzato per calcolare il `expires_at` e `refresh_at` attributi del segreto. Se non c&#39;è un&#39;associazione ambientale sul segreto, `access_token` viene scartato.

Uno scambio di credenziali è considerato un successo nelle seguenti condizioni:

* `expires_in` è maggiore di `28800` (otto ore).
* `refresh_offset` è minore del valore di `expires_in` meno `14400` (quattro ore). Ad esempio, se `expires_in` è `36000` (10 ore) e `refresh_offset` è `28800` (otto ore), lo scambio è considerato non riuscito perché `28800` è maggiore di `36000` - `14400` (`21600`).

Se lo scambio ha esito positivo, l&#39;attributo di stato del segreto è impostato su `succeeded` e valori per `expires_at` e `refresh_at` sono impostati:

* `expires_at` è l’ora UTC corrente più il valore di `expires_in`.
* `refresh_at` è l’ora UTC corrente più il valore di `expires_in`, meno il valore di `refresh_offset`. Ad esempio, se `expires_in` è `43200` (dodici ore) e `refresh_offset` è `14400` (quattro ore), `refresh_at` è impostata su `28800` (otto ore) dopo l’ora UTC corrente.

Se lo scambio non riesce per qualsiasi motivo, il `status_details` nella `meta` aggiornamenti degli oggetti con informazioni rilevanti.

#### Aggiornamento di un `oauth2-client_credentials` segreto

Se `oauth2-client_credentials` è stato assegnato un segreto a un ambiente e il suo stato è `succeeded` (le credenziali sono state scambiate con successo), viene eseguito automaticamente un nuovo scambio `refresh_at`.

Se lo scambio ha esito positivo, la `refresh_status` nella `meta` è impostato su `succeeded` while `expires_at`, `refresh_at`e `activated_at` sono aggiornati di conseguenza.

Se lo scambio non riesce, l’operazione viene tentata tre volte di più con l’ultimo tentativo non più di due ore prima della scadenza del token di accesso. Se tutti i tentativi falliscono, il `refresh_status_details` attributo dal `meta` aggiornamenti degli oggetti con i relativi dettagli.

### `oauth2-google` {#oauth2-google}

Segreti con un `type_of` valore `oauth2-google` richiede il seguente attributo in `credentials`:

| Attributo di credito | Tipo di dati | Descrizione |
| --- | --- | --- |
| `scopes` | Array | Elenca gli ambiti dei prodotti Google per l’autenticazione. Sono supportati i seguenti ambiti:<ul><li>[Google Ads](https://developers.google.com/google-ads/api/docs/oauth/overview): `https://www.googleapis.com/auth/adwords`</li><li>[Google Pub/Sub](https://cloud.google.com/pubsub/docs/reference/service_apis_overview): `https://www.googleapis.com/auth/pubsub`</li></ul> |

Dopo aver creato il `oauth2-google` segreto, la risposta include un `meta.authorization_url` proprietà. Devi copiare e incollare questo URL in un browser per completare il flusso di autenticazione di Google.

#### Riautorizzare un `oauth2-google` segreto

L’URL di autorizzazione per un `oauth2-google` Il segreto scade un’ora dopo la creazione del segreto (come indicato da `meta.authorization_url_expires_at`). Dopo questo periodo, il segreto deve essere nuovamente autorizzato per rinnovare il processo di autenticazione.

Fai riferimento a [guida all’endpoint segreti](../endpoints/secrets.md#reauthorize) per informazioni dettagliate su come autorizzare nuovamente un `oauth2-google` segreto effettuando una richiesta PATCH all’API Reactor.

## Relazione ambientale

Quando crei un segreto, devi specificare la variabile [ambiente](../endpoints/environments.md) in cui esisterà. I segreti vengono immediatamente distribuiti nell’ambiente in cui vengono creati.

Un segreto può essere associato a un solo ambiente. Una volta stabilita la relazione tra un segreto e un ambiente, il segreto non può essere cancellato dall&#39;ambiente e il segreto non può essere associato a un ambiente diverso.

>[!NOTE]
>
>L&#39;unica eccezione a questa regola è se l&#39;ambiente in questione viene eliminato. In questo caso, la relazione viene cancellata e il segreto può essere assegnato a un ambiente diverso.

Dopo che le credenziali di un segreto sono state scambiate con successo, affinché un segreto sia associato a un ambiente, l&#39;artifact di scambio (la stringa token per `token`, la stringa codificata Base64 per `simple-http`o il token di accesso per `oauth2-client_credentials`) viene salvato in modo sicuro nell’ambiente.

Dopo che l&#39;artefatto di scambio è stato salvato con successo nell&#39;ambiente, il segreto `activated_at` è impostato sull&#39;ora UTC corrente e ora è possibile fare riferimento a tale attributo utilizzando un elemento dati. Consulta la sezione [sezione successiva](#referencing-secrets) per ulteriori informazioni sui riferimenti ai segreti.

## Riferimenti ai segreti {#referencing-secrets}

Per fare riferimento a un segreto, devi creare un elemento dati di tipo &quot;[!UICONTROL Segreto]&quot; (fornito dalla [[!UICONTROL Core] estensione](../../extensions/web/core/overview.md)) su una proprietà di inoltro eventi. Durante la configurazione di questo elemento dati, viene richiesto di indicare quale segreto utilizzare per ogni ambiente. Puoi quindi creare regole che fanno riferimento a un elemento dati segreto, ad esempio all’interno dell’intestazione di una chiamata HTTP.

![Elemento dati segreto](../../images/api/guides/secrets/data-element.png)

>[!NOTE]
>
>Per aggiungere un elemento dati segreto a una libreria, è necessario disporre di almeno un elemento `succeeded` segreto associato all&#39;ambiente in cui viene creata la libreria. Ad esempio, se una libreria dispone di un elemento dati segreto che non dispone di un `succeeded` segreto configurato per [!UICONTROL Segreto di staging] Se tenti di generare la libreria nell&#39;ambiente di staging, viene generato un errore.

In fase di runtime, l’elemento dati segreto viene sostituito con l’artefatto di scambio segreto corrispondente salvato nell’ambiente.

## Passaggi successivi

Questa guida ha trattato i fondamenti dell’utilizzo dei segreti nell’API del reattore. Per informazioni dettagliate su come gestire i segreti utilizzando le chiamate API, consulta [guida all’endpoint segreti](../endpoints/secrets.md).
