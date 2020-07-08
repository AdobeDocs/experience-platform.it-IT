---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guida introduttiva all'API del profilo cliente in tempo reale
topic: guide
translation-type: tm+mt
source-git-commit: d1656635b6d082ce99f1df4e175d8dd69a63a43a
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---


# Guida introduttiva all&#39;API del profilo cliente in tempo reale {#getting-started}

Utilizzando l&#39;API Profilo cliente in tempo reale, potete eseguire operazioni CRUD di base rispetto alle risorse Profilo, come la configurazione di attributi calcolati, l&#39;accesso alle entità, l&#39;esportazione di dati Profilo ed eliminazione di set di dati o batch non necessari.

L&#39;utilizzo della guida per gli sviluppatori richiede una buona conoscenza dei diversi servizi dei Adobi Experience Platform  coinvolti nell&#39;utilizzo dei dati di Profile. Prima di iniziare a lavorare con l&#39;API del profilo cliente in tempo reale, consulta la documentazione relativa ai seguenti servizi:

* [Profilo](../home.md)cliente in tempo reale: Fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
* [Servizio](../../identity-service/home.md)identità Adobe Experience Platform: Ottieni una visione migliore del tuo cliente e del suo comportamento attraverso il collegamento di identità tra dispositivi e sistemi.
* [servizio](../../segmentation/home.md)di segmentazione Adobe Experience Platform: Consente di creare segmenti di pubblico dai dati del profilo cliente in tempo reale.
* [Experience Data Model (XDM)](../../xdm/home.md): Framework standard con cui Platform organizza i dati sull&#39;esperienza dei clienti.
* [Sandbox](../../sandboxes/home.md):  Experience Platform fornisce sandbox virtuali che dividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente le chiamate agli endpoint API di profilo.

## Lettura di chiamate API di esempio

La documentazione API del profilo cliente in tempo reale fornisce esempi di chiamate API per dimostrare come formattare correttamente le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere le chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi di  Experience Platform.

## Intestazioni necessarie

La documentazione API richiede inoltre di aver completato l&#39;esercitazione [di](../../tutorials/authentication.md) autenticazione per effettuare correttamente le chiamate agli endpoint Platform. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste nelle chiamate API di  Experience Platform, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in  Experience Platform sono isolate in sandbox virtuali specifiche. Le richieste alle API Platform richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Per ulteriori informazioni sulle sandbox in Platform, consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste con un payload nel corpo della richiesta (come le chiamate POST, PUT e PATCH) devono includere un&#39; `Content-Type` intestazione. I valori accettati specifici per ogni chiamata vengono forniti nei parametri delle chiamate.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39;API Profilo cliente in tempo reale, seleziona una delle guide endpoint disponibili.