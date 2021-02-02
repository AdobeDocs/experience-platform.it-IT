---
keywords: ' Experience Platform;home;argomenti popolari;API del servizio identità;guida per lo sviluppo del servizio identità;regione'
solution: Experience Platform
title: Introduzione
topic: API guide
description: 'Adobe Experience Platform Identity Service gestisce l’identificazione in tempo reale dei clienti tra dispositivi, canali e quasi in tempo reale, in quello che è noto come un grafico di identità all’interno di Adobe Experience Platform. '
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 1%

---


# [!DNL Identity Service] Guida per gli sviluppatori di API

Adobe Experience Platform [!DNL Identity Service] gestisce l&#39;identificazione cross-device, cross-channel e near-real-time dei clienti in quello che è noto come un grafico di identità all&#39;interno di Adobe Experience Platform.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Identity Service]](../home.md): Risolve la sfida fondamentale rappresentata dalla frammentazione dei dati del profilo cliente. Questo avviene attraverso la creazione di identità tra dispositivi e sistemi in cui i clienti interagiscono con il tuo marchio.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumo unificato in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standard con cui  [!DNL Platform] organizzare i dati relativi all&#39;esperienza dei clienti.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere o avere a disposizione per eseguire correttamente le chiamate all&#39;API [!DNL Identity Service].

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è innanzitutto necessario completare l&#39;esercitazione sull&#39;autenticazione [a2/>. ](https://www.adobe.com/go/platform-api-authentication-en) Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui verrà eseguita l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione di [panoramica sulla sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

### Routing basato su regione

L&#39;API [!DNL Identity Service] utilizza endpoint specifici dell&#39;area geografica che richiedono l&#39;inclusione di un elemento `{REGION}` come parte del percorso di richiesta. Durante il provisioning dell&#39;organizzazione IMS, una regione viene determinata e memorizzata nel profilo IMS. L&#39;utilizzo della regione corretta con ciascun endpoint garantisce che tutte le richieste effettuate utilizzando l&#39;API [!DNL Identity Service] vengano instradate nella regione appropriata.

Esistono due aree attualmente supportate dalle API [!DNL Identity Service]: VA7 e NLD2.

La tabella seguente mostra alcuni percorsi di esempio che utilizzano le aree:

| Servizio | Regione: VA7 | Regione: NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>Le richieste effettuate senza specificare una regione possono causare il routing delle chiamate all&#39;area errata o causare errori imprevisti nelle chiamate.

Se non riuscite a individuare la regione all&#39;interno del profilo IMS, contattate l&#39;amministratore di sistema per ottenere assistenza.

## Utilizzo dell&#39;API [!DNL Identity Service]

I parametri di identità utilizzati in questi servizi possono essere espressi in uno dei due modi seguenti: composito o XID.

Le identità composite sono costrutti che includono sia il valore ID che lo spazio dei nomi. Quando si utilizzano identità composite, lo spazio dei nomi può essere fornito in base al nome (`namespace.code`) o all&#39;ID (`namespace.id`).

Quando un&#39;identità è persistente, [!DNL Identity Service] genera e assegna un ID a tale identità, denominato ID nativo o XID. Tutte le varianti delle API Cluster e Mapping supportano sia le identità composite che XID nelle relative richieste e risposte. Per utilizzare queste API è necessario uno dei parametri: `xid` o una combinazione di [`ns` o `nsid`] e `id`.

Per limitare il payload nelle risposte, le API adattano le proprie risposte al tipo di costrutto di identità utilizzato. In altre parole, se trasmettete XID le risposte avranno XID, se trasmettete identità composite, la risposta seguirà la struttura utilizzata nella richiesta.

Gli esempi in questo documento non coprono la funzionalità completa dell&#39;API [!DNL Identity Service]. Per l&#39;API completa, vedete la [Guida di riferimento API Swagger](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml).

>[!NOTE]
>
>Quando nella richiesta viene utilizzato XID nativo, tutte le identità restituite saranno in formato XID nativo. Si consiglia di utilizzare il modulo ID/namespace. Per ulteriori informazioni, vedere la sezione relativa al [recupero dell&#39;XID per un&#39;identità](./create-custom-namespace.md).

## Passaggi successivi

Ora che avete raccolto le credenziali richieste, potete continuare a leggere il resto della guida per gli sviluppatori. Ogni sezione fornisce informazioni importanti sui relativi endpoint e illustra le chiamate API di esempio per l&#39;esecuzione di operazioni CRUD. Ogni chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e i payload formattati correttamente e una risposta di esempio per una chiamata riuscita.
