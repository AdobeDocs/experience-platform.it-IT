---
title: Panoramica di Chatlio Source
description: Scopri come collegare Chatlio a Adobe Experience Platform utilizzando le API o l’interfaccia utente sfruttando i webhook
badge: Beta
exl-id: 4a71d1dc-e0eb-443e-a956-8caa0e82fa18
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# [!DNL Chatlio]

>[!NOTE]
>
>L&#39;origine [!DNL Chatlio] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, leggere la [panoramica delle origini](../../home.md#terms-and-conditions).

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione di dati dalle applicazioni Streaming. Il supporto per i provider di streaming include [!DNL Chatlio].

[[!DNL Chatlio]](https://chatlio.com/) è un&#39;app di chat in tempo reale completamente integrata con [!DNL Slack] e facilita l&#39;utilizzo simultaneo di più agenti di supporto per un singolo visitatore del sito. [!DNL Chatlio] utilizza [!DNL Chatio Zapier App] per connettere [!DNL Chatlio] con oltre 2.000 app e servizi diversi.

L&#39;origine [!DNL Chatlio] consente di acquisire gli schemi evento webhook supportati e i relativi dati evento associati da [!DNL Chatlio.com] utilizzando [[!DNL Chatlio] Webhook](https://chatlio.com/docs/webhooks/).

I webhook supportati sono:

* Esportazione trascrizioni chat
* Esportazione di messaggi offline
* Nuova conversazione avviata
* Il visitatore non ha ricevuto una risposta in tempo
* Feedback lasciato dal visitatore dopo una chat

## Prerequisiti {#prerequisites}

Prima di poter creare una connessione di origine [!DNL Chatlio], è necessario verificare di disporre dei seguenti elementi:

* Un account [!DNL Chatlio]. Se non ne hai già una, visita la [[!DNL Chatlio] pagina di iscrizione](https://chatlio.com/app/#/signup) per registrarti e creare il tuo account.
* Dopo aver registrato correttamente un account, segui la [[!DNL Chatlio] documentazione sull&#39;installazione](https://chatlio.com/docs/setup/) per completare la configurazione dell&#39;account.

### Imposta webhook [!DNL Chatlio] {#set-up-webhook}

Dopo aver creato correttamente il flusso di dati, devi impostare un webhook per informare Platform sugli eventi [!DNL Chatlio]. I webhook possono inviare immediatamente notifiche quando gli attributi del cliente cambiano o quando le persone aprono i messaggi e inviano queste informazioni all&#39;origine [!DNL Chatlio].

Per ulteriori informazioni, consulta le esercitazioni su [ottenere l&#39;URL dell&#39;endpoint di streaming](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) e [configurare un [!DNL Chatlio] webhook](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook).

## Connetti [!DNL Chatlio] a Platform {#connect-to-platform}

La documentazione seguente fornisce informazioni su come creare un connettore di streaming [!DNL Chatlio] per connettersi a [!DNL Platform] utilizzando le API o l&#39;interfaccia utente:

### Connetti [!DNL Chatlio] a Platform tramite API {#connect-to-platform-using-api}

* [Crea una connessione di origine per portare  [!DNL Chatlio]  dati a Platform utilizzando le API.](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### Connetti [!DNL Chatlio] a Platform tramite l&#39;interfaccia utente {#connect-to-platform-using-ui}

* [Crea una connessione di origine per portare  [!DNL Chatlio]  dati a Platform utilizzando l&#39;interfaccia utente](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)
