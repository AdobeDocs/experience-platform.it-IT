---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida introduttiva all'API di Policy Service
topic: developer guide
translation-type: tm+mt
source-git-commit: cb3a17aa08c67c66101cbf3842bf306ebcca0305
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---


# Guida introduttiva all&#39; [!DNL Policy Service] API

L&#39; [!DNL Policy Service] API consente di creare e gestire diverse risorse correlate ad Adobe Experience Platform [!DNL Data Governance]. Questo documento fornisce un&#39;introduzione ai concetti di base da conoscere prima di tentare di effettuare chiamate all&#39; [!DNL Policy Service] API.

## Prerequisiti

L&#39;utilizzo della guida per gli sviluppatori richiede una buona conoscenza dei vari [!DNL Experience Platform] servizi coinvolti nell&#39;utilizzo delle funzionalità di governance dei dati. Prima di iniziare a lavorare con [!DNL Policy Service API], consulta la documentazione relativa ai seguenti servizi:

* [[!DNL Data Governance]](../home.md): Il framework in base al quale [!DNL Experience Platform] viene applicata la conformità all&#39;utilizzo dei dati.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
* [[!DNL Profilo cliente in tempo reale]](../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

## Lettura di chiamate API di esempio

La documentazione [!DNL Policy Service] API fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

## Intestazioni necessarie

La documentazione API richiede inoltre di aver completato l&#39;esercitazione [di](../../tutorials/authentication.md) autenticazione per effettuare correttamente le chiamate agli [!DNL Platform] endpoint. Completando l&#39;esercitazione sull&#39;autenticazione vengono forniti i valori per ciascuna delle intestazioni richieste nelle chiamate [!DNL Experience Platform] API, come illustrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti a [!DNL Data Governance], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

* `Content-Type: application/json`

## Risorse Core e personalizzate

All&#39;interno dell&#39; [!DNL Policy Service] API, tutti i criteri e le azioni di marketing sono denominati o `core` `custom` risorse.

`core` le risorse sono quelle definite e gestite  Adobe, mentre `custom` le risorse sono quelle create e mantenute dalla vostra organizzazione e sono pertanto uniche e visibili esclusivamente alla vostra organizzazione IMS. Di conseguenza, le operazioni di elenco e ricerca (`GET`) sono le uniche operazioni consentite sulle `core` risorse, mentre le operazioni di elenco, ricerca e aggiornamento (`POST`, `PUT`, `PATCH`e `DELETE`) sono disponibili per `custom` le risorse.

## Passaggi successivi

Per iniziare a effettuare chiamate tramite l&#39;API di Policy Service, selezionate una delle guide endpoint disponibili.