---
title: Panoramica sull'origine Customer.io
description: Scopri come collegare Customer.io a Adobe Experience Platform utilizzando le API o l’interfaccia utente sfruttando i webhook
badge: Beta
exl-id: 0f4ee106-c22b-465c-9c5e-83709e8424f5
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# [!DNL Customer.io]

>[!NOTE]
>
>Il [!DNL Customer.io] sorgente in versione beta. Leggi le [panoramica sulle origini](../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experienci Platform fornisce supporto per l’acquisizione di dati da applicazioni di streaming. Il supporto per i provider di streaming include [!DNL Customer.io].

[[!DNL Customer.io]](https://customer.io/) è una piattaforma di messaggistica automatizzata per gli esperti di marketing che desiderano maggiore controllo e flessibilità per creare e inviare e-mail basate su dati, notifiche push, messaggi in-app e SMS.

Il [!DNL Customer.io] origine consente di acquisire gli schemi di eventi webhook supportati e i relativi dati di eventi associati da [!DNL Customer.io] utilizzando [[!DNL Customer.io] Webhook di reporting](https://customer.io/docs/api/webhooks/).

Gli schemi evento webhook supportati sono:

* Eventi cliente
* Eventi e-mail
* Eventi SMS
* Eventi di notifica push
* Eventi messaggio in-app
* Eventi di Slack
* Eventi webhook

Per un elenco degli eventi disponibili tramite i webhook, consulta [[!DNL Customer.io] Segnalazione degli eventi del webhook](https://customer.io/docs/webhooks/#events) documentazione.

## Prerequisiti {#prerequisites}

Prima di creare un [!DNL Customer.io] connessione di origine, è necessario verificare di disporre dei seguenti elementi:

* A [!DNL Customer.io] account. In caso contrario, leggere [[!DNL Customer.io] pagina di registrazione](https://fly.customer.io/signup) per registrarti e creare il tuo account.
* Dopo aver creato l’account, dovrai far convalidare anche il tuo account. Segui i passaggi documentati in [[!DNL Customer.io] Verifica dell’account](https://customer.io/docs/account-verification/) per completare il processo.

### Configurazione [!DNL Customer.io] Webhook {#set-up-webhook}

Dopo aver creato correttamente il flusso di dati, devi impostare un webhook di reporting per informare Platform su [!DNL Customer.io] eventi. I webhook possono avvisarti immediatamente quando gli attributi del cliente cambiano o quando le persone aprono i tuoi messaggi, e inviare queste informazioni al tuo [!DNL Customer.io] sorgente. Per ulteriori informazioni, consulta le esercitazioni su [recupero dell’URL dell’endpoint di streaming](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint) e [impostazione di un [!DNL Customer.io] Webhook](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook).

## Connessione [!DNL Customer.io] alla piattaforma {#connect-to-platform}

La documentazione seguente fornisce informazioni su come creare un [!DNL Customer.io] connessione in streaming per la connessione con [!DNL Platform] utilizzando le API o l’interfaccia utente:

### Connetti [!DNL Customer.io] alla piattaforma utilizzando le API {#connect-to-platform-using-api}

* [Creare una connessione di origine e un flusso di dati per portare [!DNL Customer.io] dati a Platform tramite API.](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### Connetti [!DNL Customer.io] a Platform tramite l’interfaccia utente {#connect-to-platform-using-ui}

* [Creare una connessione di origine e un flusso di dati per portare [!DNL Customer.io] dati a Platform tramite l’interfaccia utente](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)
