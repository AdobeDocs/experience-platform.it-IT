---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Introduzione
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Guida per gli sviluppatori API di Identity Service

Adobe Experience Platform Identity Service gestisce l’identificazione in tempo reale dei clienti tra dispositivi, canali e quasi in tempo reale, in un grafico di identità noto come Adobe Experience Platform.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [Servizio](../home.md)identità: Risolve la sfida fondamentale rappresentata dalla frammentazione dei dati del profilo cliente. Questo avviene attraverso la creazione di identità tra dispositivi e sistemi in cui i clienti interagiscono con il tuo marchio.
- [Profilo](../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato in tempo reale basato su dati aggregati provenienti da più origini.
- [Experience Data Model (XDM)](../../xdm/home.md): Il framework standardizzato tramite il quale la piattaforma organizza i dati sull&#39;esperienza cliente.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere o avere a disposizione per eseguire correttamente le chiamate all&#39;API del servizio identità.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione [come leggere le chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi della piattaforma Experience.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle API della piattaforma, dovete prima completare l&#39;esercitazione [di](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in Experience Platform sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API della piattaforma richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Per ulteriori informazioni sulle sandbox in Piattaforma, consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

### Routing basato su regione

L&#39;API del servizio identità utilizza endpoint specifici per l&#39;area geografica che richiedono l&#39;inclusione di un elemento `{REGION}` come parte del percorso della richiesta. Durante il provisioning dell&#39;organizzazione IMS, una regione viene determinata e memorizzata nel profilo IMS. L&#39;utilizzo della regione corretta con ciascun endpoint garantisce che tutte le richieste effettuate utilizzando l&#39;API del servizio identità vengano instradate nella regione appropriata.

Esistono due aree attualmente supportate dalle API del servizio identità: VA7 e NLD2.

La tabella seguente mostra alcuni percorsi di esempio che utilizzano le aree:

| Servizio | Regione: VA7 | Regione: NLD2 |
| ------ | -------- |--------- |
| API Servizio identità | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| API namespace identità | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE] Le richieste effettuate senza specificare una regione possono causare il routing delle chiamate all&#39;area errata o causare errori imprevisti nelle chiamate.

Se non riuscite a individuare la regione all&#39;interno del profilo IMS, contattate l&#39;amministratore di sistema per ottenere assistenza.

## Utilizzo dell’API di Servizio identità

I parametri di identità utilizzati in questi servizi possono essere espressi in uno dei due modi seguenti: composito o XID.

Le identità composite sono costrutti che includono sia il valore ID che lo spazio dei nomi. Quando si utilizzano identità composite, lo spazio dei nomi può essere fornito tramite nome (`namespace.code`) o ID (`namespace.id`).

Quando un&#39;identità è persistente, il servizio identità genera e assegna un ID a tale identità, denominato ID nativo o XID. Tutte le varianti delle API Cluster e Mapping supportano sia le identità composite che XID nelle relative richieste e risposte. Uno dei parametri è richiesto - `xid` o combinazione di [`ns` o `nsid`] e `id` per utilizzare queste API.

Per limitare il payload nelle risposte, le API adattano le proprie risposte al tipo di costrutto di identità utilizzato. In altre parole, se trasmettete XID le risposte avranno XID, se trasmettete identità composite, la risposta seguirà la struttura utilizzata nella richiesta.

Gli esempi contenuti in questo documento non coprono le funzionalità complete dell&#39;API del servizio identità. Per l&#39;API completa, consultate il riferimento API [Swagger](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml).

>[!NOTE] Quando nella richiesta viene utilizzato XID nativo, tutte le identità restituite saranno in formato XID nativo. Si consiglia di utilizzare il modulo ID/namespace. Per ulteriori informazioni, consultate la sezione su come [ottenere l&#39;XID per un&#39;identità](./create-custom-namespace.md).

## Passaggi successivi

Ora che avete raccolto le credenziali richieste, potete continuare a leggere il resto della guida per gli sviluppatori. Ogni sezione fornisce informazioni importanti sui relativi endpoint e illustra le chiamate API di esempio per l&#39;esecuzione di operazioni CRUD. Ogni chiamata include il formato **** API generale, una **richiesta** di esempio che mostra le intestazioni richieste e i payload formattati correttamente e una **risposta** di esempio per una chiamata riuscita.
