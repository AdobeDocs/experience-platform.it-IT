---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;query
solution: Experience Platform
title: Guida all’API del servizio query
topic-legacy: query templates
description: L’API Query Service consente agli sviluppatori di eseguire query sui dati Adobe Experience Platform utilizzando SQL standard. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 1%

---

# [!DNL Query Service] Guida all’API

Questa guida per gli sviluppatori descrive i passaggi necessari per eseguire varie operazioni nell’ API Adobe Experience Platform [!DNL Query Service] .

## Introduzione

Questa guida richiede una buona comprensione dei vari servizi Adobe Experience Platform coinvolti nell&#39;utilizzo di [!DNL Query Service].

- [[!DNL Query Service]](../home.md): Consente di eseguire query sui set di dati e acquisire le query risultanti come nuovi set di dati in  [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
- [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per utilizzare correttamente [!DNL Query Service] utilizzando l&#39;API.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate in questa documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API [!DNL Experience Platform], devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Platform], come mostrato di seguito:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- nome x-sandbox: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle operazioni con le sandbox in [!DNL Experience Platform], consulta la documentazione di panoramica [sandbox](../../sandboxes/home.md).

## Chiamate API di esempio

Ora che conosci le intestazioni da utilizzare, sei pronto per iniziare a effettuare chiamate all’ API [!DNL Query Service]. Nei documenti seguenti vengono descritte le varie chiamate API che puoi effettuare tramite l’ API [!DNL Query Service] . Ogni chiamata di esempio include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

- [Query](queries.md)
- [Parametri di connessione](connection-parameters.md)
- [Query pianificate](scheduled-queries.md)
- [Viene eseguito per query pianificate](runs-scheduled-queries.md)
- [Modelli di query](query-templates.md)

## Passaggi successivi

Ora che hai imparato a effettuare chiamate utilizzando l’ API [!DNL Query Service] , puoi creare query non interattive personalizzate. Per ulteriori informazioni su come creare le query, leggere la [Guida di riferimento SQL](../sql/overview.md).
