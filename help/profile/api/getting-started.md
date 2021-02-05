---
keywords: Experience Platform ;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Guida introduttiva all'API del profilo cliente in tempo reale
topic: guide
type: Documentation
description: La guida introduttiva all'API profilo descrive i concetti chiave e le funzionalità di base che è necessario conoscere per utilizzare gli endpoint API Profilo cliente in tempo reale per eseguire operazioni CRUD di base rispetto ai dati del profilo.
translation-type: tm+mt
source-git-commit: cad9c690be986961aea2969ef0ade975f33a8ee5
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# Guida introduttiva all&#39;API [!DNL Real-time Customer Profile] {#getting-started}

Utilizzando gli endpoint API del profilo cliente in tempo reale, potete eseguire operazioni CRUD di base rispetto ai dati del profilo, come la configurazione di attributi calcolati, l&#39;accesso alle entità, l&#39;esportazione di dati del profilo ed eliminazione di set di dati o batch non necessari.

L&#39;utilizzo della guida per gli sviluppatori richiede una buona conoscenza dei diversi servizi Adobe Experience Platform coinvolti nell&#39;utilizzo dei dati [!DNL Profile]. Prima di iniziare a lavorare con l&#39;API [!DNL Real-time Customer Profile], consulta la documentazione relativa ai seguenti servizi:

* [[!DNL Real-time Customer Profile]](../home.md): Fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Ottieni una visione migliore del tuo cliente e del suo comportamento attraverso il collegamento di identità tra dispositivi e sistemi.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): Consente di creare segmenti di pubblico dai dati del profilo cliente in tempo reale.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standardizzato tramite il quale la piattaforma organizza i dati sull&#39;esperienza cliente.
* [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per eseguire correttamente le chiamate agli endpoint [!DNL Profile] API.

## Lettura di chiamate API di esempio

La documentazione API [!DNL Real-time Customer Profile] fornisce esempi di chiamate API per dimostrare come formattare correttamente le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

## Intestazioni necessarie

La documentazione API richiede inoltre di aver completato l&#39; [esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente le chiamate agli endpoint [!DNL Platform]. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste nelle chiamate API [!DNL Experience Platform], come illustrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui verrà eseguita l&#39;operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione di [panoramica sulla sandbox](../../sandboxes/home.md).

Tutte le richieste con un payload nel corpo della richiesta (come le chiamate POST, PUT e PATCH) devono includere un&#39;intestazione `Content-Type`. I valori accettati specifici per ogni chiamata vengono forniti nei parametri delle chiamate.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39;API [!DNL Real-time Customer Profile], seleziona una delle guide endpoint disponibili.