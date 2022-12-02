---
title: Guida introduttiva all’API della query di audit
description: L’API di query di audit consente di recuperare i dati delle metriche per diverse funzioni di Adobe Experience Platform. Questo documento fornisce un’introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate all’API di query di audit.
source-git-commit: 5b3459711f41430977f9d7b06f8b35801739207c
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 9%

---

# Guida introduttiva all’API della query di audit

Adobe Experience Platform consente di controllare l’attività dell’utente per vari servizi e funzionalità sotto forma di registri degli eventi di controllo. Ogni azione registrata contiene metadati che indicano il tipo di azione, la data e l’ora, l’ID e-mail dell’utente che l’ha eseguita ed eventuali attributi aggiuntivi relativi al tipo di azione.

L’API di query di audit consente di controllare l’attività dell’utente per vari servizi e funzionalità sotto forma di registri eventi di controllo. Questo documento fornisce un’introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate all’API di query di audit.

## Prerequisiti

Per gestire gli eventi di controllo, è necessario disporre delle **[!UICONTROL Visualizza registro attività utente]** autorizzazione al controllo degli accessi concessa (reperibile sotto [!UICONTROL Governance dei dati] categoria). Per informazioni su come gestire le autorizzazioni individuali per le funzionalità di Platform, consulta [documentazione sul controllo degli accessi](../../../../access-control/home.md).

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulla [come leggere le chiamate API di esempio](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

### Raccogli i valori delle intestazioni richieste

Questa guida richiede il completamento della [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente le chiamate alle API di Platform. Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione. Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedi [documentazione panoramica su sandbox](../../../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT e PATCH) richiedono un’intestazione aggiuntiva:

* Tipo di contenuto: application/json

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando [!DNL Audit Query] API, fai riferimento al [guida endpoint eventi](./events.md) e [guida all’endpoint per l’esportazione](./export.md).
