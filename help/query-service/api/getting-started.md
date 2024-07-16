---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;query;home;popular topic;query service;Query service;query service;query service;query
solution: Experience Platform
title: Guida API di Query Service
description: L’API Query Service consente agli sviluppatori di eseguire query sui dati Adobe Experience Platform utilizzando SQL standard. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
role: Developer
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 20%

---

# Guida dell’API di [!DNL Query Service]

Questa guida per gli sviluppatori descrive i passaggi necessari per eseguire varie operazioni nell&#39;API di Adobe Experience Platform [!DNL Query Service].

## Introduzione

Questa guida richiede una buona conoscenza dei vari servizi Adobe Experience Platform coinvolti nell&#39;utilizzo di [!DNL Query Service].

- [[!DNL Query Service]](../home.md): consente di eseguire query sui set di dati e di acquisire le query risultanti come nuovi set di dati in [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per utilizzare correttamente [!DNL Query Service] utilizzando l&#39;API.

### Lettura delle chiamate API di esempio

Questa guida fornisce esempi di chiamate API per illustrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate in questa documentazione per le chiamate API di esempio, consulta la sezione su [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogliere i valori per le intestazioni richieste

Per effettuare chiamate alle API [!DNL Experience Platform], devi prima completare l&#39;[esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Completando il tutorial sull’autenticazione si ottengono i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di [!DNL Platform], come mostrato di seguito:

- Autorizzazione: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in specifiche sandbox virtuali. Tutte le richieste alle API [!DNL Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sull&#39;utilizzo delle sandbox in [!DNL Experience Platform], consulta la [documentazione panoramica sulle sandbox](../../sandboxes/home.md).

## Chiamate API di esempio

Ora che sai quali intestazioni utilizzare, puoi iniziare ad effettuare chiamate all&#39;API [!DNL Query Service]. I documenti seguenti descrivono le varie chiamate API che è possibile effettuare utilizzando l&#39;API [!DNL Query Service]. Ogni chiamata di esempio include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

- [Query](queries.md)
- [Parametri di connessione](connection-parameters.md)
- [Query pianificate](scheduled-queries.md)
- [Viene eseguito per le query pianificate](runs-scheduled-queries.md)
- [Modelli di query](query-templates.md)
- [Query accelerate](./accelerated-queries.md)
- [Sottoscrizioni avvisi](./alert-subscriptions.md)

## Passaggi successivi

Dopo aver appreso come effettuare chiamate utilizzando l&#39;API [!DNL Query Service], puoi creare query non interattive personalizzate. Per ulteriori informazioni su come creare query, leggere la [Guida di riferimento SQL](../sql/overview.md).
