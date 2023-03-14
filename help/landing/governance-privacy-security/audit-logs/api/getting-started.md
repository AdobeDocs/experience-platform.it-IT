---
title: Guida introduttiva all’API di query di audit
description: L’API Query di audit consente di recuperare i dati delle metriche per varie funzioni di Adobe Experience Platform. Questo documento fornisce un’introduzione ai concetti fondamentali che è necessario conoscere prima di tentare di effettuare chiamate all’API Query di audit.
exl-id: 20eab0a8-98f7-4fee-8f91-88324e54ab18
source-git-commit: c2c5778e0a3fff7f488ad7a672123c813cca59f1
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 9%

---

# Guida introduttiva all’API di query di audit

Adobe Experience Platform consente di controllare l’attività dell’utente per vari servizi e funzionalità sotto forma di registri di eventi di audit. Ogni azione registrata contiene metadati che indicano il tipo di azione, la data e l’ora, l’ID e-mail dell’utente che l’ha eseguita ed eventuali attributi aggiuntivi relativi al tipo di azione.

L’API Audit Query consente di controllare l’attività dell’utente per vari servizi e funzionalità sotto forma di registri eventi di audit. Questo documento fornisce un’introduzione ai concetti fondamentali che è necessario conoscere prima di tentare di effettuare chiamate all’API Query di audit.

## Prerequisiti

Per gestire gli eventi di audit, è necessario disporre del **[!UICONTROL Visualizza registro attività utente]** autorizzazione di controllo dell’accesso concessa (disponibile nella sezione [!UICONTROL Governance dei dati] categoria). Per informazioni su come gestire le singole autorizzazioni per le funzionalità di Platform, consulta [documentazione sul controllo degli accessi](../../../../access-control/home.md).

### Lettura delle chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito il codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

### Raccogli i valori per le intestazioni richieste

Questa guida richiede di aver completato [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente chiamate alle API di Platform. Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

* Autorizzazione: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolati in specifiche sandbox virtuali. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione. Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedere [documentazione di panoramica sulla sandbox](../../../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT e PATCH) richiedono un’intestazione aggiuntiva:

* Content-Type: application/json

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando [!DNL Audit Query] API, fare riferimento al [guida dell’endpoint &quot;events&quot;](./events.md) e [guida dell’endpoint di esportazione](./export.md).
