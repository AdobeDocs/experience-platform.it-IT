---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Guida introduttiva all’API del profilo cliente in tempo reale
type: Documentation
description: La guida introduttiva all’API di profilo descrive i concetti chiave e le funzionalità di base necessari per utilizzare gli endpoint API del profilo cliente in tempo reale al fine di eseguire operazioni CRUD di base sui dati del profilo.
role: Developer
exl-id: 7e30610a-a7e7-43ab-a45d-fd84ef6e36ef
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 6%

---

# Guida introduttiva a [!DNL Real-Time Customer Profile] API {#getting-started}

Utilizzando gli endpoint API del profilo cliente in tempo reale, puoi eseguire operazioni CRUD di base sui dati del profilo, ad esempio configurare attributi calcolati, accedere alle entità, esportare i dati del profilo ed eliminare set di dati o batch non necessari.

L’utilizzo della guida per sviluppatori richiede una buona conoscenza dei vari servizi Adobe Experience Platform coinvolti nell’utilizzo di [!DNL Profile] dati. Prima di iniziare a utilizzare [!DNL Real-Time Customer Profile] API, consulta la documentazione dei seguenti servizi:

* [[!DNL Real-Time Customer Profile]](../home.md): fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): ottieni una visione migliore del cliente e del suo comportamento collegando le identità tra dispositivi e sistemi.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): consente di creare tipi di pubblico dai dati Profilo cliente in tempo reale.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): framework standardizzato tramite il quale Platform organizza i dati sull’esperienza del cliente.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per effettuare correttamente le chiamate a [!DNL Profile] Endpoint API.

## Lettura delle chiamate API di esempio

Il [!DNL Real-Time Customer Profile] La documentazione API fornisce esempi di chiamate API per dimostrare come formattare correttamente le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nel [!DNL Experience Platform] guida alla risoluzione dei problemi.

## Intestazioni richieste

La documentazione API richiede inoltre di aver completato [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente chiamate a [!DNL Platform] endpoint. Il completamento del tutorial sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolati in specifiche sandbox virtuali. Richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedere [documentazione di panoramica sulla sandbox](../../sandboxes/home.md).

Tutte le richieste con un payload nel corpo della richiesta (come chiamate POST, PUT e PATCH) devono includere `Content-Type` intestazione. I valori accettati specifici di ogni chiamata sono forniti nei parametri della chiamata.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando [!DNL Real-Time Customer Profile] API, seleziona una delle guide endpoint disponibili.
