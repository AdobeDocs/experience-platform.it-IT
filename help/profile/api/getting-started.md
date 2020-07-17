---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guida introduttiva all'API del profilo cliente in tempo reale
topic: guide
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Guida introduttiva all&#39; [!DNL Real-time Customer Profile] API {#getting-started}

Utilizzando l&#39; [!DNL Real-time Customer Profile] API, potete eseguire operazioni CRUD di base rispetto alle risorse Profilo, come la configurazione degli attributi calcolati, l&#39;accesso alle entità, l&#39;esportazione dei dati del profilo ed eliminazione di set di dati o batch non necessari.

L&#39;utilizzo della guida per gli sviluppatori richiede una conoscenza approfondita dei diversi servizi  Adobi Experience Platform coinvolti nell&#39;utilizzo dei [!DNL Profile] dati. Prima di iniziare a lavorare con l&#39; [!DNL Real-time Customer Profile] API, consulta la documentazione relativa ai seguenti servizi:

* [!DNL Real-time Customer Profile](../home.md): Fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
* [!DNL Adobe Experience Platform Identity Service](../../identity-service/home.md): Ottieni una visione migliore del tuo cliente e del suo comportamento attraverso il collegamento di identità tra dispositivi e sistemi.
* [!DNL Adobe Experience Platform Segmentation Service](../../segmentation/home.md): Consente di creare segmenti di pubblico dai dati del profilo cliente in tempo reale.
* [!DNL Experience Data Model (XDM)](../../xdm/home.md): Framework standard con cui Platform organizza i dati sull&#39;esperienza dei clienti.
* [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per eseguire correttamente chiamate agli endpoint [!DNL Profile] API.

## Lettura di chiamate API di esempio

La documentazione [!DNL Real-time Customer Profile] API fornisce esempi di chiamate API per dimostrare come formattare correttamente le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

## Intestazioni necessarie

La documentazione API richiede inoltre di aver completato l&#39;esercitazione [di](../../tutorials/authentication.md) autenticazione per effettuare correttamente le chiamate agli [!DNL Platform] endpoint. Completando l&#39;esercitazione sull&#39;autenticazione vengono forniti i valori per ciascuna delle intestazioni richieste nelle chiamate [!DNL Experience Platform] API, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui si svolgerà l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste con un payload nel corpo della richiesta (come le chiamate POST, PUT e PATCH) devono includere un&#39; `Content-Type` intestazione. I valori accettati specifici per ogni chiamata vengono forniti nei parametri delle chiamate.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39; [!DNL Real-time Customer Profile] API, seleziona una delle guide degli endpoint disponibili.