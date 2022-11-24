---
title: Panoramica dell’estensione Cloud Connector
description: Scopri l’estensione di inoltro degli eventi Cloud Connector in Adobe Experience Platform.
exl-id: f3713652-ac32-4171-8dda-127c8c235849
source-git-commit: c7344d0ac5b65c6abae6a040304f27dc7cd77cbb
workflow-type: tm+mt
source-wordcount: '1616'
ht-degree: 98%

---

# Panoramica dell’estensione Cloud Connector

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

L’estensione di inoltro degli eventi Cloud Connector consente di creare richieste HTTP personalizzate per l’invio di dati a una destinazione o il recupero di dati da una destinazione. L’estensione Cloud Connector è simile a Postman su Adobe Experience Platform Edge Network e può essere utilizzata per inviare dati a un endpoint che non ha ancora un’estensione dedicata.

Utilizza questo riferimento per informazioni sulle opzioni disponibili quando utilizzi questa estensione per creare una regola.

## Tipo di azione dell’estensione Cloud Connector

Questa sezione descrive il tipo di azione Invia dati disponibile nell’estensione Cloud Connector di Adobe Experience Platform.

### Tipo di richiesta

Per selezionare il tipo di richiesta necessario per l’endpoint, seleziona il tipo appropriato nel menu a discesa [!UICONTROL Tipo di richiesta].

| Metodo | Descrizione |
|---|---|
| [GET](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/GET) | Richiede una rappresentazione della risorsa specificata. Le richieste che utilizzano GET devono recuperare solo i dati. |
| [POST](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST) | Invia un’entità alla risorsa specificata, spesso causando una modifica dello stato o degli effetti collaterali sul server. |
| [PUT](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PUT) | Sostituisce tutte le rappresentazioni correnti della risorsa target con il payload della richiesta. |
| [PATCH](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PATCH) | Applica modifiche parziali a una risorsa. |
| [DELETE](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/DELETE) | Elimina la risorsa specificata. |

### URL dell’endpoint

Nel campo di testo accanto al menu a discesa Tipo richiesta, immetti l’URL dell’endpoint al quale si stanno inviando i dati.

### Parametri di query, intestazioni e configurazione corpo

Utilizza ciascuna di queste schede (Parametri query, Intestazioni ed Elementi dati del corpo) per controllare quali dati vengono inviati a un determinato endpoint.

#### Parametri query

Definisci una chiave e un valore per ogni coppia chiave-valore che si desidera inviare come parametro di stringa di query. Per immettere manualmente un elemento dati, utilizza la tokenizzazione dell’elemento dati con parentesi graffa per l’inoltro di eventi. Per fare riferimento al valore di un elemento dati denominato “siteSection” come chiave o valore, immetti `{{siteSection}}`. In alternativa, seleziona l’elemento di dati creato in precedenza scegliendolo nel menu a discesa.

Per aggiungere altri parametri di query, seleziona **[!UICONTROL Aggiungi altro]**.

#### Intestazioni

Definisci una chiave e un valore per ogni coppia chiave-valore da inviare come intestazione. Per immettere manualmente un elemento dati, utilizza la tokenizzazione dell’elemento dati con parentesi graffa per l’inoltro di eventi. Per fare riferimento al valore di un elemento dati denominato “pageName” come chiave o valore, immetti `{{pageName}}`. In alternativa, seleziona l’elemento dati creato in precedenza scegliendolo nel menu a discesa.

Per aggiungere altre intestazioni, seleziona **[!UICONTROL Aggiungi altro]**.

Nella tabella seguente sono elencate le intestazioni predefinite. Non sei limitato a utilizzare solo queste intestazioni: queste sono disponibili per praticità e, se necessario, puoi aggiungere altre intestazioni personalizzate.

