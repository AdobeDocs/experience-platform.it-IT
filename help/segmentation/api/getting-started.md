---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;api;
solution: Experience Platform
title: Guida introduttiva all’API del servizio di segmentazione
topic-legacy: developer guide
description: La seguente documentazione fornisce informazioni aggiuntive che devi conoscere per poter utilizzare correttamente l’API di segmentazione.
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Guida introduttiva all’API del servizio di segmentazione {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] consente di generare segmenti e tipi di pubblico in Adobe Experience Platform dai dati [!DNL Real-time Customer Profile].

La guida per gli sviluppatori richiede una buona comprensione dei vari servizi [!DNL Experience Platform] coinvolti nell&#39;utilizzo di [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md): Ti consente di creare segmenti di pubblico dai  [!DNL Real-time Customer Profile] dati.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [Sandbox](../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che dovrai conoscere per poter utilizzare correttamente l’ API [!DNL Segmentation] .

## Lettura di chiamate API di esempio

La documentazione [!DNL Segmentation Service] API fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

## Intestazioni richieste

La documentazione API richiede inoltre di aver completato l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente le chiamate agli endpoint [!DNL Platform]. Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste nelle chiamate API [!DNL Experience Platform], come mostrato di seguito:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- nome x-sandbox: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle operazioni con le sandbox in [!DNL Experience Platform], consulta la documentazione di panoramica [sandbox](../../sandboxes/home.md).

## Passaggi successivi

Per effettuare chiamate utilizzando l&#39;API [!DNL Segmentation Service] , seleziona una delle guide dell&#39;endpoint disponibili utilizzando la navigazione a sinistra o all&#39;interno della [panoramica della guida per gli sviluppatori](./overview.md)
