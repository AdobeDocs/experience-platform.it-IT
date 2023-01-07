---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Guida introduttiva all’API del profilo cliente in tempo reale
type: Documentation
description: La guida introduttiva all’API di profilo descrive i concetti chiave e le funzionalità di base che devi conoscere per utilizzare gli endpoint API del profilo cliente in tempo reale per eseguire operazioni CRUD di base rispetto ai dati del profilo.
exl-id: 7e30610a-a7e7-43ab-a45d-fd84ef6e36ef
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Guida introduttiva a [!DNL Real-Time Customer Profile] API {#getting-started}

Utilizzando gli endpoint API del profilo cliente in tempo reale, puoi eseguire operazioni CRUD di base rispetto ai dati del profilo, ad esempio configurare attributi calcolati, accedere alle entità, esportare i dati del profilo ed eliminare set di dati o batch non necessari.

L’utilizzo della guida per gli sviluppatori richiede una comprensione approfondita dei vari servizi Adobe Experience Platform coinvolti nell’utilizzo di [!DNL Profile] dati. Prima di iniziare a lavorare con [!DNL Real-Time Customer Profile] API, controlla la documentazione per i seguenti servizi:

* [[!DNL Real-Time Customer Profile]](../home.md): Fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Ottieni una visione migliore del tuo cliente e del suo comportamento attraverso il collegamento di identità tra dispositivi e sistemi.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): Consente di creare segmenti di pubblico dai dati Profilo cliente in tempo reale.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standardizzato tramite il quale Platform organizza i dati sulla customer experience.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente le chiamate a [!DNL Profile] Endpoint API.

## Lettura di chiamate API di esempio

La [!DNL Real-Time Customer Profile] La documentazione API fornisce esempi di chiamate API per dimostrare come formattare correttamente le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] guida alla risoluzione dei problemi.

## Intestazioni richieste

La documentazione API richiede anche di aver completato la [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente le chiamate a [!DNL Platform] endpoint. Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedi [documentazione panoramica su sandbox](../../sandboxes/home.md).

Tutte le richieste con un payload nel corpo della richiesta (come le chiamate POST, PUT e PATCH) devono includere un `Content-Type` intestazione. I valori accettati specifici per ogni chiamata sono forniti nei parametri della chiamata .

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando [!DNL Real-Time Customer Profile] API, seleziona una delle guide degli endpoint disponibili.
