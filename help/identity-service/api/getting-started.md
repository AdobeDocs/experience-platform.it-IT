---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Introduzione
topic: API guide
translation-type: tm+mt
source-git-commit: 6ffdcc2143914e2ab41843a52dc92344ad51bcfb
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 1%

---


# [!DNL Identity Service] Guida per gli sviluppatori di API

 Adobe Experience Platform [!DNL Identity Service] gestisce l&#39;identificazione cross-device, cross-channel e near-real-time dei clienti in quello che è noto come un grafico dell&#39;identità all&#39;interno  Adobe Experience Platform.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti del  Adobe Experience Platform:

- [!DNL Identity Service](../home.md): Risolve la sfida fondamentale rappresentata dalla frammentazione dei dati del profilo cliente. Questo avviene attraverso la creazione di identità tra dispositivi e sistemi in cui i clienti interagiscono con il tuo marchio.
- [!DNL Real-time Customer Profile](../../profile/home.md): Fornisce un profilo di consumo unificato in tempo reale basato su dati aggregati provenienti da più origini.
- [!DNL Experience Data Model (XDM)](../../xdm/home.md): Il framework standard con cui [!DNL Platform] organizzare i dati relativi all&#39;esperienza del cliente.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere o avere a disposizione per eseguire correttamente le chiamate all&#39; [!DNL Identity Service] API.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

### Routing basato su regione

L&#39; [!DNL Identity Service] API utilizza endpoint specifici per l&#39;area geografica che richiedono l&#39;inclusione di un elemento `{REGION}` come parte del percorso di richiesta. Durante il provisioning dell&#39;organizzazione IMS, una regione viene determinata e memorizzata nel profilo IMS. L&#39;utilizzo della regione corretta con ciascun endpoint garantisce che tutte le richieste effettuate utilizzando l&#39; [!DNL Identity Service] API vengano instradate nella regione appropriata.

Le [!DNL Identity Service] API supportano attualmente due aree: VA7 e NLD2.

La tabella seguente mostra alcuni percorsi di esempio che utilizzano le aree:

| Servizio | Regione: VA7 | Regione: NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE] Le richieste effettuate senza specificare una regione possono causare il routing delle chiamate all&#39;area errata o causare errori imprevisti nelle chiamate.

Se non riuscite a individuare la regione all&#39;interno del profilo IMS, contattate l&#39;amministratore di sistema per ottenere assistenza.

## Utilizzo dell&#39; [!DNL Identity Service] API

I parametri di identità utilizzati in questi servizi possono essere espressi in uno dei due modi seguenti: composito o XID.

Le identità composite sono costrutti che includono sia il valore ID che lo spazio dei nomi. Quando si utilizzano identità composite, lo spazio dei nomi può essere fornito tramite nome (`namespace.code`) o ID (`namespace.id`).

Quando un&#39;identità è persistente, [!DNL Identity Service] genera e assegna un ID a tale identità, denominato ID nativo o XID. Tutte le varianti delle API Cluster e Mapping supportano sia le identità composite che XID nelle relative richieste e risposte. Uno dei parametri è richiesto - `xid` o combinazione di [`ns` o `nsid`] e `id` per utilizzare queste API.

Per limitare il payload nelle risposte, le API adattano le proprie risposte al tipo di costrutto di identità utilizzato. In altre parole, se trasmettete XID le risposte avranno XID, se trasmettete identità composite, la risposta seguirà la struttura utilizzata nella richiesta.

Gli esempi in questo documento non coprono la funzionalità completa dell&#39; [!DNL Identity Service] API. Per l&#39;API completa, consultate il riferimento API [Swagger](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml).

>[!NOTE] Quando nella richiesta viene utilizzato XID nativo, tutte le identità restituite saranno in formato XID nativo. Si consiglia di utilizzare il modulo ID/namespace. Per ulteriori informazioni, consultate la sezione su come [ottenere l&#39;XID per un&#39;identità](./create-custom-namespace.md).

## Passaggi successivi

Ora che avete raccolto le credenziali richieste, potete continuare a leggere il resto della guida per gli sviluppatori. Ogni sezione fornisce informazioni importanti sui relativi endpoint e illustra le chiamate API di esempio per l&#39;esecuzione di operazioni CRUD. Ogni chiamata include il formato **** API generale, una **richiesta** di esempio che mostra le intestazioni richieste e i payload formattati correttamente e una **risposta** di esempio per una chiamata riuscita.
