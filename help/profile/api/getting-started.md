---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Guida introduttiva all’API del profilo cliente in tempo reale
topic: guida
type: Documentazione
description: La guida introduttiva all’API di profilo descrive i concetti chiave e le funzionalità di base che devi conoscere per utilizzare gli endpoint API del profilo cliente in tempo reale per eseguire operazioni CRUD di base rispetto ai dati del profilo.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# Guida introduttiva all’ [!DNL Real-time Customer Profile] API {#getting-started}

Utilizzando gli endpoint API del profilo cliente in tempo reale, puoi eseguire operazioni CRUD di base rispetto ai dati del profilo, ad esempio configurare attributi calcolati, accedere alle entità, esportare i dati del profilo ed eliminare set di dati o batch non necessari.

L’utilizzo della guida per gli sviluppatori richiede una buona comprensione dei vari servizi Adobe Experience Platform coinvolti nell’utilizzo dei dati [!DNL Profile]. Prima di iniziare a lavorare con l’ API [!DNL Real-time Customer Profile], controlla la documentazione relativa ai seguenti servizi:

* [[!DNL Real-time Customer Profile]](../home.md): Fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Ottieni una visione migliore del tuo cliente e del suo comportamento attraverso il collegamento di identità tra dispositivi e sistemi.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): Consente di creare segmenti di pubblico dai dati Profilo cliente in tempo reale.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standardizzato tramite il quale Platform organizza i dati sulla customer experience.
* [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente le chiamate agli endpoint API [!DNL Profile].

## Lettura di chiamate API di esempio

La documentazione [!DNL Real-time Customer Profile] API fornisce esempi di chiamate API per dimostrare come formattare correttamente le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

## Intestazioni richieste

La documentazione API richiede inoltre di aver completato l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente le chiamate agli endpoint [!DNL Platform]. Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste nelle chiamate API [!DNL Experience Platform], come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la documentazione di panoramica [sandbox](../../sandboxes/home.md).

Tutte le richieste con un payload nel corpo della richiesta (come le chiamate POST, PUT e PATCH) devono includere un&#39;intestazione `Content-Type`. I valori accettati specifici per ogni chiamata sono forniti nei parametri della chiamata .

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l’ [!DNL Real-time Customer Profile] API , seleziona una delle guide dell’endpoint disponibili.