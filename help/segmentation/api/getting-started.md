---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;api;
solution: Experience Platform
title: Guida introduttiva all’API del servizio di segmentazione
topic-legacy: developer guide
description: La seguente documentazione fornisce informazioni aggiuntive che devi conoscere per poter utilizzare correttamente l’API di segmentazione.
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 1%

---

# Guida introduttiva all’API del servizio di segmentazione {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] consente di generare segmenti e generare tipi di pubblico in Adobe Experience Platform dal [!DNL Real-Time Customer Profile] dati.

La guida per gli sviluppatori richiede una comprensione approfondita dei vari [!DNL Experience Platform] servizi connessi all&#39;utilizzo [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md): Consente di creare segmenti di pubblico da [!DNL Real-Time Customer Profile] dati.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience. Per utilizzare al meglio la segmentazione, assicurati che i tuoi dati vengano acquisiti come profili ed eventi in base alla [best practice per la modellazione dei dati](../../xdm/schema/best-practices.md).
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per lavorare con [!DNL Segmentation] API.

## Lettura di chiamate API di esempio

La [!DNL Segmentation Service] La documentazione API fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] guida alla risoluzione dei problemi.

## Intestazioni richieste

La documentazione API richiede anche di aver completato la [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente le chiamate a [!DNL Platform] endpoint. Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle operazioni con le sandbox in [!DNL Experience Platform], vedi [documentazione panoramica sulle sandbox](../../sandboxes/home.md).

## Passaggi successivi

Per effettuare chiamate utilizzando [!DNL Segmentation Service] API, seleziona una delle guide dell’endpoint disponibili utilizzando la navigazione a sinistra o all’interno della [panoramica della guida per sviluppatori](./overview.md)
