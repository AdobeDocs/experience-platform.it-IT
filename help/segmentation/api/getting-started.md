---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida per gli sviluppatori di Segmentation Service
topic: developer guide
translation-type: tm+mt
source-git-commit: aff81a4f3243ef77cbdfc776220a5de46e360084
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# Getting started with [!DNL Segmentation Service] {#getting-started}

 Adobe Experience Platform Segmentation Service consente di creare segmenti e generare audience  Adobe Experience Platform dai [!DNL Real-time Customer Profile] dati.

La guida per gli sviluppatori richiede una conoscenza approfondita dei vari servizi Experience Platform  coinvolti nell&#39;utilizzo [!DNL Segmentation Service].

- [!DNL Segmentation](../home.md): Consente di creare segmenti di pubblico dai dati del profilo cliente in tempo reale.
- [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Framework standard con cui  Experience Platform organizza i dati sull&#39;esperienza dei clienti.
- [!DNL Real-time Customer Profile](../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [Sandbox](../../sandboxes/home.md):  Experience Platform fornisce sandbox virtuali che dividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che dovrete conoscere per poter utilizzare con successo l&#39; [!DNL Segmentation] API.

## Lettura di chiamate API di esempio

La documentazione [!DNL Segmentation Service] API fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere le chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi di  Experience Platform.

## Intestazioni necessarie

La documentazione API richiede inoltre di aver completato l&#39;esercitazione [di](../../tutorials/authentication.md) autenticazione per effettuare correttamente le chiamate agli endpoint Platform. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste nelle chiamate API di  Experience Platform, come illustrato di seguito:

- Autorizzazione: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sull’utilizzo delle sandbox in [!DNL Experience Platform], consultate la documentazione [sulla panoramica delle](../../sandboxes/home.md)sandbox.

## Passaggi successivi

Per effettuare chiamate utilizzando l&#39; [!DNL Segmentation Service] API, selezionate una delle guide endpoint disponibili tramite la navigazione a sinistra o all&#39;interno della panoramica della guida [agli sviluppatori](./overview.md)