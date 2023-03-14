---
keywords: Experience Platform;home;argomenti popolari;identity service api;guida per gli sviluppatori identity service;region
solution: Experience Platform
title: Guida API di Identity Service
description: L’API del servizio Identity consente agli sviluppatori di gestire l’identificazione dei clienti in tempo quasi reale tra dispositivi e canali diversi, utilizzando i grafici delle identità in Adobe Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
source-git-commit: ad9fb0bcc7bca55da432c72adc94d49e3c63ad6e
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 3%

---

# Guida dell’API di [!DNL Identity Service]

Adobe Experience Platform [!DNL Identity Service] gestisce l’identificazione dei clienti in tempo reale, tra dispositivi e canali diversi, in quello che viene definito un grafico di identità in Adobe Experience Platform.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Identity Service]](../home.md): risolve la sfida fondamentale posta dalla frammentazione dei dati del profilo cliente. Lo fa collegando le identità tra dispositivi e sistemi in cui i clienti interagiscono con il tuo marchio.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce un profilo consumer unificato in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Platform] organizza i dati sull’esperienza del cliente.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere o disporre di per effettuare correttamente chiamate al [!DNL Identity Service] API.

### Lettura delle chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito il codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nel [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori per le intestazioni richieste

Per effettuare chiamate a [!DNL Platform] , devi prima completare le [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- Autorizzazione: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolati in specifiche sandbox virtuali. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedere [documentazione di panoramica sulla sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Content-Type: application/json

### Indirizzamento basato su regione

Il [!DNL Identity Service] L’API utilizza endpoint specifici per regione che richiedono l’inclusione di un `{REGION}` come parte del percorso della richiesta. Durante il provisioning dell’organizzazione IMS, un’area geografica viene determinata e memorizzata nel profilo dell’organizzazione IMS. L’utilizzo dell’area corretta con ogni endpoint assicura che tutte le richieste effettuate utilizzando [!DNL Identity Service] Le API vengono instradate all’area geografica appropriata.

Al momento sono due le aree supportate da [!DNL Identity Service] API: VA7 e NLD2.

La tabella seguente mostra alcuni percorsi di esempio che utilizzano le regioni:

| Servizio | Regione: VA7 | Regione: NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>Le richieste effettuate senza specificare un’area possono causare l’instradamento delle chiamate all’area errata o causare un errore imprevisto delle chiamate.

Se non riesci a individuare l’area geografica all’interno del profilo dell’organizzazione IMS, contatta l’amministratore di sistema per assistenza.

## Utilizzo di [!DNL Identity Service] API

I parametri di identità utilizzati in questi servizi possono essere espressi in due modi: composito o XID.

Le identità composite sono costrutti che includono sia il valore ID che lo spazio dei nomi. Quando si utilizzano identità composite, lo spazio dei nomi può essere fornito con uno dei nomi (`namespace.code`) o ID (`namespace.id`).

Quando un’identità viene mantenuta, [!DNL Identity Service] genera e assegna un ID a tale identità, denominato ID nativo o XID. Tutte le varianti di Cluster e Mapping API supportano sia le identità composite che XID nelle richieste e nelle risposte. Uno dei parametri è obbligatorio - `xid` o combinazione di [`ns` o `nsid`] e `id` per utilizzare queste API.

Per limitare il payload nelle risposte, le API adattano le loro risposte al tipo di costrutto di identità utilizzato. Cioè, se passi XID le tue risposte avranno XID, se passi identità composite, la risposta seguirà la struttura utilizzata nella richiesta.

Gli esempi contenuti in questo documento non descrivono tutte le funzionalità del [!DNL Identity Service] API. Per l’API completa, consulta [Riferimento API per Swagger](https://www.adobe.io/experience-platform-apis/references/identity-service).

>[!NOTE]
>
>Tutte le identità restituite saranno in formato XID nativo quando nella richiesta viene utilizzato XID nativo. Si consiglia di utilizzare il modulo ID/spazio dei nomi. Per ulteriori informazioni, consulta la sezione su [recupero dello XID per un’identità](./create-custom-namespace.md).

## Passaggi successivi

Ora che hai raccolto le credenziali richieste, puoi continuare a leggere il resto della guida per sviluppatori. Ogni sezione fornisce informazioni importanti sugli endpoint e illustra esempi di chiamate API per l’esecuzione di operazioni CRUD. Ogni chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e i payload formattati correttamente, e una risposta di esempio per una chiamata di successo.
