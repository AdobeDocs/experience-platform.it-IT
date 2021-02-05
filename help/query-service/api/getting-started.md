---
keywords: ' Experience Platform;home;argomenti popolari;servizio query;servizio query;query'
solution: Experience Platform
title: Guida API del servizio query
topic: query templates
description: L'API di Query Service consente agli sviluppatori di eseguire query sui dati Adobe Experience Platform utilizzando SQL standard. Seguite questa guida per apprendere come eseguire operazioni chiave tramite l'API.
translation-type: tm+mt
source-git-commit: e649ab3da077cdd8e98562199b8bdece6108a572
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 1%

---


# [!DNL Query Service] Guida API

Questa guida per gli sviluppatori fornisce i passaggi necessari per eseguire varie operazioni nell&#39;API Adobe Experience Platform [!DNL Query Service].

## Introduzione

Questa guida richiede una buona conoscenza dei diversi servizi Adobe Experience Platform coinvolti nell&#39;utilizzo di [!DNL Query Service].

- [[!DNL Query Service]](../home.md): Consente di eseguire query sui set di dati e acquisire le query risultanti come nuovi set di dati in  [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Il framework standard con cui  [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza dei clienti.
- [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per utilizzare correttamente [!DNL Query Service] utilizzando l&#39;API.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate in questa documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Experience Platform] API, è innanzitutto necessario completare l&#39;esercitazione sull&#39;autenticazione [a2/>. ](https://www.adobe.com/go/platform-api-authentication-en) Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Platform], come illustrato di seguito:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui verrà eseguita l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sull&#39;utilizzo delle sandbox in [!DNL Experience Platform], consultate la documentazione sulla panoramica delle [sandbox](../../sandboxes/home.md).

## Chiamate API di esempio

Ora che hai compreso quali intestazioni utilizzare, sei pronto a iniziare a effettuare chiamate all&#39;API [!DNL Query Service]. I documenti seguenti descrivono le varie chiamate API che potete effettuare tramite l&#39;API [!DNL Query Service]. Ogni chiamata di esempio include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

- [Query](queries.md)
- [Parametri di connessione](connection-parameters.md)
- [Query pianificate](scheduled-queries.md)
- [Esecuzione per query pianificate](runs-scheduled-queries.md)
- [Modelli di query](query-templates.md)

## Passaggi successivi

Ora che hai imparato a effettuare chiamate utilizzando l&#39;API [!DNL Query Service], puoi creare query non interattive personalizzate. Per ulteriori informazioni sulla creazione di query, consultare la [Guida di riferimento SQL](../sql/overview.md).