---
keywords: Experience Platform;home;argomenti popolari;api del servizio identità;guida per gli sviluppatori del servizio identità;area geografica
solution: Experience Platform
title: Guida all’API del servizio Identity
description: L’API del servizio Identity consente agli sviluppatori di gestire l’identificazione dei clienti tra dispositivi, tra canali e in tempo quasi reale utilizzando grafici di identità in Adobe Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
source-git-commit: ad9fb0bcc7bca55da432c72adc94d49e3c63ad6e
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 3%

---

# Guida dell’API di [!DNL Identity Service]

Adobe Experience Platform [!DNL Identity Service] gestisce l’identificazione dei clienti in tempo reale su dispositivi, canali diversi e quasi in tempo reale in quello che è noto come grafico di identità in Adobe Experience Platform.

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Identity Service]](../home.md): Risolve la sfida fondamentale rappresentata dalla frammentazione dei dati del profilo cliente. Lo fa collegando le identità tra dispositivi e sistemi in cui i clienti interagiscono con il tuo marchio.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fornisce un profilo consumatore unificato in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il quadro standardizzato [!DNL Platform] organizza i dati sulla customer experience.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere o disporre di disponibilità per effettuare correttamente le chiamate al [!DNL Identity Service] API.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate a [!DNL Platform] API, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedi [documentazione panoramica su sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Tipo di contenuto: application/json

### Routing basato su regione

La [!DNL Identity Service] L’API utilizza endpoint specifici per l’area geografica che richiedono l’inclusione di un `{REGION}` come parte del percorso della richiesta. Durante il provisioning della tua organizzazione IMS, una regione viene determinata e memorizzata all’interno del profilo dell’organizzazione IMS. L’utilizzo della regione corretta con ogni endpoint assicura che tutte le richieste effettuate utilizzando [!DNL Identity Service] Le API vengono indirizzate all’area appropriata.

Sono attualmente supportate due regioni [!DNL Identity Service] API: VA7 e NLD2.

La tabella seguente mostra alcuni percorsi di esempio che utilizzano aree geografiche:

| Servizio | Regione: VA7 | Regione: NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>Le richieste effettuate senza specificare una regione possono causare l’instradamento delle chiamate all’area errata o un errore imprevisto delle chiamate.

Se non riesci a individuare l’area geografica all’interno del profilo dell’organizzazione IMS, contatta l’amministratore di sistema per richiedere supporto.

## Utilizzo della [!DNL Identity Service] API

I parametri di identità utilizzati in questi servizi possono essere espressi in uno dei due modi seguenti: composito o XID.

Le identità composite sono costrutti che includono sia il valore ID che lo spazio dei nomi. Quando si utilizzano identità composite, lo spazio dei nomi può essere fornito con uno dei due nomi (`namespace.code`) o ID (`namespace.id`).

Quando un&#39;identità è persistente, [!DNL Identity Service] genera e assegna un ID a tale identità, denominato ID nativo o XID. Tutte le varianti delle API Cluster e Mapping supportano sia le identità composite che XID nelle loro richieste e risposte. Uno dei parametri è obbligatorio - `xid` o combinazione di [`ns` o `nsid`] e `id` per utilizzare queste API.

Per limitare il payload nelle risposte, le API adattano le risposte al tipo di costrutto di identità utilizzato. Cioè, se passi XID le tue risposte avranno XID, se passi le identità composite, la risposta seguirà la struttura utilizzata nella richiesta.

Gli esempi contenuti in questo documento non coprono la funzionalità completa del [!DNL Identity Service] API. Per l’API completa, consulta la sezione [Riferimento API Swagger](https://www.adobe.io/experience-platform-apis/references/identity-service).

>[!NOTE]
>
>Tutte le identità restituite saranno in formato XID nativo quando nella richiesta viene utilizzato XID nativo. Si consiglia di utilizzare il modulo ID/namespace. Per ulteriori informazioni, consulta la sezione su [ottenimento di un XID per un&#39;identità](./create-custom-namespace.md).

## Passaggi successivi

Dopo aver raccolto le credenziali richieste, puoi continuare a leggere il resto della guida per gli sviluppatori. Ogni sezione fornisce informazioni importanti sui loro endpoint e illustra chiamate API di esempio per l’esecuzione di operazioni CRUD. Ciascuna chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e i payload formattati correttamente e una risposta di esempio per una chiamata riuscita.
