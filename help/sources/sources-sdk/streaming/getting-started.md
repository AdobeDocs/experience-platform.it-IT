---
title: Guida introduttiva alle origini self-service (Streaming SDK)
description: Questo documento fornisce un’introduzione alle informazioni sui prerequisiti da conoscere prima di tentare di creare una nuova origine utilizzando Origini self-service (Streaming SDK).
exl-id: 6cc13279-ce0b-45bc-ad25-e2e6aafc2af0
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 12%

---

# Guida introduttiva alle origini self-service (Streaming SDK)

>[!NOTE]
>
>L’SDK di streaming per origini self-service è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, leggere la [panoramica delle origini](../../home.md#terms-and-conditions).

Origini self-service (Streaming SDK) consente di integrare la propria origine per portare i dati in streaming a Adobe Experience Platform. Questo documento fornisce un&#39;introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate all&#39;[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Processo di alto livello

Di seguito è descritta la procedura dettagliata per configurare l’origine in Experience Platform:

### Integrazione

* [Crea una nuova specifica di connessione per Streaming SDK](create.md).
* [Aggiorna la specifica del flusso di streaming con il nuovo ID della specifica di connessione](update-flow-specs.md).
* [Verifica e invia l&#39;origine di streaming](submit.md).

### Documentazione

* Per iniziare a documentare l&#39;origine, leggere la [panoramica sulla creazione della documentazione per le origini self-service](../documentation/doc-overview.md).
* Per i passaggi su come creare la documentazione utilizzando GitHub, leggi la guida su [utilizzo dell&#39;interfaccia Web GitHub](../documentation/github.md).
* Leggi la guida su [utilizzo di un editor di testo](../documentation/text-editor.md) per i passaggi su come creare documentazione utilizzando il computer locale.
* [Utilizzare il modello di documentazione API Streaming SDK per documentare l&#39;origine nell&#39;API](streaming-template-api.md).
* [Utilizza il modello di documentazione dell&#39;interfaccia utente Streaming SDK per documentare la tua origine nell&#39;interfaccia utente](streaming-template-ui.md).

Puoi scaricare i modelli di documentazione riportati di seguito:

* [Modello di documentazione API](../assets/streaming/streaming-template-api.zip)
* [Modello di documentazione per l’interfaccia utente](../assets/streaming/streaming-template-ui.zip)

## Prerequisiti

>[!IMPORTANT]
>
>L’origine che stai integrando con Experience Platform deve essere in grado di supportare un webhook a cui un endpoint può essere abbonato per inviare aggiornamenti.

Per utilizzare Origini self-service (Streaming SDK), è necessario assicurarsi di avere accesso a un’organizzazione sandbox con provisioning di Origini Adobe Experience Platform.

Questa guida richiede anche una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

## Lettura delle chiamate API di esempio

Nella documentazione di Self-Server Sources (Streaming SDK) e API [!DNL Flow Service] sono incluse alcune chiamate API esemplificative che illustrano come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

## Raccogliere i valori per le intestazioni richieste

Per effettuare chiamate alle API di Platform, devi prima completare l&#39;[esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Completando il tutorial sull’autenticazione si ottengono i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di [!DNL Experience Platform], come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in Platform, incluse quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API di Platform richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Platform, consulta la [documentazione sulle sandbox](../../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

* `Content-Type: application/json`

## Passaggi successivi

Per iniziare a creare una nuova origine con Origini self-service (SDK di streaming), consulta l&#39;esercitazione sulla [creazione di una nuova origine](./create.md).
