---
keywords: Experience Platform;home;argomenti popolari;segmentazione;segmentazione;servizio di segmentazione;api;
solution: Experience Platform
title: Guida introduttiva all’API del servizio di segmentazione
description: La seguente documentazione fornisce informazioni aggiuntive che è necessario conoscere per lavorare correttamente con l’API di segmentazione.
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 1%

---

# Guida introduttiva all’API del servizio di segmentazione {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] consente di creare segmenti e generare tipi di pubblico in Adobe Experience Platform dal tuo [!DNL Real-Time Customer Profile] dati.

La guida per gli sviluppatori richiede una buona conoscenza delle varie [!DNL Experience Platform] servizi coinvolti nell’utilizzo di [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md): consente di creare segmenti di pubblico da [!DNL Real-Time Customer Profile] dati.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente. Per utilizzare al meglio la segmentazione, assicurati che i dati vengano acquisiti come profili ed eventi in base alla [best practice per la modellazione dei dati](../../xdm/schema/best-practices.md).
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per lavorare con successo con [!DNL Segmentation] API.

## Lettura delle chiamate API di esempio

Il [!DNL Segmentation Service] La documentazione API fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito il codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nel [!DNL Experience Platform] guida alla risoluzione dei problemi.

## Intestazioni richieste

La documentazione API richiede inoltre di aver completato [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente chiamate a [!DNL Platform] endpoint. Il completamento del tutorial sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolati in specifiche sandbox virtuali. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sull’utilizzo delle sandbox in [!DNL Experience Platform], vedere [documentazione panoramica sulle sandbox](../../sandboxes/home.md).

## Passaggi successivi

Per effettuare chiamate utilizzando [!DNL Segmentation Service] API, seleziona una delle guide degli endpoint disponibili utilizzando la barra di navigazione a sinistra o all’interno di [panoramica della guida per sviluppatori](./overview.md)
