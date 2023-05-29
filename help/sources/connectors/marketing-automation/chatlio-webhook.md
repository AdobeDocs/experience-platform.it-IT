---
title: Panoramica dell’origine del catalogo
description: Scopri come collegare Chatlio a Adobe Experience Platform utilizzando le API o l’interfaccia utente sfruttando i webhook
badge: Beta
exl-id: 4a71d1dc-e0eb-443e-a956-8caa0e82fa18
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# [!DNL Chatlio]

>[!NOTE]
>
>Il [!DNL Chatlio] sorgente in versione beta. Leggi le [panoramica sulle origini](../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione di dati dalle applicazioni Streaming. Il supporto per i provider di streaming include [!DNL Chatlio].

[[!DNL Chatlio]](https://chatlio.com/) è un’app di chat live completamente integrata con [!DNL Slack] e consente a più agenti di supporto di aiutare contemporaneamente un singolo visitatore del sito. [!DNL Chatlio] utilizza [!DNL Chatio Zapier App] per connettersi [!DNL Chatlio] con oltre 2000 applicazioni e servizi diversi.

Il [!DNL Chatlio] origine consente di acquisire gli schemi di eventi webhook supportati e i relativi dati di eventi associati da [!DNL Chatlio.com] utilizzando [[!DNL Chatlio] Webhook](https://chatlio.com/docs/webhooks/).

I webhook supportati sono:

* Esportazione trascrizioni chat
* Esportazione di messaggi offline
* Nuova conversazione avviata
* Il visitatore non ha ricevuto una risposta in tempo
* Feedback lasciato dal visitatore dopo una chat

## Prerequisiti {#prerequisites}

Prima di creare un [!DNL Chatlio] connessione di origine, è necessario verificare di disporre dei seguenti elementi:

* A [!DNL Chatlio] account. Se non ne hai già una, visita il [[!DNL Chatlio] pagina di registrazione](https://chatlio.com/app/#/signup) per registrarti e creare il tuo account.
* Dopo aver registrato correttamente un account, segui la [[!DNL Chatlio] documentazione di configurazione](https://chatlio.com/docs/setup/) per completare la configurazione del tuo account.

### Configurazione [!DNL Chatlio] webhook {#set-up-webhook}

Dopo aver creato correttamente il flusso di dati, devi impostare un webhook per informare Platform su [!DNL Chatlio] eventi. I webhook possono inviare immediatamente notifiche quando gli attributi del cliente cambiano o quando le persone aprono i messaggi e inviano queste informazioni al tuo [!DNL Chatlio] sorgente.

Per ulteriori informazioni, consulta le esercitazioni su [recupero dell’URL dell’endpoint di streaming](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) e [impostazione di un [!DNL Chatlio] Webhook](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook).

## Connetti [!DNL Chatlio] alla piattaforma {#connect-to-platform}

La documentazione seguente fornisce informazioni su come creare un [!DNL Chatlio] connettore di streaming per la connessione [!DNL Platform] utilizzando le API o l’interfaccia utente:

### Connetti [!DNL Chatlio] alla piattaforma utilizzando le API {#connect-to-platform-using-api}

* [Crea una connessione sorgente da portare [!DNL Chatlio] dati a Platform tramite API.](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### Connetti [!DNL Chatlio] a Platform tramite l’interfaccia utente {#connect-to-platform-using-ui}

* [Crea una connessione sorgente da portare [!DNL Chatlio] dati a Platform tramite l’interfaccia utente](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)
