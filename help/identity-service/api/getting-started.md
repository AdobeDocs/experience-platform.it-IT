---
keywords: Experience Platform;home;argomenti popolari;identity service api;guida per gli sviluppatori identity service;region
solution: Experience Platform
title: Guida API di Identity Service
description: L’API del servizio Identity consente agli sviluppatori di gestire l’identificazione dei clienti in tempo quasi reale tra dispositivi e canali diversi, utilizzando i grafici delle identità in Adobe Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
role: Developer
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 14%

---

# Guida dell’API di [!DNL Identity Service]

Adobe Experience Platform [!DNL Identity Service] gestisce l&#39;identificazione dei clienti in tempo reale, tra dispositivi e canali diversi, in quello che viene definito un grafico delle identità in Adobe Experience Platform.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Identity Service]](../home.md): risolve la sfida fondamentale posta dalla frammentazione dei dati del profilo cliente. Ciò avviene collegando le identità tra dispositivi e sistemi in cui i clienti interagiscono con il tuo marchio.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce un profilo consumer unificato in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): framework standardizzato tramite il quale [!DNL Platform] organizza i dati sull&#39;esperienza del cliente.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere o avere a disposizione per effettuare correttamente chiamate all&#39;API [!DNL Identity Service].

### Lettura delle chiamate API di esempio

Questa guida fornisce esempi di chiamate API per illustrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogliere i valori per le intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l&#39;[esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Completando il tutorial sull’autenticazione si ottengono i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di [!DNL Experience Platform], come mostrato di seguito:

- Autorizzazione: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in specifiche sandbox virtuali. Tutte le richieste alle API [!DNL Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la [documentazione di panoramica sulle sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Content-Type: application/json

### Indirizzamento basato su regione

L&#39;API [!DNL Identity Service] utilizza endpoint specifici della regione che richiedono l&#39;inclusione di un `{REGION}` come parte del percorso della richiesta. Durante il provisioning dell’organizzazione, un’area viene determinata e memorizzata nel profilo dell’organizzazione. L&#39;utilizzo dell&#39;area corretta con ogni endpoint assicura che tutte le richieste effettuate utilizzando l&#39;API [!DNL Identity Service] vengano instradate all&#39;area appropriata.

Al momento sono presenti due aree supportate dalle API [!DNL Identity Service]: VA7 e NLD2.

La tabella seguente mostra alcuni percorsi di esempio che utilizzano le regioni:

| Servizio | Regione: VA7 | Regione: NLD2 |
| ------ | -------- |--------- |
| API [!DNL Identity Service] | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| API [!DNL Identity Namespace] | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>Le richieste effettuate senza specificare un’area possono causare l’instradamento delle chiamate all’area errata o causare un errore imprevisto delle chiamate.

Se non riesci a individuare l’area geografica all’interno del profilo organizzazione, contatta l’amministratore di sistema per assistenza.

## Utilizzo dell&#39;API [!DNL Identity Service]

I parametri di identità utilizzati in questi servizi possono essere espressi in due modi: composito o XID.

Le identità composite sono costrutti che includono sia il valore ID che lo spazio dei nomi. Quando si utilizzano identità composite, lo spazio dei nomi può essere fornito da un nome (`namespace.code`) o da un ID (`namespace.id`).

Quando un&#39;identità viene resa persistente, [!DNL Identity Service] genera e assegna un ID a tale identità, denominato ID nativo, o XID. Tutte le varianti di Cluster e Mapping API supportano sia le identità composite che XID nelle richieste e nelle risposte. Uno dei parametri è obbligatorio - `xid` o la combinazione di [`ns` o `nsid`] e `id` per utilizzare queste API.

Per limitare il payload nelle risposte, le API adattano le loro risposte al tipo di costrutto di identità utilizzato. Cioè, se passi XID le tue risposte avranno XID, se passi identità composite, la risposta seguirà la struttura utilizzata nella richiesta.

Gli esempi in questo documento non descrivono la funzionalità completa dell&#39;API [!DNL Identity Service]. Per l&#39;API completa, vedere il [Riferimento API Swagger](https://www.adobe.io/experience-platform-apis/references/identity-service).

>[!NOTE]
>
>Tutte le identità restituite saranno in formato XID nativo quando nella richiesta viene utilizzato XID nativo. Si consiglia di utilizzare il modulo ID/spazio dei nomi. Per ulteriori informazioni, vedere la sezione relativa al [recupero dell&#39;XID per un&#39;identità](./create-custom-namespace.md).

## Passaggi successivi

Ora che hai raccolto le credenziali richieste, puoi continuare a leggere il resto della guida per sviluppatori. Ogni sezione fornisce informazioni importanti sugli endpoint e illustra esempi di chiamate API per l’esecuzione di operazioni CRUD. Ogni chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e i payload formattati correttamente, e una risposta di esempio per una chiamata di successo.
