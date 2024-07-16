---
title: Segreti nell’API di Reactor
description: Scopri le nozioni di base su come configurare i segreti nell’API di Reactor per l’inoltro degli eventi.
exl-id: 0298c0cd-9fba-4b54-86db-5d2d8f9ade54
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 2%

---

# Segreti nell’API di Reactor

Nell’API di Reactor, un segreto è una risorsa che rappresenta una credenziale di autenticazione. I segreti vengono utilizzati nell’inoltro degli eventi per l’autenticazione in un altro sistema per lo scambio sicuro dei dati. Pertanto, è possibile creare segreti solo all&#39;interno delle proprietà di inoltro degli eventi (proprietà il cui attributo `platform` è impostato su `edge`).

Sono attualmente disponibili tre tipi di segreto supportati identificati nell&#39;attributo `type_of`:

| Tipo di segreto | Descrizione |
| --- | --- |
| `token` | Una singola stringa di caratteri che rappresenta un valore del token di autenticazione noto e compreso da entrambi i sistemi. |
| `simple-http` | Contiene due attributi di stringa rispettivamente per nome utente e password. |
| `oauth2-client_credentials` | Contiene diversi attributi per supportare la specifica di autenticazione [OAuth](https://datatracker.ietf.org/doc/html/rfc6749). L’inoltro degli eventi richiede le informazioni richieste, quindi gestisce il rinnovo di questi token per te in un intervallo specificato. |

{style="table-layout:auto"}

Questa guida fornisce una panoramica di alto livello sulla configurazione dei segreti da utilizzare nell’inoltro degli eventi. Per istruzioni dettagliate su come gestire i segreti nell&#39;API di Reactor, incluso un esempio di JSON della struttura di un segreto, consulta la [guida dell&#39;endpoint dei segreti](../endpoints/secrets.md).

## Credenziali

Ogni segreto contiene un attributo `credentials` che contiene i rispettivi valori delle credenziali. Quando [si crea un segreto nell&#39;API](../endpoints/secrets.md#create), ogni tipo di segreto ha attributi obbligatori diversi, come illustrato nelle sezioni seguenti:

* [&quot;token&quot;](#token)
* [&#39;simple-http&#39;](#simple-http)
* [&quot;oauth2-client_credentials&quot;](#oauth2-client_credentials)
* [&quot;oauth2-google&quot;](#oauth2-google)

### `token` {#token}

I segreti con un valore `type_of` di `token` richiedono un solo attributo in `credentials`:

| Attributo credenziali | Tipo di dati | Descrizione |
| --- | --- | --- |
| `token` | Stringa | Un token segreto riconosciuto dal sistema di destinazione. |

{style="table-layout:auto"}

Il token viene archiviato come valore statico, pertanto le proprietà `expires_at` e `refresh_at` del segreto vengono impostate su `null` al momento della creazione del segreto.

### `simple-http` {#simple-http}

I segreti con un valore `type_of` di `simple-http` richiedono i seguenti attributi in `credentials`:

| Attributo credenziali | Tipo di dati | Descrizione |
| --- | --- | --- |
| `username` | Stringa | Un nome utente. |
| `password` | Stringa | Una password. Questo valore non è incluso nella risposta API. |

{style="table-layout:auto"}

Quando viene creato il segreto, i due attributi vengono scambiati con una codifica BASE64 di `username:password`. Dopo lo scambio, le proprietà `expires_at` e `refresh_at` del segreto sono impostate su `null`.

### `oauth2-client_credentials` {#oauth2-client_credentials}

I segreti con un valore `type_of` di `oauth2-client_credentials` richiedono i seguenti attributi in `credentials`:

| Attributo credenziali | Tipo di dati | Descrizione |
| --- | --- | --- |
| `client_id` | Stringa | ID client per l’integrazione OAuth. |
| `client_secret` | Stringa | Il segreto client per l’integrazione OAuth. Questo valore non è incluso nella risposta API. |
| `token_url` | Stringa | URL di autorizzazione per l’integrazione OAuth. |
| `refresh_offset` | Intero | *(Facoltativo)* Il valore, in secondi, per l&#39;offset dell&#39;operazione di aggiornamento. Se questo attributo viene omesso durante la creazione del segreto, il valore viene impostato su `14400` (quattro ore) per impostazione predefinita. |
| `options` | Oggetto | *(Facoltativo)* Specifica opzioni aggiuntive per l&#39;integrazione OAuth:<ul><li>`scope`: stringa che rappresenta l&#39;ambito [OAuth 2.0](https://oauth.net/2/scope/) per le credenziali.</li><li>`audience`: stringa che rappresenta un token di accesso [Auth0](https://auth0.com/docs/protocols/protocol-oauth2).</li></ul> |

Quando viene creato o aggiornato un segreto `oauth2-client_credentials`, gli elementi `client_id` e `client_secret` (e probabilmente `options`) vengono scambiati in una richiesta POST a `token_url`, in base al flusso delle credenziali client del protocollo OAuth.

>[!NOTE]
>
>Il corpo della risposta del servizio di autorizzazione deve essere compatibile con il protocollo OAuth.

Se il servizio di autorizzazione risponde con `200 OK` e un corpo di risposta JSON, il corpo viene analizzato e `access_token` viene inviato all&#39;ambiente perimetrale e `expires_in` viene utilizzato per calcolare gli attributi `expires_at` e `refresh_at` per il segreto. Se non è presente alcuna associazione di ambiente sul segreto, `access_token` verrà eliminato.

Uno scambio di credenziali viene considerato riuscito nelle seguenti condizioni:

* `expires_in` è maggiore di `28800` (otto ore).
* `refresh_offset` è minore del valore di `expires_in` meno `14400` (quattro ore). Ad esempio, se `expires_in` è `36000` (dieci ore) e `refresh_offset` è `28800` (otto ore), lo scambio è considerato non riuscito perché `28800` è maggiore di `36000` - `14400` (`21600`).

Se lo scambio ha esito positivo, l&#39;attributo di stato del segreto è impostato su `succeeded` e i valori per `expires_at` e `refresh_at` sono impostati:

* `expires_at` è l&#39;ora UTC corrente più il valore di `expires_in`.
* `refresh_at` è l&#39;ora UTC corrente più il valore di `expires_in`, meno il valore di `refresh_offset`. Ad esempio, se `expires_in` è `43200` (dodici ore) e `refresh_offset` è `14400` (quattro ore), la proprietà `refresh_at` verrà impostata su `28800` (otto ore) dopo l&#39;ora UTC corrente.

Se lo scambio non riesce per qualsiasi motivo, l&#39;attributo `status_details` nell&#39;oggetto `meta` viene aggiornato con le informazioni rilevanti.

#### Aggiornamento di un segreto `oauth2-client_credentials`

Se a un ambiente è stato assegnato un segreto `oauth2-client_credentials` e il relativo stato è `succeeded` (le credenziali sono state scambiate correttamente), viene eseguito automaticamente un nuovo scambio il `refresh_at`.

Se lo scambio ha esito positivo, l&#39;attributo `refresh_status` nell&#39;oggetto `meta` è impostato su `succeeded` mentre `expires_at`, `refresh_at` e `activated_at` sono aggiornati di conseguenza.

Se lo scambio non riesce, l’operazione viene tentata altre tre volte, con l’ultimo tentativo non più di due ore prima della scadenza del token di accesso. Se tutti i tentativi non vanno a buon fine, l&#39;attributo `refresh_status_details` dell&#39;oggetto `meta` viene aggiornato con i relativi dettagli.

### `oauth2-google` {#oauth2-google}

I segreti con un valore `type_of` di `oauth2-google` richiedono l&#39;attributo seguente in `credentials`:

| Attributo credenziali | Tipo di dati | Descrizione |
| --- | --- | --- |
| `scopes` | Array | Elenca gli ambiti di prodotto di Google per l’autenticazione. Sono supportati i seguenti ambiti:<ul><li>[Google Ads](https://developers.google.com/google-ads/api/docs/oauth/overview): `https://www.googleapis.com/auth/adwords`</li><li>[Google Pub/Sub](https://cloud.google.com/pubsub/docs/reference/service_apis_overview): `https://www.googleapis.com/auth/pubsub`</li></ul> |

Dopo aver creato il segreto `oauth2-google`, la risposta include una proprietà `meta.authorization_url`. È necessario copiare e incollare questo URL in un browser per completare il flusso di autenticazione di Google.

#### Riautorizza un segreto `oauth2-google`

L&#39;URL di autorizzazione per un segreto `oauth2-google` scade un&#39;ora dopo la creazione del segreto (come indicato da `meta.authorization_url_expires_at`). Trascorso questo periodo, il segreto deve essere nuovamente autorizzato per rinnovare il processo di autenticazione.

Per informazioni dettagliate su come autorizzare nuovamente un segreto `oauth2-google` effettuando una richiesta PATCH all&#39;API di Reactor, consultare la [guida dell&#39;endpoint &quot;secrets&quot;](../endpoints/secrets.md#reauthorize).

## Relazione ambiente

Quando si crea un segreto, è necessario specificare l&#39;[ambiente](../endpoints/environments.md) in cui verrà creato. I segreti vengono distribuiti immediatamente nell’ambiente in cui vengono creati.

Un segreto può essere associato a un solo ambiente. Una volta stabilita la relazione tra un segreto e un ambiente, il segreto non può essere cancellato dall’ambiente e non può essere associato a un ambiente diverso.

>[!NOTE]
>
>L’unica eccezione a questa regola è se l’ambiente in questione viene eliminato. In questo caso, la relazione viene cancellata e il segreto può essere assegnato a un ambiente diverso.

Dopo lo scambio delle credenziali di un segreto, per associare un segreto a un ambiente, l&#39;artefatto di scambio (la stringa del token per `token`, la stringa di codifica Base64 per `simple-http` o il token di accesso per `oauth2-client_credentials`) viene salvato in modo sicuro nell&#39;ambiente.

Una volta salvato correttamente l&#39;artefatto di scambio nell&#39;ambiente, l&#39;attributo `activated_at` del segreto viene impostato sull&#39;ora UTC corrente e ora è possibile farvi riferimento utilizzando un elemento dati. Per ulteriori informazioni sui riferimenti ai segreti, consulta la [sezione successiva](#referencing-secrets).

## Segreti di riferimento {#referencing-secrets}

Per fare riferimento a un segreto, è necessario creare un elemento dati di tipo &quot;[!UICONTROL Segreto]&quot; (fornito dall&#39;estensione [[!UICONTROL Core]](../../extensions/client/core/overview.md)) in una proprietà di inoltro eventi. Durante la configurazione di questo elemento dati, viene richiesto di indicare il segreto da utilizzare per ogni ambiente. Puoi quindi creare regole che fanno riferimento a un elemento dati segreto, ad esempio all’interno dell’intestazione di una chiamata HTTP.

![Elemento dati segreto](../../images/api/guides/secrets/data-element.png)

>[!NOTE]
>
>Per aggiungere un elemento dati segreto a una libreria, è necessario avere almeno un segreto `succeeded` associato all&#39;ambiente in cui viene generata la libreria. Ad esempio, se una libreria ha un elemento dati segreto che non ha un segreto `succeeded` configurato per la sezione [!UICONTROL Segreto di staging], il tentativo di generare tale libreria nell&#39;ambiente di staging genererà un errore.

In fase di esecuzione, l’elemento dati segreto viene sostituito con il corrispondente artefatto di scambio segreto salvato nell’ambiente.

## Passaggi successivi

Questa guida descrive le nozioni di base sull’utilizzo dei segreti nell’API di Reactor. Per informazioni dettagliate su come gestire i segreti tramite chiamate API, consulta la [guida dell&#39;endpoint &quot;secrets&quot;](../endpoints/secrets.md).
