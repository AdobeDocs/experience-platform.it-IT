---
title: Guida introduttiva alle sorgenti self-service (SDK per streaming)
description: Questo documento fornisce un’introduzione alle informazioni sui prerequisiti da conoscere prima di tentare di creare una nuova origine utilizzando Origini self-service (Streaming SDK).
hide: true
hidefromtoc: true
source-git-commit: 7744fef9751212a40f8f20df52812d38130c42fc
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Guida introduttiva alle sorgenti self-service (SDK per streaming)

Origini self-service (Streaming SDK) consente di integrare la propria origine per trasferire i dati in streaming a Adobe Experience Platform. Questo documento fornisce un&#39;introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate al [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Processo di alto livello

Il processo dettagliato per configurare l’origine in Experience Platform è descritto di seguito:

### Integrazione

* [Crea una nuova specifica di connessione per SDK Streaming](create.md).
* [Aggiorna la specifica del flusso di flusso con il nuovo ID della specifica di connessione](update-flow-specs.md).
* [Verifica e invia la tua origine streaming](submit.md).

### Documentazione

* Per iniziare a documentare la tua origine, leggi la sezione [panoramica sulla creazione della documentazione per Origini self-service](../documentation/doc-overview.md).
* Leggi la guida su [utilizzo dell’interfaccia web GitHub](../documentation/github.md) per informazioni su come creare la documentazione utilizzando GitHub.
* Leggi la guida su [utilizzo di un editor di testo](../documentation/text-editor.md) per informazioni su come creare la documentazione utilizzando il computer locale.
* [Utilizza il modello di documentazione dell’API SDK per streaming per documentare la tua origine nell’API](streaming-template-api.md).
* [Utilizza il modello di documentazione dell’interfaccia utente SDK per streaming per documentare la tua origine nell’interfaccia utente](streaming-template-ui.md).

Puoi anche scaricare i modelli di documentazione seguenti:

* [Modello di documentazione API](../assets/streaming/streaming-template-api.zip)
* [Modello di documentazione dell’interfaccia utente](../assets/streaming/streaming-template-ui.zip)

## Prerequisiti

>[!IMPORTANT]
>
>Per inviare gli aggiornamenti, l’origine che si sta integrando con Experience Platform deve essere in grado di supportare un webhook a cui è possibile effettuare la sottoscrizione di un endpoint.

Per utilizzare Origini self-service (Streaming SDK), devi assicurarti di avere accesso a un&#39;organizzazione sandbox con provisioning di Adobe Experience Platform Sources.

Questa guida richiede anche una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Sandbox](../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

## Lettura di chiamate API di esempio

Origini self-service (Streaming SDK) e [!DNL Flow Service] La documentazione API fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

## Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API di Platform, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in Platform, comprese quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API di Platform richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Platform, consulta la sezione [documentazione sandbox](../../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

* `Content-Type: application/json`

## Passaggi successivi

Per iniziare a creare una nuova origine con Origini self-service (Streaming SDK), consulta l’esercitazione su [creazione di una nuova origine](./create.md).
