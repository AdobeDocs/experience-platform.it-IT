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

# Guida introduttiva all&#39;API [!DNL Real-Time Customer Profile] {#getting-started}

Utilizzando gli endpoint API del profilo cliente in tempo reale, puoi eseguire operazioni CRUD di base sui dati del profilo, ad esempio configurare attributi calcolati, accedere alle entità, esportare i dati del profilo ed eliminare set di dati o batch non necessari.

L&#39;utilizzo della guida per sviluppatori richiede una buona conoscenza dei vari servizi Adobe Experience Platform coinvolti nell&#39;utilizzo dei dati [!DNL Profile]. Prima di iniziare a utilizzare l&#39;API [!DNL Real-Time Customer Profile], consulta la documentazione dei seguenti servizi:

* [[!DNL Real-Time Customer Profile]](../home.md): fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Ottieni una migliore visualizzazione dei tuoi clienti e del loro comportamento collegando le identità tra dispositivi e sistemi diversi.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): consente di creare tipi di pubblico dai dati del profilo cliente in tempo reale.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): framework standardizzato in base al quale Platform organizza i dati sull’esperienza del cliente.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per effettuare correttamente chiamate agli endpoint API [!DNL Profile].

## Lettura delle chiamate API di esempio

La documentazione API [!DNL Real-Time Customer Profile] fornisce esempi di chiamate API per dimostrare come formattare correttamente le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

## Intestazioni richieste

La documentazione API richiede inoltre di aver completato l&#39;[esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente le chiamate agli endpoint [!DNL Platform]. Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste nelle chiamate API [!DNL Experience Platform], come illustrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in specifiche sandbox virtuali. Le richieste alle API [!DNL Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la [documentazione di panoramica sulle sandbox](../../sandboxes/home.md).

Tutte le richieste con un payload nel corpo della richiesta (ad esempio chiamate POST, PUT e PATCH) devono includere un&#39;intestazione `Content-Type`. I valori accettati specifici di ogni chiamata sono forniti nei parametri della chiamata.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39;API [!DNL Real-Time Customer Profile], seleziona una delle guide degli endpoint disponibili.
