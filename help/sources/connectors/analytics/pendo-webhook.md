---
title: Panoramica di Pendo Source
description: Scopri come collegare Pendo a Adobe Experience Platform utilizzando le API o l’interfaccia utente sfruttando i webhook
badge: Beta
exl-id: 376f18ef-1eea-4c42-8041-6fadb5906e9b
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# [!DNL Pendo]

>[!NOTE]
>
>L&#39;origine [!DNL Pendo] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, leggere la [panoramica delle origini](../../home.md#terms-and-conditions).

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione di dati da applicazioni di analisi di terze parti. Il supporto per i provider di analisi include [!DNL Pendo].

[[!DNL Pendo]](https://pendo.io/) è un&#39;app di analisi dei prodotti creata per aiutare le aziende di software a sviluppare prodotti che risuonano con i clienti. L’app consente ai produttori di software di incorporare i loro prodotti con un’ampia gamma di strumenti che possono portare a una migliore esperienza del prodotto per gli utenti e a nuove informazioni per il team di prodotto.

L&#39;origine [!DNL Pendo] consente di acquisire gli schemi evento webhook supportati e i relativi dati evento associati da [!DNL Pendo.io] utilizzando [[!DNL Pendo] Webhook](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks). L&#39;origine [!DNL Pendo] funziona con [!DNL Pendo] webhook URL.

I webhook supportati sono:

* [Guida](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide) visualizzata
* [Sondaggio](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) visualizzato/inviato
* [Punteggio promotore netto](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) visualizzato/inviato

## Prerequisiti {#prerequisites}

Prima di poter creare una connessione di origine [!DNL Pendo], è necessario verificare di disporre dei seguenti elementi:

Un account [!DNL Pendo]. Se non ne hai già una, vedi la pagina [[!DNL Pendo] registra](https://app.pendo.io/register) per registrarti e creare il tuo account.

### Configura webhook [!DNL Pendo] {#set-up-webhook}

Dopo aver creato correttamente il flusso di dati, devi impostare un webhook per informare Platform sugli eventi [!DNL Pendo]. I webhook di [!DNL Pendo] possono inviare notifiche in tempo reale ad altri servizi quando si verificano determinati eventi e inviare tali informazioni all&#39;origine [!DNL Pendo]. Per ulteriori informazioni, consulta le esercitazioni su [ottenere l&#39;URL dell&#39;endpoint di streaming](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint) e [configurare un [!DNL Pendo] webhook](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook).

## Connessione di [!DNL Pendo] alla piattaforma {#connect-to-platform}

La documentazione seguente fornisce informazioni su come creare un connettore di streaming [!DNL Pendo] per connettersi a [!DNL Platform] utilizzando le API o l&#39;interfaccia utente:

### Connetti [!DNL Pendo] a Platform tramite API {#connect-to-platform-using-api}

* [Crea una connessione di origine per portare  [!DNL Pendo]  dati a Platform utilizzando le API.](../../tutorials/api/create/analytics/pendo-webhook.md)

### Connetti [!DNL Pendo] a Platform tramite l&#39;interfaccia utente {#connect-to-platform-using-ui}

* [Crea una connessione di origine per portare  [!DNL Pendo]  dati a Platform utilizzando l&#39;interfaccia utente](../../tutorials/ui/create/analytics/pendo-webhook.md)
