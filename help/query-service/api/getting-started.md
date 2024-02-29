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

Questa guida per sviluppatori descrive i passaggi da seguire per eseguire varie operazioni in Adobe Experience Platform [!DNL Query Service] API.

## Introduzione

Questa guida richiede una buona conoscenza dei vari servizi Adobe Experience Platform coinvolti nell’utilizzo di [!DNL Query Service].

- [[!DNL Query Service]](../home.md): consente di eseguire query sui set di dati e di acquisire le query risultanti come nuovi set di dati in [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per utilizzare correttamente [!DNL Query Service] utilizzando l’API.

### Lettura delle chiamate API di esempio

Questa guida fornisce esempi di chiamate API per illustrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate in questa documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nel [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogliere i valori per le intestazioni richieste

Per effettuare chiamate a [!DNL Experience Platform] , devi prima completare le [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Completando il tutorial sull’autenticazione si ottengono i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di [!DNL Platform], come mostrato di seguito:

- Autorizzazione `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolati in specifiche sandbox virtuali. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sull’utilizzo delle sandbox in [!DNL Experience Platform], vedere [documentazione panoramica sulle sandbox](../../sandboxes/home.md).

## Chiamate API di esempio

Ora che sai quali intestazioni utilizzare, puoi iniziare a effettuare chiamate al [!DNL Query Service] API. I seguenti documenti descrivono le varie chiamate API che puoi effettuare utilizzando [!DNL Query Service] API. Ogni chiamata di esempio include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

- [Query](queries.md)
- [Parametri di connessione](connection-parameters.md)
- [Query pianificate](scheduled-queries.md)
- [Viene eseguito per le query pianificate](runs-scheduled-queries.md)
- [Modelli di query](query-templates.md)
- [Query accelerate](./accelerated-queries.md)
- [Sottoscrizioni avvisi](./alert-subscriptions.md)

## Passaggi successivi

Ora che hai imparato a effettuare chiamate utilizzando [!DNL Query Service] API, puoi creare query non interattive personalizzate. Per ulteriori informazioni su come creare le query, leggere [Guida di riferimento SQL](../sql/overview.md).
