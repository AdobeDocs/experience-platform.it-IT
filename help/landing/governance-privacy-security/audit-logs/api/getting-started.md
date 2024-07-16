---
title: Guida introduttiva all’API di query di audit
description: L’API Query di audit consente di recuperare i dati delle metriche per varie funzioni di Adobe Experience Platform. Questo documento fornisce un’introduzione ai concetti fondamentali che è necessario conoscere prima di tentare di effettuare chiamate all’API Query di audit.
exl-id: 20eab0a8-98f7-4fee-8f91-88324e54ab18
source-git-commit: c2c5778e0a3fff7f488ad7a672123c813cca59f1
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 11%

---

# Guida introduttiva all’API di query di audit

Adobe Experience Platform consente di controllare l’attività dell’utente per vari servizi e funzionalità sotto forma di registri di eventi di audit. Ogni azione registrata contiene metadati che indicano il tipo di azione, la data e l’ora, l’ID e-mail dell’utente che l’ha eseguita e altri attributi relativi al tipo di azione.

L’API Audit Query consente di controllare l’attività dell’utente per vari servizi e funzionalità sotto forma di registri eventi di audit. Questo documento fornisce un’introduzione ai concetti fondamentali che è necessario conoscere prima di tentare di effettuare chiamate all’API Query di audit.

## Prerequisiti

Per gestire gli eventi di controllo, è necessario disporre dell&#39;autorizzazione di controllo dell&#39;accesso **[!UICONTROL Visualizza log attività utente]** concessa (nella categoria [!UICONTROL Governance dei dati]). Per informazioni su come gestire le singole autorizzazioni per le funzionalità di Platform, consulta la [documentazione sul controllo degli accessi](../../../../access-control/home.md).

### Lettura delle chiamate API di esempio

Questa guida fornisce esempi di chiamate API per illustrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

### Raccogliere i valori per le intestazioni richieste

Questa guida richiede di aver completato l&#39;[esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per poter effettuare correttamente le chiamate alle API di Platform. Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

* Autorizzazione: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in specifiche sandbox virtuali. Tutte le richieste alle API [!DNL Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione. Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la [documentazione di panoramica sulle sandbox](../../../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT e PATCH) richiedono un’intestazione aggiuntiva:

* Content-Type: application/json

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39;API [!DNL Audit Query], consulta la [guida dell&#39;endpoint eventi](./events.md) e la [guida dell&#39;endpoint esportazione](./export.md).
