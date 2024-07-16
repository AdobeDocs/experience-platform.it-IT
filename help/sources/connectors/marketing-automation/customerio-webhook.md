---
title: Panoramica di Customer.io Source
description: Scopri come collegare Customer.io a Adobe Experience Platform utilizzando le API o l’interfaccia utente sfruttando i webhook
badge: Beta
exl-id: 0f4ee106-c22b-465c-9c5e-83709e8424f5
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# [!DNL Customer.io]

>[!NOTE]
>
>L&#39;origine [!DNL Customer.io] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, leggere la [panoramica delle origini](../../home.md#terms-and-conditions).

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione di dati da applicazioni di streaming. Il supporto per i provider di streaming include [!DNL Customer.io].

[[!DNL Customer.io]](https://customer.io/) è una piattaforma di messaggistica automatizzata per gli esperti di marketing che desiderano maggiore controllo e flessibilità per creare e inviare e-mail, notifiche push, messaggi in-app e SMS basati sui dati.

L&#39;origine [!DNL Customer.io] consente di acquisire gli schemi evento webhook supportati e i relativi dati evento associati da [!DNL Customer.io] utilizzando [[!DNL Customer.io] Webhook di reporting](https://customer.io/docs/api/webhooks/).

Gli schemi evento webhook supportati sono:

* Eventi cliente
* Eventi e-mail
* Eventi SMS
* Eventi di notifica push
* Eventi messaggio in-app
* Eventi di Slack
* Eventi webhook

Per un elenco degli eventi disponibili tramite i webhook, consulta la documentazione [[!DNL Customer.io] Reporting Webhook events](https://customer.io/docs/webhooks/#events).

## Prerequisiti {#prerequisites}

Prima di poter creare una connessione di origine [!DNL Customer.io], è necessario verificare di disporre dei seguenti elementi:

* Un account [!DNL Customer.io]. Se non hai letto la [[!DNL Customer.io] pagina di iscrizione](https://fly.customer.io/signup) per registrarti e creare il tuo account.
* Dopo aver creato l’account, dovrai far convalidare anche il tuo account. Segui i passaggi documentati nella pagina [[!DNL Customer.io] Verifica account](https://customer.io/docs/account-verification/) per completare il processo.

### Configura webhook [!DNL Customer.io] {#set-up-webhook}

Dopo aver creato correttamente il flusso di dati, devi impostare un webhook di reporting per informare Platform sugli eventi [!DNL Customer.io]. I webhook possono inviare immediatamente notifiche quando gli attributi del cliente cambiano o quando le persone aprono i messaggi e inviare queste informazioni all&#39;origine [!DNL Customer.io]. Per ulteriori informazioni, consulta le esercitazioni su [ottenere l&#39;URL dell&#39;endpoint di streaming](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint) e [configurare un [!DNL Customer.io] webhook](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook).

## Connessione di [!DNL Customer.io] alla piattaforma {#connect-to-platform}

La documentazione seguente fornisce informazioni su come creare una connessione in streaming [!DNL Customer.io] per connettersi a [!DNL Platform] utilizzando le API o l&#39;interfaccia utente:

### Connetti [!DNL Customer.io] a Platform tramite API {#connect-to-platform-using-api}

* [Crea una connessione di origine e un flusso di dati per portare  [!DNL Customer.io]  dati a Platform utilizzando le API.](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### Connetti [!DNL Customer.io] a Platform tramite l&#39;interfaccia utente {#connect-to-platform-using-ui}

* [Crea una connessione di origine e un flusso di dati per portare  [!DNL Customer.io]  dati a Platform utilizzando l&#39;interfaccia utente](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)
