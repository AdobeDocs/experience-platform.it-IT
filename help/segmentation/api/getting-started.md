---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida per gli sviluppatori di Segmentation Service
topic: developer guide
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---


# Getting started with [!DNL Segmentation Service] {#getting-started}

 Adobe Experience Platform [!DNL Segmentation Service] consente di creare segmenti e generare audience  Adobe Experience Platform dai [!DNL Real-time Customer Profile] dati.

La guida per gli sviluppatori richiede una conoscenza approfondita dei vari [!DNL Experience Platform] servizi che intervengono nell&#39;utilizzo [!DNL Segmentation Service].

- [!DNL Segmentation](../home.md): Consente di creare segmenti di pubblico dai [!DNL Real-time Customer Profile] dati.
- [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
- [!DNL Real-time Customer Profile](../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che dovrete conoscere per poter utilizzare con successo l&#39; [!DNL Segmentation] API.

## Lettura di chiamate API di esempio

La documentazione [!DNL Segmentation Service] API fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

## Intestazioni necessarie

La documentazione API richiede inoltre di aver completato l&#39;esercitazione [di](../../tutorials/authentication.md) autenticazione per effettuare correttamente le chiamate agli [!DNL Platform] endpoint. Completando l&#39;esercitazione sull&#39;autenticazione vengono forniti i valori per ciascuna delle intestazioni richieste nelle chiamate [!DNL Experience Platform] API, come illustrato di seguito:

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