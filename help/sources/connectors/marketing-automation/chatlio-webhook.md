---
title: Panoramica della sorgente Chatlio
description: Scopri come collegare Chatlio a Adobe Experience Platform utilizzando le API o l’interfaccia utente sfruttando i webhook
badge: "Beta"
source-git-commit: 2c13cb5a951a3144d0047b567194732acdc35dab
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# [!DNL Chatlio]

>[!NOTE]
>
>La [!DNL Chatlio] la sorgente è in versione beta. Per piacere, leggi le [panoramica di origini](../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di origini con etichetta beta.

Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, database e molti altri.

Experience Platform supporta l’acquisizione di dati dalle applicazioni Streaming. Il supporto per i provider di streaming include [!DNL Chatlio].

[[!DNL Chatlio]](https://chatlio.com/) è un&#39;app live chat completamente integrata con [!DNL Slack] e facilita l’utilizzo di più agenti di supporto per aiutare contemporaneamente un singolo visitatore del sito. [!DNL Chatlio] utilizza [!DNL Chatio Zapier App] per connettersi [!DNL Chatlio] con oltre 2000 applicazioni e servizi diversi.

La [!DNL Chatlio] source consente di acquisire gli schemi di eventi webhook supportati e i relativi dati evento associati da [!DNL Chatlio.com] utilizzando [[!DNL Chatlio] Webhook](https://chatlio.com/docs/webhooks/).

I webhook supportati sono:

* Esportazione delle trascrizioni chat
* Esportazione di messaggi offline
* Nuova conversazione avviata
* Il visitatore non ha ricevuto una risposta in tempo
* Il visitatore ha lasciato un feedback dopo una chat

## Prerequisiti {#prerequisites}

Prima di creare un [!DNL Chatlio] connessione di origine, è innanzitutto necessario assicurarsi di disporre dei seguenti elementi:

* A [!DNL Chatlio] conto. Se non ne hai già uno, visita il [[!DNL Chatlio] pagina di registrazione](https://chatlio.com/app/#/signup) per registrare e creare il tuo account.
* Dopo aver registrato un account, segui la [[!DNL Chatlio] documentazione di configurazione](https://chatlio.com/docs/setup/) per completare la configurazione dell&#39;account.

### Configurazione [!DNL Chatlio] gancio {#set-up-webhook}

Una volta creato correttamente il flusso di dati, devi impostare un webhook per informare Platform su [!DNL Chatlio] eventi. I webhook possono avvisarti immediatamente quando gli attributi del cliente cambiano o quando le persone aprono i messaggi e inviano queste informazioni ai tuoi [!DNL Chatlio] sorgente.

Per ulteriori informazioni, consulta le esercitazioni su [ottenimento dell’URL dell’endpoint di streaming](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) e [creazione di un [!DNL Chatlio] Webhook](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook).

## Connetti [!DNL Chatlio] su Platform {#connect-to-platform}

La documentazione seguente fornisce informazioni su come creare un [!DNL Chatlio] connettore streaming con cui connettersi [!DNL Platform] utilizzando le API o l’interfaccia utente:

### Connetti [!DNL Chatlio] su Platform tramite API {#connect-to-platform-using-api}

* [Crea una connessione sorgente da portare [!DNL Chatlio] in Platform tramite API.](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### Connetti [!DNL Chatlio] su Platform tramite l’interfaccia utente {#connect-to-platform-using-ui}

* [Crea una connessione sorgente da portare [!DNL Chatlio] dati a Platform tramite l’interfaccia utente](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)