>[!NOTE]
>
>Per informazioni più dettagliate su queste intestazioni, visita [https://developer.mozilla.org/it-IT/docs/Web/HTTP/Headers](https://developer.mozilla.org/it-IT/docs/Web/HTTP/Headers).

| Header | Descrizione |
|---|---|
| [A-IM](https://developer.mozilla.org/it-IT/docs/Web/HTTP/Headers/Accept) |  |
| [Accept](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept) |  |
| [Accept-Charset](https://developer.mozilla.org/it-IT/docs/Web/HTTP/Headers/Accept-Charset) |  |
| [Accept-Encoding](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Encoding) |  |
| [Accept-Language](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Language) |  |
| [Accept-Datetime](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept) | Trasmesso da un agente utente, indica la volontà di accedere a uno stato passato di una risorsa originale. A tal fine, l’intestazione `Accept-Datetime` viene trasmessa in una richiesta HTTP eseguita su TimeGate per una risorsa originale e il suo valore indica il datetime dello stato precedente desiderato per la risorsa originale. |
| Access-Control-Request-Headers | Utilizzato dai browser durante l’emissione di una [richiesta di verifica preliminare](https://developer.mozilla.org/en-US/docs/Glossary/preflight_request), per comunicare al server le [intestazioni HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers) che il client potrebbe inviare quando viene effettuata la richiesta effettiva. |
| Access-Control-Request-Method | Utilizzato dai browser quando viene rilasciata una [richiesta di verifica preliminare](https://developer.mozilla.org/en-US/docs/Glossary/preflight_request), per comunicare al server il [metodo HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods) che verrà utilizzato quando viene effettuata la richiesta effettiva. Questa intestazione è necessaria perché la richiesta di verifica preliminare è sempre un metodo [OPTION](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/OPTIONS) e non utilizza lo stesso metodo della richiesta effettiva. |
| Authorization | Contiene le credenziali per l’autenticazione di un agente utente con un server. |
| [Cache-Control](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control) | Direttive per meccanismi di caching sia nelle richieste che nelle risposte. |
| [Connessione](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Connection) | Controlla se la connessione di rete rimane aperta al termine della transazione corrente. |
| [Content-Length](https://developer.mozilla.org/it-IT/docs/Web/HTTP/Headers/Content-Length) | Dimensione della risorsa, in numero decimale di byte. |
| [Content-Type](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Type) | Indica il tipo di file multimediali della risorsa. |
| Cookie | Contiene i [cookie HTTP](https://developer.mozilla.org/it-IT/docs/Web/HTTP/Cookies) memorizzati, inviati in precedenza dal server con l’intestazione [`Set-Cookie`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie). |
| Data | L’intestazione HTTP generale contiene la data e l’ora in cui è stato creato il messaggio. |
| [DNT](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/DNT) | Esprime le preferenze di tracciamento dell’utente. |
| Expect | Indica le aspettative che devono essere soddisfatte dal server per gestire correttamente la richiesta. |
| Forwarded | Contiene informazioni provenienti dai [server reverse proxy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Proxy_servers_and_tunneling) che vengono alterate o perse quando un proxy viene coinvolto nel percorso della richiesta. |
| Da | Contiene un indirizzo e-mail Internet per un utente umano che controlla l’agente utente richiedente. |
| Host | Specifica l’host e il numero di porta del server al quale viene inviata la richiesta. |
| If-Match |  |
| If-Modified-Since |  |
| [If-None-Match](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-None-Match) |  |
| [If-Range](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Range) |  |
| [If-Unmodified-Since](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Unmodified-Since) |  |
| [Max-Forwards](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Unmodified-Since) |  |
| [Origin](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Origin) |  |
| [Pragma](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Pragma) | Intestazione specifica per l’implementazione, che può avere vari effetti ovunque lungo la catena di richieste e risposte. Utilizzato per compatibilità con le versioni precedenti delle cache HTTP/1.0 in cui l’intestazione Cache-Control non è ancora presente. |  |
| [Proxy-Authorization](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Proxy-Authorization) |
| [Range](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Range) | Indica la parte di un documento che il server deve restituire. |  |
| [Referer](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referer) | Indirizzo della pagina web precedente dalla quale un collegamento ha portato alla pagina richiesta. |  |
| TE | Specifica le codifiche di trasferimento che l’agente utente è disposto ad accettare, anche chiamato `Accept-Transfer-Encoding` in modo in modo più informale e intuitivo. |
| Esegui l&#39;aggiornamento | Il documento RFC pertinente per il campo dell&#39;intestazione [`Upgrade` è RFC 7230, sezione 6.7](https://tools.ietf.org/html/rfc7230#section-6.7). Lo standard stabilisce regole per l&#39;aggiornamento o la modifica a un protocollo diverso sulla connessione corrente client, server e protocollo di trasporto. Ad esempio, questo standard di intestazione consente a un client di passare da HTTP 1.1 a HTTP 2.0, sempre che il server decida di riconoscere e implementare il campo dell&#39;intestazione `Upgrade`. Nessuna delle parti è tenuta ad accettare i termini specificati nel campo dell&#39;intestazione `Upgrade`. Può essere utilizzato nelle intestazioni client e server. Se il campo dell&#39;intestazione `Upgrade` è specificato, il mittente DEVE anche inviare il campo dell&#39;intestazione `Connection` con l&#39;opzione `upgrade` specificata. |  |
| [Utente-agente](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/User-Agent) | Contiene una stringa caratteristica che consente ai peer del protocollo di rete di identificare il tipo di applicazione, il sistema operativo, il fornitore di software o la versione del software dell&#39;agente utente del software richiedente. |
| [Via](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Via) | Vengono aggiunti dai proxy, sia forward che reverse proxy, e possono essere visualizzati nelle intestazioni delle richieste e delle risposte. |
| [Avvertenza](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Warning) | Informazioni generali di avviso sui possibili problemi. |
| X-CSRF-Token |  |
| X-Requested-With |  |

#### Body come JSON

Definire una chiave e un valore per ogni coppia chiave-valore da inviare nel corpo della richiesta. Per immettere manualmente un elemento dati, utilizza la tokenizzazione dell’elemento dati con parentesi graffa per l’inoltro di eventi. Per fare riferimento al valore di un elemento dati denominato &quot;appSection&quot; come chiave o valore, immetti `{{appSection}}`. In alternativa, seleziona l’elemento di dati creato in precedenza scegliendolo nel menu a discesa.

Per aggiungere altre coppie chiave-valore, seleziona **[!UICONTROL Aggiungi altro]**.

#### Body come Raw

Definire una chiave e un valore per ogni coppia chiave-valore da inviare nel corpo della richiesta. Per immettere manualmente un elemento dati, utilizza la tokenizzazione dell’elemento dati con parentesi graffa per l’inoltro di eventi. Per fare riferimento al valore di un elemento dati denominato &quot;appSection&quot; come chiave o valore, immetti `{{appSection}}`. In alternativa, seleziona l&#39;elemento dati creato in precedenza scegliendolo nel menu a discesa. Puoi aggiungere uno o più elementi di dati.

### Avanzate

Le azioni all’interno delle regole nell&#39;inoltro degli eventi vengono eseguite in sequenza. Potrebbero verificarsi situazioni in cui vuoi recuperare dati da una sorgente esterna che non è presente nell&#39;evento in arrivo dal client, quindi rispondere e trasformare o inviare tali dati a una destinazione finale in un&#39;azione successiva all&#39;interno di una singola regola. Questa operazione è possibile tramite l’opzione &quot;Salva la risposta della richiesta&quot; nella sezione avanzata.

Per salvare il corpo della risposta da un endpoint, seleziona la casella **[!UICONTROL Salva la risposta della richiesta]** e definisci una chiave di risposta nel campo di testo.

Se la chiave di risposta è definita come `productDetails`, fai riferimento a tali dati in un elemento dati e poi a tale elemento in un&#39;azione successiva all&#39;interno della stessa regola. Per creare un elemento dati che fa riferimento a `productDetail`, crea un elemento dati di tipo `path` e immetti il percorso seguente:

```Json
arc.ruleStash.[EXTENSION-NAME-HERE].responses.[RESPONSE-KEY-HERE] 

arc.ruleStash.adobe-cloud-connector.reponses.productDetails 
```
