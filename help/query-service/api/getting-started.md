---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;query
solution: Experience Platform
title: Guida all’API del servizio query
topic-legacy: query templates
description: L’API Query Service consente agli sviluppatori di eseguire query sui dati Adobe Experience Platform utilizzando SQL standard. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
source-git-commit: 62463e1542d4306c5c769e5690b566a3c30c59cd
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 6%

---

# Guida dell’API di [!DNL Query Service]

Questa guida per gli sviluppatori descrive i passaggi necessari per eseguire varie operazioni in Adobe Experience Platform [!DNL Query Service] API.

## Introduzione

Questa guida richiede una buona comprensione dei vari servizi Adobe Experience Platform che utilizzano [!DNL Query Service].

- [[!DNL Query Service]](../home.md): Consente di eseguire query sui set di dati e acquisire le query risultanti come nuovi set di dati in [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per utilizzare correttamente [!DNL Query Service] utilizzando l’API .

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate in questa documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate a [!DNL Experience Platform] API, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le [!DNL Platform] Chiamate API, come mostrato di seguito:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle operazioni con le sandbox in [!DNL Experience Platform], vedi [documentazione panoramica sulle sandbox](../../sandboxes/home.md).

## Chiamate API di esempio

Ora che capisci quali intestazioni utilizzare, sei pronto per iniziare a effettuare chiamate a [!DNL Query Service] API. Nei documenti seguenti vengono descritte le varie chiamate API che è possibile effettuare utilizzando [!DNL Query Service] API. Ogni chiamata di esempio include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

- [Query](queries.md)
- [Parametri di connessione](connection-parameters.md)
- [Query pianificate](scheduled-queries.md)
- [Viene eseguito per query pianificate](runs-scheduled-queries.md)
- [Modelli di query](query-templates.md)
- [Abbonamenti agli avvisi](./alert-subscriptions.md)

## Passaggi successivi

Ora che hai imparato a fare chiamate utilizzando il [!DNL Query Service] È possibile creare query non interattive personalizzate. Per ulteriori informazioni su come creare le query, leggere il [Guida di riferimento SQL](../sql/overview.md).
