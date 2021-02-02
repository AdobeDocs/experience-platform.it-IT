---
keywords: ' Experience Platform;home;argomenti popolari;DULE;module'
solution: Experience Platform
title: Guida introduttiva all'API di Policy Service
topic: developer guide
description: L'API Policy Service consente di creare e gestire varie risorse correlate alla governance dei dati di Adobe Experience Platform. Questo documento fornisce un'introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate all'API del servizio criteri.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---


# Guida introduttiva all&#39;API [!DNL Policy Service]

L&#39;API [!DNL Policy Service] consente di creare e gestire varie risorse correlate ad Adobe Experience Platform [!DNL Data Governance]. Questo documento fornisce un&#39;introduzione ai concetti di base da conoscere prima di tentare di effettuare chiamate all&#39;API [!DNL Policy Service].

## Prerequisiti

L&#39;utilizzo della guida per gli sviluppatori richiede una buona conoscenza dei vari servizi [!DNL Experience Platform] coinvolti nell&#39;utilizzo delle funzionalità di governance dei dati. Prima di iniziare a lavorare con [!DNL Policy Service API], consulta la documentazione relativa ai seguenti servizi:

* [[!DNL Data Governance]](../home.md): Il framework in base al quale  [!DNL Experience Platform] viene applicata la conformità all&#39;utilizzo dei dati.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Il framework standard con cui  [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza dei clienti.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

## Lettura di chiamate API di esempio

La documentazione API [!DNL Policy Service] fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

## Intestazioni necessarie

La documentazione API richiede inoltre di aver completato l&#39; [esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente le chiamate agli endpoint [!DNL Platform]. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste nelle chiamate API [!DNL Experience Platform], come illustrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], incluse quelle appartenenti a [!DNL Data Governance], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui verrà eseguita l&#39;operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione di [panoramica sulla sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

* `Content-Type: application/json`

## Risorse Core e personalizzate

All&#39;interno dell&#39;API [!DNL Policy Service], tutti i criteri e le azioni di marketing sono denominati risorse `core` o `custom`.

`core` le risorse sono quelle definite e gestite  Adobe, mentre  `custom` le risorse sono quelle create e mantenute dalla vostra organizzazione e sono pertanto uniche e visibili esclusivamente alla vostra organizzazione IMS. Di conseguenza, le operazioni di elenco e ricerca (`GET`) sono le uniche operazioni consentite sulle risorse `core`, mentre le operazioni di elencazione, ricerca e aggiornamento (`POST`, `PUT`, `PATCH` e `DELETE`) sono disponibili per le risorse `custom`.

## Passaggi successivi

Per iniziare a effettuare chiamate tramite l&#39;API di Policy Service, selezionate una delle guide endpoint disponibili.