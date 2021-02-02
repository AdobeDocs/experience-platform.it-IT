---
keywords: ' Experience Platform;home;argomenti popolari;segmentazione;segmentazione;Segmentazione;Segmentation Service;api;'
solution: Experience Platform
title: Guida per gli sviluppatori di Segmentation Service
topic: developer guide
description: La seguente documentazione fornisce informazioni aggiuntive che è necessario conoscere per poter utilizzare correttamente l'API di segmentazione.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# Guida introduttiva a [!DNL Segmentation Service] {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] consente di creare segmenti e generare audience in Adobe Experience Platform dai dati [!DNL Real-time Customer Profile].

La guida per gli sviluppatori richiede una buona conoscenza dei vari servizi [!DNL Experience Platform] coinvolti nell&#39;utilizzo di [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md): Consente di creare segmenti di pubblico dai  [!DNL Real-time Customer Profile] dati.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Il framework standard con cui  [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza dei clienti.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [Sandbox](../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per poter funzionare correttamente con l&#39;API [!DNL Segmentation].

## Lettura di chiamate API di esempio

La documentazione API [!DNL Segmentation Service] fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

## Intestazioni necessarie

La documentazione API richiede inoltre di aver completato l&#39; [esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente le chiamate agli endpoint [!DNL Platform]. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste nelle chiamate API [!DNL Experience Platform], come illustrato di seguito:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui verrà eseguita l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sull&#39;utilizzo delle sandbox in [!DNL Experience Platform], consultate la documentazione sulla panoramica delle [sandbox](../../sandboxes/home.md).

## Passaggi successivi

Per effettuare chiamate utilizzando l&#39;API [!DNL Segmentation Service], seleziona una delle guide endpoint disponibili tramite la navigazione a sinistra o all&#39;interno della [panoramica della guida per gli sviluppatori](./overview.md)