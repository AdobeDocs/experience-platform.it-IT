---
title: Panoramica di Customer.io Source
description: Scopri come collegare Customer.io a Adobe Experience Platform utilizzando le API o l’interfaccia utente sfruttando i webhook
badge: Beta
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 0f4ee106-c22b-465c-9c5e-83709e8424f5
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!DNL Customer.io]

>[!NOTE]
>
>La [!DNL Customer.io] la sorgente è in versione beta. Per piacere, leggi le [panoramica di origini](../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di origini con etichetta beta.

Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, database e molti altri.

Experience Platform fornisce il supporto per l’acquisizione di dati dalle applicazioni di streaming. Il supporto per i provider di streaming include [!DNL Customer.io].

[[!DNL Customer.io]](https://customer.io/) è una piattaforma di messaggistica automatizzata per gli esperti marketing che desiderano maggiore controllo e flessibilità per creare e inviare e-mail basate su dati, notifiche push, messaggi in-app e SMS.

La [!DNL Customer.io] source consente di acquisire gli schemi di eventi webhook supportati e i relativi dati evento associati da [!DNL Customer.io] utilizzando [[!DNL Customer.io] Webhook di reporting](https://customer.io/docs/api/webhooks/).

Gli schemi di evento del webhook supportati sono:

* Eventi cliente
* Eventi e-mail
* Eventi SMS
* Eventi di notifica push
* Eventi messaggio in-app
* Eventi Slack
* Eventi Webhook

Per un elenco degli eventi disponibili tramite i webhook, consulta [[!DNL Customer.io] Reporting degli eventi Webhook](https://customer.io/docs/webhooks/#events) documentazione.

## Prerequisiti {#prerequisites}

Prima di creare un [!DNL Customer.io] connessione di origine, è innanzitutto necessario assicurarsi di disporre dei seguenti elementi:

* A [!DNL Customer.io] conto. Se non ne hai una, leggi la sezione [[!DNL Customer.io] pagina di registrazione](https://fly.customer.io/signup) per registrare e creare il tuo account.
* Dopo aver creato il tuo account, dovrai anche far convalidare il tuo account. Segui i passaggi documentati sul [[!DNL Customer.io] Verifica dell&#39;account](https://customer.io/docs/account-verification/) per completare il processo.

### Configurazione [!DNL Customer.io] Webhook {#set-up-webhook}

Dopo aver creato correttamente il flusso di dati, è necessario impostare un Webhook per la generazione di rapporti per informare Platform su [!DNL Customer.io] eventi. I webhook possono avvisarti immediatamente quando gli attributi del cliente cambiano o quando le persone aprono i tuoi messaggi e inviare queste informazioni ai tuoi [!DNL Customer.io] sorgente. Per ulteriori informazioni, consulta le esercitazioni su [ottenimento dell’URL dell’endpoint di streaming](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint) e [creazione di un [!DNL Customer.io] Webhook](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook).

## Collegamento [!DNL Customer.io] su Platform {#connect-to-platform}

La documentazione seguente fornisce informazioni su come creare un [!DNL Customer.io] connessione in streaming con cui connettersi [!DNL Platform] utilizzando le API o l’interfaccia utente:

### Connetti [!DNL Customer.io] su Platform tramite API {#connect-to-platform-using-api}

* [Creare una connessione sorgente e un flusso di dati per portare [!DNL Customer.io] in Platform tramite API.](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### Connetti [!DNL Customer.io] su Platform tramite l’interfaccia utente {#connect-to-platform-using-ui}

* [Creare una connessione sorgente e un flusso di dati per portare [!DNL Customer.io] dati a Platform tramite l’interfaccia utente](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)
