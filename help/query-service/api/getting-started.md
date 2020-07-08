---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida per gli sviluppatori di Query Service
topic: query templates
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 1%

---


# Guida per gli sviluppatori di Query Service

Questa guida per gli sviluppatori fornisce i passaggi necessari per eseguire varie operazioni nell&#39;API  Adobe Experience Platform Query Service.

## Introduzione

Questa guida richiede una conoscenza approfondita dei diversi servizi di Adobe Experience Platform  coinvolti nell&#39;utilizzo di Query Service.

- [Servizio](../home.md)query: Consente di eseguire query sui set di dati e acquisire le query risultanti come nuovi set di dati in  Experience Platform.
- [Sistema](../../xdm/home.md)XDM (Experience Data Model): Framework standard con cui  Experience Platform organizza i dati sull&#39;esperienza dei clienti.
- [Sandbox](../../sandboxes/home.md):  Experience Platform fornisce sandbox virtuali che dividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per poter utilizzare correttamente Query Service tramite l&#39;API.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate in questa documentazione per le chiamate API di esempio, vedete la sezione [come leggere le chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi di  Experience Platform.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate  API Experience Platform, è prima necessario completare l&#39;esercitazione [di](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API Platform, come illustrato di seguito:

- Autorizzazione: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in  Experience Platform sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API Platform richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sull’utilizzo delle sandbox in  Experience Platform, consultate la documentazione [sulla panoramica delle](../../sandboxes/home.md)sandbox.

## Chiamate API di esempio

Ora che hai compreso le intestazioni da utilizzare, sei pronto a iniziare a effettuare chiamate all&#39;API di Servizio query. I documenti seguenti descrivono le varie chiamate API che potete effettuare tramite l&#39;API di Query Service. Ogni chiamata di esempio include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

- [Query](queries.md)
- [Parametri di connessione](connection-parameters.md)
- [Query pianificate](scheduled-queries.md)
- [Esecuzione per query pianificate](runs-scheduled-queries.md)
- [Modelli di query](query-templates.md)

## Passaggi successivi

Ora che hai imparato a effettuare chiamate utilizzando l&#39;API di Query Service, puoi creare query non interattive personalizzate. Per ulteriori informazioni sulla creazione di query, consultate la guida [di riferimento](../sql/overview.md)SQL.