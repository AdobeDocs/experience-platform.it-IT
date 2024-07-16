---
keywords: Experience Platform;home;argomenti popolari;segmentazione;segmentazione;servizio di segmentazione;api;
solution: Experience Platform
title: Guida introduttiva all’API del servizio di segmentazione
description: La seguente documentazione fornisce informazioni aggiuntive che è necessario conoscere per lavorare correttamente con l’API di segmentazione.
role: Developer
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 7%

---

# Guida introduttiva all’API del servizio di segmentazione {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] consente di creare tipi di pubblico tramite definizioni di segmenti o altre origini in Adobe Experience Platform dai dati di [!DNL Real-Time Customer Profile].

La Guida per gli sviluppatori richiede una buona conoscenza dei vari servizi [!DNL Experience Platform] coinvolti nell&#39;utilizzo di [!DNL Segmentation Service].

- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): consente di creare tipi di pubblico dai dati di [!DNL Real-Time Customer Profile].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente. Per utilizzare al meglio la segmentazione, assicurati che i dati vengano acquisiti come profili ed eventi in base alle [best practice per la modellazione dei dati](../../xdm/schema/best-practices.md).
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per utilizzare correttamente l&#39;API [!DNL Segmentation].

## Lettura delle chiamate API di esempio

La documentazione API [!DNL Segmentation Service] fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

## Intestazioni richieste

La documentazione API richiede inoltre di aver completato l&#39;[esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente le chiamate agli endpoint [!DNL Platform]. Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste nelle chiamate API [!DNL Experience Platform], come illustrato di seguito:

- Autorizzazione: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in specifiche sandbox virtuali. Tutte le richieste alle API [!DNL Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sull&#39;utilizzo delle sandbox in [!DNL Experience Platform], consulta la [documentazione panoramica sulle sandbox](../../sandboxes/home.md).

## Passaggi successivi

Per effettuare chiamate tramite l&#39;API [!DNL Segmentation Service], seleziona una delle guide degli endpoint disponibili utilizzando la barra di navigazione a sinistra o nella [panoramica della guida per sviluppatori](./overview.md)
