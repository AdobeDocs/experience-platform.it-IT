---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Guida introduttiva all’API di acquisizione dati
type: Documentation
description: La guida introduttiva all’API di acquisizione dati descrive i concetti chiave e le funzionalità di base necessari per iniziare a acquisire dati in Experience Platform tramite API.
exl-id: 0653de2b-3268-478b-a23f-c458b6d3df7c
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 6%

---

# Guida introduttiva all’API di acquisizione dati {#getting-started}

Utilizzando gli endpoint API per l’acquisizione dei dati, puoi eseguire operazioni CRUD di base per acquisire i dati in Adobe Experience Platform.

L’utilizzo delle guide API richiede una buona conoscenza di diversi servizi Adobe Experience Platform coinvolti nell’utilizzo dei dati. Prima di utilizzare l’API di acquisizione dati, consulta la documentazione dei seguenti servizi:

* [Acquisizione batch](./overview.md): consente di acquisire dati in Adobe Experience Platform come file batch.
* [[!DNL Real-Time Customer Profile]](../home.md): fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): framework standardizzato in base al quale Platform organizza i dati sull’esperienza del cliente.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per effettuare correttamente chiamate agli endpoint API [!DNL Profile].

## Lettura delle chiamate API di esempio

La documentazione API di acquisizione dati fornisce esempi di chiamate API per dimostrare come formattare correttamente le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

## Intestazioni richieste

La documentazione API richiede inoltre di aver completato l&#39;[esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente le chiamate agli endpoint [!DNL Platform]. Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste nelle chiamate API [!DNL Experience Platform], come illustrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le richieste con un payload nel corpo della richiesta (ad esempio chiamate POST, PUT e PATCH) devono includere un&#39;intestazione `Content-Type`. I valori accettati specifici di ogni chiamata sono forniti nei parametri della chiamata.

Tutte le risorse in [!DNL Experience Platform] sono isolate in specifiche sandbox virtuali. Le richieste alle API [!DNL Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la [documentazione di panoramica sulle sandbox](../../sandboxes/home.md).
