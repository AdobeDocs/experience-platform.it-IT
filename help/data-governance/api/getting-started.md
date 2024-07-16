---
keywords: Experience Platform;home;argomenti popolari;DULE;dule
solution: Experience Platform
title: Guida introduttiva all’API del servizio criteri
description: L’API del servizio criteri consente di creare e gestire varie risorse relative alla governance dei dati di Adobe Experience Platform. Questo documento fornisce un’introduzione ai concetti fondamentali che è necessario conoscere prima di tentare di effettuare chiamate all’API del servizio criteri.
role: Developer
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 8%

---

# Guida introduttiva all&#39;API [!DNL Policy Service]

L&#39;API [!DNL Policy Service] consente di creare e gestire varie risorse relative alla governance dei dati di Adobe Experience Platform. Questo documento fornisce un&#39;introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate all&#39;API [!DNL Policy Service].

## Prerequisiti

L&#39;utilizzo della Guida per gli sviluppatori richiede una buona conoscenza dei vari servizi [!DNL Experience Platform] coinvolti nell&#39;utilizzo delle funzionalità di governance dei dati. Prima di iniziare a utilizzare [!DNL Policy Service API], consulta la documentazione dei seguenti servizi:

* [Governance dei dati](../home.md): framework tramite il quale [!DNL Experience Platform] impone la conformità all&#39;utilizzo dei dati.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

## Lettura delle chiamate API di esempio

La documentazione API [!DNL Policy Service] fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

## Intestazioni richieste

La documentazione API richiede inoltre di aver completato l&#39;[esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente le chiamate agli endpoint [!DNL Platform]. Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste nelle chiamate API [!DNL Experience Platform], come illustrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in [!DNL Experience Platform], incluse quelle appartenenti a Governance dei dati, sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la [documentazione di panoramica sulle sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

* `Content-Type: application/json`

## Risorse core e personalizzate

Nell&#39;API [!DNL Policy Service], tutti i criteri e le azioni di marketing sono denominati `core` o `custom` risorse.

Le risorse `core` sono quelle definite e gestite da Adobe, mentre le risorse `custom` sono quelle create e gestite dalla tua organizzazione e sono quindi univoche e visibili solo alla tua organizzazione. Le operazioni di elenco e ricerca (`GET`) sono pertanto le uniche operazioni consentite nelle risorse `core`, mentre le operazioni di elenco, ricerca e aggiornamento (`POST`, `PUT`, `PATCH` e `DELETE`) sono disponibili per le risorse `custom`.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l’API del servizio criteri, seleziona una delle guide degli endpoint disponibili.
